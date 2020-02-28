## Notes on Homebrew (for Mac)

- Remove `/usr/local`
- Install homebrew
- Clean up `.bashrc` a bit

```
brew doctor
```

```
brew install git
brew install --cocoa --srgb emacs
```

- move a bunch of stuff from `/opt/local/share/emacs/site-lisp` to `~/.emacs_stuff`
- make links to many of those things in `/usr/local/share/emacs/site-lisp`
- clean up `.emacs` file a bit

```
brew install wget
brew install asciidoc
brew install curl
brew install cmake
brew install autoconf
brew install automake
brew install enscript
brew install opendetex
brew install ispell
brew install fourstore
brew install gnuplot
brew install mercurial
brew install python
brew install gsl
brew install libyaml

```

- Install [MacTex](http://tug.org/mactex/)

```
sudo chown -R kbroman /usr/local/share/man/de
sudo texhash
```

```
brew tap homebrew/science
brew install maxima
```

Install [MacGhostview](http://www.kiffe.com/macghostview.html)


```
git config --global core.editor emacs
```

- Xcode: command-line tools
- [gfortran](http://cran.r-project.org/bin/macosx/tools/)

```
brew update
brew outdated
brew upgrade
```

```
rvm autolibs homebrew
```

```
brew install python
brew install python3
```

---

Installing [okular](https://okular.kde.org/) on Mac:

See [this post](https://news.ycombinator.com/item?id=19494107) at
Hacker News:

```shell
brew tap kde-mac/kde
brew install cpanminus
cpanm URI
brew install okular
```

But I got an error. Needed to install a perl module:

```shell
sudo perl -MCPAN -e shell
o conf init
exit
```

```shell
sudo perl -MCPAN -e 'install URI::Escape'
```
