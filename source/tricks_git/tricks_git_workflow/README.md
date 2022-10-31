# Git workflow

When modifications to repo want to be made, the following steps must be made:
Create your personal repo as a fork, a copy of the original one (called upstream).
Within your personal repo, you shall work on a particular branch. Same fork (personal repo) can have many branches at the same time. 
You should keep your fork copy synchronized with the upstream version. To do so, use git rebase. Check further instructions:

https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/working-with-forks/syncing-a-fork

https://stackoverflow.com/questions/7244321/how-do-i-update-or-sync-a-forked-repository-on-github


/------
Branching in upstream repo: you will polute the main repo with commits, not very good looking in public big projects, but it can be a simple solution of small ones.

Let's start creating a branch with 

git branch test
git checkout test

edit this file, commit, and merge with main branch. Lets see how it goes...