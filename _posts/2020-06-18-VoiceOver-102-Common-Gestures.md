---
layout: post
title: "VoiceOver 102: Common Gestures"
categories: accessibility
excerpt: Becoming a fluid user in VoiceOver is just a few gestures away.
decoration: square
tags: [accessibility, iOS, VoiceOver]
---

[Three basic finger gestures](/2020/06/11/Accessibility-Audit-VoiceOver-101/) can get us quite far with VoiceOver. But adding a few more things to our tool-belt will help us becoming fluid VoiceOver users and/or auditors. 

Here are the tools I would take to a desert island with me:

## Accessibility Shortcut

On the first article, we activated VoiceOver with Siri. It feels modern, sure. But, to be honest, it is not particularly practical to me.

If we go to "Settings" → "Accessibility" → "Accessibility Shortcut," we can select "VoiceOver" on that list.

With this setting, **triple tapping** the home or side button (depending on the device) will toggle VoiceOver. So convenient! Right?

Now, let's go back to interacting with our apps.

## Continuous Swipe (and Tap)

Sooner or later, one may discover naturally (or accidentally 😅) that a **single tap** on the screen moves the focus to the accessible element touched.

We can actually **continuously swipe** around the UI. VoiceOver's focus will swiftly follow our touch. And additional **single taps** will activate the element focused under our (uninterrupted) swipe.

<div class="message">
⚠️ When purposefully leveraging vision or spatial memory, these gestures can be very powerful. However, I don't particularly like (or would recommend) to solely rely on these gestures as the main way to use/audit with VoiceOver. Depending on total or partial vision can make us inadvertently use queues that are not clear or available to others.
</div>

## Scroll

To scroll, we only need the **3 finger swipe**. Up, Down, Left, or Right.

That easy!

## Two Finger Scrub

With the gestures we learned so far, going back on navigation or dismissing a modal may be a hassle. 

**Swiping a Z shape with two fingers** anywhere on the screen will solve it. This gesture will perform those actions, and it will save us a lot of time. And it will rescue us when feeling trapped too.

<div class="message">
ℹ️ The direction (or shape) of this Z does not matter! It is only necessary to go back and forth thrice. But, while getting used to VoiceOver, remembering the Zorro can be a fun mnemotechnic technique.
</div>

This gesture may not be supported in custom implementations. But it is so useful that it will be *really* expected by our users. Let's not forget adding it to our self-auditing notebook when it does not work!

## Practice, practice, practice

We may be starting to question our memory skills to remember these gestures. And, to the best of my knowledge, there is only one way to become fluent and internalize these gestures: practice.

Just keep swiping!
