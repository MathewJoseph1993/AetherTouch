# Branding Guidelines

This document serves as the design source of truth for the **Particle Morph** project. All future UI additions, marketing assets, or code expansions should adhear to these guidelines to maintain the project's premium, futuristic aesthetic.

## 1. Visual Philosophy
**"Neon Glass"**: The design language combines deep, void-like backgrounds with vibrant, neon-cyberspace accents and frosted glass surfaces. The goal is to feel immersive, modern, and reactive.

*   **Dark & Deep**: The environment is never white; it is always a deep shade of black/gray to make particles pop.
*   **Translucency**: UI elements should never be opaque solid blocks. They must float and blur the content behind them.
*   **Vibrancy**: Use high-saturation colors for interactive elements and data.

## 2. Color Palette

### Primary Colors
These define the brand identity and the default state of the particles.

| Role | Hex | RGB | Usage |
| :--- | :--- | :--- | :--- |
| **Primary Cyan** | `#00f3ff` | `0, 243, 255` | Default particles, active states, key highlights |
| **Electric Purple** | `#bc13fe` | `188, 19, 254` | Accents, gradients, secondary highlights |
| **Deep Void** | `#050505` | `5, 5, 5` | Global background color |

### Interface Colors

| Role | Value | Description |
| :--- | :--- | :--- |
| **Glass Panel** | `rgba(20, 20, 30, 0.7)` | Main UI background. Must be paired with `backdrop-filter: blur(10px)`. |
| **Text Main** | `#ffffff` | Primary readable text. |
| **Text Muted** | `#aaaaaa` | Instructions, status messages. |
| **Border** | `rgba(255, 255, 255, 0.1)` | Subtle definition for glass panels and buttons. |

## 3. Typography

**Font Family**: `Segoe UI, Tahoma, Geneva, Verdana, sans-serif`
*System fonts are preferred to reduce load times while maintaining a clean, digital look.*

*   **Headings**: Bold (`700`), often featuring a linear gradient text mask (`90deg` from Primary to Accent).
*   **Body**: Regular (`400`) or Medium (`500`).
*   **Status/Labels**: Small sizes (`0.8rem`), often uppercase or slightly spaced.

## 4. UI Components

### Glass Panels
All containers (menus, controls) must use the glassmorphism effect:
```css
background: var(--panel-bg); /* rgba(20, 20, 30, 0.7) */
backdrop-filter: blur(10px);
border: 1px solid rgba(255, 255, 255, 0.1);
border-radius: 16px;
box-shadow: 0 8px 32px 0 rgba(0, 0, 0, 0.37);
```

### Buttons
*   **Default**: Transparent background, 1px subtle white border (`0.1` opacity).
*   **Hover**: Increase background opacity (`0.15`), increase border opacity (`0.3`).
*   **Active**: Linear Gradient (`135deg` Primary to Accent), Text becomes Black or Dark Blue for contrast, Border removed.

## 5. Particle Behavior (Motion Design)
*   **Idle**: Gentle breathing or slow rotation. Never completely static.
*   **Reaction**: Smooth interpolation (`lerp`). No instant snaps.
*   **Tension**: High tension (closed hand) maps to high frequency movement (shake/jitter) or compression.
