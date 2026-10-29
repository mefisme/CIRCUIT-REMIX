# Development

How this repository is organised: the build lines, the version names, the branches, the tests and the rules every change follows.

## Build lines

| Line | Base | Contents |
|---|---|---|
| **Remix line** | Circuit Remix (now Alpha 0.08) | Circuit Remix + the features of this repository |
| **Rhythm Plus** | the official firmware 2.0.1 (build 5706) | the official firmware + the same features, nothing else |

- Every feature goes into **both** lines and is tested on both.
- A feature must not take a control away. It can add a gesture on a combination that did nothing before.
- An **S** build leaves out the features that write to the SD card by themselves. The Remix line has one now; Rhythm Plus gets one with its first such feature.
- **Play start:** the Remix line keeps Circuit Remix's start fix (`tools/startfix.py`). Rhythm Plus keeps its own (`playfix`: the first steps after Play keep the tempo), which is proven on the device. The count-in works with both.
- **Memory:** the Remix line takes its slots in Circuit Remix's RAM blocks (`tools/rhstate.py`, `OFF` and `OFF2`). Rhythm Plus has its own layout, which reuses `rhstate`'s reservation code. A layout change must leave the other line's build byte for byte the same.

## Version names

The name is stored in the firmware's version block and has at most **6 characters**.

**Rhythm Plus:**

| Stage | Meaning | Names | S build |
|---|---|---|---|
| Alpha | features still coming, may break | A0001, A0002 … | A0001S |
| Beta | all features in, bug fixes | B01, B02 … | B01S |
| Release candidate | could be the release: bug fixes only, no new features | RC01, RC02 … | RC01S |
| Release | the last release candidate, renamed | 1.0.0 | 1.0.0S |

- The number counts the builds of that stage and starts again at each stage.
- After a release: 1.0.1 for bug fixes, 1.1.0 for new features, 2.0.0 for changed behaviour.
- The S builds start when the first feature that writes to the SD card comes. Until then an S build would differ only in its name.
- Files are named `rhythmplus-<name>.syx`, so that A0003 is not confused with Circuit Remix's A0.03.

**Remix line:** Circuit Remix's version plus F, for example A0.08F, and its S build A08FS (the 6 characters leave no room for A0.08FS). The files are named `remix-<name>.syx`.

A published build never changes: its SHA-256 is in its manifest. A fix makes a new build.

## Branches and upstream

- **`main`** is this fork's own tree: English only, only the builds of the two lines and the Circuit Remix version they are built on.
- **Upstream sync:** fetch upstream and merge it into `main` on a computer, never with GitHub's "Sync fork" button. Files removed here stay removed unless upstream changes them; then the merge stops and asks. New upstream builds come in as new files: keep the newest base, remove the rest.
- **Pull requests to upstream:** a new branch from `upstream/main` with only the files of that change. Never from `main`.
- Circuit Remix builds in layers: each `tools/build_rhNN.py` adds features on the one before it, down to `build_rh01.py`. The layers of the current base stay, so a clash can be traced to the layer where it starts.
- `tools/make_guide.py` (upstream) writes the Spanish manual to `docs/MANUAL.md`. After running it, put the English text (`MANUAL_EN.md`) there and remove the Spanish files.
- Removed builds stay in the git history: `git show <commit>:tools/build_a003.py`.

## Development repository

Test builds, probes, emulator tests that need device memory dumps, and the personal flashing page live in a separate **private** repository. Built firmware (`.bin`, `.syx`) is stored nowhere: the build scripts make it again from the official firmware.

## Checks before a device test

1. **Emulator (Unicorn):** each feature runs on the built image and on the stock image with a device memory dump, and the results are compared.
2. **Disassembly (Capstone):** only the planned stock instructions change.
3. **Decompiler (Ghidra):** the new code reads as planned.
4. **Rebuild:** `python tools/verify_builds.py`; the published builds stay byte for byte the same.

Before each device test, the test list says what changed, what was tested and what was not. One feature is tested at a time.

## Firmware facts used here

- The bar position: the clock's pulse byte `[0x200126E8 + 0x20]`, +1 per pulse, back to 0 at 96 (`0x08032800`-`0x08032812`); 0 is the bar's 1.
- The stock heap is a bump allocator (`0x08025A98`; limit `[0x20002B54]`, current `[0x20002B58]`). It does not allocate after start-up; on failure it stops the processor (`bkpt`).
- Play's work on the device: 12-14 ms; 21 ms when a scene chain holds more than one scene (an extra pattern commit in the position reset `0x080340AA`).
