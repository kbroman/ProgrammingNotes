## Knitr notes

- better R script (#' for text and #+ for chunk options) -> html

      Rscript -e 'library(knitr);spin("file.R")'

- Extract R code

      purl("file.Rmd")

- chunk options can use R code as arguments

      ```{r, echo = bar < 5} # chunk option shown only if bar < 5

- Maybe need to convert Rmd file to utf-8 before using
  library(markdown)?

      iconv -f iso-8859-1 -t utf-8 originalfile > newfile

  or

      iconv -f ascii -t utf-8 originalfile > newfile


- echo can take a vector of integers to selectively show code:

      ```{r hide-par, echo=3:4}
      ## 'ugly' code that I do not want to show
      par(mar = c(4, 4, 0.1, 0.1), cex.lab = 0.95, cex.axis = 0.9,
          mgp = c(2, 0.7, 0), tcl = -0.3)
      plot(mtcars[, 1:2])
      plot(mtcars[, 4:5])
      ```
