---
layout: page
title: Using Templates
permalink: /templates/using-templates/
parent: Templates
nav_order: 6
---

# Using Templates

Templates can be simple HTML.

```html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="utf-8" />
<title>Site Title Here</title>
</head>

<body>
    <h1>heading here</h1>
    <p>a paragraph here</p>
</body>
```

But are most powerful when you use the built in [Mustache](https://mustache.github.io/mustache.5.html) Tags to dynamically load things.

{% raw %}
```html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="utf-8" />
<title>{{#title}} {{title}} | {{/title}}{{site_title}}</title>
</head>

<body>
    <h1>{{title}}</h1>
    {{{content}}}
</body>
```
{% endraw %}

In this example the {% raw %}`{{#title}} {{title}} | {{/title}}`{% endraw %} portion uses Mustache's false check to determine if the current URL has a `title` defined in its Content File's Frontmatter. If so then it will output the value of the `title`.

```html
---
title: About Page
---

# About Page

About content here.
```

The `site title` is then output from the Globally defined `site_title` in the `config.json` file.

```js
{
    "globals": {
        "domain"                : "website.com",
        "site_title"            : "A Website, On Mars",
        "site_description"      : "a website that has stuff on it",
        "author"                : "A. Person"
    },

}
```

Further down in the body the `title` is output as a heading for the page. And the page's `content` pulled from its Content File's `content` area is output.

Please note that the `content` has three {% raw %}`{{{}}}`{% endraw %} around it, because it is not just outputting raw text but instead formatted html. This is a convention of Mustache's syntax. If you forget the extra bracket it will not render correctly.

Rendering fully, the final output from the above snippets would look like this.


```html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="utf-8" />
<title>About Page | A Website, On Mars</title>
</head>

<body>
    <h1>About Page</h1>
    <p>About content here.</p>
</body>
```

This enables you to define a value one time and reuse it elsewhere, or to pull in a dynamic value that may change from URL to URL. In this instance, if you navigated away to another page then the `title` and `content` values would output different information automatically.

## Page Templates

They are dynamically loaded for Home, and first-level URLs.

```
domain.com/
domain.com/about
domain.com/contact
domain.com/work
domain.com/blog
```

The General Page Template can be found at `/themes/{active-theme}/page.ms`

Specific Page Templates can be found at `/themes/{active-theme}/pages/page-title-here.ms`

To understand how Templates are loaded and overridden, please check out the [Template Cascade](/templates/template-cascade).

## Post Templates

They are dynamically loaded for second-level URLs, and nest under their respective content type parent.

```
domain.com/blog/hello-mars/
domain.com/blog/goodbye-pluto/
domain.com/work/moby-dick/
domain.com/work/gallery-show-seven/
```

The General Post Template can be found at `/themes/{active-theme}/post.ms`

Specific Post Type Templates can be found at `/themes/{active-theme}/post-{post-type}.ms`

Specific Post Templates can be found at `/themes/{active-theme}/{post-type}/{specific-post-title-here}.ms`

To understand how Templates are loaded and overridden, please check out the [Template Cascade](/templates/template-cascade).

## Post Feed Templates

They are dynamically loaded for a valid Post Type, followed by `feed` in the second-level, and a valid Format in the third-level

```
domain.com/blog/feed/rss/
domain.com/blog/feed/json/
domain.com/writing/feed/rss/
domain.com/writing/feed/json/
```

All Feeds come in two formats: [Atom 1.0 RSS](https://tools.ietf.org/html/rfc4287) & [JSON Feed](https://jsonfeed.org/version/1).

By default the Post Type `blog` is enabled to have a Feed. Any other Post Types you create must have their respective Feeds enabled through your `config.json` file. See [Configuration](/configuration) for more details.

The General Feed Template can be found at `/themes/{active-theme}/feed.ms`

Specific Feed by Post Type Templates can be found at `/themes/{active-theme}/feed{format}-{post-type}.ms`

If you do not include a Feed Template of any kind in your theme, the format specific one baked into Charlie will be used.

The RSS version contains the following code to model from:

{% raw %}
```html
<?xml version="1.0" encoding="utf-8"?>
<feed xmlns="http://www.w3.org/2005/Atom">

<title>{{author}}'s {{post.type}} Feed</title>
<subtitle>{{site_description}}</subtitle>
<link href="http://{{domain}}/feed/" hreflang="en" rel="self" type="application/atom+xml"/>
<link href="http://{{domain}}/" hreflang="en" rel="alternate" type="text/html"/>

<updated>2012-07-15T10:50:43+10:00</updated>
<generator uri="http://charliecms.com/" version="1.0">Charlie</generator>

<author>
<name>{{author}}</name>
<uri>http://{{domain}}</uri>
</author>

<id>tag:{{domain}},2012:/feed/</id>
<rights> {{current_year}} {{author}}</rights>

{{#post.feed}}
		{{#item}}

		<entry>
			<title>{{title}}</title>
			<id>{{id}}</id>
			<updated>{{date}}</updated>
			<link rel="alternate" type="text/html" href="{{link}}" />
			<content type="xhtml" xml:lang="en">
				<div xmlns="http://www.w3.org/1999/xhtml">

					<summary>{{summary}}</summary>

				</div>
		   </content>
		</entry>

		{{/item}}
{{/post.feed}}

</feed>
```
{% endraw %}

The JSON version contains the following code to model from:

{% raw %}
```js
{
  "version": "https://jsonfeed.org/version/1",
  "user_comment": "This feed allows you to read the posts from this site in any feed reader that supports the JSON Feed format. To add this feed to your reader, copy the following URL â€” https://jsonfeed.org/feed.json â€” and add it your reader.",
  "title": "JSON Feed",
  "description": "{{site_description}}",
  "home_page_url": "{{domain}}",
  "feed_url": "https://jsonfeed.org/feed.json",
  "author": {
    "name": "{{author}}",
    "url": "{{domain}}"
  },
  "items": [
  {{#post.feed}}
	{{#item}}
    {
      "title": "{{title}}",
      "date_published": "2017-05-17T08:02:12-07:00",
      "id": "https://jsonfeed.org/2017/05/17/announcing_json_feed",
      "url": "{{link}}",
      "content_html": "{{content}}"
    }
	{{/item}}
  ]
  {{/post.feed}}
}
```
{% endraw %}

To understand how Templates are loaded and overridden, please check out the [Template Cascade](/templates/template-cascade).

## Post Archive Templates

They are dynamically loaded for a valid Post Type, followed by `pg` in the second-level, and a number in the third-level

```
domain.com/blog/pg/100/
domain.com/writing/pg/19/
```

By default the Post Type `blog` is enabled to have an Archive. Any other Post Types you create must have their respective Archives enabled through your `config.json` file. See [Configuration](/configuration) for more details.

The General Archive Template can be found at `/themes/{active-theme}/archive.ms`

Specific Archive by Post Type Templates can be found at `/themes/{active-theme}/archive-{post-type}.ms`

If you do not include an Archive Template of any kind in your theme, the one baked into Charlie will be used. It contains the following code to model from:

{% raw %}
```html
{{>header}}

<body>

<h1>{{post.type}} Archive</h1>

{{#post.archive}}

{{#item}}

<article>
	<h2><a href="{{{link}}}">{{title}}</a></h2>
	<time class="article-date">{{date}}</time>

	<p>{{summary}}</p>

</article>

{{/item}}

{{#post.pagination}}
<nav>
<ul>
{{#item}}
    <li>{{#link}}<a href="{{link}}">{{/link}}{{num}}{{#link}}</a>{{/link}}</li>
{{/item}}

</ul>
</nav>
{{/post.pagination}}

{{/post.archive}}


{{>footer}}
```
{% endraw %}

To understand how Templates are loaded and overridden, please check out the [Template Cascade](/templates/template-cascade).

## Partials Templates

Partials Templates can be found at `/themes/{active-theme}/_partials/`

They are then included in other templates with the following Tag convention:

{% raw %}
```html
{{>partial_name_here}}
```
{% endraw %}

They can be especially useful for repeating HEADER or FOOTER element areas across pages. If every page includes the same header, with the same logo, and the same menu it can be a good idea to put that into a Partial, and then include it in all your templates so you don't repeat yourself unnecessarily.

## Localized Variables

There are a few Variables available on a given Page or Post that can be called via Mustache Tags without having to first be defined in a Frontmatter block. They are usually generated dynamically under the hood.

Name          | Tag
------------- | -------------
content  | {% raw %}`{{{content}}}`{% endraw %}
link  | {% raw %}`{{{link}}}`{% endraw %}


## Calling Variables

{% raw %}
```html
{{title}}

{{date}}

{{{content}}}
```
{% endraw %}

## Calling Partials

{% raw %}
```html
{{>header}}

{{>footer}
```
{% endraw %}

## Calling Blocks

{% raw %}
```html
{{block.intro_blurb}}

{{block.sponsor_me_on_patreon_message}}
```
{% endraw %}

## Calling Loopers

{% raw %}
```html
{{#looper.blog}}

{{#item}}

<article>
	<h2><a href="{{{link}}}">{{title}}</a></h2>
	<time class="article-date">{{date}}</time>

	<p>{{summary}}</p>

</article>

{{/item}}

{{^item}}
	<li>
		<article>
			<h3>Nothing, Nada, Zip &hellip;</h3>
		</article>
	</li>
{{/item}}

{{/looper.blog}}
```
{% endraw %}

## Calling Lambdas

{% raw %}
```html
{{#f_markdown}}   

# A Title Written In markdown

Content here is drafted in **Markdown**, but will output as rendered HTML thanks to this formating lambda block.

{{/f_markdown}}
```
{% endraw %}
