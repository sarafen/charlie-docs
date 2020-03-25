---
layout: page
title: Definitions
permalink: /definitions/
nav_order: 100
---

# Definitions

## Frontmatter

A area surrounded by `---`, both before and after, at the beginning of a [Markdown](https://daringfireball.net/projects/markdown/syntax) file.

Each line contains a named Field that can be given a value. These Fields can then be output within Templates and even within that Markdown file as Mustache Tags.

```
---
field: value
---

content here...
```

## Tag

A Tag, is a [Mustache](https://mustache.github.io/mustache.5.html) Tag that outputs some piece of data or series of data. They are wrapped in curly brackets, {% raw %}`{{`{% endraw %}.

{% raw %}
```
{{tag}}

OR

{{{tag}}}

OR

{{>tag}}

OR

{{#tag}} {{/tag}}
```
{% endraw %}

## Theme

A Theme is a collection of Templates and CSS Styles at a minimum. It may also include relevant images or scripts that help define an overall Design or Aesthetic for a site. As they are separate from the main content of a site you can swap one Theme out for another and get an entirely different look.
