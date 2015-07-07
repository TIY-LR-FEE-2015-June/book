# Bower - A Package Manager for the Browser

Bower allows us to declare third-party dependencies for our app (CSS and JS) without having to commit all of their code or stay up to date with the latest version.

# Installing Bower

To install Bower for the first time run:

    npm install -g bower

# Starting a New Project with Bower

Once you have Bower installed, you can now set up your project to use Bower to list your dependencies.
To add a new `bower.json` file to any project run:

    bower init

This will start a wizard which allows you to name and add descriptions to your project.
For most of these fields you can use the default since we will not be publishing anything to the Bower registry.

# Installing and Specifying Dependencies with Bower

Now you will want to bring in your first dependency for your project.
To do this run:

    bower install <dep name> -S

This will not only install the dependency in a new `bower_components` directory, but it will also add the new package in the `dependencies` list in your `bower.json` file.

# Installing Dependencies for Existing Projects

Let's say that you have a project with an existing `bower.json` file and some listed dependencies.
To install all of the listed dependencies for a project run:

    bower install

# Some Packages You Might Want to Check Out

* `css-reset` - Resets all default CSS Styles
* `fontawesome` - Allows you to use icons based on [Font Awesome](http://fortawesome.github.io/Font-Awesome/icons/)
