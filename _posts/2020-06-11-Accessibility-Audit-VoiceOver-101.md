---
layout: post
title: "Accessibility Audit: VoiceOver 101"
categories: accessibility
excerpt: The most basic audit may be the most powerful one.
decoration: circle
tags: [accessibility, iOS, VoiceOver]
---

Anyone, regardless their knowledge, can quickly get started and audit very important aspects of accessibility in an iOS app. Let me start with VoiceOver.

## VoiceOver

In short, VoiceOver is a screen reader provided by Apple in iOS, iPadOS, watchOS, macOS, and tvOS. It allows blind and low vision users to enjoy the software on these platforms.

Using it, we can learn some of the most fundamental concepts of accessibility. And we can also start exposing important features of our apps where we need to improve.

## First Steps

Unlock an iPhone or iPad, open an (your?) app, and ask Siri to activate VoiceOver. 

At this point, VoiceOver focuses on a UI element on the screen and reads it out loud.

### Navigation

**Swipe from left to right** anywhere on the screen. This should move the focus to the next UI element. Again, VoiceOver reads it.

{% include image.html src='/public/img/2020-06-11-Swipe/LightL2RSwipe.gif' darkSrc='/public/img/2020-06-11-Swipe/DarkL2RSwipe.gif' alt='Left to Right Swipe Animation' %}

Now, **swipe from right to left**. We are back at the first item.

{% include image.html src='/public/img/2020-06-11-Swipe/LightR2LSwipe.gif' darkSrc='/public/img/2020-06-11-Swipe/DarkR2LSwipe.gif' alt='Left to Right Swipe Animation' %}

For now, this is all we need to navigate the interface.

### Interaction

Let's level up. Swipe to a button. Now, **double-tap** anywhere on the screen. That will activate that button.

{% include image.html src='/public/img/2020-06-11-Swipe/Light1F2Tap.gif' darkSrc='/public/img/2020-06-11-Swipe/Dark1F2Tap.gif' alt='Left to Right Swipe Animation' %}

We are almost experts at VoiceOver now. It is magical.

### Immersion

We could stop here, but my experience tells me to give one extra bit: Without hesitation, let's do a **triple-finger triple-tap** anywhere on the screen. (It's as simple as it sounds: tap thrice with three fingers.)

{% include image.html src='/public/img/2020-06-11-Swipe/Light3F3Tap.gif' darkSrc='/public/img/2020-06-11-Swipe/Dark3F3Tap.gif' alt='Left to Right Swipe Animation' %}

Welcome to Screen Curtain. The screen went dark, but the screen and the app are still very much alive.

I would argue this is what we should have been seeing all along. Attempting to navigate our app in this environment will provide an immense amount of perspective about how accessible it is. 

If we cannot use it, it is likely our users won't be able to use it either.

## Our roadmap

With these four (4!) simple gestures I have identified some of the most foundational accessibility issues in iOS apps. I hope you can too.

**I look to validate that all UI elements are reachable and properly described.** In other words, I note all the things I cannot navigate consistently, as well as those that are not clearly described with the VoiceOver reading.

What is the issue? Where in the app? How important is it? How to reproduce?

Answering questions like this certainly helps to lay out a roadmap. While it may look over-simplistic, the results of this self-auditing can be a strong foundation towards making an app accessible.

Speak soon!
