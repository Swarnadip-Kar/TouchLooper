# TouchLooper - TODO List

## High Priority

### UI/UX Improvements
- [ ] **Round UI buttons and sharp edges**
  - Add `borderRadius` property to all buttons
  - Smooth out panel corners
  - Apply rounded corners to knobs and faders
  - Target: Consistent 8-12px border radius across interface
  - Files to modify: `Multitrack-Looper.json` (all button widgets)

- [ ] **Transform T4 into Live Instrument Control Tab**
  - Replace looper controls with synth/instrument parameters
  - Add cutoff knob (CC assignment needed)
  - Add resonance knob
  - Add ADSR envelope controls (Attack, Decay, Sustain, Release)
  - Add LFO rate control
  - Add pitch bend slider
  - Add modulation wheel control
  - Keep volume fader for instrument output level
  - Rename tab from "T4" to "INST" or "SYNTH"

---

## Medium Priority

### Visual Enhancements
- [ ] Add gradient backgrounds to panels
- [ ] Implement LED-style indicators for recording status
- [ ] Add visual feedback for active loops (waveform display)
- [ ] Create custom color themes (dark mode, light mode)
- [ ] Add animation transitions for button state changes

### Functional Improvements
- [ ] BPM tap tempo button on master tab
- [ ] Preset save/recall system (save current settings)
- [ ] MIDI learn mode for easy remapping
- [ ] Long-press gestures for secondary functions
- [ ] Swipe gestures for tab navigation

### Master Tab Enhancements
- [ ] Add global reverb/delay send controls
- [ ] Add master EQ controls (low, mid, high)
- [ ] Add visual BPM display (larger, more prominent)
- [ ] Add beat/bar counter display

---

## Low Priority

### Documentation
- [ ] Create video tutorial for setup
- [ ] Add Logic Pro X mapping guide
- [ ] Add FL Studio mapping guide
- [ ] Create FAQ section
- [ ] Add troubleshooting flowchart

### Advanced Features
- [ ] Support for 8 tracks (with pagination)
- [ ] Scene launch buttons for Ableton
- [ ] Clip launch grid integration
- [ ] MIDI clock sync visualization
- [ ] Waveform display per track

---

## Technical Debt

- [ ] Optimize JSON file size (currently ~215KB)
- [ ] Refactor repeated widget code into templates
- [ ] Add widget ID validation script
- [ ] Create automated MIDI mapping export
- [ ] Add unit tests for MIDI signal ranges

---

## Ideas for Future Versions

### v1.1.0 - UI Polish + Instrument Control
- Round UI buttons
- T4 → Instrument control tab
- BPM tap tempo
- Visual recording indicators

### v1.2.0 - Advanced Features
- Preset system
- MIDI learn mode
- Gesture controls
- Custom themes

### v2.0.0 - Major Redesign
- 8-track support
- Waveform displays
- Scene/clip launch integration
- Complete UI overhaul

---

## Design Specifications for Rounded UI

### Button Border Radius Values
```json
{
  "type": "button",
  "borderRadius": "12px",  // Large buttons (Play, Stop)
  "borderRadius": "8px",   // Medium buttons (Undo, Clear)
  "borderRadius": "6px"    // Small buttons
}
```

### Panel Border Radius
```json
{
  "type": "panel",
  "borderRadius": "10px"   // All panels
}
```

### Knob/Fader Rounding
```json
{
  "type": "knob",
  "borderRadius": "50%"    // Perfect circles
}
```

---

## T4 Instrument Control - Proposed Layout

### Top Section - Filter Controls
- **Cutoff Knob**: CC 74 (standard filter cutoff)
- **Resonance Knob**: CC 71 (standard filter resonance)
- **Filter Type Switch**: LP/HP/BP

### Middle Section - Envelope (ADSR)
- **Attack Knob**: CC 73
- **Decay Knob**: CC 75
- **Sustain Knob**: CC 79
- **Release Knob**: CC 72

### Bottom Section - Modulation
- **LFO Rate Knob**: CC 76
- **LFO Depth Knob**: CC 77
- **Pitch Bend Slider**: Pitch bend message
- **Mod Wheel Slider**: CC 1

### Side Section
- **Volume Fader**: CC 10 (keep existing)
- **Pan Knob**: CC 10 (stereo positioning)

### MIDI Mapping Reference
```
Cutoff: CC 74 (MIDI standard for brightness)
Resonance: CC 71 (MIDI standard)
Attack: CC 73
Decay: CC 75
Sustain: CC 79 (LSB)
Release: CC 72
LFO Rate: CC 76
LFO Depth: CC 77
Mod Wheel: CC 1 (MIDI standard)
Volume: CC 10 (existing T4 volume)
```

---

## Implementation Steps

### Step 1: Round UI Buttons
1. Open `Multitrack-Looper.json` in text editor
2. Find all button widgets (search for `"type": "button"`)
3. Add `"borderRadius": "12px"` property to each
4. Find all panels (search for `"type": "panel"`)
5. Add `"borderRadius": "10px"` to each
6. Test in Open Stage Control
7. Commit changes

### Step 2: Convert T4 to Instrument Tab
1. Create new branch: `git checkout -b feature/instrument-tab`
2. Rename T4 tab to "INST"
3. Remove looper-specific buttons (Play, Stop, Overdub, etc.)
4. Add 8 knobs for synth parameters
5. Add 2 sliders for pitch/mod
6. Update MIDI mappings to standard CC numbers
7. Test with synthesizer in Ableton
8. Update documentation
9. Commit and merge

---

## Notes

- Prioritize UI rounding first (quick visual improvement)
- T4 instrument conversion is a bigger feature (plan carefully)
- Consider keeping T3 for loopers, add T5 for instruments instead?
- Get feedback from live performance before major changes

---

**Last Updated**: January 14, 2026  
**Version**: 1.0.0  
**Project**: TouchLooper