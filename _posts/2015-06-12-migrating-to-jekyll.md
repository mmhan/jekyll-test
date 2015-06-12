---
layout: post
title: "Migrating from Wordpress to Jekyll"
date: 12 June 2015 14:14:00.000000000 +06:30
categories:
- Technology
published: true
type: post
author: mmhan
wp_author:
  login: mmhan
  email: mmhan2u@gmail.com
  display_name: Mike Han
  first_name: Mike
  last_name: Han
---
- `gem install jekyll`
- `jekyll new folder_name` to create a new project or use `jekyll new .` to init current dir as jekyll project
- Pygment for syntax highlighting using python http://pygments.org/
- Or Rouge https://github.com/jayferd/rouge (smaller set of languages)

```ruby
def foo
    puts 'foo'
end
```
- `highlight` method take `ruby` as argument.
- See more at http://jekyllrb.com/docs/templates/#code-snippet-highlighting
- `jekyll build` will build a site
- `jekyll serve` will run dev server
- [Config Options](http://jekyllrb.com/docs/configuration/) can be put into `_config.yml` for build configs
- Once you've got the hang of it, simply start writing.

# Import Wordpress blog to Jekyll
- `gem install jekyll-import`
- Export your wordpress site to xml by using the tool in wp-admin
- Once the xml is in hand use


```    
$ ruby -rubygems -e 'require "jekyll-import";
        JekyllImport::Importers::WordpressDotCom.run({
        "source" => "wordpress.xml",
        "no_fetch_images" => false,
        "assets_folder" => "assets"
        })'
```

- All the images will be downloaded and placed in assets
- All the files will come with HTML extension, you may use it to convert them back to markdown later
- Import was pretty quick

```
    Imported 98 attachments
    Imported 2 pages
    Imported 70 posts
```
- Build takes quite a long long time. if `lsi: true` in options. Why??
- The templating language is quite a pain though
- It seems that `author` yaml front matter is configured with nested data which the templating engine isn't really reading.
- Also the same for `meta` to `wp_meta`
- Then there is this code that I can't seem to get rid of.
   excerpt: !ruby/object:Hpricot::Doc
     options: {}
- created a Gemfile to add github pages
- Installed octopress
