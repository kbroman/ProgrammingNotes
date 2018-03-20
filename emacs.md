## Emacs/ESS notes

### ESS

```
C-c C-j   Execute line
C-c C-r   Execute selected region
```

### Windows

```
C-x 4 b   Open region below
C-x 2     Split the selected window top/bottom
C-x 3     Split the selected window side/side
C-x 1     Close all but current window
C-x o     Switch to next window
C-x ^     Make selected window taller
C-x }     Make selected window wider
C-x {     Make selected window narrower
C-x +     Make all windows the same height (balance windows
```

---

### Customize font/face

`C-u C-x =`   (Information about face at a particular point)

- scroll down to "There are text properties here:"
- Select definition
- Select "customize this face"
- Select "Show all attributes"
- Make some changes
- Select "Apply" or "Apply and save"

---

```
C-x h  Select buffer
C-M-\  re-indent selected region
```

---

Insert unicode character:

```
C-x 8 <enter> [hex] <enter>
```

For accented characters, get help with

```
C-x 8 C-h
```

Or say

```
C-x 8 ' C-h
```

To type é, you'd do: `C-x 8 ' e`

To type ô, you'd do: `C-x 8 ^ o`


### Magit

Mode for git within emacs.

- `C-x g` to get into the mode
- Within the magit frame, press `s` to stage a particular file,
  press `S` to stage everything.
- Within the magit frame, press `cc` to commit; type commit message,
  then `C-c C-c` to finish it.
- Within the magit frame, press `Pp` to push to github.

---

### Melpa

I've been keeping track of code for major modes in `~/.emacs.d`. A lot
are available via [Melpa](https://melpa.org). The [haskell-mode
ReadMe](https://github.com/haskell/haskell-mode) has a clear
explanation of how to use it.

At the start add the following to `~/.emacs`

```lisp
(require 'package)
(custom-set-variables
 ;; custom-set-variables was added by Custom.
 ;; If you edit it by hand, you could mess it up, so be careful.
 ;; Your init file should contain only one such instance.
 ;; If there is more than one, they won't work right.
 '(package-archives
   (quote
    (("gnu" . "http://elpa.gnu.org/packages/")
     ("melpa-stable" . "http://stable.melpa.org/packages/")))))
(package-initialize)
```

Then within emacs, use the following to download package information:

```
M-x package-refresh-contents
```

Then to install haskell-mode, use:

```
M-x package-install<return>haskell-mode
```
