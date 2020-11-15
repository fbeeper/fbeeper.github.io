---
layout: post
title: Build a blog with Jekyll
categories: development
excerpt: What made this site possible?
decoration: triangle
tags: [jekyll, github, web]
---

My goal was to build a fast and simple site. I wanted to offer good user experience and privacy. I was looking to move away from the controversial World Wide Web of 2020 ([my old Medium blog](https://medium.com/@imho_ios)*\*cough\**). 

A clean, static site offers me the opportunity to control all these things, checks all the boxes to be trendy, and pushes me to step out of my Swift and iOS comfort zone.

I would like to start this blog by giving explicit credit to all the sources that helped me create it.

The main building blocks include:

* [Jekyll](https://jekyllrb.com) as the static site generator behind the scenes. 
* [GitHub Pages](https://pages.github.com), providing much more than hosting.
* And [Hyde](https://hyde.getpoole.com) offered a solid foundation theme to build on.

But many other tools, snippets, and docs helped me shape the site. Here is a quick reference:

* Jekyll has some wonderful plugins ([supported](https://pages.github.com/versions/) by GitHub Pages:)
  - [jekyll-sitemap](https://github.com/jekyll/jekyll-sitemap), to improve SEO and accessibility with a site map.
  - [jekyll-seo-tag](https://github.com/jekyll/jekyll-seo-tag), to generate SEO metadata.
  - [jekyll-feed](https://github.com/jekyll/jekyll-feed), to provide a feed for Atom readers.
  - [jekyll-mentions](https://github.com/jekyll/jekyll-mentions), to simplify @ mentions.
  - [jekyll-gist](https://github.com/jekyll/jekyll-gist), to make Github Gist embeds as simple as they can be.
* I also added other custom add-ons, thanks to:
  - [Twitter Cards on Jekyll](https://brianbunke.com/blog/2017/09/06/twitter-cards-on-jekyll), by Brian Bunke + [Twitter's reference](https://developer.twitter.com/en/docs/tweets/optimize-with-cards/overview/summary).
  - [Reading Time without Plugins](https://carlosbecker.com/posts/jekyll-reading-time-without-plugins), by Calos Becker.
  - [Jekyll Heading Anchors](https://github.com/allejo/jekyll-anchor-headings), a great solution without plugins or JS.
  - Plain link to share posts with [Tweet Button](https://developer.twitter.com/en/docs/twitter-for-websites/tweet-button/overview).
  - Simple image captions following [this advice](https://stackoverflow.com/a/43045614).
* The [Liquid](https://shopify.github.io/liquid/) docs were excellent to help me get used to this template language used by Jekyll.
* And, last but not least, [Goat Counter](https://www.goatcounter.com), is powering simple and respectful analytics. See [Privacy](/licensing/#privacy) for more info.

Shifting gears to design and accessibility, these were highly valuable:

* I got actionable feedback to improve accessibility from:
  - [Lighthouse](https://developers.google.com/web/tools/lighthouse) in Google Chrome.
  - [WAVE Web Accessibility Evaluation Tool](https://wave.webaim.org).
  - [ADAScan](https://www.adascan.com/).
* [W3C's WAI-ARIA](https://www.w3.org/TR/wai-aria-1.1/) was a useful reference to keep around.
* [The A11Y Project](https://a11yproject.com/posts/never-use-maximum-scale/) has some enlightening articles (at least for someone new to web accessibility.)
* [Contrast Finder](https://app.contrast-finder.org/) helped me build a proper color scheme.
* [Source Serif Pro](https://github.com/adobe-fonts/source-serif-pro) and [Source Code Pro](https://github.com/adobe-fonts/source-code-pro) by Adobe (under the [Open Font License](https://scripts.sil.org/cms/scripts/page.php?site_id=nrsi&id=OFL)) found in and provided by [Google Fonts](https://fonts.google.com). 
* [Font Awesome](https://fontawesome.com) supplies the icons all around.
* Syntax highlighting is heavily inspired by [Xcode 11](https://developer.apple.com/xcode/), and diff highlighting from [Github](https://github.com/desktop/desktop/issues/5027).
* I used [The Shapes of CSS](https://css-tricks.com/the-shapes-of-css/) on CSS-Tricks for my decorative graphics.
* [Supporting Dark Mode in Your Web Content](https://developer.apple.com/videos/play/wwdc2019/511/) from Apple's WWDC, showed me how to support dark mode and also exposed me to CSS variables.

I may come back with more details in the future, so... stay tuned!
