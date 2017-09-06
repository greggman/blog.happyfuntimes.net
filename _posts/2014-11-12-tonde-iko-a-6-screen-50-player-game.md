---
title: 'Tonde Iko, a 6 screen 50 player game'
date: '2014-11-12'
layout: post
excerpt_separator: "noexcerpt"
permalink: /blog/tonde-iko-a-6-screen-50-player-game/
tags:
  - HappyFunTimes
dsq_thread_id: '3216361411'
---
Some friends and I made this game using HappyFunTimes for the 2014 Steam
Carnival

<iframe width="640" height="360" src="//www.youtube.com/embed/aFMNmKYE8KM?rel=0" frameborder="0" allowfullscreen=""></iframe>

There's [a little bit more info here](http://greggman.github.io/hft-tonde-iko)

I learned that I really hate working alone. If anyone wants to partner up
please hit me up. I can't guarantee I'll say yes but I am looking.

I also learned that like HappyFunTimes you just have to make something and
iterate. Lots of things got added to the game as it was made.

It started because John Alvarado, the tech lead of the Wasteland 2 sequel, saw
HappyFunTimes and some how knew about Steam Carnival and thought it would be a
good match. His boss, Brian Fargo, was apparently friends with Brent Bushnell
and introduced us and they immediately sounded interested.

They asked what I needed. I said something like "Imaging you had like 15
projectors projecting along a 100ft wall". I think I asked for 20 monitors.
They gave me 6\. Good thing too because filling 6 with content was a lot of
work.

The game started as  a fork of [jumpjump](http://github.com/greggman/hft-jumpjump). The first thing I did was add the ability to run multiple games and have them
talk to each other. My test was using JumpJump. That worked pretty quick. I
made portals, when you jumped into a portal you'd appear the corresponding
portal in the next game.

My initial plan was just to basically keep the game just like jumpjump used to
be. I wasn't planning on making it prettier.

<img src="/images/tonde-iko/jumpjump-old.png" />

But then I needed to be able to design levels faster than typing them in in
ascii in source code I googled "open source tiled map editor" or something like
that and the first hit was [Tiled](http://www.mapeditor.org).

I downloaded it and set out to write code to read its files. I saw that by
default it used .TMX files which were in XML so I wrote some code to parts the
XML and create data the matched jumpjump. Once I got it all working I submitted
it to the Tiled issues incase someone else needed it. That's when I was
informed that Tiled directly supported JSON. DOH!! I had just wasted a day.

I switched my code to use the .json then made it load the graphics as well. I
then went and searched for open source art. I found several tilesets and tried
to use them. I made 3 of 6 levels. It took way longer than I expected.

<img src="/images/tonde-iko/level0-sm.png" />

<img src="/images/tonde-iko/level1-sm.png" />

<img src="/images/tonde-iko/level2-sm.png" />

I also made the levels 1920x1080 and it was working great. The steam carnival
guys asked me to stop by and show them how it was going. I showed them and
Brent suggested players should be able to jump/walk off the edges of the
screens to go from screen to screen instead of having to go through a portal. I
have no idea why I didn't do that originally. I think maybe it was because I
was hoping for a more random arrangement of monitors. Anyway, I added that in
and that was clearly better.

I also found out the game would be running on Intel NUCs. Specifically I3 NUCs
with Intel 4000 graphics. I borrowed one, tried the game out, it ran too slow
on a NUC at 1920x1080. The Steam Carnival guys had said they'd figure something
out if that was a problem but I didn't want them to have to go buy new machines
so I just decide to make the game run at 1280x720. I made a test level and I
could get 3 layers of tiles at 60fps at that resolution.

That turned out to be a blessing. I was using 32x32 pixel tiles and at
1920x1080 they were pretty small. I was hoping the TV would be large but they
ended up being 42inch TVs. 32x32 pixel tiles at 1280x720 on 42inch TVs turned
out to be just the right size.

At this point I was freaking out a little though. Given that it had taken about
8 hours per level to make and given that I had to redo all the levels I was a
little scared about how it was going to turn out. I tried to tell myself if it
just looked like the original JumpJump but 6 screens maybe that would still be
okay.

Fortunately John and his son Zack said they would help. I warned them it was
going to be a lot of work. John has a full time job and Zach is still in high
school. John assured me the really wanted to contribute and that they could put
in the time. I'm so thankful they were able to do that.

Zack has apparently been making pixel art for his own games for a while now so
he set off to make new tilesets. I had originally assumed he'd probably make
only 1 or 2 and we'd use the open source ones I had found but Zack is amazing
and did 5 tile sets. I really helped that he had lots of experience so he knew
exactly how to make efficient sets that could easily build levels.

Zeyu, a student at UCLA, offer to make backgrounds, graphics that go behind the
level. I was really worried that he might make something gaudy that clashed
with the levels and made it hard to see what's level and what's background but
what he added was perfect. Exactly what it needed to be.

<img src="/images/tonde-iko/level0-with-bg.gif" />

John freaked me out a little because he wanted to add lots of stuff and all I
wanted to do was be done. Fortunately he assured me he could get the stuff he
wanted to add in done quickly and he did. He added a kind of basketball game.
He added a present you could collect and exchange for a birthday hat at the end
of the game. Actually there's a funny anecdote there. On the last level there's
a cake. If you have a birthday present when you get there you get a birthday
hat + 500pnts. After that it is literally 1/4 screen to the end of the level.
In other words it's like 2&minus;3 seconds before the end of the game. I was
thinking no one was going to care about the birthday hat. In fact I thought no
one would even notice because I thought they'd make it to the cake and then
immediately head to the exit and not even notice. Well, the first day one of
the first kids that made it to the end of the game, when he go the birthday hat
he shouted and jumped up and down "I GOT A BIRTHDAY HAT! I GOT A BIRTHDAY
HAT!".  In my defense I didn't suggest getting rid of the hat. I suggested more
fanfare to make it very clear. We did add more fanfare. There's 5 shots of
confetti that cover the screen when you get the hat so I hope that helped
&#128515;

John also ended up designing most of the levels.

Another interesting thing was just watching people play the game. We ended up
changing things every day. In fact we even changed a few things while players
were playing.

For example we saw places players seemed to get stuck. Places where jumps were
too hard or where because of previous moves they'd likely fall some place over
and over and over. We fixed those over a couple of days.

Another example was the portals. Originally you'd get stucked into the portal
and then magically pop out at it's destination. They were color coded so a red
portal would take you to a red portal exit but players would get lost. John
made it so the player would go in a line from the portal to its exit while
spinning. That made it easy to see where your character went and really made
that feature work.

Another one was the doors. I had decided to put doors in the game. If you got
near one a progress meter would appear which would count down for 5 second at
which point the door would open. There was also a switch you could stand on
that would open the door immediately but it was too far from the door to allow
you to get through after you jumped off the switch. The point was supposed to
try to force players to help each other. One player could stand on the switch
and keep the door open for another player but if there were no players around a
player could still just stand by the door and it would eventually open. Well,
no one seemed to get it.

We changed to so standing on the switch the door opens immediately and the
progress meter starts filling up. As soon as you get off the switch the meters
starts going down and the door closes when the meter is empty. People
immediately got this. You can still help each other through the door and it
still does help a little in nudging players together but with the new behavior
people don't get confused. It often takes 2 or 3 tries but they figure it out
which I think they also enjoy.

Even with all that and it looking really good when I went to show it on a
Wednesday night, 3 days before the main event, it wasn't working. 3&minus;4
people could connect but then no one else could. I'd reset the whole thing and
even then people could rarely connect. I was really sweating bullets.

I bought 2 new routers, an Apple Airport Extreme and a ASUS 2700 something or
other. I bought a new network switch and I brought my Macbook Pro to run the
happyfuntimes server. I have no idea which one of those things fixed it or if
all of them contributed but fortunately on Friday it was working great and it
felt really good to see people enjoying it.

I'm glad we got a chance to make it. I'm really glad Zack, and John, and Zeyu
were there to make it way more awesome than I could have done myself. I hope I
can find more people to help make more cool HappyFunTimes games.