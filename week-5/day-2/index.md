# Tues July 28, 2015

## Review

### Prototypes

    function Person(firstName, lastName) {
      this.fullName = function () {
        return `${firstName} ${lastName}`;
      };
    }

### Handlebars

Handlebars has a few steps:

* create a handlebars template in HTML
* grab handlebars template string using jQuery and jQuery.html()
* use Handlebars.compile to get a template function from your template string
* call your new template function passing in some data to work on and get a string output with replaced by the data you pass in to your template function
* take the output string from your template function and send it into the DOM using either jQuery.html or jQuery.append.

### AJAX

Why do we use AJAX: whenever we need data that isn't included in our raw HTML file:

* Dynamic data from an API
* Extra information not included to speed up the initial page load

### Broccoli Plugins TLDR;

Added [page on the Gitbook](../../resources/broccoli.html)

## New things

### Array.prototype functions

* [`map`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map) - Return a new array of values where each value is changed by the callback

    var simpsons = [{first: 'Homer'}, {first: 'Marge'}, {first: 'Bart'}, {first: 'Lisa'}];

    var output = simpsons.map(function(familyMember) {
      return familyMember.first;
    }); // ['Homer', 'Marge', 'Bart', 'Lisa'];

* [`filter`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/filter) - Filter down array forEach element where the callback returns true

  var simpsons = [{first: 'Homer'}, {first: 'Marge'}, {first: 'Bart'}, {first: 'Lisa'}];

  var output = simpsons.filter(function(familyMember) {
    return familyMember.indexOf('i') > -1;
  }); // [{first: 'Lisa'}]

* [`reduce`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/reduce) - work towards a single value that represents the array (sum, multiples, etc)

## Lesson Github

https://github.com/tiy-lr-fee-2015-June/lesson-5.2

## Lab

In today's lab, we made a new version of our podcast site.
This time we pulled out a `render` function so that we can render an array of podcast.
Then we added an input and listened for user input using `$('input').on('input')`, then we had our callback use `Array.prototype.filter` and filtered out results based on our search term!

## Homework

For tonight's homework, we'll be working through something called a Koan.
This is a set of exercises using tests that will guide you through some of the fundamentals of Javascript along with the array functions we covered today.
For each test, you will be changing the value of `FILL_ME_IN` to make the test pass (turn green).
