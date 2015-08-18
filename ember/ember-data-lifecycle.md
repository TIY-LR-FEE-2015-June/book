# Life Cycle of an Ember Data Model

When working with Ember Data, there are a few layers between the server and your final application logic that help work to abstract away the complexity of AJAX requests and data formatting.
Following these steps can be a bit of a hassle, so let's follow a few different interactions with Ember Data to see what happens along the way.

For this documentation, assume you'll be working with CRUD for Blog Post data represented by a `post` model.

> **NOTE** This documentation is meant to be used as an introduction to Ember Data and commonly overwritten properties in Serializers and Adapters. This guide is not meant to be a full trace of every private method used in Ember Data to accomplish async operations or data transformations. For that I would recommend reading the [Ember Data API](http://emberjs.com/api/data/classes/DS.RESTAdapter.html) and clicking on the links to related source code for each method, although this level of understanding is not necessary.

## Fetching a Collection of Data

From a route, you can fetch all of the records for a particular model from the server using `this.store.findAll`.
So your route might look a bit like this:

        import Ember from 'ember';

        export default Ember.Route.extend({
            model: function() {
                return this.store.findAll('post');
            },
        });

To start off with, Ember first looks to see if a `post` model exisits.
This means it will look in your `app/models` directory for a `post.js` file and see that what you export from that file using `export default` extends from `DS.Model`.
Your model might look like this:

    import DS from 'ember-data';

    export default DS.Model.extend({
        title: DS.attr('string'),
        author: DS.attr('string'),
        body: DS.attr('string'),
    });

Now that it is confirmed that a `post` model exists, Ember Data looks for what adapter it should use to figure out how to make a request to `findAll` of the `post` models.
To start, Ember Data looks for an adapter for `post` in `app/adapters/post.js`.
If it cannot find a specific adapter for `post`, then it falls back to using the `application` level adapter in `app/adapters/application.js`.
In this file you might have something like this:

    import DS from 'ember-data';

    export default DS.RESTAdapter.extend({
      namespace: 'collections',

      host: 'http://tiny-lr.herokuapp.com',
    });

This adapter is fairly thin on things that are declared here.
Since most of the desired functionality already resides in the `DS.RESTAdapter`, only a few properties need to be changed:

* `host`: Tells Ember Data what server domain or IP address it should connect to
* `namespace`: Any part of the URL that needs to be between the `host` and the name of the model when building URLs.

Now that a working adapter is found, Ember Data calls the `findAll` method on this adapter which builds the url `http://tiny-lr.herokuapp.com/collections/posts` and sends a GET request to find all of the posts available on the server.
For the Tiny LR server, this response might return the following data:

    [
        {
            _id: "55c7cf2f2204370300000010",
            title: "Bender is Great",
            body: "I videotape every customer that comes in here, so that I may blackmail them later. Who are those horrible orange men? I videotape every customer that comes in here, so that I may blackmail them later. Hey, guess what you're accessories to. Oh sure! Blame the wizards! You know the worst thing about being a slave? They make you work, but they don't pay you or let you go. What's with you kids? Every other day it's food, food, food. Alright, I'll get you some stupid food. Whoa a real live robot; or is that some kind of cheesy New Year's costume? Who are those horrible orange men? They're like sex, except I'm having them! Yes! In your face, Gandhi! You guys go on without me! I'm going to go&hellip; look for more stuff to steal!"
        },
        {
            _id: "55c7cf08220437030000000f",
            title: "Who Knows",
            body: "You guys go on without me! I'm going to go&hellip; look for more stuff to steal! Throw her in the brig. Well, thanks to the Internet, I'm now bored with sex. Is there a place on the web that panders to my lust for violence? Who are those horrible orange men? Oh dear! She's stuck in an infinite loop, and he's an idiot! Well, that's love for you. Oh, you're a dollar naughtier than most. I love you, buddy! Ooh, name it after me! Take me to your leader!",
            
        }
    ]

Once this comes back from the server, Ember Data needs a way to take this raw JSON data and populate the local Data Store with records.

This reformatting and translation of the raw data into something that can be used by Ember Data's Store, is the responsibility of a Serializer.
Just like looking for a specific adapter, Ember Data will look for a `post` serializer before falling back to the more generic `application` serializer.
Here in the serializer, you can define how to massage this data into the format Ember expects.
By convention, Ember is expecting the data to be formatting in the following way:

    {
        "posts": [
            {
                _id: "55c7cf2f2204370300000010",
                title: "Bender is Great",
                body: "I videotape every customer that comes in here, so that I may blackmail them later. Who are those horrible orange men? I videotape every customer that comes in here, so that I may blackmail them later. Hey, guess what you're accessories to. Oh sure! Blame the wizards! You know the worst thing about being a slave? They make you work, but they don't pay you or let you go. What's with you kids? Every other day it's food, food, food. Alright, I'll get you some stupid food. Whoa a real live robot; or is that some kind of cheesy New Year's costume? Who are those horrible orange men? They're like sex, except I'm having them! Yes! In your face, Gandhi! You guys go on without me! I'm going to go&hellip; look for more stuff to steal!"
            },
            {
                _id: "55c7cf08220437030000000f",
                title: "Who Knows",
                body: "You guys go on without me! I'm going to go&hellip; look for more stuff to steal! Throw her in the brig. Well, thanks to the Internet, I'm now bored with sex. Is there a place on the web that panders to my lust for violence? Who are those horrible orange men? Oh dear! She's stuck in an infinite loop, and he's an idiot! Well, that's love for you. Oh, you're a dollar naughtier than most. I love you, buddy! Ooh, name it after me! Take me to your leader!",
                
            }
        ]
    }

So you need a way to take the raw array and set it as a property `posts` within a regular Javascript object.
While going through the Serializer, the `findAll` (as well as `findQuery`) results get passed through an `extractArray` function which takes the data from the response and translates it into a format for Ember Data to use.
To modify the `application` serializer to work with Tiny LR, your serializer could start like this: 

    import DS from 'ember-data';

    export default DS.RESTSerializer.extend({
        extractArray: function(store, type, payload) {
            var data = {};
            /**
             * Ember expects a plural version of the model name
             * as a parameter in the final payload object
             * So, we'll set that up here.
             */
            data[`${type.modelName}s`] = payload;

            /**
             * Now that we've set up the data in the format Ember Data expected
             * We can use `this._super` to call the inherited version of   extractArray
             * But instead of sending the regular payload, we'll sneak in our
             * modified `data` variable
             */
            return this._super(store, type, data);
        },
    });

Within the main `RESTSerializer`'s `extractArray` function which is called using `this._super`, each object from the JSON response is built into an instance of the Post model and the final transformation takes place.

For each property in your declared model, Ember Data transforms that property using the data type passed in to `DS.attr`.
For instance, if the server sent back the value `1` (which is a number) for your title, but your model declared that all titles should be formatted as strings, then Ember Data turns `1` into `"1"`.
Other data transformations such as dates or custom transformations are a bit more complex than just simple type casting.

And now after all this work, the data is ready and control is passed back to the Ember Router and the model finally resolves (meaning that your template is rendered with the model data found).

## Fetching a Single Instance

For working with a single instance, Ember Data works in much the same way with a small changes in the way that the URL is built and when passing through the serializer, the `extractSingle` method is called instead of `extractArray`.
The following is your router code to look up a single record using `findById`:

    import Ember from 'ember';

    export default Ember.Route.extend({
        model: function() {
            return this.store.findById('post', '55c7cf08220437030000000f');
        },
    });

Before following the need to go look this up on the server, Ember Data checks to see if you have already pulled the record down from the server to save on HTTP requests.
For this example, let's assume that you have not pulled down the required record and an HTTP request is needed.

Ember looks up an adapter and finds the same application adapter as in the first example.
This adapter builds a url to find our record `http://tiny-lr.herokuapp.com/collections/posts/55c7cf08220437030000000f` and makes a GET request that returns the following:

    {
        _id: "55c7cf08220437030000000f",
        title: "Who Knows",
        body: "You guys go on without me! I'm going to go&hellip; look for more stuff to steal! Throw her in the brig. Well, thanks to the Internet, I'm now bored with sex. Is there a place on the web that panders to my lust for violence? Who are those horrible orange men? Oh dear! She's stuck in an infinite loop, and he's an idiot! Well, that's love for you. Oh, you're a dollar naughtier than most. I love you, buddy! Ooh, name it after me! Take me to your leader!",
        
    }

However, Ember is expecting:

    {
        "post": {
            _id: "55c7cf08220437030000000f",
            title: "Who Knows",
            body: "You guys go on without me! I'm going to go&hellip; look for more stuff to steal! Throw her in the brig. Well, thanks to the Internet, I'm now bored with sex. Is there a place on the web that panders to my lust for violence? Who are those horrible orange men? Oh dear! She's stuck in an infinite loop, and he's an idiot! Well, that's love for you. Oh, you're a dollar naughtier than most. I love you, buddy! Ooh, name it after me! Take me to your leader!",
            
        }
    }

After getting back data from the server, the serializer (`application`) is loaded up and the `extractSingle` function is called.
This can be overwritten to give the expected results:

    extractSingle: function(store, type, payload) {
        var data = {};
         /**
         * Ember expects a singular version of the model name
         * as a parameter in the final payload object
         * So, we'll set that up here.
         */
        data[type.modelName] = payload;

        /**
         * Now that we've set up the data in the format Ember Data expected
         * We can use `this._super` to call the inherited version of extractSingle
         * But instead of sending the regular payload, we'll sneak in our
         * modified `data` variable
         */
        return this._super(store, type, data);
    },

Finally, the data is passed through the attribute transformers defined in your model and the model instance is sent to the route and the template is rendered.
