---
title: Fixing the wrong bug.
date: '2014-09-05'
layout: post
excerpt_separator: "noexcerpt"
permalink: /blog/fixing-the-wrong-bug/
tags:
  - Uncategorized
  - coding
  - code
  - development
  - debugging
  - bugs
dsq_thread_id: '2990083915'
---
This is hilarious. I had `Player`, the server side object that tracks the connection to a smartphone for a
single player, have a heartbeat ping because often players would just stop
playing on their phone by having their browser go into the background. In such
a case they aren't disconnected from the server. So there's this idle player in
the game waiting for a networking message. Maybe "waiting" is the wrong word,
rather it's as though the player is making no input.

I wanted to remove those players so I have a heart beat. If no input from the
player comes in 5 seconds I ping the player's smartphone. If no message comes
back in 1 second I kill the player because his browser is likely no longer
active.

So, I'm trying to ship. I test Unity. When the Unity game quits the players are
not disconnected. My (bad) intuition says "hmm, the socket must not be getting
disconnected by Unity. I don't remember this being a problem but I've almost
always tested Unity from the editor instead of exported apps. I'm testing the
apps. I try disconnecting it manually using OnApplicationExit. No change. I
figure given that maybe because the C&num; websocket stuff I'm using is
multi&minus;threaded it must be that the disconnect not actually getting
executed before the app quits.

Fine, I'll add a heartbeat to the `Game` as well as the `Player`. The current heartbeat code is embedded directy in the `Player` object. I look at the code and see the Player is not deleted when it's changed
into a `Game`. I try refactoring the code so the `Player`'s heartbeat just keeps going but I run into issues. Revert all that and decide
to implement differenty. I'll make the heartbeat code a separate class and have
both the `Player` code and the `Game` code use it separately. Run into issues again and revert all that.

I figure that my heartbeat should go at a lower level than it was. It shouldn't
be at the `Game` / `Player` level it should be at a layer between WebSockets and that. I implement that.
Spend 60&minus;90 minutes debugging. It finally works.

I go back to my Unity sample and test again. Controllers still don't get
disconnected when the game exists even though I know the ping is working.

I finally realise the issue has nothing to do with disconnecting. That was
working all along. The issue is there's a flag the game can pass `disconnectPlayersIfGameDisconnects`. In JavaScript it has 3 values. `undefined` (the default), `true` and `false`. Just a couple of days ago I added it to C&num;/Unity. It defaults to `false` in C&num;! DOH!!!! Changed it to default to `true`.

All that work adding a ping at a lower level had nothing to do with anything.
Works. 6&minus;8 hours mostly wasted. Well, let's hope that's better anyway
&#128539;