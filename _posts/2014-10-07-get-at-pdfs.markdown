---
layout: post
title:  Get at PDFs
date:   2014-10-07 09:53:12
categories: newsroom
tags: newsroom, pdf, tips
---

This post should probably be called "How to make sense of your page source" or "How to read HTML" or "Making sense of how the Internet works".

Ok, maybe I'm going a little overboard.

What I mean is this: Even though there isn't an easy way to download a PDF, that doesn't mean it's impossible. Here are a few methods to download a PDF from a website.

## .pdf

First things first, check the URL bar. Does it end in `.pdf`? If it does, that means you are viewing the raw PDF that sits on their server. All you have to do is right-click on the document and click `Save as`.

## Embedded PDF

Sometimes it's not that simple. If the document you want is in some sort of embedded viewer like on the PACER site you may need to dig into the source code of the page.

Time for some HTML 101. Note: I'm going to use the Chrome browser but something similar is available in IE and Firefox.

Every web page is simply a text document with nested elements.

For example, right click on

THIS (seriously, right click on the word to the left)

and click `Inspect Element`.

What pops up is Google Chrome's developer tools. It is showing you the source code of this page. The highlighted line is the same one that you right clicked on. Take some time and look at it.
Notice the whole highlighted line says:

```
<p>THIS (seriously, right click on the word to the left)</p>
```

See gif of this process:

![this](https://cloud.githubusercontent.com/assets/4853944/4548357/63583ce8-4e54-11e4-98cc-12326077e5d6.gif)

Without going into too much detail, you inspected the paragraph with the content of the word "THIS".

Since you didn't care about any other part of the page, you can ignore all the other code.

What your doing is essentially sleuthing out the part of the page that you want more information on, Inspecting it, then digging into the source to see if there is anything there that you can use.

The same can be done with PDFs.

Try right-clicking on a PDF and `Inspect Element`. You should see a blue underlined link. Right click on that link and say `View in new tab`.

When that opens, try right clicking on the new-tabbed PDF and simply `Save as` wherever you want it.
