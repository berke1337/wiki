# Useful command line help
### screen - creates virtual "screens" in the command line
	“Ctrl-a” “c” create new screen
	“Ctrl-a” “n” switch to next screen
	“Ctrl-a” “p” switch to prev screen
	“Ctrl-a” “d” detatch from screen
	screen -r resume screen

### SCP - Secure Copy over SSH
Remote Host -> Local host:
`scp your_username@remotehost.edu:remotefile.txt /local/dir`

Localhost -> remotehost
`scp localfile.txt your_username@remotehost.edu:/remote/dir`

### Vim
=======
A more extensive list to print out is at http://tnerual.eriogerg.free.fr/vimqrc.pdf!

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
