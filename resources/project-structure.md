# Default Project Structure

Here are the files that should appear in every project from now on:

    /
    |-.gitignore
    |-public/
    | |-index.html
    |-assets/
    | |-scss/
    | | |-app.scss
    | |-js/
    | | |-app.js
    |-Brocfile.js
    |-bower.json
    |-package.json

Along with this, include any other SCSS, HTML, or Javascript files required by the assignment.

## Example `.gitignore`

    /bower_components
    /node_modules
    /tmp

## Example `public/index.html`

    <!DOCTYPE html>

    <html lang="en">
    <head>
      <meta charset="utf-8">
      <meta name="viewport" content="width=device-width, initial-scale=1">

      <title>Project Title</title>
      <link rel="stylesheet" href="app.css">
    </head>
    <body>

      <script src="app.js"></script>
    </body>
    </html>

## Example `bower.json`

After `bower init` and a few added dependencies your `bower.json` file should look a bit like this:

    {
      "name": "assignment-name",
      "version": "0.0.0",
      "homepage": "https://github.com/username/project-name",
      "authors": [
        "Your Name <your email>"
      ],
      "license": "MIT",
      "ignore": [
        "**/.*",
        "node_modules",
        "bower_components",
        "test",
        "tests"
      ]
    }

> Note that this `bower.json` file has no dependencies yet!
> You will need to run `bower install --save` with some dependencies
> Here's a few you'll use a lot:

* jquery
* reset-css
* bourbon
* neat
* fontawesome

## Example `package.json`

After `npm init` and a few added dependencies your `package.json` file should look a bit like this:

    {
      "name": "assignment-name",
      "version": "1.0.0",
      "description": "",
      "main": "index.js",
      "scripts": {
        "test": "echo \"Error: no test specified\" && exit 1"
      },
      "author": "",
      "license": "ISC"
    }

> Note that this `package.json` file has no dependencies yet!
> NPM dependencies will mostly be used for our build tools and Node.js servers.
> You will need to run `npm install --save` with some dependencies
> Here's a few you'll use a lot:

* broccoli
* broccoli-merge-trees
* broccoli-sass
* broccoli-funnel

## Example `Brocfile.js`

    var merge = require('broccoli-merge-trees');
    var compileSass = require('broccoli-sass');

    var appCss = compileSass(['styles', 'bower_components'], 'style.scss', 'style.css');

    module.exports = merge(['public', appCss]);

> Note this `Brocfile.js` file is fairly barebones.
> For larger projects you will probably need to do more than just the above (`broccoli-funnel` and the like).


## Example `styles/app.scss`

    @include 'reset';

    /* apply a natural box layout model to all elements, but allowing components to change */
    html {
      box-sizing: border-box;
    }
    *, *:before, *:after {
      box-sizing: inherit;
    }
