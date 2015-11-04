---
layout: post
title: "Bright shiny things that break"
categories:
- Development
date: 2015-11-04T15:56:00+06:30
---

Yesterday, I came across this article that discussed "[Facebook's code quality problem][fcqp]" on Hacker News.

It says that, Facebook is now throwing 429 people at their iOS app with 18,000 classes. With graphs showing more incidents on the production server when engineers are working on it, it's been observed that Facebook is suffering code quality problems. The author concluded that if relationships between the moving parts of each system isn't well understood and well tested, it will definitely break things. Go on and give it a read if you've got the time.

As an outside observer, it's easy pointing fingers at their demise and feel smug about it. A reductive conclusion would cynically say, if you like facebook's culture of "Move fast and break things", simply adopt the mantra of __If brute force doesn't solve your problem, then you aren't using enough__.

<!--more-->

I have to admit, the problem in itself is no small feat. Who's making code reviews? How the hell are they doing it? Who resolves conflicts? Who gives the nod? Who pushes the code to release?

On the flip side of the coin, the problem would lie in maintaining a speed that's tolerable for the users that desire instant gratification and instant resolution of their problems when it comes to using apps/websites.

What happens when you can't work on a solution, but stuck on resolution of bugs? What happens when having too many heads crowd out the one voice that might just make it work? What happens when the system doesn't scale well to hundreds of user stories in the backlog?

What happens when the technical leader's time for problem solving and devising solutions – the job that he had always been good at - is no longer enough because the natural progression of things sent him up the ladder to manage people?

I, for one, am very protective of my status quo. I'd like having to go to sleep peacefully at night without a worry that a bug had managed to sneak in, or the quality of the code had just contracted "[a broken window][window]" disease. Even with those rigorous testings and reviews we are starting to suffer the growing pain of becoming too huge to have a full mental grasp of the effects and side effects of each changes that was introduced. (For my brain is small and my mind is weak)

It's not the new features and solutions that we're building that grew our product to the here and now, it's the quality code that served the users reliably at more than 99% of the times that brought us here.

As a user of my own product, I'd take a working Trello board over the [shiny][shiny] Asana any time of the day. As a co-founder and CTO of the company, I still have found no solution today.

One thing's for sure, this ain't a problem that is unique or unsolveable. I just haven't found the solution yet. That means I've got a ton of research to do.

[fcqp]: http://www.darkcoding.net/software/facebooks-code-quality-problem/
[window]: http://www.artima.com/intv/fixit2.html
[shiny]: http://www.forbes.com/sites/johnbaldoni/2013/07/23/are-bright-shiny-objects-worth-your-time-and-money/