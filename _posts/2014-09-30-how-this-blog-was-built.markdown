---
layout: post
title:  How this blog was built
date:   2014-09-30 13:20:04
categories: jekyll
tags: jekyll how-to blog
---

This blog was created using [Jekyll](http://jekyllrb.com/), a "simple, static, blog-aware site generator" that is hosted on GitHub.

The full source can be found on the [rgnewsroom organization](http://github.com/rgnewsroom/).

### How this was created:

1. Create repo
1. Clone repo locally
1. Follow [Jekyll getting started guide](http://jekyllrb.com/docs/quickstart/)
  * `gem install jekyll`
  * `jekyll new myblog`
  * `cd myblog`
  *  `jekyll serve --watch`
  * Go to `localhost:4000`
1. Voila! It works! Now put in content and style accordingly.
1. Commit and sync changes
1. Set up [GitHub pages](https://pages.github.com/) accordingly

### How to update source:

1. Clone repo to your machine
1. Change what is needed
1. Commit and sync changes

### How to edit with Prose:

1. Go to [Prose.io](http://prose.io)
1. Login to GitHub and authorize Prose to have access to your account
1. Navigate to the file you want to change
1. Edit accordingly
1. Click save on the right. Click Commit. All done!

### How to add a new post:

1. Use Prose or clone the repo locally
1. Click `New file` or create a new text document in the `_posts` folder
1. Make sure to add front matter at the beginning of the document like so:
  ```
  \---
  layout: post
  title:  How this blog was built
  date:   2014-09-30 13:20:04
  categories: jekyll
  tags: jekyll how-to blog
  \---

  ```
  * Note: remove the `\` before the `---`
1. Add your content in Markdown
  * [Markdown cheat sheet](http://nestacms.com/docs/creating-content/markdown-cheat-sheet)
1. Save the file as `YYYY-MM-DD-name-of-post.md`
