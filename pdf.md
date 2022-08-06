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

- Rotate pdf 90 degrees counter-clockwise with pdftk (just the first page):

  ```shell
  pdftk input.pdf cat 1west output output.pdf
  ```

  Rotate all of the pages 180 degrees:

  ```shell
  pdftk input.pdf cat 1-endsouth output output.pdf
  ```

- crop pdf (left top right bottom, in points)
  positive values pad margins; negative values crop

  ```shell
  pdfcrop --margins 0 -150 0 0` input.pdf output.pdf
  ```


---

### Installing `pdftk`

To install pdftk with Ubuntu, needed to [do the
following](https://askubuntu.com/a/1028983):

```shell
sudo add-apt-repository ppa:malteworld/ppa
sudo apt install pdftk
```

If that doesn't work, [here's a page with some
alternatives](https://linuxhint.com/install_pdftk_ubuntu/).
Or use the [following bash script](https://askubuntu.com/a/1046476):

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
wget https://launchpadlibrarian.net/340410966/libgcj17_6.4.0-8ubuntu1_amd64.deb \
 https://launchpadlibrarian.net/337429932/libgcj-common_6.4-3ubuntu1_all.deb \
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

To run this script, copy it in an editor and save it as
`pdftk_installer`. Then run it in a terminal with

```shell
chmod 755 pdftk_installer
./pdftk_installer
```

---

## pdfnup

pdfnup is super useful for making documents with slides + notes or
multiple slides per page. Previously it was available via
[texlive](https://tug.org/texlive/), but now I need to use
[pdfjam](https://github.com/rrthomas/pdfjam) plus the pdfnup script in
the [pdfjam extras](https://github.com/rrthomas/pdfjam-extras>).

But probably we could just get by with pdfjam; pdfnup is just a
wrapper with specific settings.

---

## pdftools

The R package pdftools uses `libpoppler-cpp-dev`

```
sudo apt install libpoppler-cpp-dev
```
