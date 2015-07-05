# CSS Syntax

Even though it may not seem like it right now, CSS breaks down to 3 simple components:

* Selectors
* Properties/rules
* Values

Each area of your CSS file will be broken down into blocks that look like this:

    selector {
        property: value;
    }

Between the curly braces, you can write many rules that apply to a single selector.

## Comments and Organization

CSS files can become a bit unwieldy and without some organization files can be a bit hard to follow.
You can counteract this by organizing your blocks and adding comments.
Comments start with `/*` and end with `*/`: anything between this will be ignored completely.

### Tips for organization:

* Break your file into sections based on where things fall on the page: start with the top, then move your way down
* Within sections start with the most broad selectors possible and then get more specific (ex `nav` would come before `nav li a`)
* Organize your properties together based on what you are trying to achieve: (ex `padding` might be grouped with `width` while `font` would be better grouped with `color`)
* Comment anything weird that you may have to fix (nudging things around to get pixel perfect results for instance)
