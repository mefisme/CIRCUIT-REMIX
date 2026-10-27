# CHANGELOG

## Alpha 0.04 (2026-10-27) — experimental

Two new builds: **Alpha 0.04** (marker `A0.04`) and **Alpha 0.04S** (marker `A0.04S`: no project copy, pack delete or sample copy). Everything is in the [manual](docs/MANUAL.md).

> ⚠️ **Experimental: needs refinement.** Almost everything new has only been checked in emulation. On the device we tested the single-track granular, the de-clicker and short loops, stereo recording, the playback start and the clock while a sample is saved. Expect bugs, noises or hangs: for serious playing, stay on **Alpha 0.03** (still in the installer). **Back up the SD card.**

What's new:
- **Track menu:** hold a track's button and pads 1-7 become a menu: stock / Stock+ / Granular page, granular on / off, line input and its gate, stereo link. It replaces pressing the track's button again.
- **Granular** (the CIRCUIT-HACKS engine, on the master DSP):
  - a Granular knob page (size, density, position, scan, pitch, sprays, window; with Shift: fine control, stereo spread, zone, reverse, gate);
  - it follows the note (Note view, keyboard, MIDI);
  - the track's filter and envelope act on it;
  - **up to 4 granular tracks at once**, each with its own settings; saved with the project.
- **Line input as a track's sound** (one track: L + R; two tracks: L and R), with a note gate.
- **Stereo link:** a track and the next one play as one stereo sound (its sample on the left, the next one on the right).
- **Stereo Sample Rec** (pad 24): L into the chosen slot, R into the next one.
- **Loops:**
  - crossfade de-clicker (Sample mode pad 19 per track; Sample Rec pad 23 for all; on by default);
  - short loops play at their own length (the original repeated them every ~128 samples);
  - the scan (Stock+ K8) moves the loop's start on every pass.
- **Stock+:** K3 (pitch LFO) and K8 (scan) from the centre: centre = still, right = free, left = synced to the tempo. Projects from Alpha 0.02 / 0.03 may sound different.
- **Sample mode, pads 9 / 10:** fit the sample to the pattern with stretch, without changing pitch.
- **Mixer cue mode** (pan page, Shift + knob): the mix on the left output, the cue on the right.
- **Micro Step:** fixed length (pad 31) and gate by press (pad 32) when entering steps.
- **Velocity view, Shift + step:** on that step, automated parameters go back to their knob.
- **Pattern Settings, Clear + pad 25:** clears the pattern's dynamics and mutation.
- **Setup:** General MIDI mode (pad 22, each track's note on K1-K8); Advanced Setup: external keyboard into the arpeggiator (pad 22) and USB merge of DIN In (pad 23).

Fixes to the original firmware:
- Playback starts sooner (≈ 10 ms from Play to the first sound; the original ≈ 18 ms) and the notes of one step sound together.
- The clock no longer stumbles while a sample is saved.
- Lost notes with many tracks on the same step (the trigger queue to the DSP overflowed).
- The Program Change channels and the Thru mode (Merge / Filter) are kept after power-off (not yet checked on the device).

## Alpha 0.03 (2026-10-25)

Two new builds (the earlier ones stay in the installer):
- **Alpha 0.03** (marker `A0.03`): Alpha 0.02 with the fix below; the same features as in the [manual](docs/MANUAL.md).
- **Alpha 0.03S** (marker `A0.03S`): Alpha 0.03 without project copy, pack delete or sample copy; nothing of the mod creates, changes or deletes files on the card.

Fix:
- **The Stock+ page works from power-on.** In Alpha 0.01 / 0.02, right after switching the device on (not after installing), Stock+ could do nothing for a few minutes. The cause is in the original firmware: the voices' DSP does not initialise, at start-up, the configuration word of its link to the main processor, and with some power-on memory contents that link switches to 16-bit words while the processor sends 24; everything Stock+ wrote was lost until the link happened to fall back into step. Now the DSP's start-up clears that word before it sets up the link (2 words of our own code).
- **Tested on the device** with the equivalent development build (RH36): Stock+ works in the first seconds after a cold start. **Back up the SD card.**

## Alpha 0.02 (2026-10-25)

Two new builds (the earlier ones stay in the installer):
- **Alpha 0.02** (marker `A0.02`): every feature in the [manual](docs/MANUAL.md).
- **Alpha 0.02S** (marker `A0.02S`): Alpha 0.02 without project copy, pack delete or sample copy; nothing of the mod creates, changes or deletes files on the card.

What's new:
- **The full Stock+ page** (press the selected track's button again):
  - K5 ring mod (Shift: its frequency);
  - K6 pitch follow (Shift: filter type stock / 24 dB / comb on the stock filter knobs; its LED in the type's colour);
  - K7 **stretch** 0.25×-4× without changing pitch (Shift: bitcrush);
  - K8 start-point scan (Shift: its depth).

  Clear + K5-K8 resets both layers. Saved with the project; Alpha 0.01 projects load as they were.
- **Fixed Recording at the external MIDI clock's tempo** (mefisme's fix, previously in A0.01F / A01FS).
- **Fix:** the Stock+ page's words no longer share DSP memory with track 8's sample (in Alpha 0.01 it could be heard on track 8 with the pitch envelope or LFO).
- **Tested on the device** with development builds: the DSP with everything on all 8 tracks plus reverb and delay, 2 minutes without dropouts; the page, its knobs and saving. **Back up the SD card.**

## Alpha 0.01F / A01FS (2026-10-24)

>
> ⚠️ **Known bug in Alpha 0.01, 0.01S, A0.01F and A01FS: track 8.** The Stock+ page's values (pitch envelope and LFO) sat in the DSP memory where track 8 reads its sample while it plays, and they are written all the time, even if you never use the page. With something playing on track 8 you may hear chirps, clicks or hiss, and its pitch may drift. **Fixed in Alpha 0.02: please update.** Alpha 0.0 / 0.0S are not affected.

Two builds with a Fixed Recording fix ([details](docs/FIXEDREC.md)):
- **Alpha 0.01F** (marker `A0.01F`): Alpha 0.01 + the fix.
- **A01FS** (marker `A01FS`): Alpha 0.01S + the fix.

With an external MIDI clock, Fixed Recording uses the clock's tempo, not the project tempo. Without an external clock, it uses the project tempo, as the original. Installer: `firmware/a0.01f/a001f_uploader.html`.

Checked in emulation (17 cases) and on the device with the FRD1 test build (the fix + read-only remote diagnostics). **Back up the SD card.**

## Alpha 0.01 (2026-10-21)

>
> ⚠️ **Known bug in Alpha 0.01, 0.01S, A0.01F and A01FS: track 8.** The Stock+ page's values (pitch envelope and LFO) sat in the DSP memory where track 8 reads its sample while it plays, and they are written all the time, even if you never use the page. With something playing on track 8 you may hear chirps, clicks or hiss, and its pitch may drift. **Fixed in Alpha 0.02: please update.** Alpha 0.0 / 0.0S are not affected.

Two new builds (the earlier ones stay in the installer):
- **Alpha 0.01** (marker `A0.01`): every feature of the [manual](docs/MANUAL.md).
- **Alpha 0.01S** (marker `A0.01S`): Alpha 0.01 without the project copy, the pack delete and the sample copy; nothing of the mod creates, changes or deletes files on the card.

New:
- **The Stock+ track knob page:** press the selected track's button again. K1 / K2 = pitch envelope (amount ±24 semitones, decay 5 ms to 4 s), K3 / K4 = pitch LFO (0.05-30 Hz, up to 24 semitones); Shift = fine control, as on the original knobs; saved with the project. The first feature with its own code in the voices' DSP (the DSP tested on the device with a diagnostic build; the page and its knobs so far in emulation only).
- **Delete a pack** on the device (Packs: Clear + pack, Clear + the same pack) and **copy a sample** to another slot, also from another pack (Sample Rec: Duplicate + A, Duplicate + B).
- **Master compressor threshold** on K5 of the Sidechain view; Clear + a Sidechain knob, one at a time.
- **Scene repeat:** in the Mixer with Shift, the repeat that is playing shows white.
- **Dynamics are recorded** into the step with Record (the velocity and micro step it played with).
- Fixes: the count-in follows the project's tempo; the send LEDs after Duplicate / Clear in the FX view; the dynamics row of the probability view.

Checked in emulation (each feature with its test; 121 gestures and ordinary actions identical to the original except what is added). **Back up the SD card.**

## Alpha 0.0 (2026-10-19)

First public release of Circuit Remix: a port of the CIRCUIT-HACKS (Circuit Tracks) features to the Circuit Rhythm 2.0.1 (build 5706), with exclusive features. Two builds:
- **Alpha 0.0** (marker `A0.0`): every feature of the [manual](docs/MANUAL.md).
- **Alpha 0.0S** (marker `A0.0S`): Alpha 0.0 without the project copy; nothing of the mod creates, changes or deletes files on the card.

Checked in emulation (the device's code run on a dump of its memory): each feature with its test, and that nothing of the original firmware is lost (115 gestures and ordinary actions identical to the original except what is added). Without the remote SysEx diagnostics of the development builds. On the device, the first features and the saving / loading of the mod's own data with the project have been tested; the rest is pending: **back up the SD card**.
