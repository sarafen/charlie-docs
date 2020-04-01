---
layout: page
title: Drafting Content
permalink: /content/drafting-content/
parent: Content
nav_order: 0
---

# Drafting Content

Content is broken into three main types that load based on different criteria.

* Pages
* Posts
* Blocks

## Pages & Posts

Pages and Posts contain [Frontmatter](/definitions/#frontmatter) at the top of their files, which is essentially localized meta data and configuration options.


```html

---
title: Hello Mars
date: 02/02/2020
teaser: This would be a Teaser
order: 2
summary: I could put a bunch of longer content here, and it would just keep on wrapping and going and doing whatever it needs to do so that I could get myself into a situation where this is at least one paragraph.
---

```

The Frontmatter block must be surrounded by two horizontal lines made of `---` characters.

A field cannot be defined with a blank value, and there cannot be any empty lines within the Frontmatter block.

Frontmatter is followed by the page's/post's content written in [Markdown](https://daringfireball.net/projects/markdown/syntax) format style.

```html

---
title: Hello Mars
date: 02/02/2020
teaser: This would be a Teaser
order: 2
summary: I could put a bunch of longer content here, and it would just keep on wrapping and going and doing whatever it needs to do so that I could get myself into a situation where this is at least one paragraph.
---

# Hello Mars

This is a Blog post.

```

### Frontmatter Core Fields

The following fields are a part of core in a multitude of ways, and gain advantages in formatting and display should you choose to use them.

Name            | format | Available for
-------------   | ------------- |
title           | STRING        | pages, posts
date            | 01/02/19      | posts
teaser          | STRING        | posts
summary         | STRING        | posts
order           | NUMBER        | pages, posts

### Advantages of making your own Fields

By default Charlie expects you to put all your images, for everything, in `/content/imgs/`. However, this organization structure might not be desirable for you.

Let's say that your site has two different kinds of Posts; blog and work. And you store images for both of these regularly, but you want to keep them separate.

You could make two folders called `imgs` at `/content/blog/imgs/` and `/content/work/imgs/`, and then put relevant imgs in each spot.

Then, in the Frontmatter of each blog Post you add a new custom field entitled `blog_img_dir` field and set it as follows:

```html
---
title: Blog Post Title Here
blog_img_dir: /content/blog/imgs
---
```

and the same for each and work Post:


```html
---
title: Work Post Title Here
work_img_dir: /content/work/imgs
---
```


Then within blog Posts or work Posts when referencing the URL of an image to display instead of using {% raw %}`{{img_dir}}`{% endraw %} you would use {% raw %}`{{blog_img_dir}}`{% endraw %} or {% raw %}`{{work_img_dir}}`{% endraw %}


for a blog Post
{% raw %}
```html
...

Look at this amazing image of a butterfly.

![Swallotail Butterfly]({{blog_img_dir}}/img.jpg)

...
```
{% endraw %}

for a work Post
{% raw %}
```html
...

Look at this amazing image of a butterfly.

![Swallotail Butterfly]({{work_img_dir}}/img.jpg)

...
```
{% endraw %}

This could become rather tedious, having to do this for every single blog or work Post that you create. Charlie provides a more global way to define a field.

If we know that we are going to use the same new folder for blog Posts, and the same new folder for work Posts, we could instead define this as a custom global in our `config.json` file.

```js
{
    "globals": {
        "domain"                : "website.com",
        "site_title"            : "A Website, On Mars",
        "site_description"      : "a website that has stuff on it",
        "author"                : "A. Person",
        "blog_img_dir"          : "/content/blog/imgs",
        "work_img_dir"          : "/content/work/imgs"
    },

    ...

}
```

Keep in in mind once you set a field as global this way, it can still be overridden in a Frontmatter field in an individual file.

This means you should be careful. For example setting the `site_title` field in the Frontmatter of a page would change the Site's Title for that page entirely. It's best if you only overwrite a global field you've made yourself. Overriding the core globals could have unforeseen consequences.

Additionally Mustache Tags will not process inside of Frontmatter fields. Which means, the following is not currently possible:

{% raw %}
```html
---
title:
custom_img_dir: {{blog_img_dir}}/custom/folder/
---

...

```
{% endraw %}

## Blocks

Blocks do not contain Frontmatter, as they are not full Pages or Posts, but are instead fragments. They can also be written in [Markdown](https://daringfireball.net/projects/markdown/syntax) format.

```html

# This is an intro statement

There's really not much more than could be said than what is being said right now.

```

They have their uses, but also their limitations. It is strongly encouraged that you use them sparingly.

Pages and Posts will pull in dynamically, based on the URL you visit. Blocks, however must be manually called within a template file for inclusion by name, minus the file extension.

For example the following could be placed within the `page.ms` file in a chosen theme and will render the contents of the selected block entitled `intro_blurb.md`.

{% raw %}
```html

{{{block.intro_blurb}}}

```
{% endraw %}

Additionally, you can call a Block into a full Page or Post Markdown file. For example, placing the following in an `index.md` content file.


{% raw %}
```html
---
title: Home Page
---

# Home Pages

This is the homepage, with it's relevant content on it.

{{{block.intro_blurb}}}

Things pickup from here.

```
{% endraw %}

You cannot embed a Block within a Block.
