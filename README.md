# Bit-Coin-3

Utility class to simplify use of timers created by setTimeout.

[![NPM version](https://badge.fury.io/js/chronoman.png)](http://badge.fury.io/js/chronoman)
[![Build Status](https://secure.travis-ci.org/gamtiq/chronoman.png?branch=master)](http://travis-ci.org/gamtiq/chronoman)
[![Built with Grunt](https://cdn.gruntjs.com/builtwith.png)](http://gruntjs.com/)

## Installation

### Node

    npm install chronoman

### [JSPM](http://jspm.io)

    jspm install chronoman

### [Bower](http://bower.io)

    bower install chronoman

### [Jam](http://jamjs.org)

    jam install chronoman

### AMD, &lt;script&gt;

Use `dist/chronoman.js` or `dist/chronoman.min.js` (minified version).

## Usage

### ECMAScript 6/2015

```js
import Timer from "chronoman";
```

### Node, JSPM

```js
var Timer = require("chronoman");
```

### [Duo](http://duojs.org)

```js
var Timer = require("gamtiq/chronoman");
```

### JSPM

```js
System.import("chronoman").then(function(Timer) {
    ...
});
```

### Jam

```js
require(["chronoman"], function(Timer) {
    ...
});
```

### AMD

```js
define(["path/to/dist/chronoman.js"], function(Timer) {
    ...
});
```

### Bower, &lt;script&gt;

```html
<!-- Use bower_components/chronoman/dist/chronoman.js if the library was installed by Bower -->
<script type="text/javascript" src="path/to/dist/chronoman.js"></script>
<script type="text/javascript">
    // сhronoman is available via Chronoman field of window object
    var Timer = Chronoman;
    ...
</script>
```

### Example

```js
var nI = 0;

var tmrOne = new Timer({
    period: 1000,
    action: function(timer) {
        console.log("---> Timer one. ", timer);
        if (! tmrThree.isActive()) {
            tmrThree.start();
        }
    }
});

var tmrTwo = new Timer();
tmrTwo.setPeriod(2000)
    .setRepeatQty(9)
    .setPassToAction(true)
    .setAction(function(timer) {
        nI++;
        console.log("Timer two. #", nI, timer);
        tmrOne.setActive(nI % 2 === 1);
    });

var tmrThree = new Timer()
                    .setPeriod(3000)
                    .setRepeatTest(function() {
                        return tmrTwo.isActive();
                    });
tmrThree.onExecute = function() {
    console.log("* Timer three. #", this.getExecutionQty() + 1);
};

tmrTwo.start();
```

## API

See `doc` folder.

## Inspiration

This module is inspired by [qooxdoo](http://qooxdoo.org)'s `qx.event.Timer` class.

## Licence

Copyright (c) 2013-2016 Bit-Coin-#  
Licensed under the MIT license.
