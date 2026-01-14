# Complete MIDI Mappings Reference

## Overview

- **MIDI Channel**: 1 (all signals)
- **Total Signals**: 40+ unique MIDI notes and CC messages
- **Protocol**: OSC → MIDI conversion via Open Stage Control

---

## Track-Specific Controls

### Track 1 (T1)

#### Transport (MIDI Notes)
- **Play**: Note 60 (Toggle)
- **Stop**: Note 61 (Push)
- **Overdub**: Note 62 (Toggle)
- **Undo**: Note 64 (Push)
- **Clear**: Note 65 (Push)

#### Mixing & FX (MIDI CC)
- **Volume**: CC 7 (0-127)
- **Feedback**: CC 11 (0-100)
- **Reverb**: CC 91 (0-127)
- **Delay**: CC 92 (0-127)
- **Double**: CC 93 (Push, 0-127)

### Track 2 (T2)

#### Transport (MIDI Notes)
- **Play**: Note 66
- **Stop**: Note 67
- **Overdub**: Note 68
- **Undo**: Note 70
- **Clear**: Note 71

#### Mixing & FX (MIDI CC)
- **Volume**: CC 8
- **Feedback**: CC 12
- **Reverb**: CC 94
- **Delay**: CC 95
- **Double**: CC 96

### Track 3 (T3)

#### Transport (MIDI Notes)
- **Play**: Note 72
- **Stop**: Note 73
- **Overdub**: Note 74
- **Undo**: Note 76
- **Clear**: Note 77

#### Mixing & FX (MIDI CC)
- **Volume**: CC 9
- **Feedback**: CC 13
- **Reverb**: CC 97
- **Delay**: CC 98
- **Double**: CC 99

### Track 4 (T4)

#### Transport (MIDI Notes)
- **Play**: Note 78
- **Stop**: Note 79
- **Overdub**: Note 80
- **Undo**: Note 82
- **Clear**: Note 83

#### Mixing & FX (MIDI CC)
- **Volume**: CC 10
- **Feedback**: CC 14
- **Reverb**: CC 100
- **Delay**: CC 101
- **Double**: CC 102

---

## Master Controls (MST Tab)

### Global Transport
- **Global Play**: Note 58 (Push) - Start all tracks
- **Global Stop**: Note 57 (Push) - Stop all tracks
- **Global Metronome**: Note 59 (Toggle) - Metronome on/off

### Performance Controls
- **Looper Speed**: CC 20 (Range: 3-124)
  - Maps to -3.00 to +3.00 semitones
  - Custom range avoids edge case asymmetry
- **Master Tempo**: CC 1 (Range: 0-127)
  - Controls global BPM
- **Master Volume**: Individual track faders on MST tab (CC 7-10)

---

## Quick Reference Table

| Function | T1 | T2 | T3 | T4 | Notes |
|----------|----|----|----|----|-------|
| **Play** | 60 | 66 | 72 | 78 | Toggle button |
| **Stop** | 61 | 67 | 73 | 79 | Push button |
| **Overdub** | 62 | 68 | 74 | 80 | Toggle button |
| **Undo** | 64 | 70 | 76 | 82 | Push button |
| **Clear** | 65 | 71 | 77 | 83 | Push button |
| **Volume** | CC7 | CC8 | CC9 | CC10 | Fader 0-127 |
| **Feedback** | CC11 | CC12 | CC13 | CC14 | Knob 0-100 |
| **Reverb** | CC91 | CC94 | CC97 | CC100 | Knob 0-127 |
| **Delay** | CC92 | CC95 | CC98 | CC101 | Knob 0-127 |
| **Double** | CC93 | CC96 | CC99 | CC102 | Push button |

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
  "steps": 122
}
```
**Rationale**: 
- Values 0-2 produce non-standard negative values (-3.20, -3.15, -3.10)
- Values 125-127 exceed +3.00
- Range 3-124 provides symmetric -3.00 to +3.00 semitone control

### Root OnTouch Code
Located in root widget, commented out by default:
```javascript
// switch(value) {
//   case 0: send('midi:daw', '/note', 1, 40, 127); // T1
//   case 1: send('midi:daw', '/note', 1, 41, 127); // T2
//   case 2: send('midi:daw', '/note', 1, 42, 127); // T3
//   case 3: send('midi:daw', '/note', 1, 43, 127); // T4
//   case 4: send('midi:daw', '/note', 1, 44, 127); // MST
// }
```
**Purpose**: Auto-focus corresponding track in DAW when switching tabs.  
**Important**: Keep commented during MIDI mapping to avoid ghost signals.

---

## Mapping in Ableton Live

### Step 1: Enter MIDI Map Mode
Click **MIDI** button (top-right corner)

### Step 2: Map Track 1 Looper
1. Click **Looper Play** → Press T1 Play button (sends Note 60)
2. Click **Looper Stop** → Press T1 Stop button (sends Note 61)
3. Click **Looper Overdub** → Press T1 Overdub (sends Note 62)
4. Click **Looper Undo** → Press T1 Undo (sends Note 64)
5. Click **Looper Clear** → Press T1 Clear (sends Note 65)

### Step 3: Map Track 1 Mixing
1. Click **Track Volume** → Move T1 Volume fader (sends CC 7)
2. Click **Send A** (Reverb) → Move T1 Reverb knob (sends CC 91)
3. Click **Send B** (Delay) → Move T1 Delay knob (sends CC 92)

### Step 4: Repeat for Tracks 2-4
Use same process with respective MIDI notes/CCs

### Step 5: Map Master Controls
1. Global Play (Note 58) → Master Scene Launch
2. Global Stop (Note 57) → Stop All Clips
3. Looper Speed (CC 20) → Looper Speed parameter
4. Master Tempo (CC 1) → Global Tempo

---

## Conflict Prevention

### Strategy
- **Sequential note ranges**: T1 (60-65), T2 (66-71), T3 (72-77), T4 (78-83)
- **Separated CC ranges**: Volume (7-10), Feedback (11-14), FX (91-102)
- **Global range**: 57-59 for master transport, CC 1 & 20 for tempo/speed

### Why This Works
- No overlapping MIDI values between different functions
- Predictable pattern (increment by 6 for next track)
- Easy to remember and debug

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

### Tab Switching
Each tab sends a unique MIDI note when touched (optional, currently commented):
- T1: Note 40
- T2: Note 41
- T3: Note 42
- T4: Note 43
- MST: Note 44

**Use case**: Auto-select corresponding track in Ableton when switching tabs.

### Shared Controls
All tabs have access to:
- Global Play/Stop buttons
- Global Metronome toggle
- Metronome volume knob (shared widget)

---

## Troubleshooting

### Issue: Double triggers during mapping

**Solution**: Ensure root onTouch code is commented out

### Issue: Speed knob jumps to wrong values

**Solution**: Verify range is set to 3-124, not 0-127

### Issue: Controls triggering wrong tracks

**Solution**: Clear all MIDI mappings and re-map fresh

---

## MIDI Monitor Tools

To verify MIDI signals are being sent correctly:

### Windows
- [MIDI-OX](http://www.midiox.com/)
- [MIDIView](https://hautetechnique.com/midi/midiview/)

### macOS
- [MIDI Monitor](https://www.snoize.com/MIDIMonitor/)

### Linux
```bash
aseqdump -p [port number]
```

### Web-based
- [WebMIDI Test Page](https://www.onlinemusictools.com/webmiditest/)

---

## Customizing MIDI Signals

To change MIDI signals, edit `Multitrack-Looper.json`:

### Example: Change Play Button MIDI Note

Find:
```json
{
  "id": "play_btn_1",
  "address": "/note",
  "preArgs": [1, 60],
  ...
}
```

Change to:
```json
{
  "id": "play_btn_1",
  "address": "/note",
  "preArgs": [1, 48],  // Now sends Note 48 instead
  ...
}
```

### Example: Change Volume CC

Find:
```json
{
  "id": "volume_fader_1",
  "address": "/control",
  "preArgs": [1, 7],
  ...
}
```

Change to:
```json
{
  "id": "volume_fader_1",
  "address": "/control",
  "preArgs": [1, 20],  // Now sends CC 20 instead
  ...
}
```

**Remember**: Update your DAW mappings after changing signals!

---

## Reference: MIDI CC Standard Usage

Common CC numbers and their typical uses:

| CC | Standard Use | TouchLooper Use |
|----|--------------|-----------------|
| 1 | Modulation | Master Tempo |
| 7 | Volume | T1 Volume |
| 8 | Balance | T2 Volume |
| 9 | - | T3 Volume |
| 10 | Pan | T4 Volume |
| 11 | Expression | T1 Feedback |
| 20 | General Purpose | **Looper Speed** |
| 91 | Reverb | T1 Reverb |
| 92 | Tremolo | T1 Delay |
| 93 | Chorus | T1 Double |

We use non-standard mappings where necessary to avoid conflicts with DAW defaults.

---

**File**: `Multitrack-Looper.json`  
**Version**: 1.0.0  
**Last Updated**: January 14, 2026
