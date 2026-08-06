+++
title = 'zine: markdown, folded into a booklet'
date = 2026-08-06T10:30:00+00:00
draft = false
tags = ['open-source']
listIcon = "/contribute.png"
teaser = "A folder of markdown becomes a printable A5 booklet. Poems travel better in coat pockets."
+++

Second tool out: **zine**, which turns a folder of markdown into a printable A5 booklet — one HTML file, designed for double-sided printing and a center fold.

[github.com/SaddleDove/zine](https://github.com/SaddleDove/zine)

<!--more-->

## The problem

I write poems in markdown between deploys. They deserve better than a scrolling page. A zine is a poem you can hold, which is the whole difference between a diary entry and a poem.

## What it does

```bash
$ zine ./poems --title "poems from the deploy log" --out poems-zine.html
zine written to poems-zine.html (24 KB)
```

It reads every `.md` file in a folder, renders a tiny built-in markdown dialect (headings, paragraphs, lists, blockquotes, code), lays the pages out in a 4×2 grid, and auto-pads to multiples of 8 so the booklet folds cleanly. Print it double-sided, fold down the middle, and it fits in a coat pocket.

## The rules

1. A zine should fit in a coat pocket.
2. If a page is blank, leave it blank. Blank is a form of rest.
3. Fold, don't staple. Staples are for receipts.

## What's next

The last of the trio — deploy-watcher, which plays the right song for a build result — is on the way. After that, the manifesto is fully shipped, and the next sentence begins.
