---
title: happyFunTimes standalone HTML5 library
date: '2016-12-05'
layout: post
permalink: /blog/happyfuntimes-standalone-html5-library/
tags:
  - HappyFunTimes
dsq_thread_id: '5358535068'
---
I finally got around to making happyfuntimes a standalone library for Electron.
This means you can easily make an HTML5 game and ship it as a native app on
Windows, Mac, Linux with happyfuntimes support.

As examples I've posted 3 of the games on itch.io

<iframe frameborder="0" src="https://itch.io/embed/99842" width="552" height="167"></iframe>

<iframe frameborder="0" src="https://itch.io/embed/100817" width="552" height="167"></iframe>

<iframe frameborder="0" src="https://itch.io/embed/101495" width="552" height="167"></iframe>

I also updated the [hft-simple example](https://github.com/greggman/hft-simple) and I added [a new "clean" example](https://github.com/greggman/hft-clean) that uses no external libraries so it should be easier to use as a base to
intergrate with other HTML5 game engines.

Even if you don't plan to use happyfuntimes they might be a good way to look
into shipping your HTML5 app as an electron app. In just a few minutes they'll
build standalone app for Windows, Mac, or Linux.