# The Missing Sails.js Getting Started Guide

Just like how the conventions and tooling of Backbone allows us to build more manageable front-end applications, the Sails.js can give us that structure and foundation for working with the server.
Sails.js heavily leans on the idea of convention over configuration: this means that it will do a lot of stuff with very little code.
This can be incredibly powerful (don't let it get to your head though).

## Getting Ready to Work with Sails.js

To run a Sails.js application you will need node.js (or equivalent JS runtime) installed on your system.
The only other requirement is to run `npm install -g sails` which should make the `sails` command available via your command line.

## Creating and Booting Your Sails.js App

To create a Sails.js project run:

    sails new app

This will create a new directory called `app` and have the default application structure for a sails app right away.
You can of course name this directory anything that you want by just changing `app` to your desired project name.

> **NOTE** The `sails new` command also pulls in all of the required `node_module` dependencies based on your globally installed version of Sails.
> You may want to run `npm update` in your new project to get updated dependencies and make sure to run `npm update -g sails` every few weeks to make sure you aren't behind.

## Running Your Sails.js Server

To start your Sails.js server you can run `sails lift` from your new project.
While this will start your server it does not reload when files change and you will need to manually reload your server every time you update a `.js` file.

Instead of running `sails lift`, you can start the server via the `app.js` file.
This means that you can start an automatically reloading server by running `nodemon app.js`.
If you are unfamiliar with `nodemon` it is a process manager that will restart a node process any time a `.js` file changes in the current directory and can generally be used to replace the `node` command and can be used in any Node.js project.

Now that the server is running, navigate to [http://localhost:1337](http://localhost:1337) and you should see the Sails.js welcome screen.

## Creating Your First Model

Now that you have a project, you can create a new model and API by running `sails generate api user`.
This will create two files:

* `api/models/User.js`
* `api/controllers/UserController.js`

You'll notice that both of these files are fairly empty besides a set of comments and a simple `module.exports` statement which exports an empty object (or an object with a `attributes` property of an empty object as in the case of the model).
It may not look like it, but because of the HEAVY conventions of Sails.js, this is all you need to have a full JSON data API (not to be confused with the [JSON API specification](http://jsonapi.org/))!

Before your can look at the API, you might notice that your terminal is barfing up a HUGE amount of warnings talking about needing to migrate.
Since we've created a new model, Sails needs to setup a place to store our data.
To do this, it needs to run an automatically created migration.
But for data safety, Sails will not run migrations without you telling it that it is ok.
For development, go to the file `config/models.js` and find the line that says `// migrate: 'alter'` and uncomment it.
This tells Sails that it should try to make safe changes to the database to accommodate your models.
Now when your server restarts, it should be good to go.

Now look at `http://localhost:1337/user` and you will see that the API is returning an empty array.

So using a tool like Postman or another REST client, make a POST request to `http://localhost:1337/user` with a `Content-Type` header set to `application/json` and then you send the body content as "Raw" with some JSON data: for example you can post:

    {
        "email": "one@test.com",
        "password": "pass"
    }

This should respond back with a set of JSON and should add `createdAt`, `updateAt`, and `id` parameters.
A quick `GET` request to `http://localhost:1337/user` will now show that the record has been saved!

# Modifying the Model Attributes & Model Schema

By default, Sails.js uses a schemaless data structure.
This means that you can pass in any attributes that you want and Sails will try to store it.
While this can be useful during demos and rapid prototyping, it is hard to maintain in a production environment where more structure is usually desired.

To create a model schema, you need to declare properties within the `attributes` object in your model.
At it's most basic form each attribute declaration will be an object with at least a `type` property.
So after adding attributes for `name` and `password` (both strings), your User model file will look a bit like this:

    module.exports = {
      attributes: {
        email: {type: 'string'},
        password: {type: 'string'},
      },
    };


However, while this will enforce type casting for the email and password fields, it will not actually change the way that Sails handles other attributes.
To test this, make a `POST` request to the user API with the following data:

     {
        "title": "My awesome post",
        "body": "Lorem ipsum dolor sit amet, consectetur adipisicing elit. Recusandae amet nesciunt nemo enim! Quaerat voluptates accusantium rem neque reprehenderit blanditiis, esse rerum earum fuga velit corrupti, consequuntur numquam unde eligendi."
    }

And you will see that the `title` and `body` were both saved.
The attributes on models by default only enforce the type listed.

To enforce that only listed attributes are stored and adhere to the listed schema, all that is needed is to change a configuration variable.
In `config/model.js` in the exported object add a line that says `schema: true`.
This will make all of the models in your current project enforce their schema and only store listed attributes.

## Required Attributes

While deep validations is out of the scope of this getting started guide, you will often want to make sure that a user sends SOME value to your API for different attributes (a bunch of empty records would be SUPER lame).
To make an attribute required just add a property of `required` and set it to `true`:

    module.exports = {
      attributes: {
        email: {
            type: 'string',
            required: true,
        },
        password: {
            type: 'string',
            required: true,
        },
      },
    };

Now if you don't set both the email and password attribute when creating a new instance of your user model via the API, then it will error out and a user will not be created.

## Behind the Magic

So you might be asking yourself: "why do we have a full API from little to no code?"
Behind all of Sails.js there are things called Blueprints.
Blueprints describe how the application should act if there is nothing overriding the default (or turning them off via configuration).

The first Blueprint that you are interacting with are the API action Blueprints which build out how default APIs behave with Sails.js.
If you do not create explicit routes to override them, the API action blueprints will be available if there is a model and matching controller.
Then from there, Sails automatically creates different controller methods for the following actions:

* `find` - Available via a `GET` request to the root of your resource `/users/` - This will show all of the records for a model, also can optionally paginate and do rough searches using query parameters.
* `findOne` - Available via a `POST` request with an id after the resource root `/users/:id` - Finds a single record for a model with a matching `id` from the URL.
* `create` - Available via a `POST` request to the root of your resource `/users/` - This will create a record using either form data or JSON input and return the created record with `id` and timestamps
* `update` - Available via a `PUT` request with an id after the resource root `/users/:id` - Updates the attributes for an existing record with a matching `id` from the URL.
* `destroy` - Available via a `DELETE` request with an id after the resource root `/users/:id` - Destroys a record with a matching `id` from the database.

If you want to override the default behavior of any of these actions, just create a function named with the action you want to override. For instance if you don't want to allow the API to delete users you could make your `UserController.js` look like:

    export.default = {
        destroy: function(req, res) {
            res.jsonx('uh uh uh you didn't say the magic word');
        }
    }

Now whenever you try to delete a user via the API, the user won't be deleted and you should see the response `uh uh uh you didn't say the magic word`.
