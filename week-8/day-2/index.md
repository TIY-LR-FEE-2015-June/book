# Monday August 17, 2015

## Layout

* Ember Term Review
* Pods
* Ember & Ember Data by Example - Contact List App

##  Ember Terms

* Model [Ember Data] - `app/models/**/*.js` - Represents a single record of data that needs to be stored (usually to a server)
* Data Store [Ember Data] - "It's like Best Buy for models?" "We don't got one of those but we can order it" - Keeps track of what models are known and references to the required adapter to get new data.
* Router - `app/router.js` - Registers how paths in the URL are matched to different routes in our application
* Route - `app/routes/**/*.js` - Populate a template with data (usually from the data store or Ember.$.ajax) using the `model` function and handles data driven action handlers. After calling the `model` function, a route does not have access to the current data given to a template.
* Component - `app/components/**/*.js` Reusable. Deal with user inputs and actions. Only know about data that is explicitly passed to them. Can compute new properties to prepare for templating.
* Computed Properties - Functions that act like object properties. Usually rely on specific properties and are recomputed when these underlying values change. Also available via computed macros for common property techniques.
* Template - `app/templates/**/*.js` - Handlebars (rendered by HTMLBars) - Describes and lays out what the user should see. Allows you to include and pass data to components. Describe what user input (clicks, mouse events, submits, etc) should fire actions to the component or route.
* Adapter [Ember Data] - `app/adapters/**/*.js` - Describes how to store data. "Should we connect to this server, that one, or local storage". Usually tells Ember Data how to build URLs and what kind of requests to make.
* Serializer [Ember Data] - `app/serializers/**/*.js` - Translates between the server data format and what Ember Data expects and vice versa.
* Addon [Ember CLI] - Adds on functionality to the build process of an Ember CLI project. This can vary on what happens under the hood, read the documentation for the addon that you install. Can be search for using emberaddons.com
* Controller *Antipattern* - Allows you to add computed properties to a routable template. Also allows you to handle user actions with reference to the current state of all data for a routeable template.
* Helpers - Special handlebars helpers that can format data for user viewing

## Common Methods

* `this._super` - Calls the current function on the parent prototype

## Pods
