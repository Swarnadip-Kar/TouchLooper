# Contributing to TouchLooper

Thank you for your interest in contributing! This document provides guidelines for contributing to TouchLooper.

## How Can I Contribute?

### Reporting Bugs

Before creating bug reports, please check existing issues to avoid duplicates.

**When reporting a bug, include:**
- **Description**: Clear description of the problem
- **Steps to reproduce**: Exact steps to reproduce the behavior
- **Expected behavior**: What you expected to happen
- **Actual behavior**: What actually happened
- **Screenshots**: If applicable
- **Environment**:
  - OS (Windows/macOS/Linux)
  - Open Stage Control version
  - DAW and version
  - Browser and version (if using remote device)

**Example bug report:**
```markdown
## Bug: Play button not responding on T2

**Steps to reproduce:**
1. Load Multitrack-Looper.json
2. Navigate to T2 tab
3. Press Play button
4. No MIDI signal sent

**Expected:** Should send MIDI Note 66
**Actual:** No signal sent

**Environment:**
- Windows 11
- Open Stage Control 1.29.8
- Ableton Live 11
- Chrome 120
```

### Suggesting Enhancements

Enhancement suggestions are welcome! Please:

1. **Check existing issues** for similar suggestions
2. **Describe the feature** clearly
3. **Explain the use case** (why it's needed)
4. **Provide examples** of how it would work

### Pull Requests

1. **Fork the repository**
2. **Create a feature branch**
   ```bash
   git checkout -b feature/amazing-feature
   ```
3. **Make your changes**
4. **Test thoroughly**
5. **Commit with clear messages**
   ```bash
   git commit -m "Add BPM tap tempo to master tab"
   ```
6. **Push to your fork**
   ```bash
   git push origin feature/amazing-feature
   ```
7. **Open a Pull Request**

## Code Style Guidelines

### JSON Formatting

- Use 2-space indentation
- Keep consistent naming conventions:
  - Widget IDs: `snake_case` (e.g., `play_btn_1`)
  - Labels: Title Case with symbols (e.g., `"▶\nPlay"`)
- Group related widgets together
- Maintain color consistency (green=play, red=stop, orange=overdub)

### Documentation

- Use clear, concise language
- Include code examples where applicable
- Keep screenshots up-to-date
- Follow Markdown best practices

## Development Workflow

### Testing Your Changes

Before submitting a PR:

1. **Load the session file** in Open Stage Control
2. **Test all modified controls** on all tabs
3. **Verify MIDI signals** using a MIDI monitor
4. **Test on multiple devices** (if possible)
5. **Check for regressions** (existing features still work)

### Version Numbering

We follow [Semantic Versioning](https://semver.org/):

- **Major** (1.0.0): Breaking changes (e.g., complete redesign)
- **Minor** (1.1.0): New features, backwards-compatible
- **Patch** (1.1.1): Bug fixes only

### Changelog

Update `CHANGELOG.md` with your changes:

```markdown
## [Unreleased]

### Added
- BPM tap tempo control on master tab

### Fixed
- Speed knob jumping to edge values
```

## Project Structure

```
touchlooper/
├── Multitrack-Looper.json         # Main session file
├── README.md                       # Main documentation
├── CHANGELOG.md                    # Version history
├── LICENSE                         # MIT License
├── CONTRIBUTING.md                 # This file
├── VERSION_MANAGEMENT.md           # Version control guide
└── docs/
    ├── setup-guide.md              # Setup instructions
    └── midi-mappings.md            # MIDI reference
```

## Areas for Contribution

### High Priority
- [ ] Visual feedback for recording status (LED indicators)
- [ ] BPM tap tempo button
- [ ] Preset save/recall system
- [ ] Better mobile responsive design
- [ ] Gesture support (long-press, swipe)

### Medium Priority
- [ ] Support for 8+ tracks
- [ ] Waveform display integration
- [ ] Custom color themes
- [ ] MIDI learn mode

### Documentation
- [ ] Video tutorials
- [ ] More DAW setup guides (Logic Pro, FL Studio, Reaper)
- [ ] Translation to other languages
- [ ] Troubleshooting FAQs expansion

## Communication

- **Issues**: For bug reports and feature requests
- **Discussions**: For questions and general discussion
- **Pull Requests**: For code contributions

## License

By contributing, you agree that your contributions will be licensed under the MIT License.

## Recognition

Contributors will be acknowledged in:
- README.md (Contributors section)
- CHANGELOG.md (for specific contributions)

## Questions?

Feel free to open an issue with the question label!

---

**Thank you for contributing!** 🎵
