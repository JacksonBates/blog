---
title: "Unhelpful Laravel Bug | Undefined offset: 0"
permalink: /laravel-routes-bug
date: 2021-03-17 13:30 +1100
tags: [laravel, post-mortem]
description: Figuring out why I got an Undefined offset 0 error message in Laravel when all online sources suggested irrelevant causes
---

Some time wasted on a silly mistake today.

I received `Undefined offset: 0` as an error response from my Laravel API. The API call and routes / controllers were identical to other attempts at something similar in other parts of the same codebase.

Numerous Stack Overflow responses explain that this happens when a database record that does not exist is referenced. However, this was a simple GET request that was failing at even returning a simple string with no attempt at reading from the database, so those responses felt irrelevant.

## What was happening?

The cause of the problem in the end was sloppy API route naming and attempting to (unwittingly) access database records that didn't exist.

Here's an example of the routes:

```php
Route::prefix('resources')->group(function () {
    Route::get('{resource}', 'ResourceController@show');
    Route::get('our-resources', 'ResourceController@showCompanyResources');
    Route::post('response', 'ResourceController@submit');
});

```

GETs to `/api/resources/:resource_id` worked fine.

POSTs to `/api/resources/response` also worked fine.

But GET to `/api/resources/our-resources` triggered the error.

Now that I type it out, the reason is pretty obvious. GET `/api/resources/our-resources` is interpreted as a call to `/api/resources/:resource_id` where the id is `our-resources`. So the @show method on the controller was intercepting the request, and not finding the correct resource (as it didn't exist in the database).

The routes are tested in the order they are listed, so `/api/resources/our-resources` is never reached.

## Fix

One quick fix is to change the order of the routes like this:

```php
Route::prefix('resources')->group(function () {
    Route::get('our-resources', 'ResourceController@showCompanyResources');
    Route::get('{resource}', 'ResourceController@show');
    Route::post('response', 'ResourceController@submit');
});

```

Alternatively, you can use more precise name-spacing for your routes to avoid these clashes.

{% include twitter_plug.html %}
