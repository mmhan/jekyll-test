---
layout: post
title: "Rails Idioms"
categories:
- Rails
date: 2015-07-20T01:12:04+06:30
external_url: https://robots.thoughtbot.com/code-review-ruby-and-rails-idioms
---

Rails framework ဟာ `1.day.from_now` လိုမျိုး idiom တွေကို အများကြီးထည့်ပေးထားတဲ့အတွက် ပုံမှန် rails သုံးတော့မှ ruby ကို စပြီးရေးဖြစ်တဲ့ ကျွန်တော့်လိုလူမျိုးတွေအတွက် အကြိုက်တွေ့ရသလို၊ purist တွေက အပြောအဆိုတွေလည်းခံရပါတယ်။ အဓိကရည်ရွယ်ချက်ကတော့ အဲ့ဒီ့ Idiom တွေကိုသုံးကာ ကုဒ်တွေကို အလွယ်တကူမြန်မြန်ဆန်ဆန် ရေးနိုင်ပြီး၊ ဖတ်ရတာလည်း ပိုလွယ်တဲ့အတွက်ပါ။

Thoughbot မှမောင်မင်းကြီးသားများက ကျွန်တော်တို့လို အခုမှ rails စရေးသူများအတွက် သုံးလို့ရရက်မသုံးြဖစ်တဲ့ idiom တချို့ကို list ထုတ်ပေးထားပါတယ်။ စမ်းကြည့်လိုက်ပါဦး။ 

<!--more-->

#1. Partials

Original:

```ruby
render partial: 'admin/shared/errors', locals: { errors: @user.errors }
```

Refactored:

```ruby
render 'admin/shared/errors', errors: @user.errors
```

#2. Determining a record’s existence


Original:

```ruby
existing_song = Song.where(user_id: user_id, album_id: album_id).first

if existing_song
```

Refactored:

```
if Song.exists?(user_id: user_id, album_id: album_id)
```

#3. Conditionals when object is nil

Original:

```erb
<%= event.end_date.nil? ? '' : event.end_date.to_s(:long) %>
```

Refactored:

```erb
<%= event.end_date.try(:to_s, :long) %>
```

#4. Conditional assignment when object is nil


Original:

```
if !town
  town = user.town
end
```

Refactored:

```
town ||= user.town
```

#5. Data migrations


Original, in a migration file:

```ruby
group_ids.each_with_index do |id, position|
  group = Group.find(id)

  if group
    group.position = position
    group.save!
  end
end
```

Refactored:

```ruby
group_ids.each_with_index do |id, position|
  update "update groups set position = #{position} where id = #{id}"
end
```