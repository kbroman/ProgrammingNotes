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
