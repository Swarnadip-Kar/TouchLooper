# Complete MIDI Mappings Reference

## Overview

- **MIDI Channels**:  
  - **Track 1**: Channel 3  
  - **Track 2**: Channel 4  
  - **Track 3**: Channel 5  
  - **Track 4**: Channel 6  
  - **Master Controls**: Channel 3 (shared with T1)  
- **Total Signals**: 40+ unique MIDI notes and CC messages  
- **Protocol**: OSC → MIDI conversion via Open Stage Control  

> **Important**: All original MIDI channel numbers were incremented by +2 to avoid using channels 1 and 2. Every `/control` and `/note` message now uses channels 3–6 as listed below.

---

## Track-Specific Controls

### Track 1 (T1) – MIDI Channel 3

#### Transport (MIDI Notes)
- **Play**: Note 60 (Toggle) → `[3, 60]`
- **Stop**: Note 61 (Push) → `[3, 61]`
- **Overdub**: Note 62 (Toggle) → `[3, 62]`
- **Undo**: Note 64 (Push) → `[3, 64]`
- **Clear**: Note 65 (Push) → `[3, 65]`

#### Mixing & FX (MIDI CC)
- **Volume**: CC 7 (0–127) → `[3, 7]`
- **Feedback**: CC 11 (0–100) → `[3, 11]`
- **Reverb**: CC 91 (0–127) → `[3, 91]`
- **Delay**: CC 92 (0–127) → `[3, 92]`
- **Double**: CC 93 (Push, 0–127) → `[3, 93]`

---

### Track 2 (T2) – MIDI Channel 4

#### Transport (MIDI Notes)
- **Play**: Note 66 (Toggle) → `[4, 66]`
- **Stop**: Note 67 (Push) → `[4, 67]`
- **Overdub**: Note 68 (Toggle) → `[4, 68]`
- **Undo**: Note 70 (Push) → `[4, 70]`
- **Clear**: Note 71 (Push) → `[4, 71]`

#### Mixing & FX (MIDI CC)
- **Volume**: CC 8 (0–127) → `[4, 8]`
- **Feedback**: CC 12 (0–100) → `[4, 12]`
- **Reverb**: CC 94 (0–127) → `[4, 94]`
- **Delay**: CC 95 (0–127) → `[4, 95]`
- **Double**: CC 96 (Push, 0–127) → `[4, 96]`

---

### Track 3 (T3) – MIDI Channel 5

#### Transport (MIDI Notes)
- **Play**: Note 72 (Toggle) → `[5, 72]`
- **Stop**: Note 73 (Push) → `[5, 73]`
- **Overdub**: Note 74 (Toggle) → `[5, 74]`
- **Undo**: Note 76 (Push) → `[5, 76]`
- **Clear**: Note 77 (Push) → `[5, 77]`

#### Mixing & FX (MIDI CC)
- **Volume**: CC 9 (0–127) → `[5, 9]`
- **Feedback**: CC 13 (0–100) → `[5, 13]`
- **Reverb**: CC 97 (0–127) → `[5, 97]`
- **Delay**: CC 98 (0–127) → `[5, 98]`
- **Double**: CC 99 (Push, 0–127) → `[5, 99]`

---

### Track 4 (T4) – MIDI Channel 6

#### Transport (MIDI Notes)
- **Play**: Note 78 (Toggle) → `[6, 78]`
- **Stop**: Note 79 (Push) → `[6, 79]`
- **Overdub**: Note 80 (Toggle) → `[6, 80]`
- **Undo**: Note 82 (Push) → `[6, 82]`
- **Clear**: Note 83 (Push) → `[6, 83]`

#### Mixing & FX (MIDI CC)
- **Volume**: CC 10 (0–127) → `[6, 10]`
- **Feedback**: CC 14 (0–100) → `[6, 14]`
- **Reverb**: CC 100 (0–127) → `[6, 100]`
- **Delay**: CC 101 (0–127) → `[6, 101]`
- **Double**: CC 102 (Push, 0–127) → `[6, 102]`

---

## Master Controls (MST Tab) – MIDI Channel 3

### Global Transport
- **Global Play**: Note 58 (Push) → `[3, 58]` – Start all tracks
- **Global Stop**: Note 57 (Push) → `[3, 57]` – Stop all tracks
- **Global Metronome**: Note 59 (Toggle) → `[3, 59]` – Metronome on/off

### Performance Controls
- **Looper Speed (Pitch)**: CC 20 (Range: 3–124) → `[3, 20]`
  - Maps to -3.00 to +3.00 semitones (custom range avoids asymmetry)
- **Master Tempo**: CC 1 (0–127) → `[3, 1]` – Controls global BPM
- **Master Volume**: CC 2 (0–127) → `[3, 2]` – Master fader

---

## Quick Reference Table

| Function | T1 (Ch3) | T2 (Ch4) | T3 (Ch5) | T4 (Ch6) |
|----------|----------|----------|----------|----------|
| **Play** | 60 | 66 | 72 | 78 |
| **Stop** | 61 | 67 | 73 | 79 |
| **Overdub** | 62 | 68 | 74 | 80 |
| **Undo** | 64 | 70 | 76 | 82 |
| **Clear** | 65 | 71 | 77 | 83 |
| **Volume (CC)** | 7 | 8 | 9 | 10 |
| **Feedback (CC)** | 11 | 12 | 13 | 14 |
| **Reverb (CC)** | 91 | 94 | 97 | 100 |
| **Delay (CC)** | 92 | 95 | 98 | 101 |
| **Double (CC)** | 93 | 96 | 99 | 102 |

---

## Button Modes

### Toggle Buttons
Send alternating 0/127 values:
- **Play** (green when active)
- **Overdub** (orange when active)
- **Global Metronome** (blue when active)

### Push Buttons
Send 127 on press, 0 on release:
- Stop, Undo, Clear, Double
- Global Play, Global Stop

---

## Special Implementation Notes

### Looper Speed Knob
```json
{
  "range": {"min": 3, "max": 124},
  "steps": 122,
  "channel": 3,
  "cc": 20
}
```
**Rationale**: 
- Values 0–2 produce non‑standard negative values (-3.20, -3.15, -3.10)
- Values 125–127 exceed +3.00
- Range 3–124 provides symmetric -3.00 to +3.00 semitone control

### Root OnTouch Code (Commented out by default)
```javascript
// switch(value) {
//   case 0: send('midi:daw', '/note', 16, 123, 127); break;
//   case 1: send('midi:daw', '/note', 16, 124, 127); break;
//   case 2: send('midi:daw', '/note', 16, 125, 127); break;
//   case 3: send('midi:daw', '/note', 16, 126, 127); break;
//   case 4: send('midi:daw', '/note', 16, 127, 127); break;
// }
```
**Purpose**: Auto‑focus corresponding track in DAW when switching tabs.  
**Important**: Keep commented during MIDI mapping to avoid ghost signals.

---

## Mapping in Ableton Live

### Step 1: Enter MIDI Map Mode
Click the **MIDI** button (top‑right corner).

### Step 2: Map Track 1 Looper (Ch. 3)
1. Click **Looper Play** → Press T1 Play button (sends Note 60 on Ch. 3)
2. Click **Looper Stop** → Press T1 Stop button (sends Note 61 on Ch. 3)
3. Click **Looper Overdub** → Press T1 Overdub (sends Note 62 on Ch. 3)
4. Click **Looper Undo** → Press T1 Undo (sends Note 64 on Ch. 3)
5. Click **Looper Clear** → Press T1 Clear (sends Note 65 on Ch. 3)

### Step 3: Map Track 1 Mixing (Ch. 3)
1. Click **Track Volume** → Move T1 Volume fader (sends CC 7 on Ch. 3)
2. Click **Send A** (Reverb) → Move T1 Reverb knob (sends CC 91 on Ch. 3)
3. Click **Send B** (Delay) → Move T1 Delay knob (sends CC 92 on Ch. 3)

### Step 4: Repeat for Tracks 2–4
Use the same process with the appropriate channel and values from the table above.

### Step 5: Map Master Controls (Ch. 3)
- Global Play (Note 58 Ch. 3) → Master Scene Launch
- Global Stop (Note 57 Ch. 3) → Stop All Clips
- Looper Speed (CC 20 Ch. 3) → Looper Speed parameter
- Master Tempo (CC 1 Ch. 3) → Global Tempo
- Master Volume (CC 2 Ch. 3) → Master Volume

---

## Conflict Prevention

### Strategy
- **Sequential note ranges**: T1 (60–65), T2 (66–71), T3 (72–77), T4 (78–83)
- **Separated CC ranges**: Volume (7–10), Feedback (11–14), FX (91–102)
- **Global range**: 57–59 for master transport, CC 1 & 20 for tempo/speed
- **Channel separation**: Each track uses a unique MIDI channel (3–6), eliminating any cross‑track interference.

### Why This Works
- No overlapping MIDI values between different functions
- Predictable pattern (increment by 6 for next track)
- Unique channels make it impossible for one track to accidentally trigger another

---

## Color Coding

### Button Colors
- **Green** (Play): `rgba(64, 255, 64, 0.8)`
- **Red** (Stop): `rgba(255, 64, 64, 0.8)`
- **Orange** (Overdub): `rgba(255, 128, 0, 0.8)`
- **Purple** (Undo): `rgba(128, 64, 255, 0.8)`
- **Blue** (Metronome): `rgba(64, 128, 255, 0.8)`

### Visual Feedback
- **Active state**: Bright, full opacity
- **Inactive state**: Gray, lower opacity
- **Touch feedback**: Button highlights on press

---

## Advanced Features

### Tab Switching (Optional)
Each tab can send a unique MIDI note when touched (currently commented out in the JSON):
- T1: Note 40 on Ch. 3 (example)
- T2: Note 41 on Ch. 4
- T3: Note 42 on Ch. 5
- T4: Note 43 on Ch. 6
- MST: Note 44 on Ch. 3

**Use case**: Auto‑select corresponding track in Ableton when switching tabs.

### Shared Controls
All tabs have access to:
- Global Play/Stop buttons (Ch. 3)
- Global Metronome toggle (Ch. 3)
- Metronome volume knob (shared widget)

---

## Troubleshooting

### Issue: Double triggers during mapping
**Solution**: Ensure the root `onTouch` code is commented out.

### Issue: Speed knob jumps to wrong values
**Solution**: Verify the range is set to 3–124, not 0–127.

### Issue: Controls triggering wrong tracks
**Solution**: Clear all MIDI mappings and re‑map fresh, paying attention to the correct MIDI channel.

### Issue: No response from a specific track
**Solution**: Confirm your DAW is listening on the corresponding MIDI channel (3–6). Check that the MIDI target in Open Stage Control is set to `midi:daw`.

---

## MIDI Monitor Tools

To verify MIDI signals are being sent correctly:

### Windows
- [MIDI‑OX](http://www.midiox.com/)
- [MIDIView](https://hautetechnique.com/midi/midiview/)

### macOS
- [MIDI Monitor](https://www.snoize.com/MIDIMonitor/)

### Linux
```bash
aseqdump -p [port number]
```

### Web‑based
- [WebMIDI Test Page](https://www.onlinemusictools.com/webmiditest/)

---

## Customizing MIDI Signals

To change MIDI signals, edit `Multitrack-Looper.json`.

### Example: Change a Play Button’s MIDI Note & Channel

Find:
```json
{
  "id": "play_btn_1",
  "address": "/control",
  "preArgs": [3, 60],
  ...
}
```

Change to:
```json
{
  "id": "play_btn_1",
  "address": "/control",
  "preArgs": [5, 48],   // Now sends Note 48 on Channel 5
  ...
}
```

### Example: Change a Volume CC

Find:
```json
{
  "id": "volume_fader_1",
  "address": "/control",
  "preArgs": [3, 7],
  ...
}
```

Change to:
```json
{
  "id": "volume_fader_1",
  "address": "/control",
  "preArgs": [4, 20],   // Now sends CC 20 on Channel 4
  ...
}
```

**Remember**: Update your DAW mappings after changing signals!

---

## Reference: MIDI CC Standard Usage

Common CC numbers and their typical uses:

| CC | Standard Use | TouchLooper Use |
|----|--------------|-----------------|
| 1  | Modulation   | Master Tempo (Ch.3) |
| 2  | Breath       | Master Volume (Ch.3) |
| 7  | Volume       | T1 Volume (Ch.3) |
| 8  | Balance      | T2 Volume (Ch.4) |
| 9  | -            | T3 Volume (Ch.5) |
| 10 | Pan          | T4 Volume (Ch.6) |
| 11 | Expression   | T1 Feedback (Ch.3) |
| 20 | General Purpose | Looper Speed (Ch.3) |
| 91 | Reverb       | T1 Reverb (Ch.3) |
| 92 | Tremolo      | T1 Delay (Ch.3) |
| 93 | Chorus       | T1 Double (Ch.3) |

We use non‑standard mappings where necessary to avoid conflicts with DAW defaults.

---

**File**: `Multitrack-Looper.json`  
**Version**: 1.0.0 (Channel‑shifted)  
**Last Updated**: July 1, 2026