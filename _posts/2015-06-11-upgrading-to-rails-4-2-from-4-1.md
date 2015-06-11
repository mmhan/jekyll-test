---
layout: post
title: Upgrading to Rails 4.2 from 4.1
date: 2015-06-11 01:25:39.000000000 +06:30
categories:
- Technology
tags: []
status: publish
type: post
published: true
meta:
  _edit_last: '1'
author:
  login: mmhan
  email: mmhan2u@gmail.com
  display_name: Mike Han
  first_name: Mike
  last_name: Han
excerpt: !ruby/object:Hpricot::Doc
  options: {}
---
![Upgrading to Rails 4.2 from 4.1]({{ site.url }}/assets/rails4.2.png)

In an effort to make use of the latest features of the rails platform in [MyanmarCarsDB](http://www.myanmarcarsdb.com), I was working on upgrading and making required changes on the codebase in last few weeks. It was triggered by the need for us to start utilising background jobs (enabled by Rails' first-class wrapper ActiveJob) and also many of the red-lines in [VersionEye](https://www.versioneye.com/) report. _(VersionEye is a notification system for software libraries dependencies giving you reports about outdated libraries of your project.)_ This blog post is to document some of the challenges and changes we had to make for your reference.

I had started out by upgrading all gems in the red by upgrading them to their latest versions. Then, there was the upgrade of rails 4.2.

As soon as the upgrade is completed, running rspec gave me the error about `validate` syntax. Apparently, a line that I had isn't working as I had intended.

<pre class="prettyprint lang-rb">    validates :name, presence: true
</pre>

I had only discovered that when I had upgraded to rails 4.2 and it raised the `ArgumentError` with the message

    Unknown key: :presence. Valid keys are: :on, :if, :unless, :prepend. Perhaps you meant to call `validates` instead of `validate`?

[Upon my research](http://api.rubyonrails.org/classes/ActiveModel/Validations/ClassMethods.html#method-i-validate) it had been found that the other method `validate` is used to `validate` the record using a symbol pointing to a defined method or a block. It meant that `validate :name, presence: true` was calling the instance method `name` and using its return as a boolean. In essence, our rspec tests weren't nearly as specific as it should have been.

Speaking of rspec, I had known for a long time that my `spec_helper` and `rails_helpers` were in a sad state due to the upgrade from rspec 2 to rspec 3\. So, I figured it was the time to sort them out too.

I simply had discarded the existing file (while keeping a reference) and overwrote those files by simply running `rails g rspec:install`. Once that easy part was over, the easier part was to find and replace `include 'spec_helper'` to `include 'rails_helper'`. There's also the need to place those missing `configure` lines that would allow me to use my custom controller macros and do request rendering.

With new Rails, there was also new version of capybara. It meant that I had to fix some of those cucumber steps that depended on `Capybara.ignore_hidden_elements` to be `false` which is no longer the default. I decided against changing it back to `true` (which could definitely come back to bite me in my ass) simply because, if capybara can't see something, it's almost definitely that my users can't see it too. Most of those problematic steps are concerning to the way selections are made when `select2` jQuery plugin was in use. Thankfully using a simple hack below is all I needed to fix the problem. It's a dirty hack, nonetheless it's just what I needed, for simple select2 drop-downs, rather than other solutions provided elsewhere.

    #features/support/select2.rb

    def select2(value, options)
      page.execute_script("$('##{options[:from]}').removeClass('select2-offscreen').show()")
      select value, options
    end

Now that ActiveJob is in play, mailer's `deliver` method is deprecated in favour of `deliver_now` and `deliver_later`. Though find and replace would have been simple matters, my use of table-less models (for contact message and etc.) would trigger `SerializationError`. It was found that `ActiveJob` required an object that could be identified using `GlobalID::Identification` which those models weren't. Thus, `deliver_now` for them.

After getting rid of a dozen of deprecation notices, and renaming `css.scss` files to simply `.scss`. Both rspec and cucumber passed readily.

However, that wasn't the end of the upgrades. We wanted to be able to run builds on top of a CI server, including those cucumber tests that may require javascript to run. It meant I had to get rid of the clunky `selenium-webdriver` that uses firefox and replace it with something else that will run a browser in headless mode. `phantomjs` and `poltergeist` were my choice. There's a guide on [EverydayRails](http://everydayrails.com/2015/01/27/rspec-switch-selenium-poltergeist.html) if you'd like to do the same for your test cases too.

With that new gem `poltergeist`, there are a couple of new methods that will be useful. You can take a screenshot with `page.driver.render('/tmp/screenshot.jpg')` and start remote debugging with `page.driver.debug`.

With all the tests passing and no warning messages left, that was mission accomplished. In the next post, I will talk about how long it took and how much trouble I went through just to get it deployed on production server.

On another note, check out this benchmark below to see how fast poltergeist was compared to selenium!

    /--- selenium-webdriver ---/
    89 scenarios (89 passed)
    537 steps (537 passed)
    5m11.288s

    /--- poltergeist ---/
    89 scenarios (89 passed)
    537 steps (537 passed)
    2m12.380s