# SASS

While CSS has come a long way in the last few years, there are still a few things that make maintaining a large codebase pretty tough.
Given enough time: our CSS file will become HUGE and include a lot of repetition.

This is where SASS comes in.
SASS allows us to better organize and maintain CSS by giving us variables, imports, mixins (these are like functions that output entire chunks of CSS).

Unfortunately, the browser (even new ones like Chrome) has no idea what to do with SASS files.
So we will need some sort of tool to take SASS and turn it in to normal CSS files.

## Building SASS with Broccoli

Broccoli works incredibly well with SASS.
But, just like pulling in the `broccoli-merge-trees`, we have to install a Broccoli plugin to compile our SASS files into regular CSS and put it as part of our build.
The plugin for this is called `broccoli-sass` and can be installed for our current project:

    npm install --save broccoli-sass

Now that we have our plugin installed, we'll need to update our `Brocfile.js`.
`broccoli-sass` gives us a function that will take in a SASS file and return a tree with our compiled CSS.
Let's for instance say we had an `assets` directory with an `app.scss` file that we want to compile into a new `app.css` file, we would need to add this to our `Brocfile.js`:

    var compileSass = require('broccoli-sass');

    var cssFiles = compileSass('assets', 'app.scss', 'app.css');

Now that we have a tree of compiled CSS files, we will need to merge this in with our existing file trees:

    module.exports = merge(['public', 'css', cssFiles]);

Now if we run `broccoli build` or restart our `broccoli-lr serve`, the SASS file `assets/app.scss` should be compiled down and a new `app.css` file is available in our `dist` directory or our development server.

## Importing Other SASS Files

Right now if you want to break up your CSS files to make them more managable, you would have to create new `link`s in your HTML file.
Adding more `link`s requires the browser to make more requests and on slower connections this can cripple the page load time or even give the user a time of unstyled content.

Instead, SASS allows us to continue breaking up our files and simply create `@import` statements in our SASS file.
In regular CSS `@import` statements let us pull in external CSS files, but this triggers a browser request to that new file.
Since SASS is compiled, `@import` statements can be a bit more smart.

When the compiler sees `@import` without any file extension, it will try to grab that file (SASS or CSS) and then include it directly in-line with your final compiled CSS code.
This means no extra requests!
So to import a file called `home-page.scss` from our `app.scss` file we would have a line of code that reads:

    @import 'home-page';

Small files that are imported like this are referred to as "partials", since they only include a small bit of our final CSS.
By convention, we usually will name partials starting with an underscore, this way we can easily tell our starting file apart from our partials.
Luckily, SASS will import files starting with underscores even without having to write this in our code.
So even if we rename `home-page.scss` to `_home-page.scss`, our import statement above will still work.

## `includesPaths` and Third-Party Includes

The way that Broccoli and Broccoli SASS are set up means that with our existing `Brocfile.js`, we will only be able to import files that live in the `assets` directory.
While this is awesome for breaking things into smaller, more manageable partials: it does not do much in terms of bringing in third party code.

So, we will need to make Broccoli SASS aware of third-party files.
When we use the function provided by `broccoli-sass`, the first argument can take an array of folders instead of just a single string.
The first folder in this array will need to be where your starting file (the name which is the second argument in the function) is located.
After that any folders in the array will be seen as part of the `includesPaths` configuration for SASS.

So if we have installed `reset-css` with Bower we could add update our `Brocfile.js`:

    var cssFiles = compileSass(['assets', 'bower_components/reset-css'], 'app.scss', 'app.css');

Now we can `@import 'reset';` in our SASS file and `reset.css` will be printed in our final `app.css` build.

## Relative Paths and Font Files

Some CSS and SCSS files may import font files when working with things like Font Awesome.
We have to be aware of this and can test things by opening the Chrome Developer tools and seeing if there are any 404 errors.

Luckily for Fontawesome there is a work around for this error (although not all libraries will have this fix).
Instead of adding `bower_components/fontawesome/css` to your `includesPaths`, you can add `bower_components/fontawesome/scss`.
Now, before you `@import 'font-awesome';` in your SASS file, you can set a `$fa-font-path` variable which let's you change where Font Awesome looks up the font files.

What's even cooler than being able to change this to a local file, we have the ability to point this to a CDN instead:

    $fa-font-path:        "//netdna.bootstrapcdn.com/font-awesome/4.3.0/fonts";
