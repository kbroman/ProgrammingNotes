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

### session handling

- `tmux ls` - list sessions
- `tmux a -t 0` - attach to 0th session
- `tmux new -s minecraft` - create new session named "`minecraft`"
- `tmux rename-session -t 0 minecraft - rename session as "`minecraft`"
- `tmux a -t minecraft` - attach to session named "`minecraft`"

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
