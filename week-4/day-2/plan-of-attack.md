# Plan of Attack - JS Data -> DOM

One common problem to solve when working on front-end applications is taking data from Javscript and putting it into the DOM so that the user can see and interact with it.

The following is just a dump of a few of the steps I go through to when trying to tackle this sort of problem.

> For this example, I am breaking down the steps that I followed to create our [Marvel Heroes List](https://github.com/TIY-LR-FEE-2015-June/exercise-4.2).
> The given task was to take an existing set of data from a `marvelData` variable and print out a list item for each hero in that dataset.

# Initialize the Project

Before we can do anything we need a new project to work with.
This means that we need to create a new folder, set up a new git repository, initialize our dependency managers (Bower and NPM), and setup our `.gitignore` and `.jscs` files.

# Setup Build Tools & Dependencies

After setting up a project, I can start to plan out my build tools.
This is where I decide what I need in terms of Broccoli plugins, and how I need to set up my `Brocfile.js`: these will probably need to be tweaked over time in our project, but I like to start with a fairly minimal set of tools to get the job done.

In this step, I'll also grab my front end dependencies with bower. For this example we only focused on the Javascript side of things so we only installed `handlebars`.

# Serve `index.html`

Now that I have my build and development tools set up, I can focus on making an `index.html` file show up in the browser.
Here, I'll create my `index.html` file, start `broccoli-lr serve`, and modify the `index.html` to pull in needed dependencies as well as any CSS or JS files that we'll be writing.

# Explore the Available Data

Since we have an `index.html` file, we can start to look at the data that we are going to be working with.
This may mean looking at an existing Javascript file, testing an API, or looking at documentation for some other data source.

My goal is to get a sample of the data available in the browser.
For the Etsy assignment this meant running `loadEtsy` and creating a `debugger` statement in the `onload` callback.
For other projects, if data is already available as a variable, then you can just open up the console.

From the console, we can type in the variable name that we want to inspect and drill down until we start to spot some data that looks like something we need to use for our problem.

> For the Marvel problem, I found an array of 25 items that was located at `marvelData.data.results`

# Create a Target Element in the DOM

Since we want to add dynamic data to the DOM, we need somewhere for this to go.
Usually this means creating something like an empty `div` element with a class name that indicates that we will be putting our final HTML from Javascript inside of this element.

    <ul class="heroes"></ul>

# Grab the Target Element from JS

Now we need a way to get our target element available in our Javascript file as a variable.
For this we used the `document.querySelector` function:

    var heroesEl = document.querySelector('.heroes');

Once I think I have the right element, I change the `innerHTML` just to make sure everything is hooked up right:

    heroesEl.innerHTML = 'Is this working?';

If this change isn't showing up in the browser I check my query string, variable spelling, HTML classes and such.

# Loop Through Data

The next step that I take is to loop through my data and try to make something show up from my data set.
Since we're looping through an array, I chose to use `forEach` to start, then I just appended the `name` property from each item to the `innerHTML` of our `heroesEl`.

    marvelData.data.results.forEach(function(character) {
        heroesEl.innerHTML += character.name;
    })

# Plan Out Template

Now we have our data, we're able to loop through it, and we have somewhere for all our new HTML to go.
So, we can start to look at making a Handlebars template so that I can do more than just print out a character's name.

To start we need a `template` element in our `index.html` file with an `id` or `class` so that we can grab it from Javascript.
Then we can fill in the HTML we want shown for each individual item from our data with Handlebars statements where we want our dynamic data:

    <template id="characters-template">
        <li>
            <span>{{ name }}</span>
            <img src="{{ thumbnail.path }}/standard_fantastic.{{ thumbnail.extension }}" alt="">
            <p>{{ description }}</p>
        </li>
    </template>

# Grab Template From Javascript

Now we need to have our template from our Javascript.
We'll start by grabbing our template element and then just storing its `innerHTML` to a variable for use later.

    var templateString = document.querySelector('#characters-template').innerHTML;

# Compile to a Handlebars Template Function

Since we have a template string, we can send this new variable to `Handlebars.compile` to create a function that will output all of our glorious HTML.


    marvelData.data.results.forEach(function(character) {
        var t = Handlebars.compile(templateString);

        heroesEl.innerHTML += character.name;
    });

# Use Template Functions

The last thing that we need to do is use our new template function and pass in our `character` as the template's context.
We'll go ahead and replace our old `character.name` and we should see our desired HTML.

    marvelData.data.results.forEach(function(character) {
        var t = Handlebars.compile(templateString);

        heroesEl.innerHTML += t(character);
    });

# Optimize

The first thing that I notice about our code is that we have declared our template function `t` within our `forEach` callback.
This means that we will run the fairly costly task of compiling a handlebars string into a function even though we are using the same `templateString` each time.
We can move this out of our `forEach` loop to gain some performance and save some memory.

    var t = Handlebars.compile(templateString);
    
    marvelData.data.results.forEach(function(character) {
        heroesEl.innerHTML += t(character);
    });

Next I'm noticing that we are pushing a TON of changes to the `innerHTML` of our `heroesEl` element.
While at first glance (and with a relatively small data set) this seems like it doesn't create a performance problem.
But, if we look at the page render using the Chrome Timeline, we can see that this small list has created over 1,400 DOM elements in memory.
What's happening is that even though its faster than the eye can see, Chrome is completely re-rendering the `.heroes` element 25 times.
So we can instead create a variable that stores all of the HTML we want to put in `heroesEl` and then AFTER our loop, we'll change `innerHTML` once:

    var t = Handlebars.compile(templateString);
    var result = '';
    
    marvelData.data.results.forEach(function(character) {
        result += t(character);
    });

    heroesEl.innerHTML = result;

Finally, this new `result` variable is confusing to follow.
Instead, we can use `array.prototype.reduce` to collect our compiled templates along the way and send the final result to `heroesEl.innerHTML`:

    heroesEl.innerHTML =  marvelData.data.results.reduce(function(previous, character) {
        return previous + t(character);
    }, '');

# Style and Update Template

Now that we have all of our Javascript done, all we have to do is update our CSS and Handlebars templates to match our needs.
