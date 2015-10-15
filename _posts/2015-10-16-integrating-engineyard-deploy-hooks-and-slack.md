---
layout: post
title: "Integrating Engineyard's Deploy Hooks with Slack"
categories:
- Rails
- Development
date: 2015-10-16T01:00:00+06:30
---

At [Rebbiz][rebbiz], we have just recently adopted [Slack][slack] as an alternative form of communication. For that, I was thinking of integrating our platform and slack together so that everyone in the team should receive a message that a new release has been deployed to [CarsDB][carsdb]. Here's what I have come up with.

<!--more-->

_I guess you could scoff at us for the slow adoption rate. What can I say, though we've tried it before, we had never found it useful. However, Rebbiz have grown to a point that simply talking loudly to each other across the open office layout is no longer effective. And it's become too noisy._

Anyway, I looked around and found [this article][source] with details to working with [Slack-API][slack-api] to post to slack from Engineyard. Although it is great and effortless, I found that its use of `slack-api` unnecessarily add more dependency on our code base and I hate having to store api keys for plethora of services.

I looked around and found that [webhooks][slack-webhooks] are also a great way to integrate with slack too! So, I created two simple rake tasks generating the body of the cross-platform call and made the call using `httparty` [gem][httparty] instead. After testing it several times on my dev environment and getting the result that I wanted, here's the code.

```ruby
# lib/tasks/slack.rake
require 'httparty'
namespace :slack do

  desc "Send a message to any channel about anything"
  task :send_message, [:channel, :message] => :environment do |t, args|
    message = args.message
    channel = args.channel
    payload = {
      channel: channel,
      text: message,
      username: "CarsDB Bot"
    }
    send_message(payload)
  end

  desc "Send a message to general channel about deploy"
  task :deploy_message, [:channel,:message] => :environment do |t, args|
    message = args.message
    channel = args.channel
    payload = {
      icon: ":shipit:",
      channel: channel,
      text: message,
      username: "CarsDB Release Bot"
    }
    send_message(payload)
  end

  def send_message(data)
    hook = "https://hooks.slack.com/services/HELLO_WORLD/HELLO_WORLD/HELLO_WORLD"
    HTTParty.post(hook, body: data.to_json).inspect
  end
end
```

Once the rake task is completed, I created the hook much to the resemblance of the given example with a little twist.

```ruby
# deploy/after_restart.rb
on_app_master do
  is_prod = config.environment_name == "prod"
  env = is_prod ? "<http://www.live.com/i|CarsDB Live>" : "<http://www.staging.com/i|CarsDB Staging>"
  branch = "<https://example.com/user/repo/branch/#{config.input_ref}|#{config.input_ref}>"
  channel = is_prod ? "#general" : "#dev-team"
  message = "#{config.deployed_by} has deployed #{branch} branch to #{env}"
  message += " (with migrations)" if config.migrate?
  message += "."
  #Run slack rake task
  run %|cd #{config.release_path} && bundle exec rake "slack:deploy_message[#{channel},:rocket: #{message}]"|
end
```

Here is what it looks like when I deploy to CarsDB.
![Integration Screenshot](/assets/2015-10-16-integration-screenshot.png)

Have fun integrating your own systems too!

[rebbiz]: http://www.rebbiz.com
[slack]: http://slack.com
[carsdb]: http://www.carsdb.com/?utm_source=slack-integration&utm_medium=blog&utm_campaign=mmhan
[source]: http://www.matthewhirst.com/posts/11
[slack-api]: https://api.slack.com
[slack-webhooks]: https://api.slack.com/incoming-webhooks
[httparty]: https://github.com/jnunemaker/httparty/