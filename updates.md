## Updating software

These are the things I do every other week to keep my computers'
software up to date.

```
brew update
brew upgrade

R -e 'update.packages(ask=FALSE)'
R -e 'update.packages(ask=FALSE, checkBuilt=TRUE)'

rvm get stable
gem update

conda update conda
conda update anaconda

npm update npm -g
npm update -g
npm install -g npm@latest
```

Also useful:

- `brew outdated` shows what packages need to be upgraded

- `brew cleanup` removes old versions of things; `brew cleanup -n`
  just shows you what would be cleaned up with out actually removing
  anything.
