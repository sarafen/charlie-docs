---
layout: page
title: App Structure
permalink: /app-structure/
parent: Structure
nav_order: 0

---

# App Structure

By default Charlie comes with the following overall structure.

```html
+-- ..
|-- (Charlie)
|
|-- app (Charlie Core Files)
|
|-- content
|   |-- _blocks
|   |-- files
|   |-- imgs
|   |-- pages
|   |   |-- 404.md
|   |   |-- index.md
|   |   +-- ..
|   +-- ..
|
|-- themes
|   |-- sample
|   |   |-- _partials
|   |   |-- pages
|   |   |   |-- 404.ms
|   |   |   |-- index.ms
|   |   |   +-- ..
|   |   |    
|   |   |-- page.ms
|   |   |-- post.ms
|   |   +-- ..
|   +-- ..
|
|-- .htaccess
|-- config.json
|-- index.php
+-- ..
```
