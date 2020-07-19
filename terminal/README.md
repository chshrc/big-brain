# Terminal
Terminal interface is the whole app interface, a CLI is just one command at a time.
The dash `-`takes you to the last directory.

```bash
cd /etc
pwd
#/etc
cd /home
pwd
#/home
cd -
pwd
#/etc
```

Those two Ctrl combinations are your friend in the terminal:
Ctrl + C sends a signal to the current command running in the CLI to kill the process executing it.
Ctrl + D sends an EOF. It can be used to sometimes exit a CLI. E.g. on the Node.js CLI.

## Operating Systems
Mac is not suited very well to learn the terminal, as it does not have a linux bash installed. Mac OS itself is a BSD-based operating system (Darwin) and therefore has it differences from a linux terminal.

## Important tips / bash
Do NOT use Ctrl + L to clear the screen, use the `clear` command! The shortcut is not available on all systems, only on those w/ emacs mapping.

Remember to use tab/double tab completion!

> !! NEVER executed any code on your command line unless you understand what every command does !!
> !! ALWAYS assume everyone wants to harm you. !!

Do *not* use Ctrl + S to stop a running command in the terminal. It tells the terminal to suspend itself.

In general do not use spaces in filenames on any system unless you have a really good reason to.

It is much safer to first create a file with `touch` and then edit it afterwards. Consider creating a file in a directory you cannot save to. Then you edited the file in vain.

Use the `type` command in bash to see if a command is an alias. You can
use the backspace `\` in front of a command like `\top` to run the
untampered command instead of the alias.

## Terminal multiplexer

`tmux` is the successor to `screen`, the oldest method to combine
multiple windows.
`tmux` adds the concept of panes in addition to windows to multiplexers. 
It is useful to use screen-centric tmux configuration to use the
muscle-memory to also apply to systems, where only screen is installed.
E.g. binding Ctrl + A instead of Ctrl + B

You have to install the `tmux` package yourself on your system. 



## Vi(m)

### About
Vi stands for 'visual' and is the visual editor on top of the editor 'X', which can be considered the predecessor of vi.
The commands executed in the command mode in vi are taken from the 'X' editor.

### Commands
`ZZ` and `:x` are useful shortcuts for `:wq` in command mode.
To exit the insert/replace mode, use Ctrl + C instead of escape.

Use `u` to undo an action and `U` to undo actions made in a whole line. Use `Ctrl`+`R` to undo the changes undone by `u`. 



