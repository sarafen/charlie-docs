---
layout: page
title: Templates
permalink: /templates/
nav_order: 2
has_children: true
---

# Templates

Templates end in a `.ms` extention. A Template can contain anything a valid `.html` file can, in addition to [Mustache](https://mustache.github.io/mustache.5.html) Tags. They are used to setup the display of a specific area of content across a given site. Their main use-case is in preventing repeat code for every individual URL found at a domain.

In this way, several URLs could share the same Template, and any updates to that Template will be reflected across all those URLs.
