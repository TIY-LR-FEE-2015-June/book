# `array.forEach`

While working with `for` loops to iterate over every item in an array is fairly common, this isn't particularly optimized and is really fragile.
Just one mistake in your `for` loop or referencing your array instead of `array[i]` can make for a terrible mess to debug.
Not to mention, this leads to an extra variable that we have to keep up with and there's not much you can do as far as code reuse.

Instead arrays provide a `forEach` function that allows us to do work on each element in the array via a [callback](callback.html).

## How it works

The `forEach` method on an array takes one argument: a callback function to be run.
This callback will receive three arguments:

* currentValue: The current element being processed in the array. (similar to `arr[x]` in a `for` loop)
* index: The index of the current element being processed in the array. (similar to your `var x` in a `for` loop)
* array: The array that forEach is being applied to.

Of course in your callback you will probably want to name these to what makes sense for your code.
It's a fairly common practice to have your callback's first argument be either `current` or the singular version of the array name.

## Replacing a `for` loop with `forEach`

For this example we'll have an array of `students`:

    var students = [
      'Alia',
      'Jackyln',
      'Scott',
      'Coleman',
      'Marvin',
      'Corbin',
      'Daniel',
      'Brent'
    ];

And now to log out each one, we could use a standard `for` loop:

    for (var x = 0; x < students.length; x++) {
      console.log(students[x]);
    }

Or we could write this using `forEach`:

    students.forEach(function (student) {
      console.log(student);
    });

## Gotchas

Right now not everything that acts like an array is actually an array.
Therefore there are a lot of Javascript objects running around that seem like they should have a `forEach` on them but don't.
This is pretty unfortunate, but it's true.

One big way that you will see this is from the results of `document.getElementsByTagName` or `document.querySelectorAll`.
These functions return an HTML Node List which still allows you to write a regular `for` loop, but does not have a `forEach` function.

We'll talk about ways around this in the next few days.
But for now: 

![sad](http://rack.3.mshcdn.com/media/ZgkyMDEzLzA3LzE4Lzc1L0RyLldoby41Mjg5ZC5naWYKcAl0aHVtYgkxMjAweDk2MDA-/571ec44d/6da/Dr.-Who.gif)
