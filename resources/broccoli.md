# Common Broccoli Plugins

Broccoli is an incredibly powerful build tool.
It works by making small changes to folders and then outputting them either to a build directory or a development server.

By default, Broccoli will serve the "tree" that you export from your `Brocfile.js` which is done using `module.exports = `.
You can read more about this in the full [Broccoli Notes](../week-2/day-3.html).

Before you send a final tree to broccoli, you will likely want to modify your source files into their final forms using plugins.
This is a list few of the most common broccoli plugins we've used and a quick reference of how to use them.

# `broccoli-merge-trees`

This plugin takes an array of either folder names as strings or outputs from other plugins.

    var merge = require('broccoli-merge-trees');

    module.exports = merge(['public', 'assets']);

This would take all of the contents of both `public` and `assets` and put it at the root of our build output.

So the following project:

    /
    |-public/
    | |-index.html
    |-assets/
    | |-app.js

Would output:

    /
    |-index.html
    |-app.js

# `broccoli-funnel`

Broccoli Funnel allows you to pull only a small amount of files from a directory and send them to your final build.
This is particularly helpful for folders like `bower_components` where you only want one or two files out of tens or possibly hundreds of files.

This plugin takes two arguments: the directory or plugin output that you are funneling through, and an options object that says how you want to funnel things.
For this options object the only real property we care about is `files` which accepts an array of files that we care about.

    var funnel = require('broccoli-funnel');

    module.exports = funnel('bower_components', {files: ['jquery/dist/jquery.js']});

A project that looks like this:

    /
    |-bower_components/
    | |-jquery/
    | | |-dist/
    | | | |-jquery.js
    | | | |-jquery.min.js
    | | | |-jquery.min.js.map
    |-assets/
    | |-app.js

Would output:

    /
    |-jquery/
    | |-dist/
    | | |-jquery.js

# `broccoli-sass`

CSS can be really tough to set up, SASS allows us to use things like variables, functions, and third party dependencies.
Broccoli SASS allows us to compile a single source file into a final destination.

The `broccoli-sass` plugin takes in a few different arguments:

* An array of folders names or input trees that contain SASS needed for the app
* An input SASS file name to start: this is relative to the first tree in the above array
* An output CSS file name


Here is an example `Brocfile.js`:

    var sass = require('broccoli-sass');

    module.exports = sass(['assets', 'bower_components/reset-css'], 'app.scss', 'app.css');

A project that looks like this:

    /
    |-bower_components/
    | |-reset-css/
    | | |-reset.scss
    |-assets/
    | |-app.scss

Would output:

    /
    |-app.css

In your `app.scss` you could now `@import 'reset'` to pull in the contents of `bower_components/reset-css/reset.scss` into your final compiled `app.css` file.

# `broccoli-inject-livereload`

When working with livereload, you usually have to click to activate the plugin, this can be a pain.
This is where `broccoli-inject-livereload` can be a lifesaver!

This plugin acts just like a regular tree in broccoli except that it will take any HTML files and add a script to automatically activate the LiveReload extension.

Here is an example `Brocfile.js`:

    var reload = require('broccoli-inject-livereload');

    module.exports = reload('public');

A project that looks like this:

    /
    |-public/
    | |-index.html
    | |-app.css

Would output:

    /
    |-index.html
    |-app.css
