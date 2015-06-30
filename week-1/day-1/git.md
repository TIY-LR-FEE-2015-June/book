# Git Review

## What is `git`?

Git is a tool that allows us to keep snapshots of our code and use these snapshots to share with team members.
On top of this, git allows us to peer back in time, go off to try new and exciting things, and maintain multiple versions of the same application.

## Why do we use `git`?

While there are other things like Dropbox and Time Machine that allow you to take snapshots and share, they don't really do things well and aren't really meant for small changes and only takes snapshots on a timer: and it's hard to jump between versions without throwing work away.
Git is much better suited for defining when and what files we want to take a snapshot of and it has a much broader uses when collaborating, working on features, maintaining project stability, and more.

> This whole book is actually written in git!

## Creating a new git project

So you have started on (or you're about to start on) your next cool idea and have decided to use git to track changes, backup, and share your code: now what?
To create a new git repository, from your project directory (be sure to check the file path in your shell prompt or with `pwd`) run `git init`.
This will create a new completely empty git project.

Right now git hasn't actually started tracking anything yet.
It's just ready and waiting for your next command.

## Different file statuses in `git`

Now that we have a completely empty project, we need to know what the status is of our project.
To get the pulse of what changes have been made since the last commit, run `git status`.
This will list all of the changes that git is aware and files and directories can fall into one of four different categories:

1. Untracked
2. Tracked with Modifications
3. Staged
4. Committed (tracked with no changes)

### Untracked Files

Untracked files are files that have been added since the last git commit and do not show up in the past git history.

### Tracked with Modifications

Files that show up as `modified` have been tracked by git in the past but have new changes that are not committed.

### Staged

Staged files are files that are ready and waiting to be committed.
These will show up in a section labeled "Changes to be Committed".


> **Note** Files that have been modified after staging will show up both under "Changes not staged for commit" and "Changes to be Committed". If you commit at this stage, only the modifications that existed before `git add` will be committed.

### Committed

Files that have not been changed since the previous commit will not show up under git status.
If no files have changed at all, you will get a message: "nothing to commit, working directory clean"

## Getting Files Ready to Committed

You have some files ready and you are ready to take your first snapshot.
Right now your files look like this:

```
/project/
|--index.html
|--main.css
|--footer.css
```

You know that your `index.html` and `main.css` files are at a good stopping point but you are still working on `footer.css`.
This is a good time to make a commit.

To move a file into staging we will run `git add`.
This command takes unlimited file names for anything that we want to get ready for commit.
Since you want `index.html` and `main.css` to be committed but not `footer.css` you would want to run `git add index.html main.css`.


Now if you run `git status` you should see that `index.html` and `main.css` are listed under "Changes to be Committed".

## Taking a snapshot!

Alright, our changes are set up and staged.
Now it is time to commit our changes!

To commit the staged files run `git commit`.
This will open up your configured editor (we set up git to use Sublime Text at our install party) and prompt you for a commit message.

When writing a commit message, try to keep things short and sweet.
Sublime text should draw a vertical line at around 80 characters: if your commit message is past this line, you probably have one of the following problems:

* You don't understand the code you are committing
* You are trying to commit multiple features

## Commit Often, Commit Small, Commit Early

Commit practices will differ slightly from company to company, but in general it is a good practice to commit often.
Some common times to commit:

* Getting to a stopping point
* Leaving the code for a day
* Finishing a files
* Fixing a single bug
* Finishing a single feature
