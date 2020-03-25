---
layout: page
title: Theme Structure
permalink: /theme-structure/
parent: Structure
nav_order: 4
---

# Theme Structure

All themes are stored within the `/themes/` folder.

Each theme is stored in its own unique folder `/themes/{theme_name}/`

The most basic theme must contain the following.

```html
_partials/
page.ms
```

A simple theme may look like this.

```html
css/style.css
imgs/logo.svg
js/scripts.js
_partials/
page.ms
```

In this example the `page.ms` is a Template. It will be used as the Template for any url you visit at your site.

For example:

```html
domain.com/
domain.com/about
domain.com/contact
```

All three of these would use the `page.ms` Template since there are no other Templates within the example Theme.

To understand how Templates are loaded and overridden, please check out the [Template Cascade](/templates/template-cascade).
