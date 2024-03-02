---
layout: post
title: "Discourse Fresh Install on Mac OS"
date: 2024-03-02 12:00:00 -0000
categories: discourse
author: chrispelatari
---

# Discourse Fresh Install on Mac OS

## Introduction
So, most of the install instructions are correct, but there are a few extra steps I had to figure out. I will go through the steps to install Discourse on Mac OS.

## Prerequisites
You need to have the following installed:
- Homebrew
- Redis
- PostgreSQL
- Ruby
- Bundler
- Node.js
- Yarn
- ImageMagick

This last one is not mentioned in the install instructions, but it is required. When running the ember app, it will fail if ImageMagick is not installed.

```sh
brew install imagemagick
```

## Install Discourse
1. Clone the Discourse repository
2. Install the dependencies
3. Create the database
4. Start the server

For number 4, I have added a dev script that uses concurrently to run both the rails server and the ember server. This is not required, but it is convenient.

```sh
# package.json
"scripts": {
  "dev": "concurrently \"bin/ember-cli server --environment=development\" \"RAILS_ENV=development bundle exec rails s\"",
  ...
}
```

## Conclusion
For me, this is the way. I got Discourse running on my Mac OS, and it only took a couple of shots of espresso and some shipleys donuts. I hope this helps you get your Discourse instance up and running. If you have any questions, feel free to reach out to me on [Mastodon](https://hachyderm.io/@blue_fenix).

Here's the command to run the dev script:

```sh
yarn dev
```
