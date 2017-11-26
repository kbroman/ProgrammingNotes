## Unix less command


### Search

| | |
|-|-|
| `/`     | forward search for a pattern |
| `?`     | backward search for a pattern |
| `n`     | next match (forward or backward, depending) |
| `N`     | previous match |
| `&`     | display only lines matching pattern |
| `esc-u` | toggle highlighting |


### Navigation

| | |
|-|-|
| `^f` | forward one window |
| `^b` | backward one window |
| `^d` | forward half window |
| `^u` | backward half window |
| `^n` | forward one line |
| `^p` | backward one line |
| `G`  | end of file |
| `g`  | start of file |


### Marked naviation

| | |
|-|-|
| `ma` | mark current position with letter a |
| `'a` | go to marked position a |
| `''` | go to previous position |


### Multiple files

| | |
|-|-|
| `:n` | go to next file |
| `:p` | go to previous file |

### General

| | |
|-|-|
| `q` | exit |
| `h` | help |
| `=` | display info about current file |


### Command-line stuff (can also do this within less)

| | |
|-|-|
| `-N` | display line numbers |
