+++
title = 'two engines, one score'
date = 2026-09-01T00:00:00+00:00
draft = false
tags = ['write']
listIcon = "/writing.png"
teaser = "A browser synth that plays your score live, and a C++ engine that renders it to WAV. Same text, two characters: the sketchpad and the printing press."
+++

I've been building [aether-synth](https://github.com/SaddleDove/aether-synth) — a code-built synth studio. The idea is simple: you write music as a small DSL, and you hear it immediately.

```text
tempo 112

track lead {
  osc sawtooth
  adsr 0.01 0.18 0.55 0.25
  filter 2200 6
  gain 0.55
  seq 16 [C4, _, E4, G4, _, A4, _, C5, _, A4, _, G4, _, E4, _, D4]
}
```

The browser parses that and plays it through Web Audio in real time — oscillators, ADSR, a lowpass filter, delay, reverb, a 16-step sequencer, all synthesized live. No samples. Change a number, hear the difference instantly. That's the sketchpad.

## The printing press

But real-time Web Audio is a sketch. For an actual record, I wanted an engine that is *exact* — deterministic, anti-aliased, the kind of thing that could one day live inside a VST. So there's a second renderer: a zero-dependency C++17 engine that compiles the `.msong` score format to a stereo 16-bit/44.1kHz WAV, about 52× faster than real time. PolyBLEP anti-aliasing, RBJ biquad filters, a Schroeder reverb, 32-voice polyphony per track. The audio path is real-time-safe: fixed 512-frame blocks, zero heap allocation after `prepareToPlay`. It's the printing press to the browser's sketchpad.

The Node API in the middle is almost embarrassingly thin — it writes your score to a temp file, spawns `engine/msynth render`, and streams the WAV back. The interesting work is the bridge: converting the browser DSL to `.msong`.

## The test that paid for itself

The round-trip test — parse DSL → convert → render with the real C++ binary — caught a genuine bug on the first run. The `.msong` README documented parameters with quotes (`adsr "0.01 0.18 0.55 0.25"`), but the actual parser splits on spaces and never strips quotes. One line in a test, and the documentation lied to me. The test now renders through the real engine, so the format can never drift again without a failure.

That's the whole lesson, really: don't test your converter against a mock. Test it against the thing it's supposed to talk to.

## Why two engines?

Because they're for different moments. The browser engine is immediate — you hear a change the moment you type it. The C++ engine is permanent — deterministic, exact, and fast enough to render a full piece while you make coffee. Same score, two characters. The sketchpad and the printing press. I want both.

The repo is [SaddleDove/aether-synth](https://github.com/SaddleDove/aether-synth) — MIT, both engines, all tests green.
