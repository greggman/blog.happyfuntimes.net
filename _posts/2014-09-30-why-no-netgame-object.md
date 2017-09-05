---
title: Why No NetGame Object?
date: '2014-09-30'
layout: post
permalink: /blog/why-no-netgame-object/
tags:
  - happyfuntimes
  - HappyFunTimes
  - coding
dsq_thread_id: '3070721870'
---
It's hard to know what the best way to design some API is. I have no idea if
the designs I picked for HappyFunTimes are good or bad or what. There are a few
minor things I'd change if I started over, mostly cosmetic but otherwise I'm
mostly happy with it.

But, a few days ago I decided to add a feature to allow multiple computers in a
single game. Up until this point HappyFunTimes has been about 1 computer
running the game and a bunch of phones as controllers but there's a project I
wanted to make that used multiple machines, in particular I wanted to make an
extremely large platform game where you'd walk down a wall or hallway with say
10&minus;15 meters of screens and take your character from one screen to the
next. Each screen would be controlled by a separate computer running the game
on that screen.

For that all I needed as the ability to move a player from computer to
computer. I added that feature in a few minutes, tested it and it worked.
Awesome!

I'd done some other projects across computers before and in every case I'd just
have to have a special URL for each computer that specified which part of a
larger virtual display that computer represented. [For example the WebGL Aquarium does this](http://webglsamples.googlecode.com/hg/aquarium/README.html) Doing it that way is great if you already know what the layout and dimensions
of your monitors will be but I'd always wanted to make a monitor layout editor
similar to OSX and Windows. To do that I needed to enable games to talk to each
other so that they could all inform at least one of them their dimensions and
so that at least one of them could send commands to the others about what part
of the large display they were supposed to represent.

And so I set out to write that.

My first thought was I'd have some kind of `sendMsgToGame` function that took the msg you want to send and an `id` for the game you wanted to send it to. It would be up to you either make up an
id yourself, probably from a url, or the system could make one up for you.

But then I thought maybe, just like players have a `NetPlayer` object that is used to handle the communication between a player and the game
I should have a `NetGame` object that does the same thing for games. This would mean, just like a
player, there would be a 'gameconnect' message and you'd get passed a `NetGame` object. If you wanted to send a message to that game you could use `someNetGame.sendCmd` and anytime a game sent you a message it would arrive on that object.

<pre><code>someNetGame.addEventListener(
    'someMsgIExpectThisGameToSendMe', 
    handleThisTypeOfMsg);
</code></pre>

I got that all working, wrote tests, made sure you could send and receive
messages, that a `disconnect` message would get emitted as well.

But... Then the last thing I did was try to implement a broadcast function, `broadcastToGames`. I knew this was a useful function because I'd used it in the WebGL Aquarium
demo I'd linked above. I'd put some camera settings sliders on one computer and
broadcast them to all the computers. Broadcasting in this way meant you'd get
the same message send back to yourself so you didn't need custom code. All the
machines received their settings from the network, even the one deciding the
settings. This was a great way to propagate the settings to all the computers.
But, when I tried to implement on top of `NetGame` it I ran into a problem.

To broadcast you'd call `someGameServer.broadcastToGames` but given the way `NetGame` worked all the other games would receive the message on the `NetGame` object that represented the computer that sent the message but, the computer
that sent the message would get the message back on its `GameServer` object, in this example `someGameServer`.

That meant it wasn't at all symmetrical.  For the camera settings example in
order to accept settings from any computer you'd have to write code like

<pre><code>// when a new game connects
someGameServer.addEventListener('gameconnect', function(netGame) {
  // setup a listener to handle setting the fov
  netGame.addEventListener('setCameraFov', setFov);
});

// Setup yet another listener for when we broadcast 
// a new fov setting because that will
// come back to us here
someGameServer.addEventListener('setCameraFov', setFov);

function setFOV(data) {
  camera.fov = data.fov;
}
</code></pre>

That just smelled bad to me. Why should you have to set things up twice? I
didn't have to in previous games. Plus, you had to track all these `NetGame` objects.

I ended up getting rid of the `NetGame` objects. There is no `gameconnect` message. Instead, messages to a game from another game always arrive on the `GameServer` for that game. So previous example of setting the camera fov removes the
second case

<pre><code>someGameServer.addEventListener('setCameraFov', function(data) {
  camera.fov = data.fov;
});
</code></pre>

Much simpler.

If you want other games to know you connected broadcast a message to them

<pre><code>var server = new GameServer({id: "foo", allowMultipleGames: true});
server.broadcastToGames('imAlive');
</code></pre>

The other games will receive the message along with your id.

<pre><code>// some other game
var server = new GameServer({id: "bar", allowMultipleGames: true});
...
server.addEventListener('imAlive', function(data, id) {
  console.log("some game just joined. Its id is " + id);
}
</code></pre>

This will print

<pre><code>some game just joined. Its id is foo
</code></pre>

Of course when you broadcast that message will come back to you so you <strong>might</strong> need to filter out your own id

<pre><code>var ourId = "foo";
var server = new GameServer({id: ourId, allowMultipleGames: true});
server.broadcastToGames('imAlive');
...
server.addEventListener('imAlive', function(data, id) {
  if (id != ourId) {
    console.log("some game just joined. Its id is " + id);
  }
}
</code></pre>

Of course depending on your needs maybe you don't want to filter. For example
if you made a screen position editor like I referenced above ideally you'd just
display the id of each machine with a rectangle to represent it. If you created
those in your `imAlive` message then not filtering would automatically give you an entry for
yourself.

If you don't supply an id it will be provided on `connect`.

<pre><code>server.addEventListener('connect', function(data) {
  console.log("my id is: " + data.id);
});
</code></pre>

That id is also available on the `GameServer` object but it is not available until it has connected.

Good:

<pre><code>var server = new GameServer();
server.addEventListener('connect', function(data) {
  console.log("my id is: " + server.id);
});
</code></pre>

Bad:

<pre><code>var server = new GameServer();
console.log("my id is: " + server.id);  // ERROR! id not available yet as server has not connected.
</code></pre>

Finally you need some way to know when a game disconnects so there's a `gamedisconnect` message

<pre><code>server.addEventListener('gamedisconnect`, function(data, id) {
  console.log("Some other game " + id + " disconnected");
});
</code></pre>

I don't know if this post made any sense. It kind of ended up being like docs.
Partly I just wanted to document the iterations. I spent a lot of time making
the `NetGame` implementation and testing it only to throw it all way. Even after I threw it
away I went through a few more smaller refactorings.

The first one was I made up a `gameid` command to pass back the gameid. I didn't like that at all though. It took me
a while to figure out how to pass it back on the `connect` message where it seemed like it belonged. Another thing that happened at the
start was I had a 2 ideas per game. The generated id AND a user assigned id. It
took a while to come back to just 1 id. Either the on you assign or the one you
let the system assign for you.

I'm feeling relatively confident that what I ended up with is a good solution.
I guess one more thing though is that I didn't push out a version until I felt
good about it. Sure there aren't lots of devs yet but taking this stuff
seriously will hopefully more confidence that I won't have to make future
breaking changes.