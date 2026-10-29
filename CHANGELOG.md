# CHANGELOG

## Alpha 0.08 (2026-10-29) — experimental

Two new builds: **Alpha 0.08** (marker `A0.08`) and **Alpha 0.08S** (marker `A0.08S`: no project copy, pack delete or sample copy). What's new is **mefisme**'s contribution (pull request 7, their A0.04F / A04FS), brought onto the current line. Everything is in the [manual](docs/MANUAL.md#transporte) ([illustrated](docs/manual/en.html)).

> ⚠️ **Experimental: needs refinement.** The count-in on the clock was tested on the device on Alpha 0.04 (mefisme's A0.04F); on the current line it has only been checked in emulation, like most of Alpha 0.04-0.07. Expect bugs, noises or hangs: for serious playing, stay on **Alpha 0.03** (still in the installer). **Back up the SD card.**

What's new:
- **The count-in follows the music's clock:** the project's tempo, or the external MIDI clock as a slave. Before, the LED task timed it: clicks 0 to 10 ms late.
- **The 1 on time:** Play goes through at the start of the count and the clock's start waits until the 1, so Play's work runs during the count.
- **During the count** nothing records and the Play LED shows stopped; Record flashes red on each click.
- **Slave:** the first click comes on the master's next bar when its position is known (Start or Song Position).
- **Visual metronome:** with the click's level at 0 (Tempo / Swing K5), Clear flashes orange on each click and each beat.
- **Faster step load on Play** (the same result with a quarter of the calls).
- **Error light:** Clear blinks red if these features cannot run on the firmware they find (it should never show).
- Shift + Play (the count, then carry on) and Play during the count (cancels it) work as before.
- **Line input:** on the track menu, pad 15 with the inputs as the source (no FX) shows dim amber; the reverb and delay returns as before.

## Alpha 0.07 (2026-10-28) — experimental

Two new builds: **Alpha 0.07** (marker `A0.07`) and **Alpha 0.07S** (marker `A0.07S`: no project copy, pack delete or sample copy). Everything is in the [manual](docs/MANUAL.md) ([illustrated](docs/manual/en.html)).

> ⚠️ **Experimental: needs refinement.** Stock+ on the granular and the synth has only been checked in emulation, like most of Alpha 0.04-0.06. Expect bugs, noises or hangs: for serious playing, stay on **Alpha 0.03** (still in the installer). **Back up the SD card.**

What's new:
- **Stock+ for every sound:** the Stock+ page (track menu, pad 2) on **granular** and **synth** tracks too:
  - the pitch envelope and LFO on each new grain's pitch / the synth's oscillators;
  - ring mod, pitch follow and the filter type (24 dB, comb) on their sound;
  - **K7 = waveshaper:** amount (gain x1-x16; for bitcrush, the bits); **Shift + K7 = its type:** soft (gold), hard (red-orange), fold (teal), bitcrush (lime);
  - **K8 = an LFO** on the grains' position (granular) or the FM amount (synth); Shift + K8, its depth;
  - the waveshaper is saved with the project and goes along with Clear + track button and Duplicate.
- **The track's distortion knob** (stock page) now also works on the granular and the synth, with the same curve as on a sample.
- On a granular or synth track the unheard sample voice no longer spends Stock+.

## Alpha 0.06 (2026-10-28) — experimental

Two new builds: **Alpha 0.06** (marker `A0.06`) and **Alpha 0.06S** (marker `A0.06S`: no project copy, pack delete or sample copy). Everything is in the [manual](docs/MANUAL.md) ([illustrated](docs/manual/en.html)).

> ⚠️ **Experimental: needs refinement.** The envelope and the line input from the FX returns have only been checked in emulation, like most of Alpha 0.04 / 0.05. Expect bugs, noises or hangs: for serious playing, stay on **Alpha 0.03** (still in the installer). **Back up the SD card.**

What's new:
- **Envelope by play mode** for the synth and the granular, on a new **Envelope page** (track menu, pad 5, rose):
  - K1 start (the attack), K2 length, K3 slope (from the centre), K4 envelope → low-pass;
  - the length by the track's play mode: **one-shot** = a percussive decay; **gated** = holds and releases; **loop** = holds for that time even after a short note;
  - on the granular, with its gate on, the envelope is the VCA;
  - saved with the project.
- **Line input from the FX returns:**
  - menu pad 15: the inputs (amber) → the reverb return (cream) → the delay return (peach);
  - the gate (pad 14) now also goes through the track's **filter** (VCA and VCF).
- The snapshot Clear + track button uses now lives in RAM: it frees project space for the envelope.

## Alpha 0.05 (2026-10-28) — experimental

Two new builds: **Alpha 0.05** (marker `A0.05`) and **Alpha 0.05S** (marker `A0.05S`: no project copy, pack delete or sample copy). **A new manual**, view by view, with a glossary of functions: [text](docs/MANUAL.md) or [illustrated](docs/manual/en.html).

> ⚠️ **Experimental: needs refinement.** The synth and the new interface have only been checked in emulation, like most of Alpha 0.04. Expect bugs, noises or hangs: for serious playing, stay on **Alpha 0.03** (still in the installer). **Back up the SD card.**

What's new:
- **Synth** (on the master DSP), as any track's sound, up to 4 tracks:
  - two oscillators (saw, pulse, triangle, sine) with sync, FM, SUB, noise, glide and octave;
  - its knob page (track menu, pad 4);
  - the track's original knobs (pitch, envelope, filters, level, sends…) act on it;
  - saved with the project.
- **New interface**, with fixed rules (the manual: "The colour code"):
  - each knob page has its colour: Stock+ sky blue, Granular lilac, Synth mint, on its knobs, the track's button and its menu pad;
  - **track menu:** the pages on pads 1-4 (stock, Stock+, Granular, Synth), only those of the track's sound; below, the toggles: 9 stereo link, 11 granular, 12 synth, 13 line input, 14 its gate. The sound only changes with the toggles. **Everything but pads 1-3 moves**;
  - **a tap on the selected track's button leaves the menu open** until you pick something or tap again; holding it, only while held. Holding a page pad shows it until you let go, like the original's view buttons;
  - Stock+ K3 / K8, the synced half: now **faster towards the left end** (8 bars by the centre, 1/16T at the end). Alpha 0.04 projects sound different;
  - off = the same colour, dim (Micro Step, Setup, Advanced Setup, the arpeggiator); in Velocity with Shift, only the marked steps in red and the others as the view draws them;
  - Synth K1 / K2 in their waveform's colour; Stock+ K6 in its own colours per filter type; the granular's gate (Shift + K8) and the synth's sync (Shift + K2) as toggles.

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
