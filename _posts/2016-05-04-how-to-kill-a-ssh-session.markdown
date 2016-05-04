---
layout: post
title: "How to Kill a SSH Session"
date: 2016-05-04T11:11:00+06:30
categories:
- development
external_url: http://blog.infertux.com/2012/12/20/properly-close-a-frozen-ssh-session/
---

Working in Myanmar, once in a while, you'd definitely run into the
problem of your WIFI connection going astray and your SSH session gets
froze up.

At these times, no matter how many times you press `Ctrl-V` it wouldn't
end your SSH session, and you'd probably end up having to close your
termnial window, tmux session and killing the process. That solves the
problem, yet if you were like me it leaves you with that itch inside
that tells you, you're doing it wrong.

Well, that itch had just became unbearable enough for me to search
around and Viola!, you simply have to press the follow keys in sequence.

```
[Enter]
~
.
```

You learn something new everyday, eh?
