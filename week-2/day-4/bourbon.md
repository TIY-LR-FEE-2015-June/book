# Bourbon

Bourbon is a SASS library that provides a bunch of helper mixins to do a lot of the more boring CSS work for us.
Some of the main features of bourbon include:

* Adding vendor prefixes for newer CSS features
* Font variables
* Modular Scale
* Basic Shapes
* Unit Conversion
* Easier Retina Screen Detection
* Animation Helpers

## Installing Bourbon

Bourbon is ready and waiting on the Bower registery and can be quickly and easily pulled into your project:

    bower install --save bourbon

After this, a wild `bourbon` directory has appeared in your `bower_components` directory.
Now we need to `@import` bourbon into our SASS files.
But, before we can do that we need to make sure that the full path to `bourbon.scss` is included in our `includesPath` in our `Brocfile.js`, so we will need to add `bower_components/bourbon/app/assets/stylesheets`:

    var includePaths = [
        'assets',
        'bower_components/reset-css',
        'bower_components/bourbon/app/assets/stylesheets'
    ];

Now you can just add an `@import 'bourbon';` line to the top of your SASS file.

## Vendor Prefix

Back in the day of dinasaurs and non-evergreen browsers, newer CSS features would have vendor prefixes.
This meant if you wanted transitions to work your CSS would look like this:

    .my-super-cool-fade {
        transition: opactiy 2s ease-in-out;
        -moz-transition: opactiy 2s ease-in-out;
        -webkit-transition: opactiy 2s ease-in-out;
        -ms-transition: opactiy 2s ease-in-out;
    }

While this class focuses mostly on new browser compatibility, and evergreen browsers means that fewer and fewer prefixes are needed (except on REALLY cutting edge features), it is a good practice to have them around.
But, writing all of these rules and keeping them up to date can be a pain.
So, Bourbon provides a bunch of SASS mixins that allow you to write a single line of code that outputs all the required vendor prefixes.

This list includes:

* [Filter](http://bourbon.io/docs/#filter)
* [Transition](http://bourbon.io/docs/#transitions)
* [Linear Gradients](http://bourbon.io/docs/#linear-gradient)
* [General Prefixes](http://bourbon.io/docs/#prefixer)

## Font Variables

When working on sites, there are a few common combinations of basic fonts that you may want to use.
Bourbon gives you some quick short hand for this by setting some really easy variables for common font-families (along with their fallbacks).

* $georgia
* $helvetica
* $lucida-grande
* $monospace
* $verdana

To see these in full expanded mode, check the [Bourbon Docs](http://bourbon.io/docs/#font-stacks).

## Modular Scale

When working with font readability and design, one common consideration is to use things like the golden ratio to determine the different font sizes to use.
Using a ratio like this helps readability and clear distinction between different levels of text.

Bourbon allows you to use a `modular-scale` mixin to allow you to write in different importance "levels" and from there the mixin will be able to figure out your proper font-size based on the golden ratio (or another ratio of your choice).

To learn more checkout this article:

http://www.svenread.com/golden-ratio-modular-scaling-on-a-responsive-website/

## Basic CSS Shapes

So far, we have used borders to create triangles and other shapes.
This can be a bit hard to get "just right".
Plus what if that triangle needs to be up instead of down now?
Bourbon has you covered with a few mixins:

* [Triangle](http://bourbon.io/docs/#triangle)

## Retina Screen Detection

Today with retina and high resolution screens, we have to start looking at supporting these devices.
This means sending different resolution backgrounds or even images and icons to different devices based on media queries.
These can be a bit obtuse to remember and no one wants to build media queries just for one difference in background.

Bourbon has a to create retina background images.

* [Retina Image](http://bourbon.io/docs/#retina-image)


## Animation Helpers

Though we haven't covered animations, Bourbon has some helpers to make animations easier to manage.
While these seem a bit verbose, they do help with cross-browser compatibility.

* [Animation](http://bourbon.io/docs/#animation)
