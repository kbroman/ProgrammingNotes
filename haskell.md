## Haskell

- using [stack](https://docs.haskellstack.org/en/stable/README/) to compile/manage

- type `stack ghci` to get interactive session

- With emacs:

  - use [`haskell-mode`](https://github.com/haskell/haskell-mode);
    install with [melpa](https://melpa.org/) as explained in the
    ReadMe file for `haskell-mode`

  - use
    [`inf-haskell`](https://wiki.haskell.org/Emacs/Inferioar_Haskell_processes)
    for interactive session: put `(require 'inf-haskell)` in `.emacs`
    and then, with a `.hs` haskell file loaded in a buffer, use `C-c
    C-l` to get interactive session with that module automatically loaded.
