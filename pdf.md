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
  [do the following](https://askubuntu.com/a/1046476):

  ```
#!/bin/bash
#
# author: abu
# date:   July 3 2019 (ver. 1.1)
# description: bash script to install pdftk on Ubuntu 18.04 for amd64 machines
##############################################################################
#
# change to /tmp directory
cd /tmp
# download packages
wget http://launchpadlibrarian.net/340410966/libgcj17_6.4.0-8ubuntu1_amd64.deb \
 http://launchpadlibrarian.net/337429932/libgcj-common_6.4-3ubuntu1_all.deb \
 https://launchpad.net/ubuntu/+source/pdftk/2.02-4build1/+build/10581759/+files/pdftk_2.02-4build1_amd64.deb \
 https://launchpad.net/ubuntu/+source/pdftk/2.02-4build1/+build/10581759/+files/pdftk-dbg_2.02-4build1_amd64.deb


echo -e "Packages for pdftk downloaded\n\n"
# install packages 
echo -e "\n\n Installing pdftk: \n\n"
sudo apt-get install ./libgcj17_6.4.0-8ubuntu1_amd64.deb \
    ./libgcj-common_6.4-3ubuntu1_all.deb \
    ./pdftk_2.02-4build1_amd64.deb \
    ./pdftk-dbg_2.02-4build1_amd64.deb
echo -e "\n\n pdftk installed\n"
echo -e "   try it in shell with: > pdftk \n"
# delete deb files in /tmp directory
rm ./libgcj17_6.4.0-8ubuntu1_amd64.deb
rm ./libgcj-common_6.4-3ubuntu1_all.deb
rm ./pdftk_2.02-4build1_amd64.deb
rm ./pdftk-dbg_2.02-4build1_amd64.deb
  ```
To run this script, copy it in an editor and save it e.g. pdftk_installer. Then run it in a terminal with

```shell
chmod 755 pdftk_installer
./pdftk_installer
```
- Rotate pdf 90 degrees counter-clockwise with pdftk:

  ```shell
  pdftk input.pdf cat 1west output output.pdf
  ```
