# Git workflow

The general repository shall be as clean as possible. To keep it in shape, master branch of the general repository (from now on, upstream repository), changes should be done from personal forks of that upstream repo and then ask the maintainers to merge your changes with the main repo. A brief summary of how to run it is given first, and the some other tips about issues that may happen during the general workflow.

## General workflow
When modifications to repo want to be made, the following steps must be made:
1. Create your personal repo as a fork, a copy of the original one (called upstream). This can be done using the web interface
2. Download a local copy of your fork using `git clone ...`
3. Within your personal repo cloned locally, you shall work on a particular branch. Same fork (personal repo) can have many branches at the same time. To create a new branch: 

```
git checkout -b my-new-branch
```
4. Edit or add files (`git add ...`), commit and push them to the dedicated branch that was created in the previous step. The git client `git gui` is one of the many tools to visualize and simplify this step.
5. Back in the web brower, go the working branch and ask for a pull / merge request to the upstream(main) branch. Add meaninful comments in the description for the reviewers.


## Keep your fork synchronized with upstream

You should keep your fork copy synchronized with the upstream version. To do so, we can simply use the web interface or use [commands in the terminal](https://stackoverflow.com/questions/7244321/how-do-i-update-or-sync-a-forked-repository-on-github "The following lines are taken from here"). 

1. Add the remote, call it "upstream":
```
git remote add upstream https://github.com/whoever/whatever.git
```

2. Fetch all the branches of that remote into remote-tracking branches
```
git fetch upstream
```
3. Make sure that you are on your master branch:
```
git checkout master
```
4. Rewrite your master branch so that any commits of yours that aren't already in upstream/master are replayed on top of that other branch:
```
git rebase upstream/master
```

Check [github documentation](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/working-with-forks/syncing-a-fork) for futher details.

## Patching

When rebasing to the upstream/master branch, we may find merge conflicts. If they are simple, we may solve them manually. Sometimes it is easier to make a patch, that is, save the differences between your personal version and the remote version in a *patch file*, and apply the changes later.

In order to generate the patch file, we use diff command. The `-N` argument is used to treat absent files as empty. The `-U` argument is used to produce such an output that can be understood by git later.

```
diff -N -U file.original file.changed > file.patch
```

To patch manually a the file `file`, the patch command is used as

```
patch < file.patch
```

Later, we can apply those changes to a fresh copy of the remote repository 

```
git am file.patch
```
And then commmit and push the changes to the remote branch.

## Dry run

Remember that exist a dry run option when pushing 

```
git push --dry-run remote origin
```