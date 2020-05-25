---
layout: post
title: Happy Global Accessibility Awareness Day
categories: accessibility
excerpt: Starting a new journey by sharing my experience on accessibility.
decoration: square
tags: [accessibility, iOS, design]
---

Happy [Global Accessibility Awareness Day](https://globalaccessibilityawarenessday.org/)!

I have been an accessibility advocate for a long time, but most of my conversations have happened in professional contexts and applied to specific projects. This blog was born, among other things, to provide a space for a larger conversation on this subject. 

Today feels like a great day to start it.

Accessibility is becoming a trending topic in the iOS community, and that makes me really happy.

But it also adds up some pressure: anything I might want to say has probably already been discussed before. 

However, I feel it is less about pure facts and unmovable truths and more about one’s journey. I would like to share with you my continuous process to learn and develop more accessible iOS apps, the roadblocks I found on the way, and some tips to hopefully make your trip a bit easier.

## We All Start Somewhere

Sometimes, when passionately defending accessibility (the classic “we need to have more empathy and fewer excuses”), advocates risk making people feel they are less for not having thought or implemented it already. 

If something is not accessible in your app, it means there is a critical bug in it. But if that’s your case, don’t let shame paralyze you. We all start somewhere.

In this first post, I would like to focus on how accessibility applies to everyone, and also start breaking down the main obstacles we may find on our way as iOS developers.

## Accessibility is for all

[One billion people](https://globalaccessibilityawarenessday.org/), about an eighth of the world’s population, receive and experience stimuli from the world in diverse visual, auditive, motor and/or cognitive ways. 

Even more, we all have had or will have different accessibility needs throughout our lives, even if only circumstantially or temporarily. 

Have you ever had your pupils dilated for an eye exam and tried to use your iPhone to find a ride-share? Do you know a family member who has developed presbyopia with age and needs a bigger font size to read your texts? 

Accessibility comes in many shapes and forms. It is not for a few, it is for all of us.

## Main Obstacles

We are empathetic to people’s diverse needs and want to give everyone equal opportunities when using our apps.

Additionally, Apple has done an outstanding job to provide accessible platforms. Even without explicitly thinking about accessibility, building iOS apps from scratch with system controls allows our apps to be accessible *by default*.

So... Why isn’t my work perfectly accessible then?!

In my experience, even in the best-case scenario, there are lots of things to consider, including a few hugely underestimated life basics:

* We don’t know what we don’t know.
* We always have tons of competing priorities.
* Even the smallest gaps take effort to bridge.
* Life, happens.

So don't feel bad if you haven't nailed accessibility instinctively. Instead, join me taking steps towards ensuring your code is accessible *by default* too.

## We don’t know what we don’t know

One of the main reasons we need to raise awareness about accessibility is because we are often oblivious to the gaps in our knowledge.

Looking back in time, I did not have any obvious need for accessibility features. For a while, I lived building apps being quite unaware of accessibility. Not that I did not care, or I did not have the time. I just simply did not know enough to properly click into this area.

*Dramatized:* Where I had a pretty simple set of layouts and a few fonts, colors, and images, now I have a myriad of interesting concepts to wrap my head around and adapt in my workflow:

> VoiceOver, Reduce transparency, On/Off labels, Grayscale, Audio descriptions, Word prediction, Mono audio, AssistiveTouch, Button shapes, Speak screen, Gliding cursor speed, Subtitles, Captioning, Closed captions, Switch control, Larger text, Speech, Increase contrast, Invert colors, Cursor color, Dictation, Siri, Bold text, Larger cursor, Zoom, Reduce motion, Hearing aids, Sticky keys, Gestures, Auto scanning, Safari reader, Guided access, Slow Keys, Touch accommodations.
> 
> From WWDC'16 [Auditing Your Apps for Accessibility](https://developer.apple.com/videos/play/wwdc2016/407/) [^1]

Thankfully, as a developer, I believe this dichotomy between fascinating and complex defines seme our most interesting challenges.

I will never be able to fully understand or represent people with consequential accessibility needs that are different than mine. But I stopped feeling bad for being late. Instead, I focused on doing my best to include everyone. I work hard to make my apps as accessible as possible and, honestly, it’s become one of my favorite parts of this work.

Want to share your experience or are looking for guidance? Let’s chat [here](https://github.com/fbeeper/fbeeper.github.io/issues/4) or reach me @fbeeper.

See you in my [next article on accessibility & competing priorities](/accessibility/2020/05/25/Accessibility-Competing-Priorities/)!

---


[^1]: Actually, today there are many more concepts that didn’t exist or weren’t represented in that 2016 slide, like Display Accommodations, Voice Control, Dynamic Type, Zoom, Live Listen, and probably even more.