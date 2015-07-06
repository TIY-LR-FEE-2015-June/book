# Basic CSS Properties

Once you have declared a block with a CSS selector, you are now ready to start styling elements on your page.

This is where CSS properties (sometimes I will call these rules) come into play.
In this course, we'll be highlighting some of the more tricky and commonly used properties.
When you are looking for how to style something and can't remember what property to use, I recommend checking [this list](https://css-tricks.com/almanac/properties/) or more importantly starting a Google search with `csstricks` which should lead you to the CSS Tricks page explaining almost every available (and even a lot of experimental) CSS properties.

# Sizing Elements

The first set of CSS properties that we covered dealt with how we can size elements.

By default, you should be able to size elements with the `width` and `height` CSS properties.
However, these properties only will not work if an element has it's `display` property set to `inline`.
While `display` is usually set to `block`, elements like `span`, `strong`, and `em` use `inline` display so that small changes like changing color or adding text changes can be made without breaking the text block.

By default, `display: block` will drop the element to the next line.
We will be covering different ways to have multiple blocks on a single line in the next few lessons.

# Adding Whitespace, Backgrounds, and Borders

When working with element styles, there are two different ways that will allow you to add some breathing room around your content:

* `margin`
* `padding`

These two work differently and this will be easier to see when we add borders and background.
The properties to style borders and backgrounds are terribly exciting and hard to remember:

* `border`
* `background`

When setting the border you must set a border size, color, and style: for example `border: 2px #a5a5a5 solid;`.
To set the background all you will need to do is set a color: `background: red;` or image: `background: url('http://placecage.com/g/360/360');`.

Now that you have a background and border, you will see that `margin` will add room outside of the border and background.
And, `padding` adds room in between your element content and the border.

# Oddities and `box-sizing`

When working with `padding`, `width`, and `border`: you may notice something odd.
You would think that the `width` property should set maximum width including your content AND any background or border you would want around it.
But this is not the default behavior of the browser.
Instead, the padding and `border` are added AROUND the `width` and `height`.
This may not seem like an issue right now, but things get really hard when you try to set things to fit in existing elements.

We can fix this by setting `box-sizing: border-box;`.
If you want to read more: check out the [original article](http://www.paulirish.com/2012/box-sizing-border-box-ftw/) by Paul Irish.
Now your element `width` and `height` properties will set the full `width` and `height` including `padding` and `border`.

# Moving Items Around

Now that you have your element sized properly, you will want to move the element around the page.

## Using Margins

To start we can use `margin` to push elements around the page.
These values can also include negative values.
While this may look like we are moving the element around the page, all we are doing is adding some room around our element.

## `position: relative;`

By default, elements have a property called `position` set to `static`.
This means that the position will only be set by the `margin`, `padding`, and `display`.

If we want to slightly tweak the existing positioning, we can set `position: relative;`.
Then the `top`, `bottom`, `left`, and `right` properties will push our element around based on where it was by default.

## `position: fixed;`

Sometimes, we want to have an element always be in the same place on the page.
For this we can set `position: fixed;`.
Then the `top`, `bottom`, `left`, and `right` will position the element based on the position to the window.
For instance `top: 0` will pin that element to the top of the window.
This will also place the element on top of the rest of the items on the page.

## `position: absolute;`

The final `position` value that we cover is `absolute`.
At first glance, this will not look too much different than `position: fixed`.
However, then you might notice that this element will be effected by scoll while `position: fixed` isn't.

But, elements with `position: absolute` look for the first parent element that isn't set to `position: static` and then will position itself based on the parent edges.

> **NOTE** Elements that use `position: absolute` will no longer be seen when other elements are trying to decide where to render.
> This includes when a parent element is trying to decide what size to be.
