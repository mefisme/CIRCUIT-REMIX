# Circuit Rhythm firmware mods

Firmware patches for the **Novation Circuit Rhythm** (reference firmware 2.0.1, build 5706), in two lines:

- **Remix line:** [Circuit Remix](https://github.com/Ghillermo/CIRCUIT-REMIX) by Ghillermo, plus the features of this repository.
- **Rhythm Plus:** the original firmware, plus the same features of this repository and nothing else.

This repository is a fork of Circuit Remix. Support the original author: https://PayPal.me/ghillermo

> **Status: in development, no release yet.** To use Circuit Remix now, use the installer from the [Circuit Remix releases](https://github.com/Ghillermo/CIRCUIT-REMIX/releases).

Legal note: the firmware provided by Novation is proprietary; installing it on any device other than a Circuit Rhythm is not allowed.

> ⚠️ **Before installing: back up the SD card.**
> - Make a full copy of the SD card (projects, packs and samples) before sending any modified firmware.
> - Do not work on important projects stored on the device while you test a build.
> - Alpha builds can have problems that damage stored projects or samples.
> - Novation's bootloader is not touched: **Sample Rec + Samples + Note** at power-on lets you go back to the official firmware with Novation Components.

## Features of this repository

In development for both lines. The count-in, the visual metronome, the faster step load and the error light are part of Circuit Remix since Alpha 0.08.

- **Count-in on the music's clock:** the count follows the Rhythm's own clock or an external MIDI clock. As a slave, it starts on the master's next bar when the master's position is known (MIDI Start or Song Position).
- **Nothing records during the count,** and the Play button's light stays as stopped until the 1.
- **Visual metronome:** with the click volume at 0, Clear flashes on each click.
- **Sample Rec count-in:** pad 23 turns it on, pad 24 starts the music and the sampling together on the 1. While the music plays, the count clicks the beats left in the bar and sampling starts on the bar's 1. Record again, in any view, cancels the count.
- **Faster step load** when Play starts.
- **Even first steps after Play** (Rhythm Plus): the steps after Play keep the tempo instead of rushing. The Remix line uses Circuit Remix's own start fix.
- **Error light:** Clear blinks red if one of these features cannot run on the firmware it finds.
- **Fixed Recording at the external clock's tempo** ([details](docs/FIXEDREC.md)); part of Circuit Remix since Alpha 0.02.

How the work is organised (lines, versions, branches, tests): [`docs/DEVELOPMENT.md`](docs/DEVELOPMENT.md).

## Circuit Remix features (Alpha 0.08)

Full manual, view by view: [`docs/MANUAL.md`](docs/MANUAL.md). What changed in each version: [`CHANGELOG.md`](CHANGELOG.md).

> ⚠️ **Alpha 0.08 is experimental:** most of what is new in Alpha 0.04-0.08 has only been checked in emulation.

**New in Alpha 0.08 (experimental):** **the count-in on the music's clock** (contributed by mefisme): the clicks follow the tempo or, as a slave, the external MIDI clock (the first click on the master's bar), the 1 is on time, nothing records during the count; a **visual metronome** (with the click at 0, Clear flashes orange on each beat); Play loads the steps faster; the line input's pad 15 with no FX, dim.

**New in Alpha 0.07 (experimental):** **Stock+ for every sound**: the Stock+ page (menu pad 2) on the granular and the synth too (pitch envelope and LFO, ring, filters, **a waveshaper on K7** with its type on Shift + K7, K8 = an LFO on the grains' position / the FM); the **track's distortion knob** on the granular and the synth too.

**New in Alpha 0.06 (experimental):** the **envelope by play mode** for the synth and the granular (Envelope page, menu pad 5: start, length, slope, → filter); the **line input from the reverb or delay returns** (pad 15) and its gate through the track's filter.

**New in Alpha 0.05 (experimental):** the **synth** (two oscillators with FM, sync, SUB, noise and glide on up to 4 tracks, with its knob page); the **new interface** (a colour per knob page; the track menu with the pages on pads 1-4 and the toggles below; a tap on the selected track's button leaves the menu open, holding shows it until you let go; only the pages of the track's sound; Stock+ K3 / K8 synced halves faster towards the left end; off = the same colour, dim).

**New in Alpha 0.04:** a track menu (hold its button); **granular** on up to 4 tracks, with its knob page, the note, the track's filter and envelope and a stereo spread; the **line input** as the sound of one or two tracks; a **stereo link** of two tracks; **stereo Sample Rec**; a loop de-clicker and short loops at their own length; Stock+ K3 / K8 synced to the tempo; fit to the pattern with stretch; a **cue mode** in the Mixer; fixed length and gate by press in Micro Step; per-step automation release; General MIDI mode; an external keyboard into the arpeggiator; USB merge; playback starts sooner and the clock does not stumble while saving.

**Ported from CIRCUIT-HACKS:**
- **Metronome with count-in:** Shift + Clear steps through no metronome / metronome / count-in only / both; one bar of count before recording (also with Shift + Play while stopped: the count, then it continues from where it stopped).
- **Quantize:** Shift + Play while the pattern plays quantizes the selected track's pattern to its steps.
- **Mixer:** Shift + track pad = mute on the next bar; Shift + knob (levels) = 100 / 0; Shift + pads 9-16 = the current scene repeats 1-8 times.
- **Clear + track button** = its knobs to default and its automation cleared.
- **Pattern Settings:** pad 26 = Nudge; pads 27 / 28 = fractal and deconstructed orders.
- **Per step:** frequency (every n passes), dynamics and sample mutation.
- **Pattern chains with rules** ("n times A, then B; the next one, C") and a chain mode per scene.
- **Sidechain view:** K1-K4 = the track's sidechain attack, hold, decay and depth; K6 soft clip, K7 / K8 master compressor attack and release.
- **FX view:** ▲ / ▼ = delay / reverb sends; Shift + knob = reverb and delay parameters; Shift + ▲ / ▼ = master filter resonance; Duplicate = reset.
- **Clear + knob = default value** in the FX and Sidechain views.
- **Arpeggiator** (Shift + pads 17-32 in Pattern Settings): order, rate, and it records with Record.
- **Custom scale** with a free period (up to 24 semitones).
- **Copy projects** to another slot or another pack (Projects view: Duplicate + A, Duplicate + B; not in the S builds).
- **Setup:** MIDI Thru with Merge and Filter; own Program Change channels (receive and send).
- The Sidechain and FX knobs with Shift show their value as brightness.
- **Master compressor threshold** on K5 of the Sidechain view.
- **Scene repeat:** in the Mixer with Shift, the playing pass is shown in white.
- **Dynamics are recorded** into the step with Record.

**Exclusive to Circuit Remix:**
- **Copy a track to another:** Duplicate + track A, then track B = B gets A's parameters and selected sample.
- **Reset a track:** Clear + track button = besides the knobs, the other parameters and the sample go back to how the project was loaded.
- **Sample and note arpeggiator:** several held sample pads arpeggiate the samples (each hit is a sample flip); in the Note view, the held keys arpeggiate the track's sample; with Record, the arpeggio is recorded into the pattern.
- **Custom scale per track,** one iteration per pad row (two if they fit).
- **The Stock+ track knob page** (hold the track's button, pad 2): K1 / K2 = pitch envelope amount and decay, K3 / K4 = pitch LFO rate and depth, Shift = fine control; K5 ring mod (Shift: frequency), K6 pitch follow (Shift: filter type stock / 24 dB / comb), K7 **stretch** 0.25×-4× without changing pitch (Shift: bitcrush), K8 start-point scan (Shift: depth); saved with the project. Its own code runs in the voices' DSP.
- **Delete a pack** on the device (Packs: Clear + pack twice) and **copy a sample** to another slot, also from another pack (Sample Rec: Duplicate + A, Duplicate + B); not in the S builds.

## Install

**Circuit Remix (now):** use the installer from the [Circuit Remix releases](https://github.com/Ghillermo/CIRCUIT-REMIX/releases):

1. Download the official firmware Circuit Rhythm 2.0.1 (build 5706) from Novation: [circuitrhythm-firmware-5706.syx](https://components.novationmusic.com/api/v2/firmwares/169/file).
2. Download the installer (`rm_uploader.zip`) from the newest release, unzip it and open `rm_uploader.html` in Chrome or Edge.
3. Close Novation Components and any DAW or MIDI program (on Windows, only one program can open a MIDI port).
4. Connect the Circuit Rhythm over USB and switch it on.
5. Pick the official `.syx` and the version, allow MIDI access, and press **Send**. Do not disconnect the device while it sends.
6. When the Circuit Rhythm asks for confirmation, press **Play** on it.

**Builds from this repository:** an installer comes with the first release.

**Back to the official firmware:** send "Official" with the same installer, or use Novation Components. If the device does not start: hold **Sample Rec + Samples + Note** while you switch it on (Novation's bootloader mode), then send the official firmware.

## Repository contents

This repository holds only the project's own work: the build scripts, the Thumb assembler, the patcher, the documentation and each version's manifest (with the SHA-256 of the result).

**It does not include** Novation code or binaries: neither the official firmware nor the patched `.syx` / `.bin`, which contain Novation's firmware. You provide the official firmware, and the patcher checks its SHA-256. Device memory dumps and third-party samples or manuals are not included either.

## Build with Python

1. Download the official firmware Circuit Rhythm 2.0.1 (build 5706) from Novation: [circuitrhythm-firmware-5706.syx](https://components.novationmusic.com/api/v2/firmwares/169/file) (Novation Components' download link; the full list is at `https://components.novationmusic.com/api/v2/firmwares`, product `circuit-rhythm`).
2. Build:

```bash
python -m pip install -r tools/requirements.txt
python tools/patch_official.py PATH/TO/circuitrhythm-firmware-5706.syx --version A0.08
```

The tool checks the official firmware's SHA-256, builds the version in `firmware/<version>/` and checks that the result is identical to the published one. `--version A0.08S` builds the version without the features that write to the SD card; `--list` lists the versions; `--all` builds them all. `python tools/verify_builds.py` rebuilds the versions and compares them with their manifests.

Circuit Rhythm, Components and Novation are trademarks of Focusrite Audio Engineering Ltd. This project is not affiliated with them.
