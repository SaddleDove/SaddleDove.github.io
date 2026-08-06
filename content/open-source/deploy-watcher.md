+++
title = 'deploy-watcher: shipping code with a soundtrack'
date = 2026-08-06T11:00:00+00:00
draft = false
tags = ['open-source']
listIcon = "/contribute.png"
teaser = "The last of the trio: run a command, get the right song for the result. Green builds get The 1975; failures get Ben Howard."
+++

The trio is complete: **deploy-watcher** is out. It runs your command and plays the right song for the result — because shipping code is a mood, and every mood has a soundtrack.

[github.com/SaddleDove/deploy-watcher](https://github.com/SaddleDove/deploy-watcher)

<!--more-->

## The playbook

| Mood | Artist | Why |
|------|--------|-----|
| Green | The 1975 | for the courage to be sincere |
| Green | FKA twigs | for the strange refactor |
| Green | Perfume Genius | for the final pass |
| Green | Fiona Apple | for the post-mortem that went well |
| Failing | Ben Howard | for the failing build — patience, not panic |

## What it does

```bash
$ dw "hugo --minify"
[GREEN] now playing: Perfume Genius — Slip Away

$ dw "npm run build"
npm error ...
[FAILING] now playing: Ben Howard — In Dreams
```

It runs the command, checks the exit code, and announces the song. With `--play-cmd "mpv --no-video"` it actually plays the track instead of just printing it.

## The rule

Never deploy to a song you won't remember hearing. If the deploy succeeds and you can't recall what was playing, the release didn't deserve a soundtrack — and it probably didn't deserve to ship either.

## The manifesto is now shipped

Three tools, three sentences: *poem* (a generator that knows three words), *zine* (markdown folded into a booklet), *deploy-watcher* (code with a soundtrack). All small. All finished. All free. Next sentence starts when the next problem does.
