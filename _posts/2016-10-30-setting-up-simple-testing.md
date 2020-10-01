---
title: Setting up a simple testing suite
permalink: /mocha-chai
date: 2016-10-30 11:33:00 +0800
tags: [testing]
---

## Getting started with testing

You may want to have your own simple test runner to ensure your functions return accurate results.

I used Mocha and Chai. Here's some sample code and a walk through for using it. Note: the challenge I wrote these tests for was _return the sum of all multiples of 3 or 5 that are below a number N, where N is an input parameter to the function_.

```js
var should = require("chai").should();
var basic = require("./multJacksonBates");

describe("basic", function() {
  it("should return 23 when passed 10", function() {
    basic(10).should.equal(23);
  });
  it("should return 78 when passed 20", function() {
    basic(20).should.equal(78);
  });
  it("should return 2318 when passed 100", function() {
    basic(100).should.equal(2318);
  });
  it("should return 23331668 when passed 10000", function() {
    basic(10000).should.equal(23331668);
  });
  it("should return 486804150 when passed 45678", function() {
    basic(45678).should.equal(486804150);
  });
});
```

## Walk through

Pre-req: Install Node & NPM, you can open and type in your OS's terminal / command line

- Create a directory for your algorithms and testing, eg: `mkdir algos`
- Navigate to said directory: `cd algos`
- `npm init` and accept all defaults
- `npm install -g mocha`
- `npm install mocha chai --save`
- Write a function you want to test, and export it:

```js
// multJacksonBates.js
function multJacksonBates(n) {
  return 23;
}

module.exports = multJacksonBates;
```

- Notice the code snippet for the test script `require`s the `multJacksonBates` function created here and names it `basic`
- Test the script with `mocha test.js`
- It should say the first test passed because it is hardcoded to return the right answer for basic(10).
- Write different code in the function so that it passes all test cases. And change the name of the function.
- You can add more functions and more tests by replicating the code snips above.

## Additional resources

If you decide to write several functions and want to test them for efficiency, you can modify the benchmark script from here: [Benchmark](http://forum.freecodecamp.com/t/algorithm-return-largest-numbers-in-arrays/16042/7?u=jacksonbates)

You can find more information about Mocha and Chai at the following links:

- [Mocha](https://mochajs.org/)
- [Chai](http://chaijs.com/)

{% include twitter_plug.html %}
