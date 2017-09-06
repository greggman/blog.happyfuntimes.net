---
title: Thinking outside the Box - Making HFT Games
date: '2015-01-17'
layout: post
excerpt_separator: "noexcerpt"
permalink: /blog/thinking-outside-the-box-making-hft-games/
tags:
  - HappyFunTimes
dsq_thread_id: '3427561655'
---
UCLA ran a game jam for HappyFunTimes in December (2014). At the start of the
jam I gave a short presentation about HappyFunTimes. It seemed like there were
some ideas that would be good to pass on so here it is reproduced.

<img src="/images/2014-12-gamejam/superhft.jpg" alt="super happy fun times game jam" />

The presentation started with some of my history of which you can find too much
of on my [gamedev blog](http://games.greggman.com). Otherwise I started off with actually showing the system and letting people
play through it. I really need to find a video of that because the videos I
have really don't do HappyFunTimes justice IMO.

<iframe width="640" height="360" src="//www.youtube.com/embed/dre02sXVgPQ?rel=0" frameborder="0" allowfullscreen=""></iframe>

So after that we got into a few specifics

<style>.slide {  border: 1px solid black; box-shadow: 3px 3px 5px 6px #ccc; padding: 1em; margin-bottom: 2em } div.slide li { font-size: xx-large; }</style>

<div class="slide">
  <h1>Why it's Easy!</h1>
  <h2>Phones are just controllers</h2>
  <image src="/images/2014-12-gamejam/controllers-vs-phones.gif"></image>
</div>

Most networked games require all kinds of crazy tech. For example an FPS
requires that one computer "run the game". The other computers send their input
to that computer. That computer then sends back the new player positions and
results. But, because that takes time each computer running the game just goes
ahead and renders the game assuming it knows what's really happening. When it
finds out from the main computer what really happened it to morphs from where
it is to where it's supposed to be. It's a lot of work and a PITA.

HappyFunTimes games on the other hand there's only one computer running the
game. The phones are just controllers. That means it's easy. From the point of
view of the game it's just like 10, 20, 100 joypads being connected. Super
easy!

<div class="slide">
  <h1>Design Considerations</h1>
  <ul><li>Players can connect or disconnect at anytime.</li><li>Players with nothing to do will leave</li></ul>
</div>

Even though I mentioned this issue many people forgot about it in their
designs. So let me re&minus;iterate <strong>PLAYERS CAN CONNECT OR DISCONNECT AT ANYTIME!</strong> To give an example of issues, many people have made games that require a
specific number of people. Say for example exactly 8 players. If you have 20
people in the room which 8 get to play? Anyone can connect to the game. It's
possible someone might connect and not even be paying attention. On top of that
people can disconnect. Maybe they get a call on the phone and answer it. Maybe
you made a turn based game and they got tired of waiting for everyone to take
their turn. You've got to take this into account in your designs.

There are solutions. One, you can design a game where people can come and go
whenever. Another is you can save some kind of session id on the player's phone
so if they disconnect then when they reconnect you and restore their state.
But, the point is you have to take that into account. For example one team made
a Risk like game. They expected everyone to stay in the game the entire
10&minus;30 minutes. What happens if someone leaves? Their game didn't take
that into account.

In my own learning experience I made the [boomboom game](https://github.com/greggman/hft-boomboom). It has 2 minute rounds. Originally when you died you were out until the next
game. The first time I showed it at a party I noticed people who got knocked
out just left the game and stopped playing. The solution was to let them play
even after they got knocked out. In Boomboom players that die get put on the
edge of the arena where they can throw bombs in and collect powerups. That way
they still have something to do. They can try taking the other players out to
end the game sooner.

<img src="/images/2014-12-gamejam/boomboom-413-players.jpg" alt="Too Many Players?" />

Can you have too many players? HappyFunTimes has no limit. The limit is only
your networking equipment and whatever latency issues you end up having. A
gazillion players will certainly have latency issues. But, even with only 30
players it quickly gets impossible to find yourself. The picture above is
boomboom with 413 players. In that particular case 400 of them are random AI
players but it gets the point across. Players can't easily find themselves even
with 25 players. I've run boomboom with 92 players once. Most people are dead
before they even figure out where they are.

What that means is you should consider how many players you want to support.
Maybe you're fine with 10&minus;30 players but if you want to make a game that
supports 50&minus;100 players you're probably going to have to have teams or
put a radar on the phone or do something to help players have a meaningful
experience.

<div class="slide">
  <h1>Multi-Screen Simon</h1>
  <img src="/images/2014-12-gamejam/simon.gif" />
</div>

At the time of this presentation the majority of the sample games I'd made had
been what my friend Atman would call "low&minus;hanging fruit". They're just
old games with lots of players. The phone is just simulating a simple game
controller. That's great and there's nothing wrong with that but there's so
much else that can be explored. The phone parts run in HTML. You could easily
make games where there's 50 buttons on the screen. Or games where every player
has different controls. Games with sliders or dials or a simulated slingshot.
You can use the device orientation. On Android/Chrome you can use the camera
and the mic. Games where the controls change by game mode. The point is <strong>THINK OUTSIDE THE BOX</strong>.

For example what about some kind of giant [Simon game](https://en.wikipedia.org/wiki/Simon_(game)). I'm not saying a Simon game is going to be super fun but using everyone's
phone to make a large control surface sounds like it could lead to some
interesting ideas.

<img src="/images/2014-12-gamejam/team-games.png" alt="Team Games" />

How about team games. In the game above blue and green form one team, red and
yellow form another team. They need to go find each other in the room and press
the correct button on their partner's phone.

Of course I suppose Red could just shout out "Hey, Yellow Player! Press the
Airplane!" so you might have to design it such that it's harder to cheat. On
the other hand people play board games and card games all the time where it
would be easy to cheat and the don't so maybe you don't have to worry about
that.

Another thing this example points out is you don't have to use the "one" big TV
screen. A game could just be played one phones. Maybe all the "one" big screen
does is announce the start of rounds and the winners.

Yet other idea is using HappyFunTimes to make games that help people to be more
social. Maybe a game where you have to walk around the room and introduce
yourself to the person who's phone matches the color on your phone and ask them
whatever question is on the phone.

<div class="slide">
  <h1>Team Trace Race</h1>
  <img src="/images/2014-12-gamejam/finger-race.gif" />
</div>

In this example players are put in teams by color. So for example everyone with
a blue background is on the blue team. One the game starts the blue players
need to find each other and then figure out how to arrange their phones to make
the figure complete. Once they do that they then have to trace the figure.
First team to trace their figure wins. The game can know if they cheat because
it knows the end of the figure on phone &#0035;1 needs to be touched before the
start of the figure on phone &#0035;2 etc..

<div class="slide">
  <h1>Controllers are Web Pages</h1>
  <pre>
    &lt;div id="buttons" class="hft-fullsize"&gt;
      &lt;div class="button" id="left">◀&lt;/div&gt;
      &lt;div class="button" id="right">▶&lt;/div&gt;
      &lt;canvas id="avatar">&lt;/canvas&gt;
      &lt;div class="button" id="up"&gt;▲&lt;/div&gt;
    &lt;/div&gt;
  </pre>
  <img src="/images/2014-12-gamejam/jumpjump-controller.png" />
</div>

Making controllers is easy because they are just web page. Just make some HTML,
use any frameworks you want. JQuery? Pixi? Three.js? (although if you use WebGL
you're limited to players with Android and iOS8+).

<div class="slide">
  <h1>Controllers are Web Pages</h1>
  <img src="/images/2014-12-gamejam/phone-is-webpage.gif" />
</div>

But, at the same time, it's a webpage. That means the browser can get in they
way. For example iOS8 added these bars you can't get rid of &#128526;

<img src="/images/2014-12-gamejam/easy-less-easy.png" alt="Easier or Less Easy" />

So, it might be easier to make portrait controllers instead of landscape
controllers. On Chrome you can use the fullscreen API to get rid of all the
browser UI. Hopefully iOS 8.1 or a future version will add something similar.

<div class="slide">
  <h1>Chome Dev Tools FTW!</h1>
  <img src="/images/2014-12-gamejam/LeadingBlackandwhiteBorzoi.gif" />
</div>

Chrome dev tools (and I'm sure Safari and Firefox and maybe even IE11+) have
some incredible features that can help you design your controllers.

It's important to remember your players will have a variety of phones from a
tiny Android to a giant iPhone 6+ or Samsung Note 4 or even an iPad or Android
tablet.

What does that mean for you? Well for example one team made a Risk like game
with really beautiful controls for choosing your move. But, they were using an
iPhone 5s to build it on and when it came time to actually play the game some
players had iPhone 4s and the controls didn't fit on the screen. How you solve
this is up to you. For a turn based game it might be okay if you can scroll
through a larger controller. For an action game it might be best if you keep
the controls as simple as possible. Another solution is to make multiple
controls, one set for people with small screens, another for people with
midsized screens, yet another for people with giant screens. That's up to you
it's just important to be aware of.

<img src="/images/2014-12-gamejam/phone-sims.png" alt="Phone Simulators" />

Phone simulators are your friend. At least the iPhone one in [XCode](https://developer.apple.com/xcode/downloads/) if you're on OSX is fast and easy to use. It's not perfect because you can't
easily simulate device orientation for example but if your game doesn't need
that feature it's great. Apparently the new [Microsoft Android simulator](http://blogs.msdn.com/b/visualstudioalm/archive/2014/11/12/introducing-visual-studio-s-emulator-for-android.aspx) can simulate device orientation. The normal Android SDK simulator is crap so
don't waste your time with that one.

Also be aware that you can [remote debug both iOS Safari and Android Chrome](http://developer.telerik.com/featured/a-concise-guide-to-remote-debugging-on-ios-android-and-windows-phone/) which can be a huge help.

<img src="/images/2014-12-gamejam/windows-r-ur-friend.png" alt="Use Browser Windows" />

You can simulate lots of players by opening browser windows. That much much
MUCH faster and easier than connecting phones every time or using the
simulator. For action games it's often a good idea to include keyboard controls
which is much easier to test on your computer then using the mouse to simulate
touch controls.

---

And that's about it. After that we made games. I'd love to show you the games.
I'm waiting on the UCLA Game Lab to post some stuff from the jam. Until then
here's a small preview of one game from the jam.

<iframe width="640" height="360" src="//www.youtube.com/embed/FBsDF4qLF7w?rel=0" frameborder="0" allowfullscreen=""></iframe>