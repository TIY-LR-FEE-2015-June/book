# Common Router Patterns in Backbone.js

There are many differing opinions when it comes to how to use the Backbone Router.
However, in almost every other client-side framework, the URL is considered VITAL.
It should reflect the views that are on screen and the data that lies behind it.
So, using Backbone's Router as a centralized way to manage the data and views shown to the user is the best way to keep the app and URL in sync.

## The `initialize` function

While the router is used to switch between different views, there are usually some pieces of your application that will be around no matter what screen you are on (think menus, sidebars, etc).


These elements and the data under them can be set up using the `initialize` function.
Since the `initialize` function is run whenever we instantiate the router, these shared elements will be immediately set up.
So let's assume we have a sidebar of contacts:

    var AppRouter = Backbone.Router.extend({
        initialize: function() {
            /**
             * Let's assume that ContactList extends Backbone.Collection
             * This represents all of our Contact models
             * @type {ContactList}
             */
            this.contacts = new ContactList();

            /**
             * Instantiate the sidebar and send in the contact list
             * SidebarView can be either an ItemView or a CollectionView
             * @type {Sidebar}
             */
            this.sidebar = new Sidebar({collection: this.contacts});

            /**
             * Put the sidebar into the DOM inside of an element
             * with an id of `sidebar`
             */
            $('#sidebar').html(this.sidebar.el);
        },
    });

