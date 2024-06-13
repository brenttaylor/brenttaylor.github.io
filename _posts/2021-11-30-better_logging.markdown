---
layout: post
title:  "Better Logging in GameMaker Studio 2"
date:   2021-11-30
author: Brent Taylor
categories: [tutorial]
tags: [game maker]
---

Logging is fundamental to development in every industry I can personally think of.  It's also something we spend so very little effort to keep clean and easy to use.  How often have we written code like this?

~~~javascript
function log(msg) {
    show_debug_message(string(current_hour) + ":" + string(current_minute) + ":"
      + string(current_second) + " - " + string(msg));
}
~~~

When called to give information on a variable, it looks something like this:

~~~javascript
log("Var with error equals: " + some_var)
~~~
A line is printed to the console like this: "20:51:52 - Var with error equals: 298"
{:.note}

This isn't too bad as these are small examples, but anyone who's been doing development for at least a year or two will have horror stories of huge blocks of completely unreadable and unmaintainable string concatenation.  You'll especially see newer developers do this, but developers of all skill levels are susceptible to being lazy, especially me.

Other languages, such as Python, have much better ways of handling situations like this in a much more readable way.  With the introduction of structs in GameMaker Studio 2.3, we can absolutely replicate that.

Let's look at how we might want string concatenation or substitution to look like in GameMaker Studio.

~~~javascript
var my_text = f("Hello {subject}!", {subject: "world"});
~~~
This should produce: "Hello world!"
{:.note}

In my opinion, this is much better.  It's a sort of an in-between of Python's `string.fmt` method and Python's `f` strings.  Let's see what our logging function might look like with this new approach.

~~~javascript
function log(msg) {
    var log_text = f("{hour}:{minute}:{second} - {log_message}",
        {
            hour: current_hour,
            minute: current_minute,
            second: current_second,
            log_message: msg
        }
    );

    show_debug_message(log_text);
}
~~~

This is much longer, but it's also significantly easier to read and maintain.

So what does our `f` function look like?

~~~javascript
function f(msg, data_pairs = noone) { // concatenation isn't always desired
                                      // so set `data_pairs` to `noone` by default
    // If `data_pairs` isn't provided, it's just a string so we can just return it
    if (data_pairs == noone) return string(msg);
    // If `data_pairs` isn't a struct, then we need to error out
    if (!is_struct(data_pairs)) throw "ValueError";

    // We don't want to modify the original string we passed in, so let's copy it
    var build_string = string_copy(msg, 1, string_length(msg));
    var keys = variable_struct_get_names(data_pairs); // Grab all the keys in data_pairs

    // Now we loop over each key to build our substitution tokens
    for (var index=0; index < array_length(keys); index++) {
        var key = keys[index]; // Grab the key
        var token = "{" + string(key) + "}"; // Build our substitution token

        // And lastly, we want to replace every instance of our token with the data
        // provided in the struct
        build_string = string_replace_all(build_string, token,
            string(variable_struct_get(data_pairs, key)) // Don't forget to cast the data
                                                         // to a string
        );
    }

    return build_string; // And return it!
}
~~~
I chose to call this function `f` simply to leverage the habits I've already formed while working with Python.  If the single letter function name bothers you, I would suggest renaming it `string_create` to stay in line with current naming conventions in GMS.
{:.note}

This approach is slower, but it's easier to use, easier to read and significantly easier to maintain.  Consider that in most cases in which you're piping text out to your console or to a file stream, speed isn't a major concern.  I think the tradeoff is worth it.

If you find this useful, consider the code to be under the public domain.  Use it in your own projects as you see fit.  Enjoy!
