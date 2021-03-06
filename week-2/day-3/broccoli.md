# Broccoli.js

Broccoli.js is a very low level build tool that allows us to build, compile, and better prepare our files for production.
This could include moving files from one directory to another or compiling languages like SASS.

# Installing Broccoli CLI

To get started with Broccoli, you will need to first globally install the `broccoli` command using npm so that you are able to run build local Broccoli.js projects.
To install this command across your computer run:

    npm install -g broccoli-cli

You will only need to run this once and then you should have a `broccoli` command available in the terminal.

# Installing Local Broccoli

Like many CLI runners, `broccoli-cli` only has the bare minimum code to give you a `broccoli` command in the terminal.
You will also need to install a local version of `broccoli` as well a any broccoli plugins needed for your project (but [that's another show](http://www.goodeatsfanpage.com/References/another_show.htm) [or at least: later in this page]).
Now you can install a local version of `broccoli` by running:

    npm install --save broccoli

Note that you should have already run `npm init` by now.

> **Note** Having a local version of broccoli allows projects to use different broccoli versions and your old projects will continue to build even if your new projects use a newer version of broccoli that may be incompatible.
> This may seem inconvenient now, but compared to other build tools which only install globally, this can be a life saver when you don't have to do massive updates to your build process just to make one small style change.

# Basics

Broccoli works by looking at and tracking changes in "trees".
You can think of trees as the folders in your project.
With a set of trees to work with, Broccoli lets standardized plugins modify these folders for a single "build".

In order for Broccoli to know how to build our project, it will need a `Brocfile.js` file to tell it what to do.
In it's most basic form, all Broccoli needs is a folder name.
To send a folder named `public` to our build we will need a `Brocfile.js` that looks like this:

    module.exports = 'public';

Whatever we set `module.exports` to is what we will see in our build outputs.

# Builds

Speaking of making our build, let's actually run a build and see what happens.
To have Broccoli build our project into a new `dist` directory in the terminal you can run:

    broccoli build dist

Now you should see the contents of your `public` directory copied into a new `dist` directory.

> **NOTE** Broccoli can't build into an existing directory, so if you want to try a new build, you will need to `rm -rf dist` before running `broccoli build` again.

# Merging Trees

So far, Broccoli doesn't seem to be doing too much to our development process.
To make Broccoli more useful, we will now install our first broccoli plugin so that we can take the contents of two folders and then stuff them together in our build directory.
The plugin that does this is called `broccoli-merge-trees` and we can install it with:

    npm install --save broccoli-merge-trees

Now that we have it installed, we can put our files together!
`broccoli-merge-tress` will give us a new `merge` function will accept an array of all of the folders that you wan to smash together.
Assume that your project has a few files `public/index.html` and `css/style.css`.
Let's say that we wanted both of these output to our new build folder.
Then our `Brocfile.js` file would look like this:

    // Pulls in the `merge` function with NPM
    var merge = require('broccoli-merge-trees');

    module.exports = merge(['public', 'css']);

And if we run `broccoli build dist`, we will have a `dist` directory with a copy of `index.html` and a copy of `style.css`.
Our whole project will look a bit like this

    /
    |- css/
    |  |- style.css
    |- dist/
    |  |- index.html
    |  |- style.css
    |- public/
    |  |- index.html
    |- Brocfile.js
    |- package.json

# Running a Broccoli Server

While single builds are great for sending things to production, they aren't too great for rapid development.
Instead, Broccoli allows us to run a small development server that includes the files that would usually be in the output files from `broccoli build`.
To run this server run:

    broccoli serve

Now if you visit http://localhost:4200, you will be able to see your temporary server.
When you change a file in your project, this will then update on the server.

# LiveReload and Broccoli Servers

When working on HTML and CSS, instant feedback is incredibly helpful.
In Chrome we can get this instant feedback by installing the [Live Reload Extension](https://chrome.google.com/webstore/detail/livereload/jnihajbhpnppcggbcgedagnkighmdlei).
But, on it's own, this extension only listens for some sort of server to tell it when to reload the page.

Luckily, there's a command called `broccoli-lr` that will allow us to run the same functionality as `broccoli`, but it has the added benefit of also triggering Live Reload!

To install `broccoli-lr`, run:

    npm install -g broccoli-lr

Now wherever you used to run `broccoli serve`, you can now replace this will `broccoli-lr serve`.
Once you have this server running, you can activate Live Reload by clicking on it (the middle small circle will be filled in when it is running).
Now whenever you change and save a file that is being watched by Broccoli, your browser should reload!
