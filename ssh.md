## ssh

Roger Peng's notes (now gone, but available on [internet archive](https://web.archive.org/web/20190503084130/http://www.biostat.jhsph.edu/bit/nopassword.html))

stackoverflow answer re avoiding passphrase:
<https://stackoverflow.com/a/25721662/897303>

```
ssh-add ~/.ssh/id_rsa &> /dev/null
```

I really don't understand this; seems you need to run both ssh-agent
and ssh-add in each shell


---

### GitHub instructions re [ssh-agent](https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/#adding-your-ssh-key-to-the-ssh-agent)

I think this is just needed on a Mac

- Start `ssh-agent` in the background (in `~/.bash_profile`?)

  ```
  eval "$(ssh-agent -s)"
  ```

- Modify (or create) `~/.ssh/config`

  ```
  Host *
    AddKeysToAgent yes
    UseKeychain yes
    IdentityFile ~/.ssh/id_rsa
  ```

- Add your private key to the ssh-agent

  ```
  ssh-add -K ~/.ssh/id_rsa
  ```

---

To change passphrase:

```
ssh-keygen -p
```
