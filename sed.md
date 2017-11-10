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


### Examples

- Want to change `\bold{blah}` to `**blah**`:

  ```
  sed 's/\\bold{\([^}]*\)}/\*\*\1\*\*/g' [file]
  ```

- Change \code{blah} to ``blah``

  ```
  sed 's/\\code{\([^}]*\)}/`\1`/g' [file]
  ```


- Change `\code{\link[pkg]{func}}` to `[pkg::func()]`.

  ```
  sed 's/\\code{\\link\[\([^]]*\)\]{\([^}]*\)}}/[\1::\2()]/g' [file]
  ```

- Change `\code{\link{func}}` to `[func()]`.

  ```
  sed 's/\\code{\\link{\([^}]*\)}}/[\1()]/g' [file]
  ```

- Changing traditional Roxygen2 docs to markdown-based:

  ```
  sed 's/\\code{\\link\[\([^]]*\)\]{\([^}]*\)}}/[\1::\2()]/g' [file.R] > tmp1
  sed 's/\\code{\\link{\([^}]*\)}}/[\1()]/g' tmp1 > tmp2
  sed 's/\\code{\([^}]*\)}/`\1`/g' tmp2 > tmp3
  sed 's/\\item /\* /' tmp3 > tmp4
  sed 's/\\href{\([^}]*\)}{\([^}]*\)}/[\2](\1)/g' tmp4 > tmp5
  \mv tmp5 [file.R]
  \rm tmp1 tmp2 tmp3 tmp4
  ```
