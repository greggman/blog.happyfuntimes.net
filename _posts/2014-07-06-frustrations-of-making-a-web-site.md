---
title: Frustrations of making a web site
date: '2014-07-06'
layout: post
excerpt_separator: "noexcerpt"
permalink: /blog/frustrations-of-making-a-web-site/
tags:
  - Uncategorized
dsq_thread_id: '3566790733'
---
Tech gets out of data. Most of the websites I've made use a [LAMP stack](https://en.wikipedia.org/wiki/LAMP_(software_bundle)). Most of them are just static pages with some JavaScript or they're wordpress
based like this one.

For [SuperHappyFunTimes](http://superhappyfuntimes.net) I felt like I wanted to use [node.js.](http://nodejs.org) SuperHappyFunTimes itself is mostly written in node.js and it seems like for
the last 2&minus;3 years it's one of the major topics so I thought I should
probably go that way.

On top of that I've never written a website with users and the ability to log
in etc and I didn't want to write my own since it's easy to make a ton of
mistakes. It seemed best to use some framework that handles all of this.

The first problem though is that ISPs that support node.js are far more
expensive than LAMP based ISPs with no limit on how much money you'll be
charged.

This is arguably one of the reasons why PHP and LAMP stacks are still hugely
popular. PHP's design lets multiple sites run on the same server. Every other
server tech except CGI requires a server per website. Sure, you can use virtual
servers but virtual servers are still way more resource intensive than a shared
LAMP stack.

So, that's a little scary. I have no current monetary plans for HappyFunTimes
so I'd prefer not to blow wads of my own money on it. (although I guess if I
value my time I have blown wads of money on it &#128539;)

Next up is frameworks. My original idea was to leverage [npm](https://www.npmjs.org/).  It's open source, it has a website and repo of "packages". Rename "packages"
to "games" and reskin the website and that seemed like enough.

Unfortunately I tried cloning the [npm-www](https://github.com/npm/npm-www) repo and bringing up its [vagrant box](http://www.vagrantup.com/). It failed.  The server it tries to clone from is gone apparently.

Then I realised npm was probably not the solution I wanted. I found this out
when I saw a friend try to use HappyFunTimes. He downloaded it from github,
typed "npm install" to install the dependences and saw it fail because someone
deleted a repo. Not an experience I wanted to put end users through.

npm uses [CouchDB](http://couchdb.apache.org/) so I spent a few days trying about CouchDB, walking through the official book.
The tech seemed pretty awesome but I ran into several errors in the book. The
book is open source so I submitted a patch to the first error I found but when
I ran into more and realized some of the issues <strong>HAD NOT BEEN FIXED IN OVER 3 YEARS</strong> I lost all confidence in CouchDB. I'm sure it's great tech but if they can't
be bother to update the docs it's hard to believe it's a good way to go.

Next up I tried different frameworks. [Nodejitsu](https://www.nodejitsu.com/) has some stuff. Again the docs and stuff seemed massively out of date. For
example they push [flatiron](http://flatironjs.org/) but as far as I can tell it's dead. How can I have any faith in them if their
own docs point to basically dead projects? So I gave up on that.

I found [Meteor](https://www.meteor.com/) which certainly seemed nice. But..., it uses websockets which as far I can
tell are resource hogs. Specifically a normal website you connect, it gives you
page, the server and your computer then disconnect. This lets the server serve
other people. WebSockets through keeps the connection open. This has the
advantage that the server can send updates and other messages to the page for
real time updates but it has the disadvantage that keeping that connection open
requires lots of memory and there's a limit number of connections a server can
handle. For my needs I don't need a realtime connection. The data on
SuperHappyFunTimes is not currently massively changing and doesn't need to be
real time.

Apparently you can turn that feature off. I haven't tried it yet. But I suppose
that's a minor issue. The bigger issue is these frameworks are scary. There's
no guarantee the teams making them will be around. You just have to pick one
and hope for the best. I look for solutions, I see "todos" on their website
that have been there for months or years, I see little activity on their repo.
Are they still working on it?