---
layout: post
title: "Migrating from Wordpress to Jekyll"
date: 2015-07-18T15:00:00+06:30
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


**Goodbye wordpress, I've moved on.**

အင်တာနက်တွေ နှေးလာတာနဲ့အတူ၊ Update တွေကို ထွက်တိုင်းလိုက်တင်ဖို့အချိန်မပေးနိုင်တဲ့ ကျွန်တော်၊ တစ်ခါမှ မရေးတဲ့ Wordpress blog ကနေ၊ အနည်းငယ်ပိုရေးမယ့် jekyll based blog တစ်ခုအနေနဲ့ ပြောင်းလိုက်ပါပြီ။ တကယ်တော့ MyanmarCarsDB ဆိုဒ်ရဲ့ သတင်းစာမျက်နှာတွေအတွက်ကို Wordpress အစား အခြားတစ်ခုပြောင်းသုံးဖို့ စဉ်းစားရင်း ရှာဖွေရင်းနဲ့ ဒါကိုတွေ့ခဲ့တယ်ပဲဆိုပါတော့။

ဒီ post မှာ jekyll အကြောင်းနဲ့ wordpress ကနေ ဘယ်လိုရွှေ့ခဲ့တယ်ဆိုတာကို အဓိကရေးသွားမှာပါ။

<!--more-->

![Jekyll](/assets/jekyll.png)

> Jekyll သည် user-friendly ြဖစ်တဲ့ wordpress မဟုတ်၊ သို့ပါ၍ hacker-friendly ဖြစ်အောင်သာ ရှင်းမည်။ သည်းခံကြပါကုန်

[Jekyll](http://jekyllrb.com) ဆိုတာက ruby gem (library) တစ်ခုပါ။ သူ့ရဲ့အဓိက feature က static site တွေကို generate လုပ်ပေးနိုင်တာပါပဲ။ PHP ကိုသုံးထားတဲ့ wordpress လို Dynamic site တစ်ခုလို page view တစ်ခုတိုင်းအတွက် page ကိုတစ်ခု generate လုပ်မှာမဟုတ်ပဲ၊ blog post တစ်ခုတင်တိုင်းတင်တိုင်း၊ page တစ်ခုအသစ်ထည့်တိုင်းထည့်တိုင်း၊ သေးသေးမွှားမွှား ပြင်ဆင်မှုတစ်ခုခုလုပ်တိုင်းလုပ်တိုင်းမှာ၊ လိုအပ်တဲ့ page တွေကိုပြန် generate လုပ်ပြီး upload ပြန်လုပ်တဲ့ သဘောရှိပါတယ်။

အဲ့ဒီ့လိုလုပ်ခြင်းအားဖြင့် ကောင်းကျိုးတွေကတော့ program တွေ PHP script တွေ run စရာမလိုတဲ့အတွက်၊ CPU လိုအပ်ချက်လျော့နည်းပြီး၊ security ပိုင်းမှာ ဘာကိုမှကို ပူစရာမလိုပါဘူး။ ဆိုးကျိုးကိုပြောပါဆိုရင်တော့ server site script တွေ run မရတော့ဘူးပေါ့ဗျာ။ အဲဒါပေမယ့် server-site အတွက်လိုအပ်လောက်တဲ့ page view တွေ tracking လုပ်တာတို့၊ comment တွေ လက်ခံတာတို့စတဲ့ blog တွေနဲ့ပါတ်သက်တဲ့ feature တွေကိုတော့ Google Analytics တို့၊ Disqus တို့လို service တွေ အများကြီးရှိတဲ့ခေတ်ကြီးမှာ လွမ်းစရာမရှိပါဘူး။ ဒီ့အြပင် github pages က jekyll ကိုသုံးထားတော့ အလွယ်လေး `git push` တစ်ခုနဲ့တင် publish လည်းလုပ်လို့ရနေပြီဗျာ၊ server တွေဘာတွေတောင်မလိုတော့ဘူး။

## Step 1 : Installation

ကဲဒီတော့ ဘယ်ကစမလဲဆိုတော့ `ruby` နဲ့ `rubygems` ရှိပြီးသားစက်မှာ `jekyll` ကိုအရင်သွင်းလိုက်။

    gem install jekyll

Project အသစ်တစ်ခုလုပ်ဖို့အတွက်၊​ `jekyll new /path/to/project_folder` သို့မဟုတ်​ ရှိပြီးသား directory တစ်ခုမှာ `jekyll new .` ဆိုပြီး jekyll project တစ်ခုကိုစလိုက်​ေပါ့။

## Step 2 : Writing blog

    jekyll serve

အဲ့ဒီ့ code လေးကို terminal မှာ run လိုက်တာနဲ့ `localhost:4000` မှာ ကိုယ် create လုပ်ထားတဲ့ project ကို အစမ်းမြင်ရပြီလေ။

အဲ့တော့မှ `_posts` folder အောက်ထဲမှာ HTML ဖိုင်ဖြစ်ဖြစ်၊​ Markdown ဖိုင်ြဖစ်ြဖစ် တစ်ခုခုကို `2015-07-18-my-post-title` ဆိုတဲ့ file နာမည်ပေးပြီး ရေးချင်တာရေး၊ ဒါဆို blog post တစ်ခုြဖစ်ပြီ၊ `_page` အောက်မှာ About Me တို့ Contact Me တို့ထားရင်ရေးလို့ရပြီ။

## Step 3 : Configurations

`_config.yml` file ကိုပြင်ရင်လိုချင်တဲ့ ပုံစံပြင်လို့ရမှာပေါ့။ အောက်မှာ sample လေးတွေ့နိုင်ပါတယ်။ အပြည့်အစုံကိုတော့ jekyll site ရဲ့ [Config Options](http://jekyllrb.com/docs/configuration/) မှာကြည့်လိုက်ပေါ့။

```yaml
# Site settings
title: mmhan
description: > # this means to ignore newlines until "email:"
  This is a personal blog of Mike Myat Min Han @ mmhan.
  I talk about my musings and technology, at times.
email: contact@mmhan.net
author: mmhan
baseurl: ""	#path to site
url: "http://mmhan.github.io" # the base hostname & protocol for your site
twitter_username: mmhan
github_username:  mmhan
timezone: Asia/Rangoon
excerpt_separator: <!--more-->
paginate: 10
paginate_path: "/index/:num/"
```

Post ကိုတစ်မျိုး page ကိုတစ်မျိုး စသဖြင့် ပုံပြောင်းချင်ရင် `_layouts` ကိုဝင်၊ Header တွေ Footer တွေပြောင်းချင်ရင် `_includes` ထဲကိုဝင်စသဖြင့်ပေါ့။

## Step 4 : Syntax Highlighting

Hacker friendly blogging platform ြဖစ်တဲ့အတွက် syntax highlighting က built-in ပါပြီးသားလေ။

ဒါပေမယ့် github မှာလို <code>\`\`\`ruby</code> ဆိုပြီးရေးချင်တော့ `redcarpet` gem ကို သုံးဖို့ `_config.yml` ထဲသွားပြောရတာပေါ့။

```yaml
# Build settings
markdown: redcarpet
```

## Step 5: Import Wordpress Blog

အရင်ဆုံး wordpress ကနေ xml file ကို Export tool နဲ့ export လုပ်၊ ပြီးရင် gem တစ်ခုထည့်ရမယ်။

```
gem install jekyll-import
```

ပြီးတာနဲ့ ဒီလိုလေး run လိုက်။

```
$ ruby -rubygems -e 'require "jekyll-import";
        JekyllImport::Importers::WordpressDotCom.run({
        "source" => "path/to/wordpress_export.xml",
        "no_fetch_images" => false,
        "assets_folder" => "assets"
        })'
```

ဓါတ်ပုံတွေသိပ်မများဘူး၊ ဆိုရင်အရမ်းမြန်တယ်။ များရင်တော့ အင်တာနက်ပေါ်မူတည်တာပေါ့။ ပြီးသွားရင် ဟောဒီ့လိုပြတယ်။

```
Imported 98 attachments
Imported 2 pages
Imported 70 posts
```

## Step 6: Deploy

Github ပေါ်တင်ဖို့အတွက် `Gemfile` ထည့်ပေးဖိုတော့လိုတယ်။ ေဟာဒီ့လိုလေး


```ruby
source 'https://rubygems.org'

require 'json'
require 'open-uri'
versions = JSON.parse(open('https://pages.github.com/versions.json').read)

gem 'jekyll', '~> 2.4'
gem 'github-pages', versions['github-pages']
```

အဓိကက compatibility အတွက်ပါ။

ပြီးရင်တော့ github ရဲ့ `username.github.io` ဆိုတဲ့ main site အတွက်တင်ချင်ရင် အဲ့ဒီ့နာမည်အတိုင်းပေးထားတဲ့ repo ရဲ့ master ကို push လုပ်လိုက်ပြီး အဲ့ဒီ့ link ကိုသွားလိုက်ရုံပဲ။

တခြား repo ဆိုရင်တော့ `gh-pages` ဆိုတဲ့ branch ကို push လုပ်ပေးရမယ်၊ ပြီးရင် `username.github.io/repo-name` ကိုသွားကြည့်လိုက်။

## What's next?

အခုတော့ [MyanmarCarsDB](http://www.myanmarcarsdb.com/?utm_source=migration-from-wordpress-to-jekyll&utm_medium=blog&utm_campaign=mmhan_blog) ရဲ့ သတင်းဆိုဒ်မှာ သုံးဖို့ API ကို ဘယ်လို liquid tag တွေနဲ့ generate လုပ်မလဲ ကြည့်နေတယ်။ အဲ့တော့... အကြောင်းထူးရင်၊ အလုပ်ဖြစ်ရင်ပြောပြမယ်။

စမ်းြကည့်လိုက်ဦးနော်၊ tips တွေ tricks တွေရှိရင်လည်းပြောပြ၊ မသိရင်လည်းမေး။