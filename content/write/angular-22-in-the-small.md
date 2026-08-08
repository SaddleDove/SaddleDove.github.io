+++
title = 'Angular 22, in the small'
date = 2026-08-08T00:00:00+00:00
draft = false
tags = ['write']
listIcon = "/writing.png"
teaser = "Signals, zoneless change detection, and the sharp edges of shipping a static Angular app to GitHub Pages."
+++

I've been building a small static app in Angular 22 — nothing that needs a backend, nothing that needs a build server of its own. Just TypeScript, a page, and some data. The kind of thing that should be boring. It wasn't, entirely, and the interesting parts are worth writing down.

## The new defaults are good

Angular 22 ships with the stack that used to require persuasion: standalone components everywhere, signals for state, and zoneless change detection by default. No zone.js, no NgModules, no `ChangeDetectorRef` archaeology. The mental model is finally honest: a signal changes, a template recomputes, done.

For a small app this is a genuine relief. I wrote no services-of-services, no state library, no ceremony. The framework got out of the way and the code that remained was mostly mine.

## TypeScript 6 will scold you

The sharpest edge was the toolchain's version discipline. Angular 22's build pipeline *requires* TypeScript 6 (the peer range is narrow: `>=6.0 <6.1`), and Node 22.12+ or 24.x. My first `npm install` died in an ERESOLVE knot because I'd reached for TypeScript 5.9 out of habit.

The other surprise: TypeScript 6 promotes `baseUrl` to a hard error — deprecated with intent, gone in 7. I deleted it, switched to plain relative imports, and the config got *smaller*. That felt like the compiler doing me a favor disguised as an inconvenience.

## Four megabytes, lazily

The app needs a large pronunciation dictionary at runtime — too big for the bundle, wrong to block the first paint on. The clean trick: copy it from `node_modules` into the build's assets folder via `angular.json` globs, then `fetch` it lazily at runtime. The dictionary never touches the JavaScript bundle; the page boots fast, and the analysis starts the moment the data lands. Four megabytes of JSON parses in a few hundred milliseconds, and nobody notices. That's the whole art of shipping data like this: nobody notices.

## GitHub Pages, properly

Static Angular deploys to GitHub Pages fine, with one ancient gotcha: the base href. The app lives at `/repo-name/`, not `/`, so every asset URL is wrong until you build with `--base-href=/repo-name/`. Do that, and it's a standard Actions workflow: build, `upload-pages-artifact`, `deploy-pages`. The Pages API even lets you flip the source to "GitHub Actions" without touching the settings UI. Push to main, and the page updates itself.

## Build on a small box

The build runs on a rented server with two gigabytes of RAM and no fast path to GitHub. That shaped the workflow in useful ways: an Ansible playbook drives everything — provisioning, syncing source, `npm ci`, build — and source moves over rsync rather than git clone when the direct connection is flaky. Two gigabytes is enough for Angular if you give Node a ceiling (`NODE_OPTIONS=--max-old-space-size=1400`) and a couple of gigabytes of swap for the spikes. The machine is tiny and slow, and I've stopped caring: the build is reproducible, which matters more than it is fast.

## The machine's guess

The one thing I keep coming back to: the analysis this app performs is, at bottom, a guess. Perfect matches it can hear; the slant ones, the off-ones, the private ones a writer keeps for themselves — those are exactly the ones machines miss. You can ship the algorithm and still be honest about its limits. That's not a bug in the tool. That's the point of the tool: it does the mechanical part, so you can do the part that hears.
