# Common Git Issues

## Unknown Upstream Error

When you are trying to push code to Github you may see a warning or error saying 

    fatal: The current branch develop has no upstream branch.
    To push the current branch and set the remote as upstream, use

    git push --set-upstream origin develop

What this is saying is that you have a local git branch that git does not know where to sync up to.
By adding `--set-upstream` we are tellin local git that whenever we are on the current branch and run `push` or `pull` we should connect to the following remote branch `origin develop` by default.
Once your run `-set-upstream` you will no longer have to specify the branch to push to for this current project and branch.

In comparison, if you want to send your code to a different remote you can specify this.
For instance we could send our current branch to the `heroku` remote and `develop` branch: `git push heroku develop`.
But, if we run `git push`, it will continue to send to our default not `heroku develop`.

## GH Page Deploy

Sometimes when running `gh-page-deploy` you may get an error that says that your local branch is behind from the remote branch.
This has to do with the way that we are sending things to github pages and the way that our build step destroys the file history from our `dist` directory everytime we run it.

To fix this issue, go to your repository on Github.
Then click on the "Branches" link at the top:

![Branches](branches.png)

From there you should see your `master`, `develop`, and `gh-pages` branches.
Click on the trash can next to your `gh-pages` branch and this will delete that branch on Github.

Now you can run `gh-page-deploy` and you should not have the error happen and your build will be sent to GH Pages!
