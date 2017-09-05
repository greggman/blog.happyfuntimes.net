---
title: The Story of HappyFunTimes
date: '2014-09-15'
layout: post
permalink: /blog/the-story-of-happyfuntimes/
tags:
  - HappyFunTimes
  - SuperHappyFunTimes
dsq_thread_id: '3084824501'
---
I never intended to make HappyFunTimes what it is today. This is I guess an
example of what happens when you just do something. Things happen.

It started off when I was working on Chrome. I learned about WebSockets. I
might have seen some tutorial on how easy they are to use. I think I read about
Socket.IO, a popular library that can use WebSockets and it just occured me, as
it has several others, that it would be easy to use WebSockets to make certain
kinds of games.

My first game was [PowPow](https://code.google.com/p/powpow/). You can see the commit history shows it was made around April 10, 2011\.
That's 3 years before I started on HappyFunTimes. In fact the video linked to
on that page is from April 8th. At the time I had people using their laptops as
controllers. After that one day playing I tried making phone controllers. Being
April 2011 it was still common for Android phones NOT to have multi&minus;touch
or to have broken multi&minus;touch so if you go look at the code in that repo
you'll see the iPhone controls are Left/Right/Fire (3 fingers) but the Android
controls are "point the direction you want to go, tap to fire" (1 finger)

At the time I thought it would be good to make a library but when you're
working full time, or when I am, it's often hard to find motivation to do
things outside of work. I suppose that's kind of stupid since I made PowPow
outside of work but it only took a few days. So, I guess I have no idea why I
find motivation for some things and not others. If I had infinite time and
infinite motivation there are sooo many things I'd work on.

As a side note, in 2012 I used the same tech for our Molyjam game, "[Octopi Everything](https://github.com/greggman/octopus)" which I plan to port to HappyFunTimes (if I can motivate myself &#128539;)

Then last year in June 2013 I quit my job at Google. I traveled and goofed off
and didn't really know what I wanted to do. In March I found myself in Kyoto
for Bitsummit. There I met Eddie Lee and Kalin of [Funktronic Labs](http://funktroniclabs.com) along with [Sagar Patel](https://twitter.com/sagzorz), [Andrew Palmer](https://github.com/andyp123), and [Edwon](http://www.edwon.tv/). Also in Tokyo I had previously met [Alvin Phu](http://dotwarriorgames.com/) and they were all so inspring. Everyone was working on something. Alvin in
particular had a fulltime job with crazy Japanese overtime and still was
working his ass off on his own game.

So, I started feeling like I should get off my ass and start working on
something. I still had no idea what but I should at least spend time making
something, anything. I thought about it and though, "ok, fine. I guess I'll
turn that code from powpow and octopi into a library finally and then maybe
make a mobile game after". I thought it would take at most a couple of weeks. I
didn't intend to make any money. I just thought it would be fun to put out the
library and maybe have a game jam (which I still need to do!)

And, it did only take a couple of weeks at most. A few days to pull out the
library. A few hours to make the [first sample](http://github.com/greggman/hft-simple). But, if you've been to a game jam in the last few years or paying attention
to indie dev everyone and their sister is using Unity3D. So, I felt like if I
wanted to get any usage I needed a Unity3D version so you could make the games
in Unity. Since [the controllers have to be written in JavaScript](#why-javascript) I needed JSON support for Unity because JSON is how JavaScript communicates.
There's something called JSON.Net but it didn't fit my use case. It's a fine
library I guess but in order to support the features I needed it required .NET
4.0 and Unity only supports .NET 2.0. So, [I had to write my own](http://github.com/greggman/dejson.net). That was probably several days of work. As another aside I find it super
frustrating to think "I'm going to do X and I'll be done in a couple of hours"
only to find that I first have to do "Y" which itself is going to take hours to
days. I did get to learn some deep dark secrets of .NET though and with that
working I reproduced [the simple example in Unity](http://github.com/greggman/hft-unitysimple)

Next up I thought I should try dual stick controls. Partly because I wanted to
make a unity example that shows walking a character around. So I hacked
together [ShootShoot](http://github.com/greggman/hft-shootshoot).

With that working I got a [unity character example working](http://github.com/greggman/hft-unitycharacterexample) which didn't take too long but took longer than expected dealing with
UnityScript vs C&num; issues.

After that I wanted to see how a platformer would play so I threw together [JumpJump](http://github.com/greggman/hft-jumpjump/) and shortly after that I decided I wanted to make something showing off round
based play among other things and wrote [BoomBoom](http://github.com/greggman/hft-boomboom).

I ran into another issue which was I could not get consistent performance out
of Chrome using the Canvas 2D api so I ended up writing JumpJump and BoomBoom
in WebGL. That ended up making some useful libraries like a [single quad single draw call tile map renderer](https://github.com/greggman/hft-utils/blob/master/dist/tilemap.js) as well as a [runtime color adjustable sprite system](https://github.com/greggman/hft-utils/blob/master/dist/sprite.js).

In writing these games though things kept popping up. For example, originally
you'd need to go to long and complex Urls. To play jumpjump for example you
might open a browser and go to `http://localhost:8080/examples/jumpjump/gameview.html` then you'd get out your phone and go to `http://192.168.2.9:8080/examples/jumpjump/index.html`. That's a lot to type, especially on a phone. Of course I used bookmarks and
other things to make it go faster but eventually I got tired of typing so I
thought, "hmm, I'll write a script that generates an index.html that lists all
the controllers". I wrote that. I also wrote ones to list the games. Now I
could go to `http://localhost:8080/games.html` to pick a game and controllers could go to `http://192.168.2.9:8080/` and pick the corresponding game. That was much better. So much less typing.

But then, I realized if there's only one game running why not just send the
controller there automatically. So added a script to the page contollers go to
that lists the games to check which games are running. If there is only one
just go to it. This was awesome. Now I'd start a game, then on the phone I'd
just go to `http://192.168.2.9:8080` and it would automatically join the game! It seemed so awesome!

That led to the next step. Using the same code, when game disconnects the
phones get notified so I used the same code that checks if any other games are
running. If there is only 1 game running I jump to that game. The effect was
that the system felt like a virtual console. I'd start it up, phones would
connect, they'd jump into the game, and if I switched games they'd all jump to
the new game. This was feeling really really great. There was even the added
and unintended bonus that I reloaded the same game the controllers would see
that as the one game running and reconnect. That was great for development. I'd
tweak the game and click "reload" in the browser. That would have the effect of
having all the controllers auto&minus;reload. Faster iteration times FTW!

It still sucked though to ask people to go to their phone and type in something
like `http://192.168.2.9:8080`. I knew about Captive Portals. They are those things you see when you use
hotel WiFi or coffee shop WiFi and it asks you to log in inside the browser. If
I could get HappyFunTimes to support something like that I could make it so
when players connect to the WiFi they automatically connect to the game, no
typing anything at all. It took a few days but I got it working. Note that
feature only works on iOS and it only works if you configure your router a
certain way to let HappyFunTimes respond to certain requires but the effect is
pretty amazing. On Android some of the same code means if HappyFunTimes is
setup this way users can just got to any Url to connect so I tell them go to to `h.com` or something like that and they connect.

These things are simple to explain and maybe it seems obvious but my impression
is most people don't really get it until they see it in action. I think even
tech heads think "Yea, type some long address and you're in" but when I
actually demo HappyFunTimes in a room full of people and they see everyone
effortlessly connect and play some games and they see me switch everyone to new
games and go through all the demos it's pretty impressive.

Announcing HappyFunTimes got a few people using it and I quickly realized I had
some problems. All the games had to be checked into the same repo, or at least
there was no easy way to separate individual games from the system. On top of
that I had tried to show it at a certain event run by industry people. I sent
them a link thinking "these are game developers, they won't have a problem
following the 5 steps to install to check it out".  Instead I got back a
message something like "Wow, that looks hard". Of course at the time I didn't
intend for end users or regular gamers to install it but gees!!, if an actual
developer was bitching about installing node.js and cloning a git repo then
there's no way anyone else is ever going to get anywhere except for the most
dedicated.

So, those two issues led to do things.

<ol>
<li>I absolutely had to make an installer for at least Windows and OSX

It had just install and work, no setup.<p></p></li>
<li><p>I had to find a way to separate the games and make it easy for others to add their own games to the system.</p></li>
</ol>

Those two things led to several features. For the installer it wasn't enough
just to install. I also had to come up with a way to easily connect phones to
the local game without having to configure your router and without having to
type long cryptic Urls.

My first solution was to make happyfuntimes.net and write a script that scanned
for the local happyfuntimes. Basically if you're running Chrome on Android it
could figure out your local ip address. Say `192.168.2.37`. It would then ping every address on that network and see if it got the
correct response. It worked! But, iOS Safari doesn't have the feature to look
up the local ip address. My next solution was if I can't find out the local ip
address then I'll just guess. Most routers use a common set of addresses. I'll
just try them all. Unfortunately trying them all took &gt; 5 minutes. I added
some heuristics to guess better and therefore faster but it mostly didn't work
well.

Then the more obvious ideas was I should change happyfuntimes.net so when
happyfuntimes starts it tells happyfuntimes.net its ip address. When a phone
goes to happyfuntimes.net, happyfuntimes.net can see the matching ip address
and tell the phone where to go. Problem solved!!  Telling users to go to
happyfuntimes.net is not as nice as auto&minus;connecting but it's not a
cryptic Url so it's easy to explain to users. Of course I wish is was just `hft.com` or something simularly short but short URLs are expensive &#128526;

Next up was separating the games. npm, the node package manager, suggested a
way to do it. It took a lot of trial and error though to finally get it working
but the result is http://superhappyfuntimes.net and the related system.

The funny thing is though I never intended to take it this far. Each piece is
just the next logical step as I built things up. I don't know if there is
anything to take away from that except that just doing stuff for the hell of it
often leads places. Make some simple game or demo or app and you'll likely end
up with pieces of code or tech that you can use on the next thing or you'll see
how to tweak what you're making into the something else and after a while
you've made way more than you ever expected. I guess like they say, "Just do
it!"


### Why JavaScript

There are several reasons.

<ol>
<li>It means no install required. Users can show up at some event and participate immediately.

Potentially even other phones like Firefox OS phones or Windows phones or Xiaomi Phones <em>should</em> all work.<p></p></li>
<li><p>It requires no approval from Apple.

I'm happy that Apple seemingly does a good job of keeping malware off of iOS but I'm not so happy that they have to approve every app. Even if your app is not malware they might say no.</p></li>
<li><p>It lets anyone make a custom controller.

</p><p>Theoretically you could use any language but Apple strikes again. Even <em>if</em> I decided to make an app Apple does not allow code to be downloaded into an iOS app except for JavaScript executed by Safari embedded into your app. So, even if I made an app, JavaScript is the only choice Apple allows. Of course you're always free to transpile from some other language into JavaScript. With iOS8 now finally supporting WebGL that means in the near future the sky's the limit on where to go with controllers in JavaScript! I'm looking forward to what people come up with.</p></li>
</ol>