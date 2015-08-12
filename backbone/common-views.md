# Common View Patterns in Backbone.js

When writing Backbone views we often do a lot of the same thing.
Sticking to a common pattern is great because a lot of apps follow the same needs, then you can use the standard pattern and focus your time on what makes your app special: events, application states, and user interactions.

The following are a few of the really common patterns that we have in backbone.
In general, your views will have at a minimum: a template, a render function (turns data from the collection or model into HTML or child views), and an initialize function (sets up events to listen to from the collection or model that need to fire the `render` function).
This is a list of the common mixes of `render` and `initialize` functions that can be used for different data.

## Simple Item View

Item views represent a single model (this may or may not be in a collection).
When you initialize an item view you will need to in a model property:

    var ItemView = Backbone.View.extend({
        /**
         * This is just here as a reminder that we have a
         * model not a collection
         * @type {varies}
         */
        model: null,

        /**
         * Replace this with the template for your view
         * if you get an error `this.template is not a function`
         * you likely have a syntax error in your handlebars template
         * or you need to check your template name
         * @type {function}
         */
        template: AppTemplates.myTemplate,

        /**
         * Sets up our view to rerender whenever our model changes
         */
        initialize: function() {
            this.listenTo(this.model, 'change', this.render);
        },

        /**
         * Display data to the user using our template
         * @return {Backbone.View} the current view (allows for chaining)
         */
        render: function() {
            /**
             * Sets a variable html to the output of our template 
             * after getting the underlying data for this view
             */
            var html = this.template(this.getData());

            /**
             * Sets the contents of the DOM element that our View
             * instance is attached to with our template output
             */
            this.$el.html(html);

            /**
             * Allows chaining
             */
            return this;
        },

        /**
         * Gets the data from our model or returns an empty object
         * this stops the error: cannot read property toJSON of undefined
         * @return {object} data to send to the template function
         */
        getData: function() {
            var data = {};

            if (this.model) {
                data = this.model;

                if (this.model.toJSON) {
                    data = this.model.toJSON();
                }
            }

            return data;
        }
    });

### Marionette Equivalent - [`Marionette.ItemView`](http://marionettejs.com/docs/v2.4.2/marionette.itemview.html)

While the `getData` function here does help with some common errors, the `Marionette.ItemView` is much more robust at rendering and staying up to date with a single model or even a collection if you don't need child views.
Do note that if you send a collection to a `Marionette.ItemView`, then in your template you will have to do an each loop over an `items` property.

## Simple Collection View

While item views can be used to represent a collection, it is much more likely that you will want to use a collection view.
The big difference between Collection Views and Item Views is that a Collection view will ALWAYS represent a collection and it is broken down into smaller Item Views so that you can handle events at a per item level instead of having to muck up your templates with ways to reference your model id.

    var CollectionView = Backbone.View.extend({
        /**
         * This is just here as a reminder that we have a
         * collection not a model
         * @type {varies}
         */
        collection: null,

        /**
         * This is a reference to the ItemView constructor
         * that needs to be used to create each individual
         * child view for every model in our collection
         * change this to the ItemView you want to use
         * @type {Backbone.View (constructor)}
         */
        childView: ItemView,

        /**
         * Sets up our view to rerender whenever our collection changes
         */
        initialize: function() {
            this.listenTo(this.collection, 'sync add change', this.render);
            this.render();
        },

        /**
         * Display data to the user using our template
         * @return {Backbone.View} the current view (allows for chaining)
         */
        render: function() {
            /**
             * Set up an $el variable so we don't have to fight with
             * the this variable and context in our forEach callback
             * @type {jQuery Selector}
             */
            var $el = this.$el;

            /**
             * Set up a ChildView constructor using the `childView`
             * property on our current CollectionView
             * @type {Backbone.View (constructor)}
             */
            var ChildView = this.childView;

            /**
             * Loops over all of the models in our collection
             * allowing us to create child views
             */
            this.collection.forEach(function(model) {
                /**
                 * Creates a new child view for our current model
                 * that we are looping over 
                 * @type {ChildView}
                 */
                var childView = new ChildView({
                    model: model
                });

                /**
                 * Initially renders our child view and then puts the
                 * child view element into our collection view
                 */
                $el.append(childView.render().el);
            });

            /**
             * Allows chaining
             */
            return this;
        },
    });

### Marionette Equivalent - [`Marionette.CollectionView`](http://marionettejs.com/docs/v2.4.2/marionette.collectionview.html)

Currently as it stands, our implementation of CollectionView will rerender everything any time new items are added, when the collection syncs to the server, or when models change.
But this will lead to a lot of unnecessary renders and a lot of child views that are created and then never used (these are known as "Zombie Views").
This can also lead to some weird things with events firing even though you don't see something on screen.
`Marionette.CollectionView`s take care of this by only adding (or removing) the child views that are affected when the collection data is updated or changed.

Luckily, the `Marionette.CollectionView` uses a `childView` just like the pattern above.
But TRUST me, extending from `Marionette.CollectionView` will reduce ALOT of your code and make your app a lot more resilient.

## To `el` or Not to `el`?

While this isn't quite a View pattern, I wanted to discuss the difference between having an `el` as part of your view prototype or not.
Setting an `el` property when running `Backbone.View.extend` can be really awesome for quick testing, but it has some issues when working on a larger scale.
So you have three options: define the `el` in your constructor, define an `el` when you instantiate the view, or don't define an `el` and manually add the view to the DOM using something like `$('#target).append(view.el)`.

