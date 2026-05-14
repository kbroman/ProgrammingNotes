## tmux

 ### change prefix

The default prefix for tmux is `C-b` but that conflicts with emacs so
you'd have to press C-b twice every time you want to move back a character.
So I changed it to `C-\` though I'm still getting used to typing it.

```
unbind-key C-b
set -g prefix C-\\
```

### creating/navigating panes

- `C-\ %` - split panes
- `C-\ "` - split panes vertically
- `C-\ <arrow key>` - change to other pain
- `C-\ c` - new window
- `C-\ p/n` - previous or next window
- `C-\ o` - next pane
- `C-\ t` - show time (press any key to exit)
- `C-\ [0-9]` - select window by number
- `C-\ &` - close current window
- `C-\ <space>` - toggle among pane layouts
- `C-\ x` - kill pane

### session handling

- `tmux ls` - list sessions
- `tmux a -t 0` - attach to 0th session
- `tmux new -s minecraft` - create new session named "`minecraft`"
  (`-s` for target session)
- `tmux rename-session -t 0 minecraft - rename session as "`minecraft`"
- `tmux a -t minecraft` - attach to session named "`minecraft`"
  (`-t` for target client)
- `tmux new -s session_name -d` - create new session but don't attach
  to it
- `tmux kill-session -t session_name` - close session

### commands

- `C-\ :` - enter command mode
- `new -n console` - new window named `console`
- `new -n processes htop` - new window named `processes` and start `htop`

### remote sessions

- `ssh <remote host> -t tmux attach-session`
  (not sure I'd use this, though)

### choosing session, windows, and panes

- `C-\ s` and `C-\ w` enter "tree mode"

- `q` to exit tree mode


### running a command

To start minecraft server within tmux session:

```
cd /home/pi/minecraft
tmux new-session -d -s "minecraft" ./start.sh
```

To get it to start at boot, I created a script to run every minute
that checks if there's a tmux minecraft session and if not start one:

```
#!/bin/bash

if tmux has-session -t minecraft > /dev/null 2>&1; then
    :
else
    cd /home/pi/minecraft;tmux new-session -d -s "minecraft" ./start.sh
fi
```

Then used `crontab -e` to have it run once a minute:

```
*/1 * * * * /home/pi/minecraft/start_tmux.sh
```

### Highlight active pane

Put the following in `.tmux.conf`

```
# gray background for inactive pane
set -g window-style 'fg=colour244,bg=colour236'
set -g window-active-style 'fg=colour250,bg=colour234'
```
