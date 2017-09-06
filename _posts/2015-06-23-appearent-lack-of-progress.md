---
title: Apparent lack of Progress
date: '2015-06-23'
layout: post
excerpt_separator: "noexcerpt"
permalink: /blog/appearent-lack-of-progress/
tags:
  - HappyFunTimes
dsq_thread_id: '3887491210'
---
a bloggy post...

It's been just over year since I publicly announced HappyFunTimes. Back than I
showed the system at [Picotachi in Tokyo](http://www.picopicocafe.com/?id=picotachi-en) and since then, at least visually, NOTHING HAS CHANGED &#128526;

By that I mean I spent April last year making the games and examples and since
that I've done nothing but infrastructure. And, it's hard to stop doing
infrastructure. It always seems like there's more to do to make HappyFunTimes
more approachable and more to do just to clean up.

In that year a lot has happened and if you look at all the code that's been
checked in to all the HFT repos i've don't a buttload of stuff. There's the
Unity3D plugin. There's the fact that the Unity3D plugin has effectively a 1
step install (after watching art students struggle with the more programmer
oriented way it used to be). That includes making installers for Windows and
OSX and a native (but ugly) app for OSX. It includes [making more docs](http://docs.happyfuntimes.net/docs) and even making a mobile app (though I'm not sure I'm going to push it much
because I feel it also breaks a bunch of stuff. Maybe I'll bring that up in
another blog post).

There's also a ton I feel like I'd kind of like to do. For example I'd like to
re&minus;do superhappyfuntimes.net to not use meteor. I'd probably like to
re&minus;fashion it more as a gallery with much larger pages about each
project. Especially because many HappyFunTimes projects seem to be
installations rather than things you can play at home at a party. But that's
lots of work not making games.

I've thought about switching to use something like Node&minus;Webkit or
Electron as the desktop app. That would make it easy to make UI related stuff
cross platform. For example all the hft command line switches I could make a
cross platform UI for. It would also make it launch with a clear app on all 3
desktop platforms vs just a command line wrapper. But again that's more work
that's not games.

That HTML5 Gamepad Emu lead to the idea that maybe the basic Unity3D plugin
should use the same code so that people just getting started have far less work
to do. If they just want a simple controller they can add it to their game in a
few lines. Unfortunately Unity3D's input system isn't really designed for 100s
of players so I can't just emulate it but I can probably make the changes
needed minimal. Still that's more work that's not games.

And, the truth is, games are all that matters. Games are what people will see.
Games are what people experience when I show it off and so far while [there are a ton of ideas](http://docs.happyfuntimes.net/docs/ideas.html) I've pretty much done none of them. The games I have to show are either
low&minus;hanging fruit of 30 year old games with lots of players or else
simple tech demos just showing that the system works.

So ... I'm trying to whittle down the list of <strong>must do</strong> infrastructure and then concentrate on more games. If you want to collaborate
please speak up!