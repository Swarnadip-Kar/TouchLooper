# TouchLooper Setup Guide

Complete installation and configuration guide for TouchLooper MIDI controller.

## Table of Contents

1. [System Requirements](#system-requirements)
2. [Software Installation](#software-installation)
3. [MIDI Port Setup](#midi-port-setup)
4. [Open Stage Control Configuration](#open-stage-control-configuration)
5. [Ableton Live Mapping](#ableton-live-mapping)
6. [Testing](#testing)
7. [Troubleshooting](#troubleshooting)

---

## System Requirements

### Computer
- **OS**: Windows 10/11, macOS 10.14+, or Linux
- **RAM**: 4GB minimum (8GB recommended for Ableton)
- **CPU**: Dual-core 2.0GHz or better
- **Network**: WiFi (for remote device access)

### Mobile Device (Optional)
- **OS**: Android 6.0+ or iOS 12+
- **Screen**: 7-10 inch recommended (phone works but smaller)
- **Browser**: Chrome, Safari, or Firefox

### Software
- Open Stage Control v1.29.8+
- Ableton Live (any version with Looper device)
- Virtual MIDI port driver

---

## Software Installation

### Open Stage Control

**Windows:**
1. Download from [openstagecontrol.ammd.net](https://openstagecontrol.ammd.net/download/)
2. Extract ZIP to `C:\Program Files\OpenStageControl`
3. Run `open-stage-control.exe`

**macOS:**
1. Download DMG file
2. Drag to Applications
3. Right-click → Open (first time, to bypass security)

**Linux:**
```bash
wget https://github.com/jean-emmanuel/open-stage-control/releases/download/v1.29.8/open-stage-control-1.29.8-linux-x64.zip
unzip open-stage-control-1.29.8-linux-x64.zip
cd open-stage-control
./open-stage-control
```

---

## MIDI Port Setup

### Windows - loopMIDI

1. Download [loopMIDI](https://www.tobias-erichsen.de/software/loopmidi.html)
2. Install and launch
3. Create new port: Name it "TouchLooper"
4. Port appears in Ableton's MIDI preferences

### macOS - IAC Driver

1. Open **Audio MIDI Setup** (Spotlight → "Audio MIDI")
2. **Window** → **Show MIDI Studio**
3. Double-click **IAC Driver**
4. Check **"Device is online"**
5. Port name: "IAC Driver Bus 1"

### Linux - ALSA

Already available, no setup needed.

```bash
# List MIDI ports
aconnect -l
```

---

## Open Stage Control Configuration

### Launch OSC with MIDI

**Windows:**
```cmd
cd C:\Program Files\OpenStageControl
open-stage-control.exe -p 8080 -s "midi:TouchLooper"
```

**macOS:**
```bash
open-stage-control -p 8080 -s "midi:IAC Driver Bus 1"
```

**Linux:**
```bash
./open-stage-control -p 8080 -s "midi:ALSA_PORT_NAME"
```

### Load Session

1. Open browser: `http://localhost:8080`
2. Click **Browse** (top-left)
3. Navigate to `Multitrack-Looper.json`
4. Click **Load**
5. Interface appears with 5 tabs (T1, T2, T3, T4, MST)

### Remote Access (Smartphone)

1. Find computer IP address:
   - **Windows**: `ipconfig` in Command Prompt
   - **macOS**: System Preferences → Network
   - **Linux**: `ip addr show`

2. On smartphone (same WiFi):
   - Open browser
   - Go to `http://COMPUTER_IP:8080`
   - Example: `http://192.168.1.100:8080`

3. Add to home screen:
   - **iOS**: Share → Add to Home Screen
   - **Android**: Menu → Add to Home Screen

---

## Ableton Live Mapping

### Prepare Ableton

1. **Preferences** → **Link/Tempo/MIDI**
2. Find your virtual MIDI port (TouchLooper / IAC Driver)
3. Enable **Track** and **Remote**
4. Click **OK**

### Create Tracks

1. Create 4 audio tracks (Cmd/Ctrl + T × 4)
2. Name them: Track 1, Track 2, Track 3, Track 4
3. Add **Looper** device to each track (from Audio Effects)
4. Ensure all loopers visible on screen

### MIDI Mapping Process

#### Enter MIDI Map Mode
Click **MIDI** button (top-right) - interface highlights in blue

#### Map Track 1

**Looper Controls:**
1. Click **Looper Play button** → Press **T1 Play** → Shows "Note Ch. 1 60"
2. Click **Looper Stop button** → Press **T1 Stop** → Shows "Note Ch. 1 61"
3. Click **Looper Overdub button** → Press **T1 Overdub** → Shows "Note Ch. 1 62"
4. Click **Looper Undo** → Press **T1 Undo** → Shows "Note Ch. 1 64"
5. Click **Looper Clear** → Press **T1 Clear** → Shows "Note Ch. 1 65"

**Mixing:**
1. Click **Track 1 Volume** → Move **T1 Volume fader** → Shows "Ctrl Ch. 1 7"
2. Click **Send A knob** → Move **T1 Reverb knob** → Shows "Ctrl Ch. 1 91"
3. Click **Send B knob** → Move **T1 Delay knob** → Shows "Ctrl Ch. 1 92"

#### Map Tracks 2, 3, 4

Repeat same process for each track using their respective tabs.

**Track 2**: Notes 66-71, CC 8, 94, 95  
**Track 3**: Notes 72-77, CC 9, 97, 98  
**Track 4**: Notes 78-83, CC 10, 100, 101

#### Map Master Controls (MST Tab)

1. Create **Return Track A** (Reverb) and **Return Track B** (Delay)
2. **Global Play** (Note 58) → Scene Launch or Master Play
3. **Global Stop** (Note 57) → Stop All Clips button
4. **Looper Speed** (CC 20) → Any Looper's Speed knob
5. **Master Tempo** (CC 1) → Tempo control

#### Exit MIDI Map Mode
Click **MIDI** button again to save mappings

### Save Your Setup

**File** → **Save Live Set As** → Name it (e.g., "TouchLooper Setup")

All mappings are now saved with this project.

---

## Testing

### Quick Test Checklist

- [ ] T1 Play button starts Track 1 looper
- [ ] T1 Stop button stops immediately
- [ ] T1 Overdub enables overdubbing (button turns orange)
- [ ] T1 Volume fader controls track volume
- [ ] T1 Reverb/Delay knobs affect sound
- [ ] Repeat for T2, T3, T4
- [ ] Master volume faders work on MST tab
- [ ] Global Play/Stop work from any tab
- [ ] Looper Speed knob changes loop speed
- [ ] Master Tempo knob changes BPM

### Full Test Procedure

1. **Arm Track 1** (click track arm button)
2. **Press T1 Play** → Should show red recording circle in Looper
3. **Play notes/audio** into the loop
4. **Press T1 Play again** → Recording stops, playback starts
5. **Press T1 Overdub** → Button turns orange, overdub enabled
6. **Add more notes** → Layers on top of existing loop
7. **Press T1 Stop** → Immediate stop
8. **Press T1 Play** → Restarts from beginning
9. **Press T1 Undo** → Removes last overdub layer
10. **Press T1 Clear** → Clears entire loop

If all steps work, mapping is successful!

---

## Troubleshooting

### No MIDI Received in Ableton

**Symptoms**: Buttons don't trigger anything

**Solutions**:
1. Check MIDI port enabled in Ableton Preferences
2. Verify OSC launched with correct `-s midi:PORT` flag
3. Restart both OSC and Ableton
4. Use MIDI monitor tool to verify signals being sent

### Ghost Signals During Mapping

**Symptoms**: Extra MIDI signals appear when switching tabs

**Solution**: Root onTouch code is already commented out in the file. If you see issues:
1. Edit session in text editor
2. Verify root `onTouch` contains `//` comment markers
3. Save and reload

### Can't Access from Smartphone

**Symptoms**: Browser can't connect to `http://IP:8080`

**Solutions**:
1. Ensure both devices on **same WiFi network** (not guest network)
2. Check firewall allows port 8080
3. Try computer's IP address, not computer name
4. Restart router if needed
5. Try accessing locally first (`localhost:8080`) to verify OSC running

### Speed Knob Jumps to Wrong Values

**Symptoms**: Speed knob shows -3.20 or values beyond +3.00

**Solution**: This is already fixed in the provided file (range 3-124). If you modified it:
1. Open session file in text editor
2. Find `looper_speed` widget
3. Verify: `"range": {"min": 3, "max": 124}`
4. Save and reload

### Controls Triggering Wrong Track

**Symptoms**: T1 button triggers T2 looper

**Solutions**:
1. Enter MIDI Map Mode in Ableton
2. Right-click ALL existing mappings → Delete
3. Exit MIDI Map Mode
4. Restart Ableton
5. Re-map everything fresh from T1 to T4

### Interface Too Small on Phone

**Solutions**:
1. Use landscape orientation
2. Use tablet instead of phone (recommended: 7-10 inch)
3. Zoom out in browser (pinch gesture)
4. Consider customizing button sizes in JSON

---

## Performance Tips

### Optimize Latency
1. Use wired connection when possible (vs. WiFi)
2. Set Ableton buffer size to 128-256 samples
3. Close unnecessary browser tabs on smartphone
4. Disable browser animations in OSC settings

### Live Performance Checklist
- [ ] All MIDI mappings tested
- [ ] Ableton project saved
- [ ] Smartphone fully charged
- [ ] Smartphone in "Do Not Disturb" mode
- [ ] WiFi network stable (or use localhost)
- [ ] Backup MIDI controller available (just in case)

### Recommended Ableton Setup
- **Tempo**: Set to your performance BPM
- **Metronome**: Enabled and routed to headphones
- **Return Tracks**: A = Reverb, B = Delay
- **Looper Settings**: Set feedback to 100% initially
- **Save as Template**: For quick load next time

---

## Next Steps

- Read [MIDI Mappings Documentation](midi-mappings.md) for complete reference
- Customize colors and layout (edit JSON file)
- Explore master speed control for creative effects
- Practice switching between tabs during performance

**Need help?** Open an issue on GitHub!
