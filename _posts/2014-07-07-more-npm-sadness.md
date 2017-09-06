---
title: more npm sadness
date: '2014-07-07'
layout: post
excerpt_separator: "noexcerpt"
permalink: /blog/more-npm-sadness/
tags:
  - Uncategorized
dsq_thread_id: '2839485402'
---
I feel bad these last few posts are rants but ...

I needed to make http json requests. I have a snippet of code I've been using
for the last 4 years. It's about 90 lines line. It's for client side browser
JavaScript. I needed something similar for server side node.js code. At first I
thought I'd write my own. Having just submitted a pull request for [the github package](http://npmjs.org/package/github/) I'm generally familar with how to make a request. It seems pretty straight
forward.

But..., I decide, well, in the spirit of npm I should see if there's already a
package for this. I quick search and [request-json](http://npmjs.org/package/request-json) comes up. The API looks simple. How bad can it be? I take a brief look at the
code. It's in coffeescript. That's a little scary as now I need a coffeescript
compiler but what the heck, let's give it a try.

<pre><code>$ npm install request-json --save
npm http GET https://registry.npmjs.org/request-json
npm http 200 https://registry.npmjs.org/request-json
npm http GET https://registry.npmjs.org/request-json/-/request-json-0.4.10.tgz
npm http 200 https://registry.npmjs.org/request-json/-/request-json-0.4.10.tgz
npm http GET https://registry.npmjs.org/request/2.34.0
npm http 200 https://registry.npmjs.org/request/2.34.0
npm http GET https://registry.npmjs.org/request/-/request-2.34.0.tgz
npm http 200 https://registry.npmjs.org/request/-/request-2.34.0.tgz
npm http GET https://registry.npmjs.org/qs
npm http GET https://registry.npmjs.org/json-stringify-safe
npm http GET https://registry.npmjs.org/node-uuid
npm http GET https://registry.npmjs.org/forever-agent
npm http GET https://registry.npmjs.org/tough-cookie
npm http GET https://registry.npmjs.org/form-data
npm http GET https://registry.npmjs.org/tunnel-agent
npm http GET https://registry.npmjs.org/http-signature
npm http GET https://registry.npmjs.org/aws-sign2
npm http GET https://registry.npmjs.org/oauth-sign
npm http GET https://registry.npmjs.org/hawk
npm http 304 https://registry.npmjs.org/json-stringify-safe
npm http 200 https://registry.npmjs.org/node-uuid
npm http 304 https://registry.npmjs.org/forever-agent
npm http 304 https://registry.npmjs.org/form-data
npm http 200 https://registry.npmjs.org/qs
npm http 304 https://registry.npmjs.org/http-signature
npm http 304 https://registry.npmjs.org/tunnel-agent
npm http 304 https://registry.npmjs.org/hawk
npm http 304 https://registry.npmjs.org/aws-sign2
npm http 304 https://registry.npmjs.org/tough-cookie
npm http 304 https://registry.npmjs.org/oauth-sign
npm http GET https://registry.npmjs.org/combined-stream
npm http GET https://registry.npmjs.org/async
npm http GET https://registry.npmjs.org/assert-plus/0.1.2
npm http GET https://registry.npmjs.org/ctype/0.5.2
npm http GET https://registry.npmjs.org/asn1/0.1.11
npm http GET https://registry.npmjs.org/punycode
npm http GET https://registry.npmjs.org/sntp
npm http GET https://registry.npmjs.org/boom
npm http GET https://registry.npmjs.org/hoek
npm http GET https://registry.npmjs.org/cryptiles
npm http 304 https://registry.npmjs.org/assert-plus/0.1.2
npm http 304 https://registry.npmjs.org/ctype/0.5.2
npm http 304 https://registry.npmjs.org/combined-stream
npm http 200 https://registry.npmjs.org/async
npm http 304 https://registry.npmjs.org/sntp
npm http 304 https://registry.npmjs.org/asn1/0.1.11
npm http 304 https://registry.npmjs.org/cryptiles
npm http GET https://registry.npmjs.org/delayed-stream/0.0.5
npm http 200 https://registry.npmjs.org/boom
npm http 200 https://registry.npmjs.org/punycode
npm http 200 https://registry.npmjs.org/hoek
npm http GET https://registry.npmjs.org/punycode/-/punycode-1.3.0.tgz
npm http 304 https://registry.npmjs.org/delayed-stream/0.0.5
npm http 200 https://registry.npmjs.org/punycode/-/punycode-1.3.0.tgz
</code></pre>

WTF!!!! Seriously?

<pre><code>npm uninstall request-json --save
</code></pre>

Here's the code I wrote.

<pre><code>"use strict";

var url = require('url');

var sendJSON = function(apiurl, obj, options, callback) {
  var options = JSON.parse(JSON.stringify(options));
  var parsedUrl = url.parse(apiurl);

  options.hostname = parsedUrl.hostname;
  options.port = parsedUrl.port;
  options.method = options.method || 'POST';
  options.headers = options.headers || {};
  options.path = parsedUrl.pathname;

  var body = JSON.stringify(obj);
  var headers = options.headers;

  headers["content-length"] = Buffer.byteLength(body, "utf8");
  headers["content-type"] = "application/json; charset=utf-8";

  var callCallback = function(err, res) {
    if (callback) {
      var cb = callback;
      callback = undefined;
      cb(err, res);
    }
  };

  var protocol = parsedUrl.protocol.substring(0, parsedUrl.protocol.length - 1);
  var req = require(protocol).request(options, function(res) {
    res.setEncoding("utf8");
    var data = "";
    res.on("data", function(chunk) {
      data += chunk;
    });
    res.on("error", function(err) {
      callCallback(err);
    });
    res.on("end", function() {
      if (res.statusCode == 301 ||
          res.statusCode == 302 ||
          res.statusCode == 307 ||
          res.statusCode == 308) {
        sendJSON(res.headers["location"].toString(), obj, options, callCallback);
      } else if (res.statusCode &gt;= 400 &amp;&amp; res.statusCode &lt; 600 || res.statusCode &lt; 10) {
        callCallback(new Error("StatusCode: " + res.statusCode + "\n" + data));
      } else {
        try {
          callCallback(null, JSON.parse(data));
        } catch &#x2709;&#xFE0F; {
          e.content = data;
          callCallback&#x2709;&#xFE0F;;
        }
      }
    });
  });

  if (options.timeout) {
    req.setTimeout(options.timeout);
  }

  req.on("error", function&#x2709;&#xFE0F; {
    callCallback(e.message);
  });

  req.on("timeout", function() {
    callCallback(new error.GatewayTimeout());
  });

  req.write(body);
  req.end();
};

exports.sendJSON = sendJSON;
</code></pre>

less than 100 lines vs 25k lines. Why do I need 25k lines? Maybe it supports
some things my 100 lines doesn't? Authentication can be handled by setting `options.auth` to the appropriate thing. Headers can be set in `options.headers`. What else is there? Yea I see it supports streaming the body. That's
literally &lt; 10 lines of code to add. I see stuff about cookies but cookies
are sent in the headers which means you can add cookie support by setting
headers. Maybe it's a structure thing? I'd prefer a few separate libraries I
combine rather than a library where someone else has already combine them. At
least for something as seemingly low level as "make a request for some json".

Maybe I'm looking at it the wrong way but it sure seems like something is wrong
when I need 25k lines to do something that seems like it should take only a few.