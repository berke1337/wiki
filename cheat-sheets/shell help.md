# Useful command line help

### screen - creates virtual "screens" in the command line

Screen is a useful "window manager" of sorts within the terminal. Always works
in full screen, unlike tmux (see section below). Supports multiple windows that
can be switched between. Each screen can have multiple windows, and each window
can have a program running in it independent from other windows or screens.

All commands aimed at controlling screen while in a screen must be prefixed with
a key combination. By default this combination is "Ctrl-a". Other commands not
related to screen can be run as normal. Here is a list of common screen
commands to run from inside screen:

| Key | Action                                                  |
|-----|---------------------------------------------------------|
| c   | create new screen window                                |
| n   | switch to next window                                   |
| p   | switch to prev window                                   |
| d   | detach from screen (it stays running in the background) |

Some screen commands are run from outside a screen session, for instance to
connect or list currently running screen sessions. They can also be run from
inside screen as regular commands, which can be useful to tell, for instance,
which screen you are connected to.

```bash
# List all screen sessions that can be connected to
screen -list

# Reconnect to a screen listed above. If no argument is given after -r and only
# one screen session is running, it will reconnect to that one. Otherwise, it
# lists available screens to connect to. Tab completion works to choose one!
screen -r <screen_name>

# Attempt to reconnect to an existing session, or if none exist, start a new one
screen -R
```

### tmux - pretty much like screen, but newer and supports panes

Tmux is very similar to screen, but is newer, and doesn't have to be in full
screen all the time. This is nice, because you can then see two (or more)
different terminal prompts side-by-side and interact with them all. To start
tmux, simply run `tmux`, and to reconnect to a detached session, run
`tmux attach`. When all sessions in tmux are exited from, tmux itself will exit.
Tmux runs a server that others can connect to through sockets in /tmp, so
multiple users can connect to one tmux session at once. One disadvantage of not
working in full screen is that scrolling does not work. To scroll, use a
separate command found in the table below. All commands below require a prefix,
like screen. By default tmux uses a prefix of "Ctrl-b", but you can change it
in ~/.tmux.conf

| Key            | Action                                                  |
|----------------|---------------------------------------------------------|
| c              | create new tmux window, shown in the tabs at the bottom |
| any number key | switches to the window with the specified number        |
| any arrow key  | switches to the pane in the direction of the arrow key  |
| hold arrow key | resizes the current pane in the direction of the arrow  |
| ,              | rename the tmux window                                  |
| %              | create a vertical split (new pane)                      |
| "              | create a horizontal split (new pane)                    |
| n              | switch to next window                                   |
| p              | switch to prev window                                   |
| d              | detach from screen (it stays running in the background) |
| [              | start scrolling, press q to exit. Line # is at the top  |


### SCP - Secure Copy over SSH

Remote Host -> Local host:
`scp your_username@remotehost.edu:remotefile.txt /local/dir`

Localhost -> remotehost
`scp localfile.txt your_username@remotehost.edu:/remote/dir`

### Navigating in bash
http://ss64.com/bash/syntax-keyboard.html

### Vim

A more extensive list to print out is at
http://tnerual.eriogerg.free.fr/vimqrc.pdf

| Key                    | Action                                  |
|------------------------|-----------------------------------------|
| x                      | delete char                             |
| i                      | insert text                             |
| A                      | append at end of line                   |
| dw                     | delete word                             |
| d$                     | delete until eol                        |
| dd                     | delete whole line                       |
| rx                     | replace char with x                     |
| cM                     | change. delete and go to insertion.     |
| R                      | replace mode                            |
| __motions__                                                      |
| w                      | start of next word excluding first char |
| e                      | start of next word including first char |
| $                      | to eol                                  |
| 0                      | start of line                           |
| __history & copying__                                            |
| u                      | undo                                    |
| p                      | put prev deleted content                |
| y                      | yank                                    |
| __view__                                                         |
| G                      | bottom of file                          |
| gg                     | top of file                             |
| nG                     | go to line n                            |
| /                      | search                                  |
| n                      | next                                    |
| N                      | previous                                |
| ?                      | search back                             |
| __external cmd__                                                 |
| :!cmd                  | execute cmd                             |
