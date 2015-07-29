# `HTMLElement.prototype.addEventListener`

So far we've added click event handlers by setting `onclick` to a callback function.
But this has some fallbacks.

Let's for instance say we had a `button` and we wanted to run two callbacks after it was clicked.
So we try this:

    var buttonEl = document.querySelector('button');

    buttonEl.onclick = callbackA;
    buttonEl.onclick = callbackB;

Unfortunately this code will only ever run the `callbackB` function.

This means that if we add a click handler using `onclick` at the top of our file, and then accidentally set `onclick` later: then we would have unexpected results.

## Multiple Event Handlers

To add multiple event callbacks on a single HTMLElement, we can call `addEventListener`.
This function accepts a string for the event name you are listening for, then the callback to be run when the event fires.
So our code above becomes:

    var buttonEl = document.querySelector('button');

    buttonEl.addEventListener('click', callbackA);
    buttonEl.addEventListener('click', callbackB);

Now both `callbackA` and `callbackB` will be run when our button is clicked.

Also, we aren't limited to just click events, there are a ton of other common events:

* click - fires when the user clicks down AND releases over the element
* mouseover - fires when the user cursor moves over the element
* mousedown - fires when the user clicks down over the element
* mouseup - fires when the user releases a mouse click over the element
* change - fires when an input value has been changed AND focus is lost (user has typed and moved on to the next input)
* input - fires on every change to value even before the user moves to the next input

> **Interesting** HTMLElement actually inherits `addEventListener` from `EventTarget.prototype`.
