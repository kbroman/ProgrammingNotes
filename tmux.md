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

### remote sessions

- `ssh <remote host> -t tmux attach-session`
