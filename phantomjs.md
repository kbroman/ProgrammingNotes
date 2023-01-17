## phantomjs

- download the linux 64-bit version from <https://phantomjs.org/download.html>

- extract with `tar xvf`

- copy the file `bin/phantomjs` to `~/.local/bin/`

- add the following to `~/.bashrc` ([see this](https://github.com/ariya/phantomjs/issues/15449#issuecomment-888733781))

  ```
  export OPENSSL_CONF=/etc/ssl
  ```
