# Default Project Structure

Here are the files that should appear in every project from now on:

    /
    |-.gitignore
    |-index.html
    |-bower.json

Along with this, include any required CSS and Javascript files.
You should name these based on what makes sense.

## Example `.gitignore`

    /bower_components

## Example `index.html`

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

## Example `main.css`

    /* apply a natural box layout model to all elements, but allowing components to change */
    html {
      box-sizing: border-box;
    }
    *, *:before, *:after {
      box-sizing: inherit;
    }
