A is for Airship
================

An Engineer's Blog

By [Andy Sayler](https://www.andysayler.com)

# Prerequisites
* [hugo](https://gohugo.io/) (extended edition)
* [golang](https://go.dev/)
* git

# Development
1. `$ hugo server -D`

# Build
1. `$ rm -rf ./public`
2. `$ HUGO_ENV=production hugo`

# Install or Update hugo
1. Download latest `hugo_extended_VERSION_linux-amd64.tar.gz` from https://github.com/gohugoio/hugo/releases/
2. `$ tar -xvf hugo_extended_VERSION_linux-amd64.tar.gz`
3. `$ mv hugo ~/bin/`

# Update Theme
1. `$ hugo mod get -u ./...`

