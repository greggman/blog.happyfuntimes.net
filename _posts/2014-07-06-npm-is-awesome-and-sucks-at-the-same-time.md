---
title: npm is awesome and sucks at the same time.
date: '2014-07-06'
layout: post
excerpt_separator: "noexcerpt"
permalink: /blog/npm-is-awesome-and-sucks-at-the-same-time/
tags:
  - Uncategorized
dsq_thread_id: '2834669330'
---
npm is a node package manager. It's pretty cool. You make a folder and type
"npm init". You answer a few questions and it makes a "package.json" file
recording those answers. From then on you can install one of the 81000+
"packages" by typing "npm install packagename &minus;&minus;save". The
"&minus;&minus;save" part make it update the package.json file to record that
your project needs the package you just installed. That means if you give a
copy of your project to someone else they only need the parts you actually
wrote. The rest will be downloaded for them.

It also helps you update packages to current versions etc..

So that sounds great in theory. The problem is finding anything useful and
working. 81000 packages in a lot. How do you find the good ones? I have no
idea.

For example I needed a library to zip and unzip files. I search for zip on [npmjs.org](http://npmjs.org) and see there's a package, [adm-zip](https://www.npmjs.org/package/adm-zip), with 19000+ stars. Clearly it's a popular package so I install it and start
writing my code.

The first problem they can zip up folders but you can't easily choose any kind
of filter? Want to zip up a folder but skip the ".git" or ".svn" folders or
skip files that end in ".pyc" or ".o" or ".bak". Too bad for you, write your
own from scratch.

So I submitted a patch. It's been 3 weeks and I haven't heard a peep out of the
maintainers. In fact even with 19000+ stars there's been no commits in 3
months.

So, having written the filter I write some code to zip up a folder.  The very
first set of files I build a zip from don't unzip with the standard "unzip"
program built into OSX. Seriously!? WTFBBQ? 19000+ people and it makes bad
files? Lucky for me it was the first test I made. Imagine if I had not found
that bug for months.

Looking at the code it leaves a lot to be desired. I often write crap code to
but a zip library is not that hard to write. There aren't lots of design
decisions to make. It shouldn't be that hard.

I go looking for other libraries. Results are mixed. Most of the libraries
require the entire contents of the zip to be in memory either compressed or
uncompressed. That's arguably unacceptable. You can have multi&minus;gigabyte
zip files. You need to be able to stream them through the library. I looked for
something along those lines. Didn't find anything. Needed to get shit done so
I'm using [JSZip](https://www.npmjs.org/package/jszip) and [Moxie-Zip](https://www.npmjs.org/package/moxie-zip) and have a TODO in my notes to replace them with something that steams.

On top of lots of non&minus;working packages there are packages that seem like
they should be small that have way too many dependencies. For example I needed
a prompt library since because of node's event driven model that's harder than
non event driven languages. Sure I could roll my own but who knows what dragons
lurk there. Better to use something where the dragons have already been slain.

So I do a search and the first thing that comes up is the "[prompt package](https://www.npmjs.org/package/prompt)" with 5000+ stars. I install it and see it install 20+  dependences.
Seriously? I need 20+ dependencies. That's 186000 lines of code just to present
a prompt?

<ul>
<li>Then I read the docs and I see this.

<pre><code>var schema = {
  properties: {
    name: {
      pattern: /^[a-zA-Z\s\-]+$/,
      message: 'Name must be only letters, spaces, or dashes',
      required: true
    },
    password: {
      hidden: true
    }
  }
};

//
// Start the prompt
//
prompt.start();

//
// Get two properties from the user: email, password
//
prompt.get(schema, function (err, result) {
  //
  // Log the results.
  //
  console.log('Command-line input received:');
  console.log('  name: ' + result.name);
  console.log('  password: ' + result.password);
});
</code></pre>

Pretty easy right? The output from the above script is:

<pre><code>$ node examples/property-prompt.js
prompt: name: nodejitsu000
error:  Invalid input for name
error:  Name must be only letters, spaces, or dashes
prompt: name: Nodejitsu Inc
prompt: password:
Command-line input received:
  name: Nodejitsu Inc
  password: some-password
</code></pre></li>
</ul>

That makes no sense. Object properties in JavaScript do not have a guaranteed
order so there's no reason to believe the above example would ask for "name"
before "password".

I think "oh, maybe their sorting the properties alphabetically" so I check the
code. Nope! So, no confidence in this package &#128526;  I did at least file an
issue to point out the problem. So far no response.

Switch to the [asks package](https://www.npmjs.org/package/asks). Hey, only 30000+ lines of code just to prompt the user?!? &#128526;

Now before you think I'm just complaining I do try to fix things when I can. I
needed to interface with github. I thought maybe I could find a library. I did
a search and found the [github package](https://www.npmjs.org/package/github). Yea! Unfortunately the only API I needed was the [Releases API](https://developer.github.com/v3/repos/releases/) and the github package had no support. Since I didn't find any other solutions
I just added it myself and submitted a pull request AND I GOT A RESPONSE! Yea,
a package that is still actively maintained! Still waiting for a response to
the second pull request.

To be fair this has nothing to do with npm which is awesome. It has to do with
various libraries which are not. This is not unique to JavaScript or node.js.
I've found lots of poorly written and bloated libraries in every language I've
used. I appreciate that people are making their code available and that it
solves people's needs. I just kind of wish their was some trustworth curation
about which packages actually work and have a quality code base.