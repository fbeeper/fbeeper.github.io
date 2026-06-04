---
layout: post
title: "Exploration Got Cheap.<br/>Human Review Did Not."
categories: agentkitten
excerpt: "Software Engineering exploration got cheaper. A chunk of review process did too. A human understanding changes and standing behind it... did not."
decoration: circle
permalink: agentkitten/2026/06/04/Exploration-Got-Cheap-Human-Review-Did-Not/
tags: [agentkitten, AI, coding, agent]
---

For as long as I've worked in the field, software architectures that last (the ones you want to, not the ones you _have_ to live with) often come from knowing the bird's eye view. However, when the calendar is tight, exploration gets squeezed. So we know how to commit to _a_ direction quite early. We build plans with what's known while trying to prepare for what isn't. We break it into steps, and commit to discover the rest of the shape through delivery. This can still be good discipline (arguably is more agile!), and we make it work.

However, the tax on exploration has dropped. AI has made it cheaper (setting aside the cost of tokens): I can generate a grand version, _see_ for myself how it holds, and push it further in the time I have. 

It certainly does not remove the human part. You can fake it for social media, but the initiative, judgement, and critical thinking are still ours. We decide what's done, and whether the shape is right.

And the same goes at the other end: once a concept is deeply explored, breaking it into deliverable pieces (even when that means big refactors) got cheaper too.

It is tempting to brush that last bit and conclude the whole software-engineering job got cheaper and we can just ship the big thing.

It didn't. One part at the center didn't move at all.

## The part that didn't move

Even code reviewing split in two. 

A serious chunk got cheaper: AI reviews code better and better. They are fast and tireless. They can catch many things we'd be embarrassed to ship (or even show another human).

So, this is raising the floor of what's worth your time. But... it does not shorten the human's afternoon. And it certainly does not transfer ownership.

That is the part that didn't get cheaper. A person understanding your change and standing behind it, gated by human attention. That's as scarce as it's ever been.

The trap is letting the cheapness of exploration leak: You explore big, it works, and you try to deliver the exploration artifact. 

But **the output of exploration is understanding, not a merge.**

## Why chewable isn't negotiable

Assume the "cheap" review already happened. The developer ran the machine over their own change and fixed what it found. What's left, is the human part.

Today, I still struggle with how casually large PRs are accepted. A Swift pull request north of 2000 lines is routinely treated as a normal thing to ask another engineer to review. It is not.

At that size, you can't review it without extreme guidance from the author. And even with it... you drift. 

When attention thins out, you start pattern-matching, you validate the shape and miss the substance: Understanding it.

**Reviewers are not a gate for a LGTM.** 

They are there to find what you missed. The blind spots. The assumptions. The places where understanding was incomplete. We are there help each other grow (or fail less spectacularly... that is, if we let our reviewers be effective).

Tests count too. A 2000 line PR that is “only 800 lines of feature code” is still a 2000-line PR. It's so tempting to wave off size (I've done it myself!) when "most of it is tests." But tests stay to subtly encode assumptions, and they become a template for the next change. Skim them in review and you won't save time... you will have shipped fake peace of mind for the future.

## A small but illustrative example

[AgentKitten](https://github.com/fbeeper/agentkitten), my new Swift library for building AI agents, is meant to be agnostic to inference providers. Pick an inference model provider and swap it at "no cost". That promise only holds if adding one provider is tractable. So, adding OpenAI as a new provider was a test of the architecture, not just a feature.

I explored the whole thing first, exactly as the new economics invite: I worked with a coding agent for a complete OpenAI provider modeled on the existing ones. It came back _fast_. One rather large change covering the whole surface: text, tools, structured output, token counting, compaction. Of course it compiled and tests passed. And it worked on every manual test I threw at it.

As exploration, a success: in an afternoon I had an end-to-end answer to "what does this provider look like across the whole surface?"

As delivery, unmergeable: Long stretches were a near word-for-word clone of the existing Anthropic provider with the nouns swapped. A clone inherits assumptions faster than you can inspect them. I couldn't review it without drifting. As expected, I closed it.

**Code I cannot faithfully review is one I cannot own.**

I knew that the provider surface is meant to be more modular. I designed the API boundary for this. A provider isn't one all-or-nothing conformance. It is a set of responsibilities. Some stacked, some not. Each gated by its own seam: text inference, tool calls, structured inference, and history compaction.

You should be able to stop at any feature and still have a complete and honest provider. A text-only inference provider isn't half-finished, it's finished if it says "I don't do tools" out loud.

That "large but cheap" exploration is now meant to be broken down in smaller bits, a process that is also become relatively cheap.

The angle for cutting this one was obvious to me in this case: cut PRs to fulfill the 4 main responsibilities of a provider. I broke the work down as separate and stacked branches in git worktrees. One capability per branch, each built on the last.

With this I:

- Made my reviews feasible. I could read a change end to end without drifting off.
- Proved a partially-featured provider can ship and fully work.

And, it made the AI reviews tangibly better too. A focused diff gets a focused review, the model started catching things that actually mattered. With both of us so much more focused, I was able to improve a bunch of things along the way.

By the end, the work stopped being a clone exactly where cloning was ineffective (or plain wrong). But the exploration stayed valuable without forcing reviews to inherit its size.

## TL:DR;

Software Engineering exploration got cheaper. A chunk of review process did too. A human understanding changes and standing behind it... did not.

**Explore big and fast**. Push architecture further than you otherwise would.

**Deliver it small and honest**. Broken down into chewable pieces a person (and the model) can actually understand and own. 

Large exploration and small delivery are not contradictory. They are the same workflow.
