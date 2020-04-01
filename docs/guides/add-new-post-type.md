---
layout: page
title: Add A New Post Type
permalink: /content/add-a-new-post-type/
parent: Guides
nav_order: 0
---

# Add A New Post Type

## Set up a new post type's content

In this example we will be creating a new post type: `blog`.

1. Create a folder with the name of your desired post type in the `/content/` directory.
2. create the first `blog post` within that new folder. We'll call ours `hello-mars.md`.
3. Make sure your file contains a Frontmatter block, even if it is empty, though it is recommended it at least have a title.
4. Lastly, begin drafting content after the Frontmatter block. You can use [Markdown](https://daringfireball.net/projects/markdown/syntax) to format the text.


```html
---
title: Hello Mars
---

# {% raw %}{{title}}{% endraw %}

Welcome to the Hello Mars Post on my Blog!
```

Note: You have access to the local Frontmatter fields in a document. You can use the {% raw %}`{{title}}`{% endraw %} Tag here to access the local title field, instead of writing the title out twice.

In our example we'd benefit from adding additional Frontmatter fields.

```html
---
title: Hello Mars
date: 02/02/2020
teaser: This would be a Teaser
order: 0
---
```

## Set up a new post type's template

You may be fine with the default `post.ms` template, but you may find yourself wanting `blog Posts` to look different in some way. This can be achieved by taking advantage of the [Template Cascade](/templates/template-cascade).

1. Create a new template using the `post-{type}.ms` naming scheme. In this example we'll call it `post-blog.ms` in the root of the active theme's folder.

2. You can copy over the contents of the `post.ms` file as a guide to build from, or create your own from scratch utilizing the Frontmatter fields, and the content field.

{% raw %}
```html
{{>header}}

<body>

<h1>{{title}}</h1>
<span class="date">{{date}}</span>

{{{content}}}

</body>
```
{% endraw %}

Now you have a custom Template that will only affect how `blog posts` are displayed.


## Optional: Set up a new template for one specific blog post

1. Create a new folder in your active theme's root, named the same as your post type. In this example `blog`.
2. Create a file with the same name as the specific blog post you want to make a template for. `hello-mars.ms`.
3. Copy over the contents of the `post.ms` file as a guide to build from, or create your own from scratch utilizing the Frontmatter fields, and the content field.

Only the Hello Mars `blog post` will have this template. All other `blog posts` will use the `post-blog.ms` template or if you opted to not set that up, then the `post.ms` template. Please see the [Template Cascade](/templates/template-cascade) to learn more about how this works.

## Create a looper for our new post type

Loopers will let you display a dynamic list of items of your custom post type throughout your site. This is especially useful if you'd like to show a list of your latest blog posts on your `/blog` page.

There is a blog looper [included by default](/configuration/#loopers).

However, to create a looper for a post type named something else you can just copy it and append it below with a comma.

```js
    "loopers" : {
        "blog" : {
            "loop_type"         : "default",
            "content_filter"    : "blog",
            "sort_by"           : "date",
            "date_format"       : "F j, Y",
            "limit"             : 3,
            "offset"            : 0
        },
        "custom_post_type" : {
            "loop_type"         : "default",
            "content_filter"    : "custom_post_type",
            "sort_by"           : "date",
            "date_format"       : "F j, Y",
            "limit"             : 3,
            "offset"            : 0
        }
    }
```

## Display a list of your blog posts on /blog

Add the following code to your `themes/{theme_name}/pages/blog.ms` file, if this file doesn't exist you can create it.

{% raw %}
```html
{{#looper.blog}}

{{#item}}
  <li>
      <article>
      	<h2><a href="{{{link}}}">{{title}}</a></h2>
      	<time class="article-date">{{date}}</time>

      	<p>{{summary}}</p>

      </article>
  </li>
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

This will display the 3 most recent blog posts, sorted by date; as defined by the blog looper in the `config.json` file, and if there are none it will output: "Nothing, Nada, Zip".
