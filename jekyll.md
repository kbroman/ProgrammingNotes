## Notes on jekyll


What I'd done originally (but see bundler business, below; that's what
I use now):

```
gem install jekyll
jekyll build
jekyll serve
```

---

To make a new website, copy over

```
Rakefile
_includes
_layouts
_plugins
_posts
assets/themes
```

Then edit:

```
index.md
_config.yml
_includes/themes/twitter/default.html
```

---

Put `.md` files in `pages/` and anything else in `assets/`.

(Actually that's not true. Jekyll will convert all `.md` files to
`.html`, regardless of the directory structure.

---

Re bundler with github pages:
See <https://help.github.com/articles/using-jekyll-with-pages/>

```
gem install bundler
```

Make `Gemfile` containing: `gem install github-pages`

Instead of `jekyll serve` use:

```
bundle exec jekyll serve
```

May need to first do:

```
bundle install
```

To update bundler:

```
bundle update
```
