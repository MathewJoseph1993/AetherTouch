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
All code lives in `index.html` (~1000 lines):
- **Lines 1-250**: HTML structure and embedded CSS
- **Lines 250-300**: Global state object and config
- **Lines 300-530**: Three.js setup and shape generators
- **Lines 530-860**: MediaPipe hand tracking and gesture processing (`onResults`)
- **Lines 860-1000**: Animation loop and event handlers

### Core Technologies
- **Three.js (r128)**: 3D rendering with BufferGeometry particle system (5000 particles)
- **MediaPipe Hands**: Real-time hand landmark detection (up to 2 hands)
- **Vanilla JavaScript**: No frameworks

### State Management
Global `state` object tracks:
- Hand detection flags (`handDetected`, `twoHandsDetected`)
- Gesture states (`isPinching`, `isGrabbing`, `isDoublePinching`, `isSteering`)
- Transform values (`objectOffset`, `objectRotation`, `twoHandScale`)
- Smoothed input values (`tension`, `pinchStrength`, `hand2PinchStrength`)

### Gesture Priority (highest to lowest)
1. **Namaste Reset**: Palm distance < 0.2 → reset all transforms
2. **Double Pinch**: Both hands pinching → elastic zoom + steering
3. **Single Pinch**: One hand → grab, drag, rotate
4. **Idle**: No pinch → breathing animation, auto-rotation

## Key Code Locations

| Function | Purpose |
|----------|---------|
| `switchShape(name)` | Morphs particles to target shape |
| `onResults(results)` | Processes MediaPipe landmarks, detects gestures |
| `animate()` | Main render loop, applies transforms |
| `shapes.*` | Shape generators (sphere, heart, flower, saturn, buddha, fireworks) |

## Coding Standards

- **KISS Architecture**: Single-file, no frameworks
- **Performance**: Pre-allocate arrays, minimize GC in animation loop
- **Smoothing**: Use lerp (0.08-0.15) for all visual transitions
- **Pinch Detection**: Smoothed threshold > 0.6 (not raw distance)

## Branch Workflow

- `main` is protected, requires PR
- Feature branches: `feature/name` or `fix/description`
- Target 60 FPS for smooth gesture interactions
