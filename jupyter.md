## Jupyter notebooks


- Installed by installing [anaconda](https://anaconda.com/downloads)

- Open/create new notebook by typing

  ```
  jupyter notebook
  ```

- To allow use of julia in jupyter notebooks, run `julia` and type:

  ```
  using Pkg
  Pkg.add("IJulia")
  ```

- To allow use of R in jupyter notebooks, run R and do:

  ```r
  install.packages("IRkernel")
  IRkernel::installspec()  # for all users
  ```

- For htmlwidgets (e.g., with
  [R/qtlcharts](https://kbroman.org/qtlcharts), use
  `htmlwidgets::saveWidget()` to save to a file and then
  `IRdisplay::display_html()` to display the result within the
  notebook.

  ```r
  library(qtlcharts)
  library(htmlwidgets)
  library(IRdisplay)

  x <- rnorm(100); y <- x*3 + rnorm(100)
  plt <- iplot(x,y, chartOpts=list(width=700, height=500, pointsize=5))
  saveWidget(plt, "demo.html", selfcontained=FALSE)
  display_html('<iframe srd="demo.html" width=800 height=600></iframe>')
  ```
