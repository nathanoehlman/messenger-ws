# messenger-ws

This is a simple messaging implementation for sending and receiving data
via websockets.


[![NPM](https://nodei.co/npm/messenger-ws.png)](https://nodei.co/npm/messenger-ws/)

[![Build Status](https://img.shields.io/travis/DamonOehlman/messenger-ws.svg?branch=master)](https://travis-ci.org/DamonOehlman/messenger-ws) 

## Example Usage

```js
var pull = require('pull-stream');
var queue = require('pull-pushable')();
var messenger = require('messenger-ws')('ws://localhost:3000/echo');

messenger(function(err, source, sink) {
  if (err) {
    return console.error(err);
  }

  // log data coming from the socket
  pull(source, pull.log());

  // wire the queue to sink
  pull(queue, sink);
});

setInterval(function() {
  queue.push('current time: ' + Date.now());
}, 150);

```

## License(s)

### ISC

Copyright (c) 2014, Damon Oehlman <damon.oehlman@gmail.com>

Permission to use, copy, modify, and/or distribute this software for any
purpose with or without fee is hereby granted, provided that the above
copyright notice and this permission notice appear in all copies.

THE SOFTWARE IS PROVIDED "AS IS" AND THE AUTHOR DISCLAIMS ALL WARRANTIES WITH
REGARD TO THIS SOFTWARE INCLUDING ALL IMPLIED WARRANTIES OF MERCHANTABILITY
AND FITNESS. IN NO EVENT SHALL THE AUTHOR BE LIABLE FOR ANY SPECIAL, DIRECT,
INDIRECT, OR CONSEQUENTIAL DAMAGES OR ANY DAMAGES WHATSOEVER RESULTING FROM
LOSS OF USE, DATA OR PROFITS, WHETHER IN AN ACTION OF CONTRACT, NEGLIGENCE OR
OTHER TORTIOUS ACTION, ARISING OUT OF OR IN CONNECTION WITH THE USE OR
PERFORMANCE OF THIS SOFTWARE.