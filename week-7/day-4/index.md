#EMBER!!!!

# Creating a New Project

To create a new project with Ember run:

    ember new project-name

You will of course replace `project-name` with the name of your project.

This will create the basic folder structure for a new ember project and pull in dependencies with NPM and Bower AND it initializes an initial commit with Git.

If Bower or NPM install fails, is canceled or times out: move into your new project directory and run `npm install && bower install` to pull in your required dependencies.
If either shows up blank, attempt to run `ember serve`, if this errors run `rm -rf node_modules && npm install` to reload node dependencies.
Currently this means that you will also have to initialize a git project and make your first commit.
