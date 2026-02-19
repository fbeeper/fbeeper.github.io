---
layout: post
title: Dark Mode Bauhaus
categories: design
hidden: true
excerpt: A little story about my Bauhaus-inspired decorations in Dark Mode.
decoration: circle
tags: [design, dark mode]
---

When building this site I went for a minimalistic design. Inspired by Medium, an ornamented serif font helps make it feel less technical. The otherwise plain design keeps it modern. And to make it more personal, I added some bright colored geometrical decorations. 

They are a homage to the hallmark of Bauhaus design:

Without getting into detail, Wassily Kandinsky, who taught at the Bauhaus, studied shapes and color and theorized about their properties and relationships. Each color and shape was associated with some psychological properties and got inherently connected. From [these studies](https://www.documenta-bauhaus.de/images/docA_BI_7KandinskyW12015_132_04.jpg?w=1242) arose the well known yellow triangle, blue circle, and red square of the Bauhaus. [Modern studies](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC3769683/) deem Kandinsky's findings not too accurate. Still, having [tested](https://www.getty.edu/research/exhibitions_events/exhibitions/bauhaus/new_artist/form_color/interactive/) myself, my choices coincided with Kandinsky's model. It does not make it correct, but it is serendipitous.

I feel this Bauhaus choice sharply (but beautifully) contrasts with the serif font that is *not* associated *at all* with the Bauhaus design. After all, are living an era of remixes.

## Accessible Color

Now, combining my initial color picks with the existing text was not going to be a recipe for success. I cared about providing solid readability in *every* scenario. So, I had to ensure proper color contrast of the text over the graphics.

{% include image.html src='/public/img/2020-05-17-First-Color-Choice.png' retinaSrc='/public/img/2020-05-17-First-Color-Choice@2x.png' alt='A bright yellow triangle, a bright blue circle, and a bright red circle. Illegible dark grey text &ldquo;fbeeper&rdquo; on top.' caption='Sample of my initial out-of-context color choices. <br>The text is not easy to read.' %}

From here, the closest colors that would satisfy legible contrast ratios did not work for me. So I kept tuning them until they did. That is, I liked the individual colors, they worked together, they had a 4.5+ contrast ratio with my font color, and they looked good on the site.

{% include image.html src='/public/img/2020-05-17-Second-Color-Choice.png' retinaSrc='/public/img/2020-05-17-Second-Color-Choice@2x.png' alt='A light yellow triangle, a light blue circle, and a light red circle. Legible dark grey text &ldquo;fbeeper&rdquo; on top.' caption='My light mode color choices (with proper contrast.)' %}

## Dark Mode

To support dark mode, I had to play a game with more variables. The colors for the light background did not match the new dark environment even when having a theoretically correct contrast. Dark mode colors need a different luminosity to be easy on the eye:

{% include image.html src='/public/img/2020-05-17-Third-Color-Choice.png' retinaSrc='/public/img/2020-05-17-Third-Color-Choice@2x.png' alt='Dark mode shapes and colors: A dark yellow triangle, a dark blue circle, and a dark red circle. Legible white text &ldquo;fbeeper&rdquo; on top.' caption='My dark mode color choices.' %}

None of this is novel or mindblowing, but I felt it was a short and sweet sample to share what is behind the scenes when designing for accessibility and dark mode.

--

<div class="message">
✍️ Edited on Sunday, Nov 15, 2020: Shortened article.
</div>