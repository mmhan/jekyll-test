---
layout: post
title: "Todd Gardner: JavaScript Forensics"
categories:
- development
- javascript
date: 2016-04-21T20:30:00+06:30
external_url: https://www.youtube.com/watch?v=Xvdnewmdokc
---

Helpful tips on figuring out some of the trickiest bugs in production for javascript applications.

<!--more-->

##\#1 Script Error: Unknown impact, infrequent

There're times where error message contains nothing at all.

That usually happens when you are loading cross-origin resources and something went wrong.

**When that happens:**

> add `crossorigin` attribute to `<script>` tag to get better error messages


##\#2 Undefined method

No change to scripts but has new errors.

Comes from changes of 3rd Party

##\#3 Cannot read property `foo` of undefined.

When you check out the stack trace, there is only "anonymous function".

**Solution** Check async checkbox from, chrome inspector's source tab, you'll get a good stack trace.

##\#4 `fooThat` is not a function.

Doesn't happen locally. Shouldn't be undefined. If a certain script that doesn't get loaded, it could break the whole app.

There could be times when a script will fail to load.

Be more cautious about using 3rd party's API. Make sure it's there before calling anything.

##\#5 Browser crashing

How to find out memory leak.

Use Timeline tab from chrome debugger. Use WASD to navigate the timeline.

When you dig in, you will find where memory usage jumps.