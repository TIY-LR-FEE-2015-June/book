# Default Project Structure

Here are the files that should appear in every project from now on:

    /
    |-.gitignore
    |-public/
    | |-index.html
    |-assets/
    | |-app.scss
    |-Brocfile.js
    |-bower.json
    |-package.json

Along with this, include any required CSS and Javascript files.
You should name these based on what makes sense.

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
    </head>
    <body>

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
      ],
      "dependencies": {
        "reset-css": "~2.0.20110126",
        "fontawesome": "~4.3.0"
      }
    }

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
      "license": "ISC",
      "dependencies": {
        "broccoli": "rtablada/broccoli#feature/server-returns",
        "broccoli-merge-trees": "^0.2.1",
        "broccoli-sass": "^0.6.6"
      }
    }

## Example `Brocfile.js`

    var merge = require('broccoli-merge-trees');
    var compileSass = require('broccoli-sass');

    var appCss = compileSass(['styles', 'bower_components'], 'style.scss', 'style.css');

    module.exports = merge(['public', 'bower_components', appCss]);


## Example `styles/app.scss`

    /* apply a natural box layout model to all elements, but allowing components to change */
    html {
      box-sizing: border-box;
    }
    *, *:before, *:after {
      box-sizing: inherit;
    }
