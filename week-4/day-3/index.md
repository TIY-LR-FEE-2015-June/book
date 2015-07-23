# Wednesday July 22


## Questions from Last Night's Reading

* When would we use prototype? (Shared functionality)
* if `[]` are `{}` then what's the difference (`instanceof`)
* prototype vs assignment and regular `{}` (Constructors)
* Prototypes and Scope (private variables)
* Getters and Setters

## Outline

* [`this` with regular objects](https://github.com/TIY-LR-FEE-2015-June/lesson-4.3/blob/327e923c6053e04d1963f5843f7a41082ed3c3b6/prototype.js)
* [returning objects from functions](https://github.com/TIY-LR-FEE-2015-June/lesson-4.3/blob/bfe493390cbeed11ede16175471e0b0a169e8f90/prototype.js)
* [Basic constructors](https://github.com/TIY-LR-FEE-2015-June/lesson-4.3/blob/7b114c5e0eace3af93295c5a25957e2505df4df0/prototype.js)
* [Basic prototype inheritance](https://github.com/TIY-LR-FEE-2015-June/lesson-4.3/blob/172fcfc96761bf36bcafbdbcdcd59cb869045905/prototype.js)
* [Overriding Prototype Functions](https://github.com/TIY-LR-FEE-2015-June/lesson-4.3/blob/2d9115f4a5db413d4ce50621fb3141cea2c2a353/prototype.js)
* [Private Variables](https://github.com/TIY-LR-FEE-2015-June/lesson-4.3/blob/cc02150c00b27b8496a252735255706601425f9e/prototype.js)

## Exercises

* [MathArray Prototype](https://raw.githubusercontent.com/TIY-LR-FEE-2015-June/lesson-4.3/master/math-array.js)
* [US Citizen (private SSN)](https://github.com/TIY-LR-FEE-2015-June/lesson-4.3/blob/master/citzen.js)

## Suggested Reading

There's been still some confusion about "what is a function", "what does a method mean", "what does property mean".
So, if you ask any of those questions and can't answer quickly, then read:

* [Objects and Properties](http://bonsaiden.github.io/JavaScript-Garden/#object.general)
* [Constructors](http://bonsaiden.github.io/JavaScript-Garden/#function.constructors)
* [Prototype](http://bonsaiden.github.io/JavaScript-Garden/#object.prototype)
* [`instanceof`](http://bonsaiden.github.io/JavaScript-Garden/#types.instanceof)
* [Functions](http://bonsaiden.github.io/JavaScript-Garden/#function.general)
* [`this`](http://bonsaiden.github.io/JavaScript-Garden/#function.this)

## Extra Reading

Once again, try reading the Eloquent Javascript chapters from the last two days:

* [Prototypes and Objects](http://eloquentjavascript.net/06_object.html)
* [Values](http://eloquentjavascript.net/01_values.html#h_sVZPaxUSy/)
* [Numbers](http://eloquentjavascript.net/01_values.html#h_flOCH3CuFg)
* [Arithmetic](http://eloquentjavascript.net/01_values.html#h_RfBT3HMnYs)
* [Variables](http://eloquentjavascript.net/02_program_structure.html#h_rAGNsfewCX)
* [Defining A Function](http://eloquentjavascript.net/03_functions.html#h_tqLFw/oazr)

## Homework

Tonight you will be working on the prototype exercise:

* https://github.com/tiy-lr-fee-2015-June/assignments/tree/master/4.3-prototypes

### Getting Started on HW

> Setup for tonight's HW
> * Create new folder `4.3-prototypes`
> * Initialize git in this new project
> * Copy `constructors.js`
> * Create `.jscsrc` and set things up for Airbnb code style
> * Commit to `master`
> * Create github repo (`hub create`)
> * Push
> * Switch to `develop`
> * Succeed!

## Gems from the Slackiverse

Since Slack isn't permanent I will try to start copying some of the most helpful questions and answers from the slack rooms:

### Better Prompt for Question 4</dt>

    // Create a constructor called `KeepSecret`. The constructor function
    // itself should accept a parameter called `secret` it should keep this
    // as a private variable. Add a function to `KeepSecret` that is called
    // `squeal` that returns the secret string.

### Better Prompt for Question 5

    // Create a constructor called `Key`. Create another constructor
    // called `Safe`. Make the Safe constructor take 2 arguments. The
    // first argument can be any piece if data to keep safe. This must
    // be stored using a private variable like you did with KeepSecret.
    // The 2nd param to the `Safe` constructor needs to be an instance
    // of `Key` you need to store it as a private variable. Then, add a
    // function to the Safe prototype called `unlock` that accepts a key. 
    // If the key matches the key that was used to create the Safe; then
    // return the secret data.

### What is a `property`?

When we talk about a `property` all we mean is that there is a value on an object.

If I want a `property` called `say` on a Dog equal to `life if rough`, then I should be able to run `var d = new Dog()` and when I check the value `say` it should always return `life is rough`.

### What is a `method`?

When we talk about a `method` that just means that there is a function available on an object.

So if an assignment says that a Cat should have a method `growl`, I should be able to create a Cat with `var c = new Cat()` and then run `c.growl()`.
