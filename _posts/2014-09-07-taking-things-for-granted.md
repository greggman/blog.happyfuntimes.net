---
title: Taking things for granted
date: '2014-09-07'
layout: post
permalink: /taking-things-for-granted/
tags:
  - Uncategorized
  - git
  - github
  - noobs
  - automation
dsq_thread_id: '3260311241'
---
I'm trying my best to SHIP the minimum viable product version of HappyFunTimes
but it seems like every day I finish one thing only to find 2 more.

One of the things I learned early on is that many Unity devs are fairly new to
many parts of software development. I keep forgetting that. One simple example
is a friend wanted to use HappyFunTimes. He's not an experienced programmer but
he can hack stuff together in Unity. When he finds out he also needs to program
the controllers in JavaScript and HTML5 he's done. That's not something he
knows how to do. Of course he could learn how but he's probably got a limited
amount of time to get something done and learning JavaScript and HTML5 is not
going to fit in that amount of time.

I have several ideas about that which I can list in another post.

Today though I was working on automatic uploading new versions of
HappyFunTimes. There's a lot of steps and it's best to automate them. Since I
expect lots of bugs it's best I automate that early to avoid the frustration of
updating and hopefully so I don't forget a step and mess up.

One of the issues is keeping everything in sync. To make a release I need to

<ol>
<li>Create an installer for Window</li>
<li>Create an installer for Mac</li>
<li>Check what the newest version of HappyFunTimes is online</li>
<li>Check what version I have locally and make sure it's newer than the one online.</li>
<li>Check the versions of the installers match the version I expect them to be.</li>
<li>Create a github release</li>
<li>Upload the installers</li>
</ol>

At least that's what I thought the steps were. One issue though is that when I
make a release on github it takes a snapshot of all the files in the repo. It
would nice of those files matched what's in the installers. Especially because
if you want to install in Linux I don't have an installer so it would be nice
if you could get the correct version of the files from github. In order to do
that I'd need to check

<ol>
<li>That my local git repo is <em>clean</em>.

In other words I need to prove there are no changes sitting around not committed.<p></p></li>
<li><p>That the local git hash matches the one one github

This proves the files on github match the local files</p></li>
</ol>

So I checked if there's an easy way to do that. I think there is. But ... then
I realize I should probably do the same thing when you publish a game. I've
already written all the code to automate publishing a game although it doesn't
have that feature.

But, then I realize my code for publishing a game is all written using node.js
and requires using git and github. I suspect more often than not Unity
developers don't know github nor git and I suspect most of them don't have the
time to learn.

I'm not sure what to do there. I think the system is automated enough that if
you didn't know git and github and all you wanted to do is publish a game you
could do that by signing up with github, then typing one command and entering
your github username / password. That would upload your game. That's not really
appropriate for github though. Github is only free if your game is open source
which means you need to check in all your code at least.

Hmmm. I'm going to have to think about this. Maybe I could check the code in
for you if you want? Or maybe MVP just means you've got to learn github and git
and I can try to get that more automated later.

I know the devs that know git and github generally think "yea, do that. It's
easy" but having worked with less experienced devs I know there's some big and
frustrating hurdles there.

