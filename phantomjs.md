## phantomjs

- download the linux 64-bit version from <https://phantomjs.org/download.html>

- extract with `tar xvf`

- copy the file `bin/phantomjs` to `~/.local/bin/`

- add the following to `~/.bashrc` ([see this](https://github.com/ariya/phantomjs/issues/15449#issuecomment-888733781))

  ```
  export OPENSSL_CONF=/etc/ssl
  ```

- an alternative is
  [CapserJS](https://www.npmjs.com/package/casperjs), but both
  phantomjs and casperjs seem to have been abandoned

---

### Example for scraping an email

The main problem I had here was the timeout: it tended to try to grab
the result (and got an error) before they were available.

```javascript
var page = require('webpage').create();
page.open('https://www.wisc.edu/directories/?q=FIRSTNAME+LASTNAME', function(status) {

    setTimeout(function() {
        email = page.evaluate(function() {
            x = document.getElementById("people-results");
            y = x.getElementsByClassName("person_email");
            return y.length + " " + y[0].firstElementChild.innerText;
        });

        console.log(email);
        phantom.exit();
    }, 2000);

});
```
