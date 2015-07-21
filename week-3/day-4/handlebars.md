# Handlebars

When working with Javascript, a common use case is to take data from Javascript (wether in memory or from a remote server or API) and turn it into HTML on the page.

Assume we want to put a student's name in an `h2` with a `span` around the `lastName` and then have a `p` with the student's age
Doing this with pure Javascript strings can be a real pain.

    var student = {
        firstName: 'Homer',
        lastName: 'Simpson',
        age: 36
    };

    var output = "<h2>" student.firstName + "<span>" + student.lastName + "</span></h2><p>" + student.age + "</p>";

This is bad for just a small bit of HTML, imagine a large app.

This pain is where a templating language can help us out!

## Handlebars Templating Languages

The Handlebars templating language is a small library that allows us to define and create templates so that we can quickly and easily output HTML from our Javascript without having to deal with huge strings and a bunch of `"HTML" + varName + "MOAR HTML"` in our Javascript files.

At the most basic form, Handlebars will allow you to write HTML and then where you want a property from your object, you will just surround that property name with `{{` and `}}`.

What does this look like?
The above example could be changed to a Handlebars string that looks like this:

    var templateString = "<h2>{{firstName}} <span>{{lastName}}</span></h2><p>{{age}}</p>";

So we are able to get rid of the `+` mess.
But Handlebars isn't complete magic.
We will need to turn our `templateString` into something that will output HTML.

This is where the `Handlebars.compile` function comes in: it accepts our template string (with curly braces and all) and then outputs a function that will turn our data into HTML.

    var template = Handlebars.compile(templateString);

Now we can create the same output as before by passing `student` to the new `template` function.

    var output = template(student);

## Get that HTML out of my Javascript!!!

Does this HTML in your Javascript look ugly?
No?
Well... I THINK SO!

Luckily, we can write our Handlebars templates in our HTML file so that HTML (or HTML like things) can stay out of our Javascript!

In HTML5, a new element called `template` was introduced which allows us to write HTML or other bits of templating without them being automatically rendered to the browser.
So now we can move our `templateString` from our JS to our HTML:

    <template id="student-info">
        <h2>{{firstName}} <span>{{lastName}}</span></h2>
        <p>{{age}}</p>
    </template>

This allows us to add whitespace, and formatting to make our template more readable.
But now we need a way to get our templateString back into our JS file.
Luckily, this can easily be done using a mix of `document.querySelector` and `HTMLElement.innerHTML`!

    var templateString = document.querySelector('#student-info').innerHTML;

Now the rest of our JS can remain as before and all together things look a bit like this:

    var student = {
        firstName: 'Homer',
        lastName: 'Simpson',
        age: 36
    };

    var templateString = document.querySelector('#student-info').innerHTML;
    var template = Handlebars.compile(templateString);
    var output = template(student);

Now our `output` variable will be the following string:

    <h2>Homer <span>Simpson</span></h2>
    <p>36</p>

> **NOTE** This only sets `output` to a string, it does not add this HTML to the DOM.
> You will have to set some `innerHTML` to the `output` string to add it to the DOM and make this available to the user.
> For instance if you had a `contentEl` element representing a `<div class="content></div>` then you could set `contentEl.innerHTML = output`.
> And now your DOM would show:

    <div class="content">
        <h2>Homer <span>Simpson</span></h2>
        <p>36</p>
    </div>

> **NOTE** In many other Handlebars examples, you may see something like `<script type="text/x-handlebars-template" id="student-info">` rather than using the `template` tag.
> While both work, `template` is a more up to date and acceptable way to declare templates without rendering things to your browser.
> By setting the `type` for a `script` tag to something other than `text/javascript`, the contents won't be rendered or interpreted by JS, but IMO this is rather fragile and templates aren't scripts since they don't actually DO something.


## Advanced Handlebars Action

"That's pretty sweet" you might be thinking to yourself.
But just like Billy Mays always said: "BUT WAIT THERE'S MORE!!!"

Handlebars is more than just pulling in basic properties from an object: there's a ton more that you can do!!!

### `this` in Handlebars

When working with Handlebars, the `this` variable is set to whatever you pass to your template.
But for ease of use, you can just leave off `this.` in your templates instead of writing something like this:

    <h2>{{this.firstName}} <span>{{this.lastName}}</span></h2>
    <p>{{this.age}}</p>

### Nested Properties

Let's say that our `student` object has changed and now `firstName` and `lastName` are now part of a `profile` object:

    var student = {
        profile: {
            firstName: 'Homer',
            lastName: 'Simpson'
        },
        age: 36
    };

With handlebars, we can grab properties in "nested" objects just like we would in Javascript by using "dot" notation:

    <h2>{{firstName}} <span>{{lastName}}</span></h2>
    <p>{{age}}</p>

### Loops and `{{#each}}{{/each}}`

Quite often when working with Handlebars and templates, you may want to go through a large array of different data objects.
To make this easier, Handlebars allows you to loop part of your template over an array with an block helper.
To start out a loop you will have `{{#each <varName> as |item|}}`.
This means that anything between `{{#each}}` and `{{/each}}` would be output for each item in an array.
And whatever you specify in the `as` area of the `each` will be the item you are currently looping through.

Let's say that our student from before had an array of grades:

    var student = {
        profile: {
            firstName: 'Homer',
            lastName: 'Simpson'
        },
        age: 36,
        grades: [
            {
                assignment: 'Week 1',
                points: 0.5
            },
            {
                assignment: 'Week 2',
                points: 0.75
            }
        ]
    };

Now we can make a list of our student's grades using the `each` helper:

    <h2>{{firstName}} <span>{{lastName}}</span></h2>
    <p>{{age}}</p>
    <ul class="grades">
        {{#each grades as |grade|}}
            <li>{{assignment}} - {{points}}</li>
        {{/each}}
    </ul>

Given our student above as the set context, this template will output:

    <h2>Homer <span>Simpson</span></h2>
    <p>36</p>
    <ul class="grades">
            <li>Week 1 - 0.5</li>
            <li>Week 2 - 0.75</li>
    </ul>

