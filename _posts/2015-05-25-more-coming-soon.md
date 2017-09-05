---
title: More coming soon
date: '2015-05-25'
layout: post
permalink: /blog/more-coming-soon/
tags:
  - happyfuntimes
  - HappyFunTimes
dsq_thread_id: '3814308784'
---
I've spent some time getting a native phone app working. I don't like the idea
of an app because it can make things complicated for the user (attach to HFT
WiFi, wait you didn't download the app? Detach from HFT Wifi, download app,
reattach to HFT wifi, launch app) Ugh! Or, if your HFT Wifi has internet then
you probably get the problem of everyone using it to watch youtube videos and
post images to fb/twitter/instagram and eating all your bandwidth making
interacting with your installation really laggy &#128526;

But, Eddo at UCLA can't or won't find creative solutions for the limits of the
browser on iOS so he wants an app. So I've made one. It seems to work but will
still take weeks to get on the app stores (iOS and Android). I'm worried it
will ruin HappyFunTimes though. Devs will assume they should use the app. The
experience will suck. No one will get it.

On the Android front though I made the non app (browser) version go fullscreen.
At least on my tests it works. One of the problems with HappyFunTimes and
phones it's (a) it's hard to test anything without more people and &#127866;
it's hard to find out what issues there will be without lots of phones.

Anyway, that  removes some of the need for an app on Android. Once the browser
has gone fullscreen there's no more address bar, back button, etc and you can
control the orientation (no more "please turn your phone" for landscape
controllers.

The app also means I can prevent the phone from going to sleep. On the other
hand you still have all the normal phone issues of different phones with
different screen sizes and different versions of their internal webview so you
still need to be conservative and/or creative in your designs.

One thing that's killing me is all the testing required to get this stuff to
work. Examples: Need to test launching the app on iOS and Android. Does it
connect to your game. Need to test both apps, do they correctly disconnect if
you exit the app. Need to test do they recover from a bug in the controller.
Need to test they switch games correctly. Need to test if you use the browser
to go to the game it switched you to the app. Need test if you use the
auto&minus;connect installation mode all those paths work. That adds up to
hours of testing. People might say find an automated way to test but given
there's 3&minus;4 moving parts (the phone or simulator, the phone's browser,
happyfuntimes running somewhere, happyfuntimes.net running locally, etc) and
you need touch guestures on the phone and exiting and re&minus;starting the app
for certain tests I'm at a loss of how to test other than manually. Even if
there was a way I suspect it would take 4&minus;8 weeks of work to get it
setup.

That doesn't include the testing I need to do just for HappyFunTimes itself
like testing OSX and Windows installers work, that the Unity plugin works on
both platforms starting from a fresh install, and other things. I fact I
shipped a broken version, 0.0.26, where I had quickly changed the buttons on
several samples from text icons to svg images. At a glance it seemed to work
but then it turned out of you long pressed both Android and iOS would pop up a
"Save Image?" message. DOH!!! Preventing that required different workarounds
for both browsers. 0.0.28 should be up that fixes that.

I'm also working on getting HTML5 Gamepad emulation working. Actually I have
that working and am in the process of cleaning it up. With that, if you already
have an HTML5 game with gamepad support you can just add a script to your page
and get HappyFunTimes support. I'm mixed on if that's a good idea because most
games designed for the gamepad API probably need a full Xbox style controller
with 12 buttons, 2 analog sticks and a d&minus;pad. Using HappyFunTimes for
that will probably make HappyFunTImes look bad because as we all know touch
screen d&minus;pads suck! On the other hand though if someone is at a gamejam
and they're using an HTML5 based game engine they can use HappyFunTimes with
almost no changes, just design the game to handle as many players as possible,
add the script, bam! It also means once Unity5 and Unreal start supporting the
HTML5 gamepad API (assuming they don't already) then you could use that too.
...Although I'm just going to guess without looking that they put some
artificial limit on the number of controllers in their API &#128526;

The reason that came up is we had a short 2 button game jam at the [Pico Pico Cafe](http://www.picopicocafe.com) in Tokyo where [Lexaloffle Games](http://www.lexaloffle.com) is based. We decided to try to make it possible to interface Pico&minus;8 with
HappyFunTimes and in the process I realized it would be pretty easy to emulate
the HTML5 Gamepad API. Of course if you use that you're probably not really
taking advantage of [all the interesting creative ways you could use HappyFunTimes](/blog/thinking-outside-the-box-making-hft-games/) but I'd rather you use it then not. Maybe you'll be inspired to take it to the
next level &#9786;