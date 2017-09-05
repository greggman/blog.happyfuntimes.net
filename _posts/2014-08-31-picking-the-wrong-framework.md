---
title: Picking the wrong Framework?
date: '2014-08-31'
layout: post
permalink: /picking-the-wrong-framework/
tags:
  - Uncategorized
dsq_thread_id: '3215844402'
---
I struggled with deciding how to implement superhappyfuntimes the website.

There's a million options from a LAMP stack to python, node.js, ruby, go, and
the zillions of frameworks written on top of them. I was mostly sold on using a
node.js since I like the idea of one language on both the client and server.

In some ways though superhappyfuntimes is a really simple site. All it needs is
a database of games. At the moment there's no logging in, no user accounts,
etc. That might change. Ideally when you register a game it should be
registered to you so you and only you have permission to edit it. But, seeking
my minimum viable product (mvp) that stuff can wait. Still, it seemed like a
good idea to pick a framework that supports that stuff so I can easily add it
later.

At the same time, sometimes I thought maybe I should do it with no framework.
Just checking an big .json file with an array of info from all the games.
There's not likely to be more than 100 games for a while. I can hope for more
but realistically it's going to stay small. But still, I'd need a way to edit
that file. I didn't want to have to edit it by hand anytime someone wanted to
add a game. I could write tools to edit it but that's basically rewriting all
the stuff I'd get from a framework.

Ultimately I picked Meteor. It was really easy to get started, it just worked,
no set up, and they even had deployment somewhat solved. So, it was easy to get
things basically working.

But, you knew there was a <em>but</em>...Meteor is heavy. Each user that connects gets a not&minus;too&minus;small
JavaScript app downloaded to their browser. That app then contacts the server
to get database info, by default using WebSockets which itself is heavy. That
might be fine if you're trying to write a gmail clone but it's not so fine if
you're trying to keep expenses small. I'm running superhappyfuntimes out of my
pocket. I'd prefer if I only needed one small server and not a whole server
farm. The pages superhappyfuntimes serves are for the most part static. They
only need to be updated when a new game is added or updated, otherwise they're
the same for every user. I'm running on a single 512meg digital ocean server. I
suspect that's not enough for more than a few users with meteor whereas if I
had some kind of static page server it would probably be enough for thousands
of users?

So now the question. Do I throw meteor under the bus and re&minus;write? Is
there someway to leverage what's there? Apparently meteor's current solution to
static pages so to run a full browser on the server (phantomjs) and capture the
pages that area created. I'm not even sure that would work. Browsers are huge
memory hogs. I'd probably have to run it offline, capture the pages, then
upload the results. That means I'd be back to manually running it and no
realtime update unless I setup yet another server.

Meteor is pretty awesome. Although I don't have too much experience with other
frameworks some cool things about meteor are that it's default development
environment is 100% live. Edit any .js, .html, or .css file and the moment you
save it it updates. The server restarts, your page reloads, it's seriously
awesome! It also has a relatively nice templating system.

Maybe I should switch to another framework? I have no idea which one to switch
to. Or maybe I should just pull apart meteor's pieces and pair it down to just
what I need? Or maybe I should start over from scratch? The public interfaces
that update the game database are already handled it might actually be
relatively simple to switch it all to custom code. I've no idea at the moment.

Sigh. I want to be working on games, not on infrastructure. Oh well. Live and
learn. &#128539;