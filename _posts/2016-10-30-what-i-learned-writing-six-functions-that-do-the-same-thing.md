---
layout: default
title: What I learned writing 6 functions that all do the same thing
permalink: /six-functions
---

# What I learned from writing six functions that all do the same thing

A couple weeks ago, a camper started an unofficial algorithm competition on Free Code Camp’s Forum.

The challenge seemed simple enough: _return the sum of all multiples of 3 or 5 that are below a number N, where N is an input parameter to the function_.

But instead of just finding any solution, the competition required you to focus on efficiency. It encouraged you to write your own tests, and to benchmark the performance of your solutions.

This is a breakdown of every function I tried and tested, including my tests and benchmark scripts. At the end, I’ll show the function that blew all of my own out of the water, and taught me a valuable lesson.

## Function #1: Array, push, increment

```js
function arrayPushAndIncrement(n) {
  var array = [];
  var result = 0;
  for (var i = 1; i < n; i++) {
    if (i % 3 == 0 || i % 5 == 0) {
      array.push(i);
    }
  }
  for (var num of array) {
    result += num;
  }
  return result;
}
module.exports = arrayPushAndIncrement; // this is necessary for testing
```

For problems like this, my brain defaults to: build an array, then do something to that array.

This function creates an array and pushes any numbers that meet our condition (divisible by 3 or 5) into it. It then loops through that array, adding all the values together.

## Setting up testing

Here are the automated tests for this function, which use Mocha and Chai, running on NodeJS.

If you want more information about installing Mocha and Chai, I’ve written a detailed guide here: [Setting up a simple test suite](/blog/mocha-chai).

I wrote a simple testing script using the values P1xt provided. Notice that in the script below, the function is included as a module:

```js
// testMult.js
var should = require("chai").should();
var arrayPushAndIncrement = require("./arrayPushAndIncrement");

describe("arrayPushAndIncrement", function() {
  it("should return 23 when passed 10", function() {
    arrayPushAndIncrement(10).should.equal(23);
  });
  it("should return 78 when passed 20", function() {
    arrayPushAndIncrement(20).should.equal(78);
  });
  it("should return 2318 when passed 100", function() {
    arrayPushAndIncrement(100).should.equal(2318);
  });
  it("should return 23331668 when passed 10000", function() {
    arrayPushAndIncrement(10000).should.equal(23331668);
  });
  it("should return 486804150 when passed 45678", function() {
    arrayPushAndIncrement(45678).should.equal(486804150);
  });
});
```

When I ran the test using mocha testMult.js it returned the following:

For all future functions in this article, assume they passed all tests. For your own code, add tests for each new function you try.

## Function #2: Array, push, reduce

```js
function arrayPushAndReduce(n) {
  var array = [];
  for (var i = 1; i < n; i++) {
    if (i % 3 == 0 || i % 5 == 0) {
      array.push(i);
    }
  }
  return array.reduce(function(prev, current) {
    return prev + current;
  });
}

module.exports = arrayPushAndReduce;
```

So this function uses a similar approach to my previous one, but instead of using a for loop to construct the final sum, it uses the fancier reduce method.

## Setting up performance benchmark testing

Now that we have two functions, we can compare their efficiency.

```js
// performance.js
var Benchmark = require("benchmark");
var suite = new Benchmark.Suite();
var arrayPushAndIncrement = require("./arrayPushAndIncrement");
var arrayPushAndReduce = require("./arrayPushAndReduce");

// add tests
suite
  .add("arrayPushAndIncrement", function() {
    arrayPushAndIncrement(45678);
  })
  .add("arrayPushAndReduce", function() {
    arrayPushAndReduce(45678);
  })
  // add listeners
  .on("cycle", function(event) {
    console.log(String(event.target));
  })
  .on("complete", function() {
    console.log("Fastest is " + this.filter("fastest").map("name"));
  })
  // run async
  .run({ async: true });
```

If you run this with node performance.js you’ll see the following terminal output:

```
arrayPushAndIncrement x 270 ops/sec ±1.18% (81 runs sampled)
arrayPushAndReduce x 1,524 ops/sec ±0.79% (89 runs sampled)
Fastest is arrayPushAndReduce
```

So using the reduce method gave us a function that was _5 times faster_!

If that isn’t encouraging enough to continue with more functions and testing, I don’t know what is!

## Function#3: While, Array, Reduce

Now since I always reach for the trusty for loop, I figured I would test a while loop alternative:

```js
function whileLoopArrayReduce(n) {
  var array = [];
  while (n >= 1) {
    n--;
    if (n % 3 == 0 || n % 5 == 0) {
      array.push(n);
    }
  }
  return array.reduce(function(prev, current) {
    return prev + current;
  });
}
module.exports = whileLoopArrayReduce;
```

And the result? A tiny bit slower:

```
whileLoopArrayReduce x 1,504 ops/sec ±0.65% (88 runs sampled)
```

## Function#4: While, sum, no arrays

So, finding that the type of loop didn’t make a huge difference, I wondered what would happen if I used a method that avoided arrays altogether:

```js
function whileSum(n) {
  var sum = 0;
  while (n >= 1) {
    n--;
    if (n % 3 == 0 || n % 5 == 0) {
      sum += n;
    }
  }
  return sum;
}
module.exports = whileSum;
```

As soon as I started thinking down this track, it made me realize how wrong I was for always reaching for arrays first…

```
whileSum x 7,311 ops/sec ±1.26% (91 runs sampled)
```

Another massive improvement: nearly _5 times faster again_, and **27 times** faster than my original function!

## Function#5: For, sum

Of course, we already know that a for loop should be a little faster:

```js
function forSum(n) {
  n = n - 1;
  var sum = 0;
  for (n; n >= 1; n--) {
    n % 3 == 0 || n % 5 == 0 ? (sum += n) : null;
  }
  return sum;
}
```

This uses the ternary operator to do the condition checking, but my testing showed that a non-ternary version of this is the same, performance-wise.

```
forSum x 8,256 ops/sec ±0.24% (91 runs sampled)
```

So, a little faster again.

My final function ended up being **28 times** faster than my original.

I felt like a champion.

I was over the moon.

I rested on my laurels.

## Enter Maths

The week passed and the final solutions from everyone were posted, tested, and collated. The function that performed the fastest avoided loops altogether and used an algebraic formula to crunch the numbers:

```js
function multSilgarth(N) {
  var threes = Math.floor(--N / 3);
  var fives = Math.floor(N / 5);
  var fifteen = Math.floor(N / 15);

  return (3 _ threes _ (threes + 1) + 5 _ fives _ (fives + 1) - 15 _ fifteen _ (fifteen + 1)) / 2;
}
module.exports = multSilgarth;
```

Wait for it…

```
arrayPushAndIncrement x 279 ops/sec ±0.80% (83 runs sampled)
forSum x 8,256 ops/sec ±0.24% (91 runs sampled)
maths x 79,998,859 ops/sec ±0.81% (88 runs sampled)
Fastest is maths
Fastest is maths
```

So the winning function was roughly **_9,690 times faster_** than my best effort, and **_275,858 times faster_** than my initial effort.

If you need me, I’ll be over at Khan Academy studying math.

Thanks to everyone that participated and shared their solutions in the spirit of helping other campers learn new methods.

{% include twitter_plug.html %}
