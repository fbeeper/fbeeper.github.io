---
layout: post
title: "Who Owns the AI Agent Loop?"
categories: agentkitten
excerpt: "Presenting AgentKitten: a Swift package for building provider-agnostic AI agents on Apple platforms."
decoration: triangle
permalink: agentkitten/2026/05/13/Who-Owns-the-AI-Agent-Loop/
tags: [agentkitten, AI, agent, harness]
---

**Who Owns the AI Agent Loop?** is not particularly a new question.

If you've been building features with LLMs over the last few years you've likely used frameworks like LangChain/LangGraph, Vercel AI SDK, LlamaIndex, Google ADK, etc. Alternatively, you may be deeply exposed to chatbots, coding agents, and/or assistants. All of the above, roughly circling around the same idea, are flavors of the **AI Agent loop being a mix of large language models and software scaffolding** (typically called a *harness*).

What's surprising is that for Swift and Apple platform developers, a solid version of the harness-building toolset doesn't seem to exist yet. Working on some exploratory features, I kept having to relearn and rebuild the same scaffolding every time I wanted to try a different provider. The kind of thing a framework exists to solve. And since a clean Swift abstraction of it didn't already exist, I built mine:

**[AgentKitten](https://github.com/fbeeper/agentkitten): a Swift package for building provider-agnostic AI agents on Apple platforms.**

---

## The Agent - Harness Spectrum 

*(### Feel free to skip this section if you are already proficient in the concepts of Agents and Harnesses. ###)*

There has been a popular definition doing its rounds for a while where *"Agent = Model + Harness"*. This captures something really useful. However, I think there is a more nuanced spectrum to grasp.

Early language models generated text. Then, models were trained to request tool execution: to say "call this function with these arguments" rather than just describing what should happen. That may be clearest split of responsibility between Agent and Harness. But harnesses went further, mostly compensating: managing memory the model couldn't maintain, adding validation loops for outputs it couldn't reliably verify, imposing step limits for when it may not be able to recognize it was stuck. And many of today's models have internalized much of that: planning, self-correction, knowing when a task is done. So the harness has shifted its responsibilities. 

What surely stays in the harness isn't just what the model can't do, but what the model should not self-govern regardless of capability: the policies that define what it's allowed to do, the approval gates that keep a human in consequential decisions, the trace that makes the whole thing auditable, etc.

The harness' boundary keeps shifting as models improve. Models are internalizing capabilities that required explicit harness scaffolding just a year ago. It is plausible that a significant portion of what today's harnesses provide will be absorbed by the models, by protocols, or by higher-order orchestration. But what probably stays is whatever the model shouldn't self-govern regardless of capability.

An on-device model (tight context window, narrower general-purpose reasoning, running locally with privacy guarantees by design) will likely continue to need more active help from the harness. For example, context compaction could be critical, and/or validation loops can compensate for less reliable self-correction.

A frontier cloud model (abundant context window, broader reasoning, remote endpoint) shifts the weight elsewhere. Cost per token matters, data exposure is a real concern, and observability of consequential actions may be key.

There is a world of harness primitives that may stay exactly the same either way: tools, policies, and traces. And other core primitives, although used differently, may also have a shared surface like validation loops and state. In any of these stable concepts, what really changes is the configuration and where the harness ends up doing most of its work.

---

## What AgentKitten's abstraction covers

The two providers AgentKitten currently ships with are at opposite ends of the spectrum. Chosen not because they're the only ones worth supporting, but because they make the clearest test of what the abstraction does and doesn't cover:

* Anthropic's API is remote, stateless, with open history, and tool loop-delegating. You can rather easily work the history, and get tool calls mid-inference and everything after that is your code.
* Apple's Foundation Models SDK is on-device, stateful, local, history and tool loop-owning. It keeps its transcript rather close to its chest, and dispatches tools through its session internally.

The abstraction holds across both ends of that range reasonably well. Where it leaks, provider-specific behavior remains accessible rather than hidden behind forced generalization. That leakage is intentional, not a failure mode.

Also, AgentKitten isn't a pipeline DSL. There are frameworks that compose model calls into step graphs well. This framework is focused instead on ongoing interactive sessions with state, effectively controlling tools, and a loop that persists for as many turns as the conversation requires.

---

## What AgentKitten's loop ownership gives you

I have four immediate examples worth being specific about. Each one a problem the framework handles so you don't have to rebuild it:

### 1. Tool execution policy

The decision your app can make before anything runs.

* Apple's FoundationModels dispatches tools through its session internally. You implement the tool, the model decides to call it. It runs. There is no moment between the model's decision and the execution where your app participates.
* Anthropic's API hands you the tool call and trusts you to do whatever you want. But "whatever you want" is left entirely to you to implement from scratch.

`ToolExecutionPolicy` is that missing moment, made explicit by AgentKitten. Before any tool call executes, your policy sees the call and returns one of three decisions:

```swift
  public protocol ToolExecutionPolicy: Sendable {
      func resolve(
          call: PendingToolCall,
          context: ToolExecutionContext
      ) async -> ToolExecutionDecision
  } 
  
  public enum ToolExecutionDecision: Sendable, Equatable {
      case execute
      case deny(reason: String)
      case requiresApproval
  }
```

Here, `.execute` is the silent path for background agents or specific calls that run unattended. Meanwhile, `.deny` lets the policy refuse a call and surface a reason back to the model. That way, it can try a different approach rather than failing silently. And `.requiresApproval` suspends the turn and emits a `toolApprovalRequired` event. The turn stays live. The model is waiting, until the caller resolves it.

The `PendingToolCall` given to your implementation carries something worth singling out: The `modelRationale`. This is the model's own self-reported rationale for wanting to make this tool call. It is available as UX context. With it, you can avoid generic messaging but provide the model's actual reasoning. The field is marked explicitly in the source documentation as "UX context only — may be nil, inaccurate, or adversarially supplied" which is the brutal truth. But for interactive approval flows it could be the difference between a bare permission dialog and one that gives the user something meaningful to respond to.

Lastly, the approval resolution sits on the session:

```swift
  for try await event in turn.events {
      if case .toolApprovalRequired(let call) = event.kind {
          let approved = await showApprovalDialog(
              toolName: call.name,
              rationale: call.modelRationale
          )
          if approved {
              try await session.approve(callID: call.id)
          } else {
              try await session.deny(callID: call.id, reason: "User declined.")
          }
      }
  }
```

### 2. Per-turn overrides
  
Controlling what the model can see and do one step at a time.

Let's explain this through an example: It is well known some agent patterns may benefit from separating planning from execution. With this separation we can let the model reason without access tools with side effects. Then, open them back up once there's a plan. `TurnOverrides` lets you change model, inference settings, or tool availability for a single turn without touching the agent or session as a whole:

```swift
  let planningOverrides = TurnOverrides(
      availableTools: .include(["read_file", "list_directory"])
  )
  let planTurn = try await session.send(task, turnOverrides: planningOverrides)
  let executionTurn = try await session.send("Execute the plan.")
```

Because models can be swapped per turn, planning can run on a faster model while execution runs on a more capable one, all within a shared session history. That orchestration logic belongs to the application, not the provider.

The policy can also read typed custom environment values you've threaded through `TurnOverrides`. Which means things like your tool approval logic can branch on turn state without coupling your tool definitions to that state. A turn running in an elevated-trust context can auto-approve. The same agent running for a guest user can require confirmation for every write operation. The policy is the seam between the agent's behavior and your app's trust model.

### 3. Context Compaction

The on-device constraints aren't a phase.

As of today, Apple Foundation Models have a smaller context window (4096 tokens) than a frontier cloud model (around 200k to 1M tokens). This isn't a temporary problem, so multi-turn conversations within the same context will hit the limit faster than you'd want them to. Especially with tool results accumulating in history. Truncation loses context. Not doing multi-turn may make the features significantly worse. Summarization is simple, but it is well proven to work: Compress older turns, and even preserve recent ones for increased fidelity of recent context. And have the ability for it to fire timely and automatically at the right threshold, without the caller managing it per session.

```swift
  let behavior = AgentBehavior(
      systemPrompt: "You are a search assistant.",
      defaultAutomaticCompactionPolicy: .enabled(
          trigger: .percentOfContextWindow(0.5)
      )
  )
```

Same exact configuration can work for all providers. The adapter handles the mechanics. The policy is yours. You can even define a different provider to summarize than those being used for inference.

Even if you were fully vibe-coding, I wouldn't want to reimplement this support in every fresh agent harness you build per project. For context, getting that architecture right took five consecutive pull requests and some inversions of the ownership model.

### 4. Powerful Tool Hooks

Beyond permissions, intercepting tool calls before and after execution opens up a range of use cases that execution policy alone can't cover.

Privacy is the most fun example to talk about this one: Apple's on-device inference and Private Cloud Compute offer a strong privacy guarantee by design. But the moment you're outside that (calling a remote model) what reaches the inference endpoint becomes your responsibility.

Redaction and rehydration is a pattern tool hooks make possible. You can strip PII from the data before it reaches the model by replacing a user's email with a placeholder the model can work with. Then, intercept tool calls before they execute to rehydrate those sentinels back to real values. And strip again on the way out if tool results contain sensitive data before they would otherwise be fed back to the model.

`ToolHook` intercepts tool calls at both points.

```swift
  public protocol ToolHook: Sendable {
      var name: String { get }
      var phases: Set<ToolHookPhase> { get }

      func beforeExecute(
          _ call: PendingToolCall,
          context: ToolExecutionContext
      ) async throws -> PendingToolCall

      func afterExecute(
          _ call: PendingToolCall,
          outcome: ToolCallOutcome,
          context: ToolExecutionContext
      ) async -> ToolCallOutcome
  }
```

`beforeExecute` receives the pending call and allows to inspect and/or instrument it (arguments modified, placeholders swapped in, or the call cancelled outright). `afterExecute` allows inspection and instrumentation of the outcome (letting you redact or reshape the result before it feeds back to the model).

With proper redaction, the model never sees what it shouldn't while the tools operate on real data.

Of course, this kind of privacy is only as good as your detection and replacement logic. A home-rolled redaction middleware would reasonably alarm a security expert, and I'm not claiming this solves the remote inference privacy problem in a comprehensive sense. But it does give you a principled interception point for simple, well-defined cases. Which is hopefully more than you have without AgentKitten.

---

## The part that makes evaluation possible in AgentKitten

Every `AgentSession` keeps a live `AgentTrace`: an append-only structured record of every event. Turn starts, tool calls with arguments, results, compaction events, validation outcomes, errors. Each entry carries a turn identifier, a monotonic timestamp, and a semantic kind.

```swift
  let entries = await session.trace.snapshot()

  for entry in entries {
      switch entry.kind {
      case .toolCallStarted(let call):  // tool name, arguments
      case .toolCallCompleted(let call, let outcome):  // result, hooks that ran
      case .compactionApplied:  // what was summarised, what was preserved
      case .turnCompleted(let status):  // completed, cancelled, or failed
      // ...
      }
  }
```

This is not a log but a structured record with a stable schema across providers, prompt changes, and time. That stability is what should make evaluation possible: compare runs, build test fixtures from real sessions, assert on tool call patterns, track whether a prompt change improved or regressed behavior.

If the scaffold regenerates this concept fresh every time, you can't do any of that. The abstraction being stable enough to evaluate was the goal from the start, not a feature added later.

---

## Questions I expect

- **Isn't this just a Swift *{Insert Famous Framework Name Here}* wannabe?**
  
  Yes, roughly. But there is good value on it being natively built for the platform in Swift, and possibly from being rather narrowly scoped.
  
- **Can't a coding agent just generate this?**
  
  Yes. But you can't effectively evaluate something that has a different shape every time you change it.

- **The abstraction leaks.**
  
  Possibly! It just tries to cover common cases cleanly and leave provider specifics for you to reach through with your custom implementation.
  
- **Shouldn't the provider own the loop?**
  
  Sometimes. Use the underlying SDK/API if you're building a single-provider chat feature. This is for when you need what the provider won't give you, or want to stay nimble to migrate between them.
  
- **Providers will absorb it all.**
  
  Good! The durable part should be the app-specific control surface they won't solve.

- **On-device constraints are a temporary phase.**

  On-device and frontier are in a permanent chase. I feel the gap shifts, but doesn't really close.

- **No one's asking for this.**

  Teams are reinventing it silently inside product codebases. Latent, not absent.

- **Show me production usage.**

  Not there yet.

---

## Where it stands

While I flattened the repository history before making it public, the repository **history of AgentKitten spanned more than 570 commits and 130 pull requests of rethinking the shape of things**.

And, yes, it is built using AI coding tools, but steered carefully and deliberately. The design decisions are mine. The iteration was painfully real: The tool hook design went through at least two architectures. Context compaction was born as an overly-simplistic retrofit, but ended as an automated (and highly customizable) one. And I lost count of how many iterations I went through to get to the current configuration/overrides architecture.

Just being honest, "I iterated on this a lot" is a more accurate description than just "I designed it."

It's still early: the test coverage/quality is being improved, the provider surface will grow, and some API edges will shift before a 1.0. I'm very open to input and collaboration.

The repository is at [https://github.com/fbeeper/agentkitten](https://github.com/fbeeper/agentkitten). 

Run `swift run Playground --help` to see examples of what it can do.

Looking forward for your input!
