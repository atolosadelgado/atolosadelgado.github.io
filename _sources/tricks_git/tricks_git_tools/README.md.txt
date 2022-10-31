## Git tools

Ancillary tools for git are tig, git gui. They are available in linux repos. The tig command shows the git logs, and a git alias can be used instead. As git client, git gui is one of many, check others as well!

Linux tools useful when dealing with git local repos:
For comparing directories use meld. 
For comparing files use kompare (GUI), diff (terminal)

Diff command can be used for patching, with the arguments -N -U. Output can be used directly by git am command. When you have modifications on an old copy of the repo, it is easier to download a fresh copy, diff the files of interest, and patch the new copy with git am command.

