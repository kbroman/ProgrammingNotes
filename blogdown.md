## blogdown

These are the steps I took to create my
[blogdown-based blog](https://github.com/kbroman/blog):

- At <disqus.com>, I logged into my (previously-created) account, and
  chose "Get started" and then "I want to install Disqus on my site",
  using the short name `kbroman-blog`

- Installed the blogdown package via `devtools::install_github("rstudio/blogdown")`

- Installed hugo via `blogdown::install_hugo()`.

- Made a directory for new site and changed into it.

- Created the template with `blogdown::new_site(serve=FALSE)`

- Removed `content/post/*.*`

- Put `public/` into a `.gitignore` files with `echo "public/" > .gitignore`

- Initialized git repository:

  ```
  git init
  git add .
  git commit -m "Initial commit"
  ```

- Added `ReadMe.md` and `LICENSE` files.

- Created `static/images` directory and added `cc-by.svg` and `karl.png`.

- Edited `config.toml`, namely these fields:

  - `title`
  - `disqusShortname`
  - GitHub `url`
  - Twitter `url`
  - `description`
  - `url` for `logo.png` to `karl.png`

- Created subdirectory `layouts/partials`
  and copied
  [`disqus.html`](https://github.com/rbind/daijiang/blob/master/layouts/partials/disqus.html)
  from [the repo](https://github.com/rbind/daijiang) for
  [Diajiang's website](https://daijiang.name/) into it. (Needed this
  to get [disqus](https://disqus.com) working.)

- Added `Makefile`

- Copy `themes/hugo-lithium-theme/layouts/partials/footer.html` into
  `layouts/partials` and edit to replace the "Powered by hugo" with a
  CC-BY badge.

- Replace `content/about.md` with my info

- Add a couple of posts to `content/post`

- Add `content/post/*.html` to `.gitignore`:

  ```
  echo "content/post/*.html" >> .gitignore
  ```

- Created a new repository on github

- Locally, added `"remote` and pushed to github.

  ```
  git remote add origin git@github.com:kbroman/blog
  git push -u origin master
  ```

- Changed `master` branch to `source`

  ```
  git checkout -b source
  git push -u origin source
  ```

- On github, changed default branch to `source`.

  - Went to <https://github.com/kbroman/blog/branches>
  - Clicked "change default branch" button
  - Selected "source"
  - Clicked "Update"
  - Said "Yes, I'm sure"

- Deleted master branch

  ```
  git branch -d master
  git push --delete origin master
  ```

- Removed `public/` subdirectory again

- Cloned repository into that directory

  ```
  git clone git@github.com:kbroman/blog public
  ```

- Changed into the `public` folder and created an orphan branch,
  `gh-pages`, then cleared everything out.

  ```
  git checkout --orphan gh-pages
  git rm -r --cached .
  rm -r .gitignore *
  ```

- Move back one directory and run `make deploy`.

- Added a file `static/css/custom.css` to change the highlighting of
  hyper links, and added a line to `config.toml` so it would be used.
  Learned from the error message that `customCSS` in the `config.toml`
  file needs to be an array:

  ```
  customCSS = ["css/custom.css"]
  ```
