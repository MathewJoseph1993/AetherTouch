# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

AetherTouch is a touchless interactive 3D particle system using hand gesture recognition. It's a **single-file HTML application** (`index.html`) with no build process, package manager, or external dependencies beyond CDN-hosted libraries.

## Running the Application

Serve over HTTP/HTTPS (required for camera access):

```bash
# Python
python3 -m http.server 8000

# Node.js
npx serve .

# VS Code: Right-click index.html -> "Open with Live Server"
```

## Architecture

### Single-File Structure
All code lives in `index.html` (~1200 lines):
- **Lines 1-260**: HTML structure and embedded CSS
- **Lines 260-340**: Utility classes (`OneEuroFilter`, `GestureDebouncer`)
- **Lines 340-410**: Configuration and global state object
- **Lines 410-620**: Three.js setup and shape generators
- **Lines 620-1010**: MediaPipe hand tracking and gesture processing (`onResults`)
- **Lines 1010-1180**: Animation loop and event handlers

### Core Technologies
- **Three.js (r128)**: 3D rendering with BufferGeometry particle system (5000 particles)
- **MediaPipe Hands**: Real-time hand landmark detection (up to 2 hands)
- **Vanilla JavaScript**: No frameworks

### Filtering & Smoothing System
- **OneEuroFilter**: Industry-standard adaptive low-pass filter for position smoothing
- **GestureDebouncer**: Temporal filtering to prevent rapid state transitions
- **Hysteresis thresholds**: Different enter/exit thresholds for pinch detection (0.65/0.50)

### State Management
Global `state` object tracks:
- Hand detection flags (`handDetected`, `twoHandsDetected`)
- Gesture states (`isPinching`, `isGrabbing`, `isDoublePinching`, `isSteering`)
- Transform values (`objectOffset`, `objectRotation`, `twoHandScale`)
- Smoothed input values (`tension`, `pinchStrength`, `hand2PinchStrength`)
- Hand identity tracking (`primaryHandLabel`) to prevent swap issues

### Gesture Priority (highest to lowest)
1. **Namaste Reset**: Palm distance < 0.15 → reset all transforms and filters
2. **Double Pinch Zoom**: Both hands pinching → elastic zoom
3. **Two-Hand Steering**: One hand pinching, other open → rotate Z-axis
4. **Single Pinch Grab**: One hand pinching → drag and rotate
5. **Idle**: No pinch → breathing animation, auto-rotation

## Key Code Locations

| Function/Class | Purpose |
|----------------|---------|
| `OneEuroFilter` | Adaptive smoothing for hand positions |
| `GestureDebouncer` | Temporal filtering for gesture states |
| `onResults(results)` | Processes MediaPipe landmarks, detects gestures |
| `animate()` | Main render loop, applies transforms |
| `switchShape(name)` | Morphs particles to target shape |
| `shapes.*` | Shape generators (sphere, heart, flower, saturn, buddha, fireworks) |

## Coding Standards

- **KISS Architecture**: Single-file, no frameworks
- **Performance**: Pre-allocate arrays, minimize GC in animation loop
- **Smoothing**: Use lerp (0.08-0.15) for visual transitions, OneEuroFilter for input
- **Pinch Detection**: Use hysteresis (enter: 0.65, exit: 0.50) with debouncing
- **Gesture Transitions**: Always reset filters/debouncers when switching modes

## Branch Workflow

- `main` is protected, requires PR
- Feature branches: `feature/name` or `fix/description`
- Target 60 FPS for smooth gesture interactions
