---
title: New HappyFunTimes for Unity Coming Soon
date: '2016-05-13'
layout: post
permalink: /blog/new-happyfuntimes-for-unity-coming-soon/
tags:
  - Uncategorized
dsq_thread_id: '4842607609'
---
TL;DR: HappyFunTimes for Unity will soon be a stand alone library.

HappyFunTimes started as a HTML5 project with HTML5 based games and therefore
needed an HTML5 based server to serve those games. Originally I put all my
sample games into the same repo. As I wanted to make it easier for others to
add games I came up with a way for the games to live outside of the main
HappyFunTimes app/folder. This also made HappyFunTimes kind of like a mini game
console since there was a menu to pick games from.

That design influenced how the Unity version worked where games also needed to
be installed because a web server needed to serve the files to the controller
and a websocket server needed to pass the messages from the game to the
controllers.

Well, I'm pleased to announce that's changing. The "game console" like feature
of HappyFunTimes isn't really much of a feature for most people. Most people
make a single game for a game jam, event, or installation and that's all they
need.

So, lately, I've been working hard to make the Unity plugin do everything on
its own. I've put in a web server and websocket server. This means you should
be able to just stick it in any Unity project. No need for special ways to
export. No need to "install it in happyfuntimes". Just export from Unity like a
normal unity project then run the project.

This also means theoretically you could export to iOS, Android, PS4, etc, run
the game there and have people join with their phones. I say theoretically
because I haven't tested those platforms yet.

It also means making controllers is simpler. In the old version the server was
doing lots of stuff. Your controller files got inserted into templates. The
templates used requirejs, something most Unity devs were not familiar with. The
new plugin, since it doesn't have to integrate with anything else, means all
that has been simplified. Make your own full .HTML files however you want. No
more templating getting in your way or messing up your CSS.

Yet another thing you should be able to do is turn it on and off from Unity. In
other words you could make game that supports 1&minus;4 players using
traditional gamepads but have an option to use HappyFunTimes for more players.

Installation mode should still work as will multiple computer based games.

Crossing my fingers people find this more useful.