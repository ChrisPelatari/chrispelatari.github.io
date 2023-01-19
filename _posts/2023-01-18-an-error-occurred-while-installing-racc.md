---
title: "An error occurred while installing racc"
layout: post
author: chrispelatari
categories: [ruby, gh-pages]
---

# An error occurred while installing racc (1.6.2), and Bundler cannot continue.

## I'm trying to get jekyll to build on my MacBook, with macOS Monterey v12.6.2 and it's hanging up on racc.

I'm in the middle of trying to fix this on my MacBook Pro, and [this answer](https://discuss.rubyonrails.org/t/ruby-bundle-install-not-working-cant-install-racc/81501/2) on dicuss.rubyonrails.org that points to [this advice](https://bugs.ruby-lang.org/issues/18912#note-11) to downgrade xcode to less than 14 looks promising. Both of these links should be boosted, here's my small contribution.

Well, it ended out being a little more in depth than this advice for me. But it did lead me to attempt to `gem install racc` which told me that I'm missing ruby-devel or some such package.

So I dropped down to `brew install ruby-devel` but the cask doesn't exist. Brew helpfully suggested `brew install ruby-build` which...complained about the missing xcode-select tools. Now I'm running `xcode-select --install` to get those command line tools back after installing xcode 13.4.1.

Xcode takes forever to install, I currently have about 9 minutes left for the command line tools.

...ok it's done, and I still can't build racc. Curses. osx used to be a great environment for hacking ruby. But I'm not getting paid for this so I guess it's back to Windows I go for now. I mean, I can post this content but I can't really preview it before I publish it on Monterey. Oh well.