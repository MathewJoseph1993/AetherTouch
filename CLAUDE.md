# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

AetherTouch is a touchless interactive 3D particle system using hand gesture recognition. It's a **single-file HTML application** (`index.html`) with no build process, package manager, or external dependencies beyond CDN-hosted libraries.

## Development

**No build system** - This is a single HTML file with CDN dependencies.
- No `npm install`, no bundler, no tests, no linting
- Just serve and refresh browser to see changes

### Running the Application

Serve over HTTP/HTTPS (required for camera access):

```bash
# Python
python3 -m http.server 8000

# Node.js
npx serve .

# VS Code: Right-click index.html -> "Open with Live Server"
```

### Keyboard Shortcuts
- **SPACEBAR**: Reset position, scale, rotation (same as Namaste gesture)

## Architecture

### Single-File Structure
All code lives in `index.html` (~1320 lines):
- **Lines 1-210**: HTML structure and embedded CSS
- **Lines 210-345**: Utility classes (`OneEuroFilter`, `GestureDebouncer`)
- **Lines 345-380**: Fingerpose gesture definitions
- **Lines 380-470**: Configuration, filters, debouncers, state object
- **Lines 470-660**: Three.js setup and shape generators
- **Lines 700-1120**: MediaPipe hand tracking and gesture processing (`onResults`)
- **Lines 1120-1280**: Animation loop with momentum, visual feedback
- **Lines 1280+**: Event handlers

### Core Technologies
- **Three.js (r128)**: 3D rendering with BufferGeometry particle system (5000 particles)
- **MediaPipe Hands**: Real-time hand landmark detection (up to 2 hands)
- **Fingerpose (0.1.0)**: Custom gesture recognition (pinch, open_hand, fist)
- **Vanilla JavaScript**: No frameworks

### Filtering & Smoothing System
- **OneEuroFilter**: Adaptive low-pass filter for position smoothing
- **GestureDebouncer**: Temporal filtering to prevent rapid state transitions
- **Hysteresis thresholds**: Different enter/exit thresholds for pinch detection (0.55/0.40)
- **Fingerpose boost**: Adds up to 15% to pinch detection, 30% to tension

### State Management
Global `state` object tracks:
- Hand detection flags (`handDetected`, `twoHandsDetected`)
- Gesture states (`isPinching`, `isGrabbing`, `isDoublePinching`, `isSteering`)
- Transform values (`objectOffset`, `objectRotation`, `twoHandScale`)
- Smoothed input values (`tension`, `pinchStrength`, `hand2PinchStrength`)
- Hand identity tracking (`primaryHandLabel`) to prevent swap issues
- Momentum state (`velocity`, `angularVelocity`, `momentumActive`)
- Fingerpose scores (`gestureScores`, `gestureScores2`)
- Namaste cooldown (`namasteCooldownUntil`)

### Gesture Priority (highest to lowest)
1. **Namaste Reset**: Palm distance < 0.28 → reset all transforms and filters (500ms cooldown)
2. **Double Pinch Zoom**: Both hands pinching → elastic zoom with glow effect
3. **Two-Hand Steering**: One hand pinching, other open → rotate Z-axis
4. **Single Pinch Grab**: One hand pinching → drag and rotate with momentum on release
5. **Idle**: No pinch → breathing animation, auto-rotation

## Key Code Locations

| Function/Class | Purpose |
|----------------|---------|
| `OneEuroFilter` | Adaptive smoothing for hand positions |
| `GestureDebouncer` | Temporal filtering for gesture states |
| `pinchGesture`, `fistGesture` | Fingerpose gesture definitions |
| `gestureEstimator` | Fingerpose estimator instance |
| `onResults(results)` | Processes MediaPipe landmarks, detects gestures |
| `animate()` | Main render loop, applies transforms, momentum, visual feedback |
| `switchShape(name)` | Morphs particles to target shape |
| `shapes.*` | Shape generators (sphere, heart, flower, saturn, buddha, fireworks) |

## Visual Feedback System
- **Grab**: Warm orange color shift (30% tint)
- **Zoom**: White glow + 40% larger particles
- **High Tension**: Red color shift + position jitter + size pulsing
- **Momentum**: Object glides after release (friction 0.92)

## Coding Standards

- **KISS Architecture**: Single-file, no frameworks
- **Performance**: Pre-allocate arrays, minimize GC in animation loop
- **Smoothing**: Use lerp (0.08-0.15) for visual transitions, OneEuroFilter for input
- **Pinch Detection**: Use hysteresis (enter: 0.55, exit: 0.40) with debouncing
- **Fingerpose**: Boost-only mode (don't replace distance detection)
- **Gesture Transitions**: Always reset filters/debouncers when switching modes

## Branch Workflow

- `main` is protected, requires PR
- Feature branches: `feature/name` or `fix/description`
- Target 60 FPS for smooth gesture interactions
