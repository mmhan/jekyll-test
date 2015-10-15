---
layout: post
title: "Speed Up Your Rails App by 66% - The Complete Guide to Rails Caching"
categories:
- Rails
date: 2015-07-19T02:09:04+06:30
external_url: http://www.nateberkopec.com/2015/07/15/the-complete-guide-to-rails-caching.html
---

I've always been a big fan of caching mechanisms used in rails ever since I read the rail's guide about caching. I had found that the design patterns that has been used to accomplish it had been so profoundly beautiful that I had implemented the pattern in other non-rails projects too. My fascination for it was even more enhanced when I found the practice of 37signal and DHH's [Russian Doll Caching](https://signalvnoise.com/posts/3113-how-key-based-cache-expiration-works).

[MyanmarCarsDB](http://www.myanmarcarsdb.com/?utm_source=rails_caching&utm_medium=blog&utm_campaign=mmhan_blog) goes through intensive periods of cache optimizations based on those practices and readings that caching is the only part of MyanmarCarsDB that requires its own documentations.

Nevertheless, we've been running into some issues with cache, mainly because the CacheStore we've been using has been the primitive `ActiveSupport::Cache::FileStore`.

The rigorous approach to caching detailed here is gonna be a big help to solving the problem we've been facing.