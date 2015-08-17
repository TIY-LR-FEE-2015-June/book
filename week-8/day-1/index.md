# Monday August 17, 2015

## Layout

* Ember Questions
* Component/Route Review
* ES6 Modules, Fat Arrow, and Template Strings
* Ember Data

## Lecture

### Ember Questions

* Ember vs Backbone (scope and jobs)
    - Scope, stability, conventions
* Builds - We will cover this Thursday
    - TLDR; A build is a one time run of your build, `ember serve` rebuilds after every file change.
* Environments - We will cover this Thursday
    - TLDR; there are small changes that you will want to make between different versions of your app (testing, production, etc)
* Controllers - We will cover this Next Week
    - TLDR; Controllers allow you to manage data and state for a single route AFTER it has been loaded
* Helpers - We will cover this Wednesday
    - TLDR; Ember uses handlebars helpers to modify how you display data from your template to your user
* Actions - We will cover this Wednesday
    - TLDR; Components kind of disable bubbling and put it back in your control, but there is an older convention that we will talk about
* `modelFor` vs other methods - We will cover this Today
    - TLDR; Passing around data is hard, there are better conventions for this
* Block vs Inline components - `link-to`
    - TLDR; Components allow you to modify the contents of themselves, but `link-to` is flexible and allows you to either create it as an inline component or a component block
* `homeRoute` - We will cover this on Friday
    - This is an option for Ember CLI Materialize to modify the link in the main navigation.

### Component & Routes

* Routes do what?
    - Setup data
    - Actions that are specific to JUST THAT ROUTE (actions that aren't reusable)
* Components
    - Morph data for a specific usecase (map and reduce, filter, etc)
    - Actions that are reusable or need to tweak user input before passing on responsibility

### ES6 Syntax

* Modules
    - No more globals
    - `import ___ from '____'`
    - `export default`
    - http://www.2ality.com/2014/09/es6-modules-final.html
* Fat Arrow
    - No more `_this`
    - Shorter syntax
    - Less questions about 'what does this mean'?
* Template Strings
    - Back Tick vs quotes
    - Pull in JS with ${___}

### Ember Data
