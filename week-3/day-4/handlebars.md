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
