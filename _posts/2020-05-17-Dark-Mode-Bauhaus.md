---
layout: post
title: Dark Mode Bauhaus
categories: design
excerpt: A little story about my Bauhaus-inspired decorations in Dark Mode.
decoration: circle
tags: [design, dark mode]
---

You may have noticed the little colorful geometric figures that decorate this site. Let me talk a bit about the process that brought them to me. And let's use it as an excuse to talk about Dark Mode too.

In terms of design, I wanted something somewhat minimalist. I chose Medium back in 2014 because of its design and I still wanted to keep it as a reference. After a lot of thought, I chose [Hyde](https://hyde.getpoole.com) as my base template because it was pretty much where I wanted to go.

First, I stripped the background color of the sidebar. I reduced the color palette to an even more minimal (now semantic) color palette. And, then, tuned the colors to my liking while providing accessible contrasts. 

Following my reference, I switched to a serif font. An ornamented font helps make it feel less technical. And, in a clean site, it still feels modern. And it [may (or not)](https://en.wikipedia.org/wiki/Serif#Readability_and_legibility) improve the readability of my body text.

At this point, I needed a touch of bright color to fully represent my taste.

I decided early on that I wanted my homepage to have three excerpts per page. Three posts called for three different graphics. And, maybe even three colors?

After *many* attempts, the design that sparked joy was the colorful geometric shapes you can see today. And, in a way, it is a homage to the hallmark of Bauhaus design:

Without getting into any detail, Wassily Kandinsky, who taught at the Bauhaus, studied shapes and color and theorized about their properties and relationships. Each color and shape was associated with some psychological properties and got inherently connected. From [these studies](https://www.documenta-bauhaus.de/images/docA_BI_7KandinskyW12015_132_04.jpg?w=1242) arose the well known yellow triangle, blue circle, and red square of the Bauhaus.

[Modern studies](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC3769683/) deem Kandinsky's findings not too accurate. Still, having [tested](https://www.getty.edu/research/exhibitions_events/exhibitions/bauhaus/new_artist/form_color/interactive/) myself, my choices coincided with Kandinsky's model. It does not make it correct, but it is serendipitous.

I feel this Bauhaus choice sharply (but beautifully) contrasts with the serif font that is *not* associated *at all* with the Bauhaus design. After all, are living an era of remixes.

Now, combining my initial color picks with the existing text was not going to be a recipe for success. I cared about providing solid readability in *every* scenario. So, I had to ensure proper color contrast of the text over the new graphics.

{% include image.html src='/public/img/2020-05-17-First-Color-Choice.png' retinaSrc='/public/img/2020-05-17-First-Color-Choice@2x.png' alt='A bright yellow triangle, a bright blue circle, and a bright red circle. Illegible dark grey text &ldquo;fbeeper&rdquo; on top.' caption='My initial out-of-context color choices. <br>The text is not easy to read.' %}

I rolled up my sleeves and found a [decent tool to find fitting contrast alternatives](https://app.contrast-finder.org/). The numerically obvious choices were not my cup of tea, so I kept tunning my colors till they worked. That is, I liked the individual colors, I felt they worked well together, they had a 4.5+ contrast ratio with my font color, and they looked smooth on the site.

{% include image.html src='/public/img/2020-05-17-Second-Color-Choice.png' retinaSrc='/public/img/2020-05-17-Second-Color-Choice@2x.png' alt='A light yellow triangle, a light blue circle, and a light red circle. Legible dark grey text &ldquo;fbeeper&rdquo; on top.' caption='My light mode color choices (with proper contrast.)' %}

To support dark mode, I had to play a game with more variables. I picked the previous colors on a light background. They did not match the new dark environment. Even when having a theoretically correct contrast.

Besides stiving for a good contrast ratio for the text, dark mode colors need an appropriate brightness to be easy on the eye. So, with some sweat but no tears, I achieved my new darker, and contrast-worthy colors.

{% include image.html src='/public/img/2020-05-17-Third-Color-Choice.png' retinaSrc='/public/img/2020-05-17-Third-Color-Choice@2x.png' alt='Dark mode shapes and colors: A dark yellow triangle, a dark blue circle, and a dark red circle. Legible white text &ldquo;fbeeper&rdquo; on top.' caption='My dark mode color choices.' %}

In hindsight, I knew all this from watching Apple WWDC talks on dark mode and participating in building color schemes for an iOS app. But like this, it felt more personal and worth sharing. Also, having 100% creative freedom made it more fun.

Interested in knowing why the pentagon is orange? Should I talk more about creating semantic color palettes? What about dark mode implementation in CSS? Ping me @fbeeper or [leave a comment](https://github.com/fbeeper/fbeeper.github.io/issues/3).