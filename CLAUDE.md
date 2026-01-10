# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

AetherTouch GTM is a **Revenue Operations Dashboard** built as a single-file 3D application.
It uses **Three.js** and **MediaPipe Hands** to visualize GTM data (Funnel, Journey, Globe) controlled by hand gestures.

## Architecture Improvements (Phase 8+)

### 1. The "Intelligent" Data Layer
- **`DataConnector` Class**: Handles data fetching.
    - **Adapters**: `GoogleSheetAdapter`, `LocalFileAdapter`, `MockAdapter`.
    - **`parseUnifiedData`**: Auto-maps keys like `conversion`, `revenue` to the internal schema.
    - **State**: `state.data` holds the live metrics.

### 2. Generative Shape Logic
Shapes are no longer static functions. They read `state.data` to determine geometry:
- **`funnel()`**: Uses `state.data.funnel.conversion_rate` to calculate `topRadius` vs `bottomRadius`.
- **`journey()`**: Uses `state.data.regions` to calculate spline thickness.

### 3. Contextual Geometry (SceneExtras)
- **`sceneExtras` Group**: Holds all non-particle objects (Rings, Lines). **MUST BE CLEARED** via `clearSceneExtras()` when switching shapes.
- **`activeLabels` Array**: Stores objects `{ element, position }`. The `animate()` loop projects these 3D positions to 2D CSS transform every frame.

### 4. DOM Layers
- `#canvas-container`: The Three.js WebGL canvas.
- `#labels-layer`: Container for floating 3D text labels (pointer-events: none).
- `.legend-panel`: Static UI for color coding.
- `#bottom-dock`: Glassmorphism controls.

## Development Rules

1.  **Single File**: Keep everything in `index.html`. Do not create external JS/CSS files.
2.  **No Build Step**: Must run via `python3 -m http.server` or `npx serve`.
3.  **Holographic Cleanup**: Always call `clearSceneExtras()` before drawing a new shape, or labels/rings will persist and overlap.
4.  **Vertex Colors**: The `funnel` uses vertex colors. If you need to tint it, use `material.color.lerp` in the animation loop (we enabled this in Phase 8.6).

## Key Functions

| Function | Purpose |
|----------|---------|
| `createFunnelGuides()` | Generates the cyan/orange rings and vertical struts |
| `createLabel(text, y)` | Adds a floating HTML label to the `activeLabels` array |
| `switchShape(name)` | Clears extras, resets state, and calls the shape generator |
| `animate()` | Main loop. Handles Physics -> Gestures -> **Label Projection** -> Render |

## Branch Status
- **Current**: `feature/saas-overhaul` (Stable, Phase 8 complete)
- **Next**: `release/v1.0` (Deployment)

## Commands
- **Run**: `npx serve .`
- **Deploy**: Create `vercel.json` (Phase 9)
