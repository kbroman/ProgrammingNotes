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

- Use `gs` to reduce file size

  ```shell
  gs -dNOPAUSE -dBATCH -sDEVICE=pdfwrite -dCompatibilityLevel=1.4 \
  -dPDFSETTINGS=/printer -sOutputFile=output.pdf input.pdf
  ```

  For `PDFSETTINGS` you can use `/screen`, `/ebook`, `/printer`, or
  `/prepress`.
