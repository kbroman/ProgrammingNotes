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
  (Note: don't want to escape `{` here; `\{` means something
  different. Also, `!` at the end negates the range selection.)

  ```
  sed '/\\begin{tabular/,/\\end{tabular/!d' [file]
  ```
