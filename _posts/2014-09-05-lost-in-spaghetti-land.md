---
title: lost in spaghetti land
date: '2014-09-05'
layout: post
permalink: /blog/lost-in-spaghetti-land/
tags:
  - database
  - SuperHappyFunTimes
  - metadata
  - sychronization
dsq_thread_id: '3260312962'
---
I'm having a hard time reasoning about what should go where and who should do
what in this system.

As an example superhappyfuntimes needs a database of games for the game
gallery. Each game needs things like "Name", "Description", "id" and then what?
By that I mean for example if I have a URL to a repo I could figure out the id.
The id will be in the repo's root folder "package.json" file.

Or I could instead have just an "id"&minus;&gt;"repo" map. Then I don't need to
look in the "package.json" file. But, now that data is in 2 places. In other
words if I have an "id"="mario" that points to some repo
"http://mydomain.com/sonic.git" then I look inside the package.json file in
that repo and see the "id"="sonic". Oops?

I guess that's part of the problem with this distributed system. I have to
trust people not to mess it up. At the time I wrote this you send a "repo" url
to superhappyfuntimes. It goes and reads the package.json file as well as the
releases. It then saves that data on superhappyfuntimes something like

<pre><code>{
  "gameId": "Qurby",
  "gameType": "html",
  "name": "Qurby's Fun Times",
  "description": "Qurby with Attitude",
  "repoUrl": "https://github.com/greggman/qurby.git",
  "versions": [
    {
      "version": "v1.2.3",
      "notes": "",
      "releaseUrl": "https://github.com/greggman/qurby/releases/v1.2.3/qurby.zip"
    }
  ]
}
</code></pre>

Now there's an issue though. When I go to install it happyFunTimes will ask
superhappyfuntimes for that info. It will then download qurby.zip from that url
but inside that zip it might say it's actually a different game. This is
arguably no different than I'm guessing Google Play or the App Store. A game
might say in the store its id is "com.someCompany.someApp" but the apk itself
might say it's "com.otherThing.otherApp". I'm sure their stores check the
packages match their ids but being distributed I can't do that before the fact.
I can only do it after.

Similarly since I'm not hosting the files that releaseUrl might no longer
exist. Maybe that's ok. I'll certainly print an error. I'm thinking maybe I
should run some script that checks all the releaseUrls once in a while to see
if they are still valid. If not remove them from the gallery.

I suppose ideally I'd download them and serve them myself but that would cost
money.