# Git tools

There are many git commands and options. For newcomers and people with terrible memory there are tools for simplifying the daily work with git. 

## Visualizing commits and branch structure

There are several options for checking the history of a repository. An already prepared tool for this is called `tig`. Alternatively, the command `git log` gives this information as well, but some arguments have to be used in order to get a nice output, for example
```
git log --graph --abbrev-commit --decorate --format=format:'%C(bold blue)%h%C(reset) - %C(bold cyan)%aD%C(reset) %C(bold green)(%ar)%C(reset)%C(bold yellow)%d%C(reset)%n''          %C(white)%s%C(reset) %C(dim white)- %an%C(reset)' --all
```

This can be called as an alias. The global configuration of git can be stored in a file `~/.gitconfig`.

```
[alias]
        lg1 = log --graph --abbrev-commit --decorate --format=format:'%C(bold blue)%h%C(reset) - %C(bold green)(%ar)%C(reset) %C(white)%s%C(reset) %C(dim white)- %an%C(reset)%C(bold yellow)%d%C(reset)' --all
        lg2 = log --graph --abbrev-commit --decorate --format=format:'%C(bold blue)%h%C(reset) - %C(bold cyan)%aD%C(reset) %C(bold green)(%ar)%C(reset)%C(bold yellow)%d%C(reset)%n''          %C(white)%s%C(reset) %C(dim white)- %an%C(reset)' --all
        lg = !"git lg2"
```

Shell alias can be an alternative to git alias configuration.

## Stage, commit, push

There are many so called git clients available for these actions. One that can be found in standard linux software repositories is called `git gui`. Check for others as well

Ancillary tools for git are tig, git gui. They are available in linux repos. The tig command shows the git logs, and a git alias can be used instead. As git client, git gui is one of many, check others as well!

## Templates of CI/CD

Check this (web)[https://repository.prace-ri.eu/git/help/ci/examples/index.md#cicd-templates]

## Git LFS

Check this (web)[https://docs.gitlab.com/ee/topics/git/lfs/]. Tldr: big files can be part of a repository without being tracked. This minimizes the size of the repo.

## Git clang format

Check HSF tutorials about Git. Check [git clang format](https://ortogonal.github.io/cpp/git-clang-format/)
