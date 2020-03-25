---
layout: page
title: Globals
permalink: /globals/
nav_order: 7
---


# Globals

There are a few variables available no matter what URL you visit and are defined as such.



## Global Variables

Name          | Value                   | Customizable?
------------- | -------------           |
current_year  | the current year        | X
site_domain  | string                        | Y
site_title | string                     | Y
site_description | string               | Y
site_author | string                         | Y
img_dir | path defined from site root   | Y
files_dir | path defined from site root | Y


Most Global Variables can be overridden within your `config.json` file. Please see [configuration](/configuration) for more information.


## Global Lambdas

Name            | Use as Tags
-------------   | -------------
f_uppercase     | {% raw %}`{{#f_uppercase}} STRING {{/#f_uppercase}}`{% endraw %}
f_lowercase     | {% raw %}`{{#f_lowercase}} STRING {{/#f_lowercase}}`{% endraw %}
f_capitalize    | {% raw %}`{{#f_capitalize}} STRING {{/#f_capitalize}}`{% endraw %}
f_markdown      | {% raw %}`{{#f_markdown}} STRING {{/#f_markdown}}`{% endraw %}
f_date_FORMAT   | {% raw %}`{{#f_date_FORMAT}} 01/02/20|7:30PM {{/#f_date_FORMAT}}`{% endraw %}


### f_date_FORMAT Types

Examples shown are given `01/02/20|7:30PM` as input.

Name            | Outputs as        | Example Output
-------------   | -------------     |
f_date_[RFC339](https://tools.ietf.org/html/rfc3339)   | `"Y-m-d\TH:i:sP"`   | 2020-01-02T19:30:00+00:00
