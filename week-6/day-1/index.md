# Monday August 3, 2015

Today we'll be looking at object responsibilities, documenting our code, and an introduction to testing.

# Lecture

## Responsibility

When working with Objects and functions, you should try to limit the responsibility of objects as much as possible.
Whenever possible, limit your functions or objects to a single role or use.

* show `Deck.prototype.setup` - extract `buildDeck` function
* naming `and`
* don't mess with your arguments

## Collaborators

When planning out the objects for an application, it is also important to know what each object can talk to.

* Limiting collaborators
* Layering interactions
* Delegating (middle-management)

## Documenting Code

* install `Docblockr` in ST3
* Arguments/Params vs Returns
* doc block a few functions

## Testing Setup

* `npm install -g testem` - Runs our tests and reloads on each saved file
* `brew install phantomjs` - Browser that runs from the command line
* `testem.json` - configures testem
    - `"framework": "mocha+chai"` - sets what test framework we are using
    - `"src_files"` - what files to include in our tests
    - `"launch_in_dev": ["PhantomJS"]` - where to run our tests

## Mocha Basics

* `describe` - creates a unit (what function or object are we testing?)
* `it` - creates a single test
* `beforeEach` - set up to do before every test in the current unit

## Chai

Chai sits on top of mocha and is what checks if things are returning what they should.
Think that Chai wraps `console.assert` BUT A TON BETTER!!!

* BDD - Behavior Driven Development - How should this work?
    - If I give you these two things I `expect` you give me ___ back
* `expect` style testing
    - Chaining
        * `.to`
        * `.be`
        * `.been`
        * `.is`
        * `.that`
        * `.which`
        * `.and`
        * `.has`
        * `.have`
        * `.with`
        * `.at`
        * `.of`
        * `.same`
    - Common Assertions
        * `.a` - checks the expected type
        * `.ok` - expects a truthy value
        * `.true` - expects `=== true`
        * `.exist` - expects not `undefined` or `null`
        * `.equal` - expects `===` to provided value
        * `.instanceof` - expects `instanceof` a constructor
        * `.property` - expects a property (optionally checks if that property is equal to a value)
* Test `Card`, `Hand`, `Hand.prototype.addCards`, `Hand.prototype.resetCards`

## Test Driven Development

As a way to move things forward, we can start by writing our tests first.
Then as we describe the way that our objects should behave, we can write code to make this happen.

# Exercises
