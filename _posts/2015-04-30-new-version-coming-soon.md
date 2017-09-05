---
title: New Version Coming Soon
date: '2015-04-30'
layout: post
permalink: /blog/new-version-coming-soon/
tags:
  - HappyFunTimes
dsq_thread_id: '3724924797'
---
I've been trying forever to ship a Unity3D plugin. After seeing [Uniduino](http://www.uniduino.com/) though and working with the art/design students at UCLA I felt like I needed
to do a lot more work before shipping it. Lots of docs, videos, etc... Still
not done but

<!-- more -->

I was going to try to push it today and .... my mac broke.  Sigh....

Anyway, hopefully I can push out a new App soon and get the plugin out as
well.

The latest plugin does a few things the old one didn't

One it handles the name system a little better. The old manual way still works
but otherwise `NetPlayer.Name` will always hold the current user's name. If you want to know if it changed
add an event listener to `NetPlayer.OnNameChanged`

Another is the plugin will now launch HappyFunTimes if it's not already
running. Similarly if it can't launch it it will direct you to install it.
Hopefully that will make it easier for non&minus;techies to get started

Also added a `PlayerConnector` script. Most of the examples use the `PlayerSpawner` script which spawns a prefab anytime a player connects. This allows many
players to play. 10, 20, 30 is not uncommon.

The `PlayerConnector` script on the other hand helps you to connect players to `GameObject`s already in your scene. That fits the use case that many users have that just
want to use the phone for input but don't want to support lots of players, just
the 1 &minus; 4 they have already in their scene.

The `PlayerConnector` also has the option to let a disconnected player reconnect. You can set how
many seconds they have until their player is given to someone else waiting to
play. You can also swap players. So let's say you have a 3 player game and 5
people connect. 3 play the game, when one dies you can tell HappyFunTimes to
swap out that person for one of the other players waiting to play. You can use
a similar feature boot out all players at the end of round and take the next
set of waiting players.

Hopefully you'll find those features useful.... once I get access to a machine
I can code on (current at an internet cafe)