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
