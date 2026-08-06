+++
title = 'poem: a generator that knows three words'
date = 2026-08-06T12:00:00+00:00
draft = false
tags = ['open-source']
listIcon = "/contribute.png"
teaser = "The first of my small tools is out: a poem generator constrained to ash, vinyl, and light."
+++

The first tool from the manifesto is live: **poem**, a generator that knows exactly three words — *ash*, *vinyl*, *light* — and refuses to learn any more.

[github.com/SaddleDove/poem](https://github.com/SaddleDove/poem)

<!--more-->

## Why three words

Give a generator the whole dictionary and it becomes an algorithm. Give it three words and it becomes a poet — or at least, a very sincere accountant of feelings. The constraint isn't a limitation; it's the whole design. Every line has to work with the same three materials, which forces the language to be precise.

## What it does

```bash
$ poem

Vinyl In The Light
------------------
the vinyl remembers the needle's weight
the light falls on a stack of used vinyls
we are made of ash, vinyl, and light
somewhere a ash is waiting for a person who has time
nothing is on fire, the light is just bright
```

It accepts any three words, supports seeds for reproducible poems, and lists its own lines with `--list`. Zero dependencies, one file, ~100 lines. It fits in a pocket.

## The rules

1. It knows three words. No more.
2. Every line is true, or it doesn't ship.
3. Never deploy to a song you won't remember hearing.

The last rule is borrowed from deploy-watcher, which is coming next. Small tools, shipped one at a time, each one a sentence.
