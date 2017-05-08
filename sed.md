## sed

- Delete all blank lines

  ```
  sed '/^$/d' [file]
  ```

- Delete all lines up to the first blank line

  ```
  sed '1,/^$/d' [file]
  ```

- Change `http` to `https` throughout (`g` here is for multiple instances on a line)

  ```
  sed 's/http:\/\//https:\/\//g' [file]
  ```

- Things that don't work: `\d` and `+`.

- For `\d+`, use `[0-9][0-9]*`

- Delete everything _except_ between `\begin{tabular` and `\end{tabular`
  (Note: you don't want to escape `{` here; `\{` means something
  different. Also, `!` at the end negates the range selection. Also
  note that you don't need to escape the backslashes.)

  ```
  sed '/\begin{tab/,/\end{tab/!d' [file]
  ```

- This does the same thing. The `p` prints the selected lines and the
  `-n` prevents printing _every_ line.

  ```
  sed -n '\begin{tab/,/\end{tab/p' [file]
  ```

- For search/replace part, can use any character as delimiter:

  ```
  sed 's|/usr/bin|/usr/local/bin|g' [file]
  ```

- If you indicate bits in the search part with `\(` and `\)`, you can
  use them in the replace part with `\1`, `\2`, ...
