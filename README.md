# What is this?

Just a set of basic git hooks to prevent:

- Merges
- Commits to master (including cherry picking)
- Rebases to master from branches other than develop.

# Are you using it?

Yes, at my current job we have some git guidelines that can be confusing for some developers the first time they used them, or for people not familiar with git.

As we want to have a git log as clean as possible we have:

- Two permanent branches: master and develop.
- Feature branches. When complete, develop must be pulled, rebased to the feature branch for conflict analysis, and then the feature branch is rebased to develop.
- Commits from develop to be rebased to master for a release.

# How do I use the hooks?

Remember that local hooks are pushed along with your code.

This means that after a clone, your local repo will not have any kind of hooks.

Because of this, I created the setup-hooks script that must be executed for any new clone.

You can place it anywhere in your repository along with the .git-hooks folder, and when run will link the hooks from .git-hooks folder to \<repo\_root\>/.git/hooks enabling them.

For your convenience, you can download the code as a [Zip file](https://github.com/juliogonzalez/git-master-develop-hooks/archive/master.zip) to unzip it at your repo.

# Are there any limitations?

**First thing to keep in mind: These hooks are just a help to prevent common mistakes not a way to really enforce the guidelines.**

**This means that under some circumstances it will be still possible to merge, or to change master with commits from branches other than develop.**

So remember this:

- As said before, the local hooks are not pushed with the repo, so it is your developers' duty to install them using the setup-hooks script.
- More important: you can still force fast-forward merges (--ff) that will not be detected by the hooks (I could not find a way to detect them and so far it seems it is not possible).
- It is still possible to change the master branch from other branches at a remote by using git rebase --hard <remote>/<branch>
- There could be other ways to evade the restrictions.
