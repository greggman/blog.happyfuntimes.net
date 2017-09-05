---
title: Simplifying HappyFunTimes
date: '2016-06-16'
layout: post
permalink: /simplifying-happyfuntimes/
tags:
  - Uncategorized
dsq_thread_id: '4924876524'
---
I’m feeling rather stupid.

So a little over two years ago I started taking the code from [PowPow](http://code.google.com/p/powpow) and turning it into a library. That became [HappyFunTimes](http://docs.happyfuntimes.net) which I’ve spent the better part of 2 years working on.

<!-- more -->

Since PowPow was an HTML5 / Browser based game it needed a server to serve the
pages and manage websockets. It used a node.js based server and so one thing
lead to another

1. Make a server to server the game
2. Make game
3. Make more games in same repo
4. Make game menu so I don’t have to type long urls like

        http://localhost:8080/game/name-of-game/game.html

5. Make controller menu so I don’t have to type long urls on phone like

        http://192.168.1.10:8080/game/name-of-game/index.html

6.  Make controller menu automatically connect to running game so you don't even have to choose
7.  Generate the both menus.

    basically scan the repo/games/*/game.html
8.  Make it possible to have games outside of repo

    Given it’s a web server this means some kind of configuration that says for a given URL path look for that game’s files in some other folder so now instead of scanning there’s a json file that says

        {
          games: [
            “/path/to/game1”,
            “/path/to/game2”
          ]
        }

9.  So then we need to know the name of the game.Now every game needs package.json to supply metadata about the game

Okay, now it feels like a virtual console but we don’t want users to have to
edit the json file sooo.

*    make add game / remove game commands to help edit the json file

*   make install / uninstall commands which will take a zip file, unzip to some folder, then add the path to the json (call add game)
*   since that’s still too much work for users make the system have a website “store” where you can download these zip files and have them installed automatically just by clicking them
*   That means you need a way to make these zip files, to make sure they have the proper package.json, icon.png, screenshot.png, etc.. so make a packaging command
*   Make the server to host these files
*   Make a publish command so users can add files to this server
*   Unity games get built but we need them turned into these zip files since the controller/phone files need to get served by the web server. So, make build command that exports from unity then builds zip file.
*   Unity users are afraid of the command line so make custom unity builder that does it all inside unity.

On a separate path, given that there was this virtual console that all the
games were running in it meant somehow all the games needed to stay compatible
with the virtual console even as I continued to add more features. This lead to
code to deal with versions. The game listed what version of happyfuntimes it
was created with and happyfuntimes would attempt to turn off new features so
the game couldn’t accidentally use them. This also lead to features to check if
the user has the version of happyfuntimes needed for the game. Game needs
version 1.4, user only has 1.3, user gets prompted to upgrade their
happyfuntimes.

On and on and on. All of that added up to months and months and months of work
and all for nothing. No one wanted the virtual console. I’m not even sure I
wanted it. I didn’t really think about it. Rather I started with HTML5 and web
servers and this is just the path it lead to.

So finally a few months ago I decided to make unity serve the files itself (web
server running inside unity). This removed the need for a special build. It
removed the need for node at all. This means users can just export their game
like normal. no special instructions needed. They can put them on itch.io or
steam or wherever they want. no need to register them with my “store”. It
wasn’t totally straight forward but so many things are simpler that way.

So now I’m revisiting the HTML5 stuff. [Electron](http://electron.github.io) has become a thing and it should be relatively easy to make standalone
Electron based versions of HTML5 games (with or without HappyFunTimes).

I’m trying to convert the HTML5 based happyfuntimes games I have to Electron
and as I do I’m deleting 85% of all the code I wrote over the last 2 years. All
the commands for adding, removing, installing, uninstalling games. All the
commands for building the zip, uploading to the store, etc. All the stuff for
listing games installed on your system. All the stuff for versioning. All of
the stuff related to publishing on superhappyfuntimes. All of the stuff related
to downloading from superhappyfuntimes. All of the stuff related to listing
games and controllers.

It’s just so kind of sad so much work kind of wasted. How I would love to get
all that time back.

In my defense &#128539; 2 years ago Electron wasn’t a thing. On top of that 2
years ago I didn’t want to write a C&num; web server. Leaving the server in
node and just writing the minimal code to do the websocket communication was
easy to get things working. It also meant that upgrading the node server (like
installation mode) got added for free to other platforms like unity and that
that would theoretically be true of I added say Unreal support or GameMaker
support. I'd only need to write the client portion of the library (small) and
the server code would be shared.

But, now, in hindsight I can see it was a huge detour. Maybe I couldn’t get to
where I am today without that path. But that doesn’t make it any less heart
breaking to see all that code I wrote turn out to be useless.

