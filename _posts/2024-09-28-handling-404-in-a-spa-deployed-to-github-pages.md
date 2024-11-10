---
layout: post
title: Handling 404 in a SPA deployed to GitHub Pages
date: 2024-09-28
categories: [GitHub Pages, SPA]
author: chrispelatari
---

Credit where it's due, I found this via [this blog post](https://dev.to/lico/handling-404-error-in-spa-deployed-on-github-pages-246p)

I recently deployed a Single Page Application (SPA) to GitHub Pages. Everything was working great until I tried to refresh the page. When I did that, I got a 404 error. This is because GitHub Pages doesn't support SPA routing out of the box. This is how I fixed it.

## I simply added an echo statement to the command that builds the SPA for those of us who like to see what's going on during the build process.

The meat of the addition is the cp command, but there's no visual feedback that it's working. I added the echo statement to let me know that the cp command is running.

```json
"build": "vue-tsc --noEmit && vite build --mode production && echo 'copying index.html to 404.html in ./dist' && cp ./dist/index.html ./dist/404.html",
```

This is the command that builds my SPA using [Vite](https://vitejs.dev/). The `cp` command copies the `index.html` file to `404.html`. This way, when a 404 error occurs, the SPA will still load.

This was a difficult one to figure out. I hope this helps someone else.