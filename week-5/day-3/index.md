# Wednesday July 29, 2015

### JS Concat

* When to use concat
* Order matters
* Source Maps - I don't want to see an error on line 20000!
  
    var tree = concat(tree, {
      outputFile: '/output.js',
      inputFiles: ['loader.js', '**/*']
    });

### Underscore.js

Many array functions were added as part of the Javascript language in the last few years in a specification called ES5.
Because of this older mobile browsers and IE don't implement all things.

To fill in these gaps and give a lot of conveniences, a library called Underscore was created.
Unlike other libraries Underscore doesn't change the `Array.prototype` object.
Instead it wraps arrays (similar to how jQuery wraps around HTML elements) and then that result will have all of the standard functions we just covered: `forEach`, `filter`, `map`, `reduce`, `all`, and more!


## Pass By Reference, Side Effects, Mutability, and such

When working with objects, you have to be aware what happens when you pass those objects to functions.
Unlike strings, numbers, and booleans: objects (including arrays) are passed by reference.
When a variable is passed by reference, this means that any changes to that variable will effect it beyond that function.
For instance this function working with an array:

    var changeFirstValue = function(arr) {
        arr[0] = 'Hi';
    };

If we pass in an array, the first element will be changed forever (or at least until we change it again).

    var a1 = ['Hello', 'world'];
    changeFirstValue(a1);

    console.log(a1); // Prints: ['Hi', 'world']

This means that without proper discipline, it is very easy to write functions that have strange side effects if you aren't careful when working with objects.
This ability for objects and variables to change over time is called mutability.

### Strict Immutability

One way to manage side effects is to force yourself to write and use immutable.
This means that not only do you not modify objects within functions, you also will not change the value of a single variable name.
So, if you created `a1` as an array of `['Hello', 'world']`, a fully immutable program would never change `a1` like so: `a1 = [1, 2];`.

### Cloning and Assignment

A step beyond toward practicality is to make sure that whenever you change the value of an object, you should explicitly reset it. Also note that when you reset the value of this object with this mindset, you would create a complete copy of the original instead of keeping any reference of the original object.
To do this, underscore's `clone` function will come in handy, letting you create a copy without referring to the original point in memory from the old object.
So now let's see what our `changeFirstValue` function would look like:

    var changeFirstValue = function(arr) {
        var cp = _.clone(arr);
        cp[0] = 1;

        return cp;
    };

Then we could use this to reset our first value in `a1`:

    var a1 = ['Hello', 'world'];
    a1 = changeFirstValue(a1);

This code is more explicit that `a1` is being changed.


### Prototypes and Objects

While "Strict Immutability" and Reassignment help to keep code explicit about when variables change, this can be restrictive when working with objects.
Especially when working with objects and application state this can get really awkward.
So, one rule of thumb to follow is that objects should only modify themselves or delegate changes to child objects.

For instance when looking at two warring `Character` objects:

    function Character(health, strength) {
        this.health = health;
        this.strength = strength;
    }

At first you might think to add an `attack` function to the Character prototype:

    Character.prototype.attack = function(enemy) {
        enemy.health -= this.strength;
    };

However this fails for a few reasons.
Our character knows too much about its enemy.
Characters shouldn't let anyone to go around messing with their health points.
Plus let's look at how this would look when we run it:

    var hero = new Character(100, 10);
    var grunt = new Character(60, 4);

    hero.attack(grunt);

Look at this code: what object is changing?

Let's look at how we could make this stick to cleaner roles:

First we'll make `health` and `strength` private properties and create `takeDamage` and `getStrength` functions to get to these properties without letting things to get out of hand:

    function Character(health, strength) {
        this.takeDamage = function(amount) {
            health = health - amount;
        };

        this.getStrength = function() {
            return strength;
        };
    }

Then we would need to update `attack` on our prototype:

    Character.prototype.attack = function(enemy) {
        enemy.takeDamage(this.getStrength());
    };

It's better, but we're still left with `hero.attack(grunt)`. And we are directly modifying our `enemy` (even if it is via the `takeDamage` function).

We can instead clear this up by changing things around and making an `attackedBy` function.

    Character.prototype.attackedBy = function(enemy) {
        this.takeDamage(enemy.getStrength());
    };

Now look at our app code:

    var hero = new Character(100, 10);
    var grunt = new Character(60, 4);

    hero.attackedBy(grunt);

It reads cleaner, if we are reading just the start of the line, we can see that we are calling the `attackedBy` function on our `hero` variable and we can assume that the `hero` might be modified.

> As a rule of thumb, do everything you can not to make modifications to arguments from your functions directly.
