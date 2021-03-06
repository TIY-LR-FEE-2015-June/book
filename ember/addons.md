# Using Ember CLI Addons

When working with Ember CLI, there are times where you want to be able to bring in different build steps or different libraries.
Since many tools are incredibly common, these are often available as Ember CLI Addons that add functionality to your project without writing any code (or very little).

Listed below are a few common Addons we've used and you might want in your project.

## SASS

Installation: `npm install broccoli-sass`

Notes: This addon makes Ember CLI look for an `app/styles/app.scss` file which will be compiled and used for your app styling.

## Meyer Web CSS Reset

Installation: `ember install ember-cli-meyer-reset-sass`

Notes: This addon requires you to already have installed `broccoli-sass`.
It only sets up the import trees for SASS so in your `app.scss` file, you will need to add `@import 'reset';` just like when you have used reset.css in the past.

## Bourbon (SASS)

Installation: `ember install ember-cli-bourbon`

Notes: This addon requires you to already have installed `broccoli-sass`.
Unlike reset, this package will try to create a new `app.scss` file for you with the line `@import 'bourbon';`.
Beware if you already have an `app.scss` file as tihs will completely replace any existing ones, it will not try to merge things.

## Neat (SASS)

Installation: `ember install ember-cli-neat`

Notes: This addon requires you to already have installed `broccoli-sass` using `npm install --save-dev broccoli-sass`.
Unlike reset, this package will try to create a new `app.scss` file for you with the line `@import 'neat';`.
Beware if you already have an `app.scss` file as tihs will completely replace any existing ones, it will not try to merge things.
This package will also pull in bourbon, so you do not need to install `ember-cli-bourbon` if you want to use neat.

## Lodash (Basically the Same as Underscore.js)

Installation: `ember install ember-lodash`

Notes: This addon allows you to import lodash modules, it does not expose lodash as a global `_` variable.
To use lodash add an `import _ from 'lodash/lodash';` to the top of files where needed.
