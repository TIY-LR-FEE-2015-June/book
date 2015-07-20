# Javascript Code Style (jscs)

When working on a team, having a consistent style of code, helps developers to more quickly understand and get up and running.
Whether it is an old project you haven't worked on in a while or something completely new, a consistent style guide allows you to focus on just the task at hand rather than whether this project uses tabs or spaces (among many other things).

## What is a "Style Guide"

Style guides differ from company to company, but most at least include the way that you layout your code.
Some common things may include:

* How to name variables?
* How to name variables with multiple words?
* How many spaces (or tabs) should lines be indented?
* Should you use shorthand vs explicit code (such as a single line `if` statement)?
* Should you use `{}` or `new Object()`?
* Should you use `==` or `===` by default?

But, style guides (such as [the Airbnb Style Guide](https://github.com/airbnb/javascript)) may be much more strict and talk about things like when to declare functions, when to use new language features, and more.
These are still considered style guides, but the most companies will limit the scope of their style guides to just cover things like whitespace and equality operators.

## Enforcing Style Guides with `jscs`

While there are a few different tools that will enforce a style guide for your code, the most popular tool for the job right now is [`jscs`](http://jscs.info/).
JSCS will read through your Javascript file and based on how you configure it, JSCS can alert you when you are not meeting the requirements of your style guide.

## Installing JSCS

To install JSCS, run:

    npm install -g jscs

Once this is installed, you can run `jscs` from the command line.

## Installing JSCS Linters in Sublime Text

While it is totally possible to use the `jscs` command from the terminal or add it to the build process: it is much better to have instant feedback in your editor.
For this, we can install a plugin for Sublime Text that will check for JSCS warnings every time we save our file.

The package that we will be using is called `SublimeLinter-jscs`.
To install this, follow the normal procedure of installing a plugin with Package Control.

Now, whenever your files would normally be linted for syntax errors, JSCS will also check for style errors!

## Configuring JSCS

To configure JSCS in your project, start by creating a new file called `.jscsrc`.
This will be a JSON file that contains all of your configuration options for a single project and allows each project to have its own style guide while still giving the proper warnings for each one.

While there are many different configuration options available for JSCS, most of your configuration can be brought in by choosing an existing `preset`.
For this class, we'll be using the `airbnb` preset, so your `.jscsrc` file will look like this:

    {
        "preset": "airbnb"
    }

## Fixing JSCS Errors

Once you have a `.jscsrc` file and have set up the JSCS linter in Sublime, you should now see lint errors show up when you save your Javascript file (unless you don't have any errors of course).
We could go through and manually fix these errors: however since most of the style guide has to do with whitespace and block notation, matching the style guide should be pretty easy for a plugin to handle for us!

So, for this, we can install the `JSCS-Formatter` package in Sublime Text.
Now you can use the keyboard shortcut `CMD+SHIFT+H` and the plugin will automatically try to fix your JSCS errors.

> **NOTE** This formatter isn't perfect and if you have a major syntax error, running automatic formatting could make your code jumble even worse. If your code looks like a tornado passed through, undo the formatting with `CMD+Z` and then save and see if there is a syntax error that you need to fix before trying to auto format again.
