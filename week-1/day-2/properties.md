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
