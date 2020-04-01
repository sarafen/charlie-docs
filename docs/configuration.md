---
layout: page
title: Configuration
permalink: /configuration/
nav_order: 1
---


# Configuration

By default Charlie comes with a `config.json` file located in the root directory. This file contains three main sections that you can use to configure your site.

It is must be written in valid [JSON](https://www.json.org/json-en.html), be sure to adhere to that. Be especially careful of trailing commas.

<!-- If you are fearful of writing raw json, you can instead use the Configurator Tool. -->

```js

{
    "globals": {
        "site_domain"           : "website.com",
        "site_title"            : "A Website, On Mars",
        "site_description"      : "a website that has stuff on it",
        "site_author"           : "A. Person",
        "img_dir"               : "/content/imgs",
        "files_dir"             : "/content/files"
    },
    "settings" : {
        "theme"                 : "sample",
        "archives" : {
            "blog" : {
                "enabled"       : true,
                "limit"         : 10
            }
        },
        "feeds" : {
            "blog" : {
                "enabled"       : true,
                "limit"         : 50
            }
        }
    },
    "loopers" : {
        "blog" : {
            "loop_type"         : "default",
            "content_filter"    : "blog",
            "sort_by"           : "date",
            "date_format"       : "F j, Y",
            "limit"             : 3,
            "offset"            : 0
        }
    }
}


```


## Globals

There are default [Global Variables](/globals) defined by Charlie that you can choose to overwrite here.

Name          | Value
------------- | -------------
site_domain  | string
site_title | string
site_description | string
site_author | string
img_dir | path defined from site root
files_dir | path defined from site root


## Settings

Name          | Value
------------- | -------------
theme  | string containing name of active theme
maintenance_mode | true/false


## Loopers

Loopers are small defined data sets that collect a grouping of content that you can output in your Template Files.

There is a blog loop included by default.

```js

"blog" : {
            "loop_type"         : "default",
            "content_filter"    : "blog",
            "sort_by"           : "date",
            "date_format"       : "F j, Y",
            "limit"             : 3,
            "offset"            : 0
        }


```

The `blog` attribute is the name of your looper.

And then you can define it with the following configuration options.


Name          | Value
------------- | -------------
loop_type  | "default" or "feed"
content_filter | post type name
sort_by | Frontmatter field to sort by
date_format | If this post type has a date, format it as defined
limit | how many to include
offset | start list offset by a number


You can define as many loopers as you have need of. However, be careful. Loopers are available to all pages, which means they take up memory.

It's also a good idea to keep your limit within reason. If you have 300 blog posts on your site, it would not be a good idea to create a looper that has a limit of 250.
