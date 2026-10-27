# Fixed Recording at the external MIDI clock's tempo

Circuit Rhythm 2.0.1 (build 5706). Part of Circuit Remix since Alpha 0.02 and of every build in this repository.

## What it does

With an external MIDI clock (for example a Circuit Tracks as master and the Rhythm as slave), **Fixed Recording** in the Sample Rec view uses the tempo of the incoming clock. Without an external clock, it uses the project tempo, as the original firmware does.

Fixed Recording pads, Sample Rec view, row 3:

| Pad | Function |
|---|---|
| 17 | Fixed Recording on / off |
| 18 | ½ bar |
| 19 | 1 bar |
| 20 | 2 bars |
| 21 | 4 bars |

It works with the recording threshold on or off. The length is set when the recording starts. A tempo change during the recording does not change it.

Recording length at 4/4:

| Length | Samples (48 kHz) | Time |
|---|---|---|
| ½ bar | 720000 × 8 / BPM | 120000 / BPM ms |
| 1 bar | 720000 × 16 / BPM | 240000 / BPM ms |
| 2 bars | 720000 × 32 / BPM | 480000 / BPM ms |
| 4 bars | 720000 × 64 / BPM | 960000 / BPM ms |

Example: external clock at 110 BPM, 1 bar = 104727 samples = 2.18 s.

The saved sample can be up to 255 samples (about 5 ms) shorter than the table. The original firmware trims the recording in blocks of 256 samples.

## Limits

**Whole BPM only.** The firmware keeps every tempo as a whole number, one byte. The clock tick measures the external clock and rounds it to the nearest whole BPM (`0x08032430`: `round(period × 0x9C4 / 2^32)`), and the Fixed Recording length is computed from that number. The stock firmware has the same limit: its own tempo can only be set in whole BPM.

- A master with a whole-number tempo gives the exact length. The Circuit Tracks only has whole-number tempos.
- A master with a decimal tempo (for example a DAW at 97.5 BPM) gives a length for the rounded tempo (98 BPM). The error is up to 0.5 BPM:

| Master tempo | Used | 1 bar | 4 bars |
|---|---|---|---|
| 97.5 | 98 | 12.6 ms short | 50 ms short |
| 120.4 | 120 | 6.6 ms long | 27 ms long |
| 120.5 | 121 | 8.2 ms short | 33 ms short |
| 40.5 | 41 | 72 ms short | 289 ms short |

The error is larger for slow tempos and long recordings. A fix for decimal tempos would compute the length from the measured clock period instead of the rounded BPM; this is not done.

**Tempo changes.** The measured BPM is updated about once a beat. A recording that starts right after a tempo change can use the tempo of the previous beat.

## How it works

The tempo store of the clock object (RAM `0x200126E8`, vtable `0x08068EFC`, tempo store at `+0x14`) holds two 32-bit words:

- word 0: the tempo set on the device (the project tempo);
- word 1: the tempo measured from the external clock, written by the clock tick (`0x08032430`) about once a beat, only with an external clock.

The original firmware reads word 0 at two places, each `ldr r0, [r4, #0x10]; movs r1, #0; bl 0x0803FC58`:

| Call | Function | Computes |
|---|---|---|
| `0x0803CEA0` | `0x0803CE98` | target length in samples and the stop timer (15000 × n / BPM + 50 ms), when the sampler state becomes 3 (recording) |
| `0x08058FE0` | `0x08058F9C` | the length in ms (32000 ms when Fixed Recording is off) |

`tools/fixedrec.py` changes these two `bl` into calls to its own function (72 bytes after the stock image). The function returns word 1 when all of these are true:

- the clock object has its vtable `0x08068EFC`;
- the store is the clock's tempo store;
- word 0 of the clock's external-clock store (`+0x48`) is not 0;
- word 1 is 40 to 240 BPM.

Otherwise it returns word 0, as the original firmware does.

## Files

| File | Use |
|---|---|
| `tools/fixedrec.py` | the fix module |
| `tools/emu_fixedrec.py` | emulation test of the fix |

## Tests

### Emulation

```bash
python -m pip install unicorn capstone==5.0.7 keystone-engine
python tools/emu_fixedrec.py stock/circuitrhythm-firmware-5706-STOCK.bin firmware/a0.04/circuitrhythm-5706-A0.04.bin
```

The test runs `0x0803CE98` and `0x08058F9C` from the original image and from the built image in Unicorn, with test stores and a test clock object. 17 cases: project tempo without an external clock, external clock, BPM outside 40–240 and at the limits, both store buffers, another store, wrong vtable, the four lengths, Fixed Recording off, and registers kept as the calling convention requires. Result: 17/17 pass on the first builds with the fix (A0.01F, A01FS) and on FRD1.

### On the device (FRD1)

FRD1 was a private test build (stock + the fix + the remote USB diagnostics). It is not published: the public builds carry no remote diagnostics.

Circuit Tracks as clock master, Circuit Rhythm as slave, project tempo 90 BPM:

- The clock object, its vtable, the tempo store (`0x20012788`) and the external-clock store (`0x20012868`) were at the expected addresses.
- The measured BPM (word 1) followed the Tracks: 100, 120 and 110.
- The fix code in flash was identical to the build.
- Eight recordings (pads 9–16) at 110 and 120 BPM, with tempo changes between them: every length matched the clock tempo, not the project tempo. Each WAV was the target length or up to 93 samples (1.9 ms) shorter (the 256-sample trim of the original firmware).

### On the device (first release build)

A0.01F and A01FS (the first builds with the fix, Alpha 0.01 + the fix) hold the same fix code as FRD1. With the release build (no diagnostics): external clock 100 BPM, project tempo 90 BPM, 1 bar on pad 9 → 115200 samples = 2.400 s, the clock tempo's length.
