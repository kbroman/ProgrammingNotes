## Command-line pdf stuff

- `poppler-utils` package:

   ```shell
   apt install poppler-utils
   ```

- `pdfunite` to combine PDFs into one file

  ```shell
  pdfunite file1.pdf file2.pdf file3.pdf output.pdf
  ```

- `pdfseparate` to pull out a range of pages, with one file per page

  ```shell
  pdfseparate -f 2 -l 10 input.pdf output%d.pdf
  ```

  Alternatively, `pdftk` to pull out selected set of pages (for
  example to delete a page):

  ```shell
  pdftk input.pdf cat 1-2 4-end output output.pdf
  ```

- Use `gs` to reduce file size

  ```shell
  gs -dNOPAUSE -dBATCH -sDEVICE=pdfwrite -dCompatibilityLevel=1.4 \
  -dPDFSETTINGS=/printer -sOutputFile=output.pdf input.pdf
  ```

  For `PDFSETTINGS` you can use `/screen`, `/ebook`, `/printer`, or
  `/prepress`.

- To install pdftk with Ubuntu 18.04 (Bionic), needed to
  [do the following](https://askubuntu.com/a/1028983):

  ```shell
  sudo add-apt-repository ppa:malteworld/ppa
  sudo apt install pdftk
  ```

- Rotate pdf 90 degrees counter-clockwise with pdftk:

  ```shell
  pdftk input.pdf cat 1west output output.pdf
  ```
