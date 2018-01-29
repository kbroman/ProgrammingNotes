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

`C-u C-x` =   Information about face at a particular point

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
