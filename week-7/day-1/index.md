# Monday August 10, 2015

# Lecture

## Questions

- Routing
- Filtering
- Following instructions
- `url` vs `urlRoot`
- "slightly similar" & "lots of files"
- term review

## Debugging

## Repetition, Patterns, and Marionette

## Events and Fetch

## Terms to Know

* **[Model](http://backbonejs.org/#Model)** - Stores properties for a single "record" that needs to be synced with the server or other data source
    - Useful methods: `set`, `get`, `save`, `destroy`, `fetch`
* **[Collection](http://backbonejs.org/#Collection)** - Container for working with multiple models, useful for sorting, filtering, fetching all (or mulitple) models from the server.
    - Useful methods: `fetch`, `get`, `add`, `find`, `findWhere`, `filter`
* **[View](http://backbonejs.org/#View)** - DOM representation of underlying data: responsible for rendering and user events/interactions (clicks, submits, etc)
    - Useful methods: `$`, `remove`
    - Useful properties: `initialize`, `$el`, `template`, `render`, `events`
* **[Router](http://backbonejs.org/#Router)** - Responsible for hooking up data into views and translating the URL/Address Bar into an "Application State" (what the user should see based on the URL).
    - Useful methods: `navigate`
    - Useful properties: `routes`
