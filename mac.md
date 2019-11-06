## Notes on Mac OS X

- to install command line tools:

  ```
  xcode-select --install
  ```

- to change dashboard background, replace these files:

  ```
  /System/Library/CoreServices/Dock.app/Contents/Resources/
  dbgrid.png
  dbgrid\@2x.png
  ```

- to copy to/from clipboard: pbcopy, pbpaste

  ```
  echo 'hello' | pbcopy
  pbpaste > hello.txt
  ```

- screen shot a region

  ```
  cmd-shift-4
  ```

  press spacebar to move the selected region around, to
  adjust; press `<esc>` to cancel
