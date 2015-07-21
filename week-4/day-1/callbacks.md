# Callbacks

When working with Javascript there is often a lot of our code that we want run once something else happens rather than right away.
This could be a reaction to when a user clicks, when some amount of time has passed, or even when we get new data from the server.

To react to these types of actions, we can create "Callbacks".
Callbacks are just functions that are run in reaction to something happening.
Usually callbacks are created and passed as an argument to another function: like in the case of `window.setTimeout`:

    window.setTimeout(function () {
        console.log('You have waited all this time');
    }, 2000);

On other occassions such as `onclick` or `onhover`, you can set a callback to be run using a setter:

    var buttonEl = document.querySelector('button');

    buttonEl.onclick = function () {
        console.log('You have clicked a button!');
    };

## Context and Callback Arguments

When creating callbacks and sending them to different functions, carefully read the documentation and be aware of what the context of `this` will be when your callback is run, and whether or not you will receive any arguments.

If you are careful, you can sometimes use the same function as both a callback and a regular function.
But, this does mean that you have to REALLY be aware of `this` and your arguments.
