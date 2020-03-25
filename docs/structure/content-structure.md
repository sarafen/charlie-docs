---
layout: page
title: Content Structure
permalink: /content-structure/
parent: Structure
nav_order: 3
---

# Content Structure

All content is stored within the `/content/` folder, and structured as follows.

## Home

```html
content/pages/index.md
```

## Pages

```html
content/pages/{name}.md
```

examples:

```html
content/pages/about.md
content/pages/work.md
content/pages/blog.md
```

## Posts

```html
content/{post_type}/{name}.md
```

examples:

```html
content/work/moby-dick.md
conten/blog/welcome-to-my-blog.md
```

### Post Feeds

Valid RSS Atom 1.0, and JSONFeed are provided dynamically, and can be accessed by navigating to:

```html
domain.com/{post_type}/feed/{format}/
```

examples:

```html
domain.com/blog/feed/rss/
domain.com/blog/feed/json/
```

### Post Archives

Paginated Archive listings are provided dynamically, and can be accessed by navigating to:

```html
domain.com/{post_type}/pg/{num}/
domain.com/{post_type}/pg/{num}/
```

examples:

```html
domain.com/blog/pg/100/
domain.com/blog/pg/19/
```

Note: Archives for `blog` Post Types are enabled by default. Any custom Post Types you create will need to be enabled in your `config.json` file. Please see [configuration](/configuration) for more information.

## Blocks

Blocks are useful when you need to have a small piece of content repeat across pages, but you don't want to manually write out all the html within a `.ms` template file. This keeps your content within a `.md` file for easier access and formatting.


```html
content/_blocks/{name}.md
```

examples:

```html
content/_blocks/intro_blurb.md
content/_blocks/sponsor_me_on_patreon_message.md
```
