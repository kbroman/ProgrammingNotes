## ssh

Roger Peng's notes: <http://www.biostat.jhsph.edu/bit/nopassword.html>

stackoverflow answer re avoiding passphrase:
<http://stackoverflow.com/a/25721662/897303>

```
ssh-add ~/.ssh/id_rsa &> /dev/null
```

I really don't understand this; seems you need to run both ssh-agent
and ssh-add in each shell
