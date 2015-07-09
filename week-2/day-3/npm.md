# NPM

NPM (Node Package Manager) allows us to manage command line javascript dependencies.
These packages and modules can be used to create everything from small command line applications, to build tools, or even full servers for HUGE web applications.
Really the sky is the limit for what you can do with Node, but for now: we'll be using it for our build and development tools.

# Global Installing Packages

With NPM you can either install packages locally or globally.
Local packages will only work for a single project, while global packages usually give us command line operations that can be run system wide.

For instance we installed [Bower](../day-1/bower.html) as a global package so that we could then use the `bower` command in multiple projects without having to first run `npm install bower` every time we needed to pull in some dependency.
Similarly, many build tools will have at least some piece that could be globally installed.
To install an npm package globally, you can run:

    npm install -g <package_name>

This will install the package in `/usr/local/lib/node_modules`, and if the package has command line commands, these will be added to `/usr/local/bin` so that they can now be run.

# Project Initialization and `package.json`

While some commands like `bower` can run on just the globally installed package, most other projects using node.js will need to have specific dependencies.
This allows your project this week to have a dependency that is on version 1.0 while next week you could use the same dependency but use version 2.0.
At the same time, when you are working with a team, you need a way to grab the right dependencies easily (and hopefully without having to commit a ton of files in the process).

NPM allows us to do this by listing our dependencies in a `package.json` file.
First we need to set up a `package.json` file.
Luckily, we can set this up with a single command:

    npm init

This command will launch a few questions that will fill-out and create a `package.json` file.

# Installing Dependencies

After initializing our `package.json` file, it doesn't start with any listed dependencies.
So, we need to fix this!

We can install packages and add them to our `package.json` file by running:

    npm install --save <package_name>

For many of your projects, you'll likely want to install multiple packages at once:

    npm install --save <package_name_1> <package_name_2>

# Versions

When you install a package with NPM, it will automatically grab the latest version of the specified package.
But sometimes this isn't what you want.

While you can install specific versions from the command line: it is more likely that you realize that you grabbed the wrong version AFTER you've already pulled things in.
So in this case, the best way to change versions is to go to your `package.json` file, change the version number for a library, and then you have to make NPM look up this new version:

    npm update

When you run update, NPM will not only find the new version that you changed, but it will also look for the best version for every dependency in your `package.json` file.

# Installing NPM Packages For Existing Projects

Many times, you will get an existing project or folder structure with a `package.json` file already in it.
This could be when you're working with a team, starting files for an assignment, or files provided by a scaffolding software.
Luckily, installing all the listed dependencies for a project is as easy as running:

    npm install

When no package names are passed to this command, NPM looks in `package.json` and installs the right versions for all of your packages!

> **NOTE** If you already have one version of a package installed, `npm install` won't try to install a newer version. Only packages that are not installed at all in the current project will be looked up.
