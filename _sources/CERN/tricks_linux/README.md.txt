# Linux tricks

Table of tricks :)

* [Console file manager](#Console-file-manager)
* [Remove path from env var](#remove-path-from-env-var)
* [Comparing directories or files](#comparing-directories-or-files)
* [Workaround alias](#workaround-alias)
* [Find command with exec argument](#find-command-with-exec-argument)
* [Encapsulate sourcing of scripts](#encapsulate-sourcing-of-scripts)
* [Pomodoros and remind function](#pomodoros-and-remind-function)

General Cheat sheet

https://linuxcommandlibrary.com/

## Console file manager

Check this (link)[https://www.tecmint.com/linux-terminal-file-managers/]

## Remove path from env var

Check this (link)[https://stackoverflow.com/questions/11119203/how-to-remove-a-path-from-ld-library-path-in-tcsh]

```
LD_LIBRARY_PATH=$(echo $LD_LIBRARY_PATH | perl -pe "s[$DIR_TO_REMOVE][]g;")
export LD_LIBRARY_PATH
```

## Workaround alias

Including a backslash in the middle of the word of a command prevents bash to use the alias

```shell
$ alias 'python3=echo kk'
$ python3
kk
$ py\thon3
Python 3.6.8 (default, Jun 23 2022, 19:01:59)
[GCC 8.5.0 20210514 (Red Hat 8.5.0-13)] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>>
```

## Comparing directories or files,

Linux tools useful when dealing with git local repos:
* For comparing directories use meld command. 
* For comparing files use kompare (GUI), diff (terminal)

## Find command with exec argument

When initializing a local repository, we may need to add files with certain pattern. For that, we can use exec option of find command as this:

```shell
find . -name "*.cpp" -not -name "**.py*"  -exec git add {} \;
```

## Encapsulate sourcing of scripts

I used to put the source of different packages in `.bashrc`. This is a bad idea by several reasons
* You may have to switch between versions of software
* Sourcing scripts can generate output
* Environmental variables that may not be used should not be setup.

There are different ways to setup the sourcing of scripts

1. Using alias, 

```shell
alias root6='source /usr/local/root_6.26.06/bin/thisroot.sh'
```

2. Using functions,

```shell
function setup-local-root {
 source /usr/local/root_6.26.06/bin/thisroot.sh
 source /usr/local/lcio/setup.sh

 export QTDIR=/opt/Qt/5.15.2/gcc_64/
 export QTLIB=$QTDIR/lib
 export QTINC=$QTDIR/include
 export PATH=$QTDIR/bin:$PATH
 export TIMEMORYDIR=/usr/local/timemory
 export PATH=$TIMEMORYDIR/bin:$PATH

 export VecGeom_DIR=/usr/local/vecgeom/lib/Cmake/VecGeom
}
```
3. Creating a separate shell script which contains the body of the previous function for example.

4. In case of Python, use a virtual envirnonment
```shell
python3 -m venv venv
source venv/bin/activate
pip install -r ...
```


## Pomodoros and remind function

Example of linux custom notifications. The remind custom function, taken from [here](https://letsdebug.it/post/30-linux-desktop-notifications/), it is useful to remind you to get up the chair and walk around :)

You can put this piece of sh code in bash configuration file `.bashrc`, profile, or bin directory together with other scripts.

```shell
alias pomodoro25='remind "Time to \"exercise\"!" in 25 minutes'
function remind () {
  local COUNT="$#"
  local COMMAND="$1"
  local MESSAGE="$1"
  local OP="$2"
  shift 2
  local WHEN="$@"
  # Display help if no parameters or help command
  if [[ $COUNT -eq 0 || "$COMMAND" == "help" || "$COMMAND" == "--help" || "$COMMAND" == "-h" ]]; then
    echo "COMMAND"
    echo "    remind <message> <time>"
    echo "    remind <command>"
    echo
    echo "DESCRIPTION"
    echo "    Displays notification at specified time"
    echo
    echo "EXAMPLES"
    echo '    remind "Hi there" now'
    echo '    remind "Time to wake up" in 5 minutes'
    echo '    remind "Dinner" in 1 hour'
    echo '    remind "Take a break" at noon'
    echo '    remind "Are you ready?" at 13:00'
    echo '    remind list'
    echo '    remind clear'
    echo '    remind help'
    echo
    return
  fi
  # Check presence of AT command
  if ! which at >/dev/null; then
    echo "remind: AT utility is required but not installed on your system. Install it with your package manager of choice, for example 'sudo apt install at'."
    return
  fi
  # Run commands: list, clear
  if [[ $COUNT -eq 1 ]]; then
    if [[ "$COMMAND" == "list" ]]; then
      at -l
    elif [[ "$COMMAND" == "clear" ]]; then
      at -r $(atq | cut -f1)
    else
      echo "remind: unknown command $COMMAND. Type 'remind' without any parameters to see syntax."
    fi
    return
  fi
  # Determine time of notification
  if [[ "$OP" == "in" ]]; then
    local TIME="now + $WHEN"
  elif [[ "$OP" == "at" ]]; then
    local TIME="$WHEN"
  elif [[ "$OP" == "now" ]]; then
    local TIME="now"
  else
    echo "remind: invalid time operator $OP"
    return
  fi
  # Schedule the notification
  echo "notify-send '$MESSAGE' 'Reminder' -u critical" | at $TIME 2>/dev/null
  echo "Notification scheduled at $TIME"
}
```
