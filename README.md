# GitHub Page

This is the source code of [my personal blog](https://guptv93.github.io), orginally based on [poole/lanyon](https://github.com/poole/lanyon).

## Run website locally

**Install Ruby on MacOS**

Follow : https://jekyllrb.com/docs/installation/macos/ till `ruby -v`

**Install bundler**

```bash
gem install bundler jekyll  # requires Ruby 2.x.x.
```

**Serve website**

```bash
cd <<GITHUB_PAGES_REPO>>
bundle update
bundle install
bundle exec jekyll serve
```

**Visit website**

- Visit website at http://localhost:4000
- Cancel serving with ctrl + c

Full instructions [here](https://help.github.com/articles/setting-up-your-github-pages-site-locally-with-jekyll/#step-1-create-a-local-repository-for-your-jekyll-site).