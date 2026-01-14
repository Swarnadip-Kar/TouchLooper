# Changelog

All notable changes to TouchLooper will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [1.0.0] - 2026-01-14

### Added
- Initial release with 4-track looper interface
- Complete T1-T4 layout with identical control patterns
- Master tab (MST) with global controls
- Looper speed control with symmetric range (3-124 for -3.00 to +3.00)
- Master tempo control (CC 1)
- Individual track controls: Play, Stop, Overdub, Undo, Clear, Double
- Per-track FX: Reverb and Delay knobs
- Per-track Volume fader and Feedback knob
- Global controls: Master Play, Master Stop, Metronome toggle
- Master volume control on MST tab
- 40+ unique MIDI signals properly mapped
- Touch-optimized button sizes for live performance
- Color-coded interface (green/red/orange/purple)

### Technical Details
- All signals on MIDI Channel 1
- Note-based control for buttons (60-83)
- CC-based control for knobs/faders (1-102)
- JSON configuration with 5,000+ lines
- OSC protocol support
- Cross-platform compatibility

### Design Decisions
- Looper speed range 3-124 (avoids edge case asymmetry)
- Root onTouch code commented out (prevents ghost signals during mapping)
- Sequential MIDI note numbering for easy memorization
- Separated CC ranges to prevent conflicts

---

## [Unreleased]

### Planned Features
- Visual feedback for loop recording status
- Preset save/recall system
- Support for 8+ tracks with pagination
- BPM tap tempo control
- Gesture support (long-press, swipe)
- Waveform display integration

---

**Legend:**
- `Added` - New features
- `Changed` - Changes in existing functionality
- `Deprecated` - Soon-to-be removed features
- `Removed` - Removed features
- `Fixed` - Bug fixes
- `Security` - Security fixes
