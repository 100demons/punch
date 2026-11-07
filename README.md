# PUNCH — twelve OPL2-style percussion engines for the Model:Cycles

PUNCH is one added machine for the **Elektron Model:Cycles**, OS 1.13: twelve percussion voices built on a
two-operator FM engine in the manner of the Yamaha OPL2, with extended fixed ratios for modern sounds and alien
harmonics. Raw, heavy and digital.

This repository is the machine's **source package**, published so that other projects can port it. It is not a
firmware and contains none.

**Hear it:** [PUNCH on YouTube](https://www.youtube.com/watch?v=MH_buA0-jHs)  
**Flasher:** [100demons.github.io/cycles-engines/flasher](https://100demons.github.io/cycles-engines/flasher/) —
tick PUNCH and bring your own official `model-cycles_OS1.13.syx`.

## The engines

SHAPE picks the engine. The names are shown on the machine's screen.

| SHAPE | Engine | What it is |
|---:|---|---|
| 0 | KIK | Kick: the classic FM kick, three octaves of pitch drop into a sine body |
| 1 | TOM | Tom: tuned membrane, one octave of pitch drop |
| 2 | BNG | Bongo: high, short and tight |
| 3 | CNG | Conga: lower and rounder, with a short bend |
| 4 | DJB | Djembe: hand drum, pitch drop and FM body |
| 5 | TAI | Taiko: big low drum, deep pitch drop, FM body |
| 6 | TIM | Timpani: felt thud and a long membrane |
| 7 | MAR | Marimba: fundamental plus tuned overtone, mallet click |
| 8 | BLK | Woodblock: short, hard pitched click |
| 9 | GNG | Gong: low inharmonic metal, long FM decay |
| 10 | BUB | Bubble: pitch rises into the note |
| 11 | ZAP | Laser: four-octave pitch fall |

## The knobs

| Knob | What it does |
|---|---|
| PITCH / FINE | the note, as on every machine |
| COLOR | the FM depth |
| SHAPE | the engine (the table above) |
| SWEEP | the ratio, 1:4 to 15X, stepped |
| CONTOUR | shapes the model's movement |
| DECAY | the decay, or release when GATE holds the note |
| GATE | on: holds the note for its length |
| PUNCH | on: MAR gets vibrato, GNG gets tremolo; the other engines ignore it |

## Status

| | |
|---|---|
| Package | `cycles-mod/0.1`, the model27/cycles-engines package format |
| Slot in the flasher | 8 (the OS numbers it machine 7) |
| Committed object | `punch.o`; `core/build_engine.py punch --check` passes |
| Emulated | a voice-loop test exists in the source tree; this package's manifest records no date |
| Tested on a real Model:Cycles | **not yet** |
| License | MIT |

PUNCH makes its own envelopes; the stock amp chain is not called. A silent voice is not computed. The OS still
sets the volume and applies velocity after the voice.

## Package layout

```
tools/machines/punch/
  manifest.json    the package: build recipe, symbols, claims, tests, compatibility
  card.json        the flasher card: label, description, status, video
  punch.c          the voice-loop bridge
  punch_dsp.h      the FM engine (two operators, OPL2-style log-sine and power tables)
  punch_tables.h   the generated tables
  punch_icons.h    the splash artwork
  punch.o          the committed relocatable object
  LICENSE          MIT
```

There is no firmware here: the package is applied to the user's own official OS file by a host such as
[cycles-engines](https://github.com/100demons/cycles-engines).

## Build and check the object

The package builds with the **cycles-engines** toolchain. Copy `tools/machines/punch/` into a cycles-engines
checkout as `engines/punch/`, then:

```sh
export M68K_CROSS=/path/to/bin/m68k-elf-        # or have m68k-elf-gcc on PATH
python3 core/build_engine.py punch --check
```

`--check` rebuilds `punch.o` from `punch.c` and the manifest's recipe and compares it with the committed object.
The composer and the flasher never need the toolchain: they place the committed object.

## Install

Easiest: tick **PUNCH** in the [flasher](https://100demons.github.io/cycles-engines/flasher/) and bring your own
official OS 1.13 file. Or download `punch-1.0.zip` from this repository's Releases and add the folder to your own
build.

## Credits

- Engine, tables and design: **100demons**, MIT.
- The OPL2 is named as the synthesis model; no Yamaha code, ROM dump or sample is included. See
  [THIRD-PARTY-NOTICES.md](THIRD-PARTY-NOTICES.md).

## Changelog

See [CHANGELOG.md](CHANGELOG.md).
