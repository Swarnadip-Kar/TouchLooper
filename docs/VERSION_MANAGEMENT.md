# Version Management Guide

Guide for managing and tracking versions of TouchLooper.

## Version Structure

We use the `versions/` folder to store snapshots of each release:

```
versions/
├── v1.0/
│   ├── Multitrack-Looper.json
│   ├── CHANGELOG_v1.0.md
│   └── README_v1.0.md
├── v1.1/
│   └── ...
└── v2.0/
    └── ...
```

## Creating a New Version

### Step 1: Decide Version Number

Follow [Semantic Versioning](https://semver.org/):

- **Major (X.0.0)**: Breaking changes (e.g., complete UI redesign, incompatible MIDI changes)
- **Minor (1.X.0)**: New features, backwards-compatible (e.g., new tab, new controls)
- **Patch (1.1.X)**: Bug fixes only (e.g., fixed button position, corrected MIDI signal)

### Step 2: Create Version Folder

```bash
mkdir -p versions/v1.1
```

### Step 3: Copy Files

```bash
# Copy main session file
cp Multitrack-Looper.json versions/v1.1/

# Copy documentation (optional)
cp CHANGELOG.md versions/v1.1/CHANGELOG_v1.1.md
cp README.md versions/v1.1/README_v1.1.md
```

### Step 4: Update CHANGELOG.md

Move items from `[Unreleased]` to a new version section:

```markdown
## [1.1.0] - 2026-02-01

### Added
- BPM tap tempo button on master tab
- Visual recording indicators

### Fixed
- Speed knob jumping to edge values
- Metronome volume not persisting
```

### Step 5: Create Git Tag

```bash
git add .
git commit -m "Release v1.1.0 - Added tap tempo"
git tag -a v1.1.0 -m "Version 1.1.0 - Tap tempo and recording indicators"
git push origin main
git push origin v1.1.0
```

### Step 6: Create GitHub Release

1. Go to GitHub repository
2. Click **Releases** → **Draft a new release**
3. Choose tag: `v1.1.0`
4. Release title: `v1.1.0 - Tap Tempo & Recording Indicators`
5. Description: Copy from CHANGELOG
6. Attach: `versions/v1.1/Multitrack-Looper.json`
7. **Publish release**

## Version Comparison

To compare versions:

```bash
# Compare two JSON files
diff versions/v1.0/Multitrack-Looper.json versions/v1.1/Multitrack-Looper.json

# Or use a visual diff tool
code --diff versions/v1.0/Multitrack-Looper.json versions/v1.1/Multitrack-Looper.json
```

## Rolling Back to Previous Version

```bash
# Copy old version to main directory
cp versions/v1.0/Multitrack-Looper.json ./

# Or use git
git checkout v1.0.0 Multitrack-Looper.json
```

## Backup Before Major Changes

Before making significant changes:

```bash
# Create backup with timestamp
cp Multitrack-Looper.json "backups/backup_$(date +%Y%m%d_%H%M%S).json"
```

## Version Naming Conventions

- **Development**: `v1.1.0-dev` (work in progress)
- **Release Candidate**: `v1.1.0-rc.1` (testing phase)
- **Stable**: `v1.1.0` (official release)

## Best Practices

1. **Test thoroughly** before creating a version
2. **Document all changes** in CHANGELOG
3. **Tag commits** for easy reference
4. **Keep old versions** for rollback capability
5. **Update README** with new features
6. **Test MIDI mappings** after any changes

## Example Workflow

```bash
# Start working on new feature
git checkout -b feature/tap-tempo

# Make changes to Multitrack-Looper.json
# Test thoroughly in Open Stage Control and Ableton

# Commit changes
git add Multitrack-Looper.json
git commit -m "Add tap tempo button to master tab"

# Merge to main
git checkout main
git merge feature/tap-tempo

# Create version backup
mkdir -p versions/v1.1
cp Multitrack-Looper.json versions/v1.1/

# Update CHANGELOG
# ... edit CHANGELOG.md ...

# Commit version
git add .
git commit -m "Release v1.1.0"
git tag -a v1.1.0 -m "Version 1.1.0 - Tap tempo"
git push origin main
git push --tags
```

## File Size Tracking

Keep track of session file size growth:

```bash
# Check file size
ls -lh Multitrack-Looper.json

# Compare with previous version
ls -lh versions/*/Multitrack-Looper.json
```

Typical sizes:
- v1.0: ~75 KB
- Recommended max: <500 KB

If file grows too large, consider:
- Removing unused widgets
- Simplifying CSS
- Optimizing JSON structure

---

For questions, see [CONTRIBUTING.md](CONTRIBUTING.md)
