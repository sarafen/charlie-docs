---
layout: page
title: Template Cascade
permalink: /templates/template-cascade/
parent: Templates
nav_order: 5
---

# The Template Cascade

Templates are loaded dynamically based on a cascade. The first file found is loaded.

At a minimum your theme must include a `page.ms` file in the theme root, as this is always the last stop in the cascade.

## Home

```html
domain.com/

--> themes/{active-theme}/pages/index.ms
----> themes/{active-theme}/page.ms
```

## Pages

```html
domain.com/{request}/

--> themes/{active-theme}/pages/{request}.ms
----> themes/{active-theme}/page.ms
```

## Posts

```html
domain.com/{post_type}/{request}/

--> themes/{active-theme}/{post_type}/{request}.ms
----> themes/{active-theme}/post-{post-type}.ms
------> themes/{active-theme}/post.ms
--------> themes/{active-theme}/page.ms
```

## Post Feeds

```html
domain.com/{post_type}/feed/{format}/

--> themes/{active-theme}/feed{format}-{post-type}.ms
----> themes/{active-theme}/feed{format}.ms
----> (built-in default template)
```

## Post Archives

```html
domain.com/{post_type}/pg/{num}/

--> themes/{active-theme}/archive-{post-type}.ms
----> themes/{active-theme}/archive.ms
----> (built-in default template)
```

## 404

If no content can be found for a request, then the `themes/{active-theme}/pages/404.ms` is used.
