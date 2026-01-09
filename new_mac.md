## New Mac

- got a new M4 Mac Mini and need to do a bunch of things since I'm moving from

- had to remove /usr/local/bin/git

- had to reinstall R and basically all R packages; it wasn't clear how to do this automatically so I used

  ```r
  pkgs <- list.files("~/Rlibs")
  for(pkg in pkgs) install.packages(pkg)
  ```

- install gfortran; see <https://mac.r-project.org/tools/>

- new links for pandoc and quarto

  ```
  sudo ln -s /Applications/RStudio.app/Contents/Resources/app/quarto/bin/tools/aarch64/pandoc /usr/local/bin
  sudo ln -s /Applications/RStudio.app/Contents/Resources/app/quarto/bin/quarto /usr/local/bin
  ```


