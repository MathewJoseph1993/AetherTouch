# AetherTouch 🌌✋

> **"Any sufficiently advanced technology is indistinguishable from magic."** - Arthur C. Clarke

**AetherTouch** is a futuristic, touchless interactive particle system that allows you to manipulate 3D objects using hand gestures, inspired by the holographic interfaces seen in movies like *Iron Man*.

<!-- TODO: Add a demo GIF or screenshot here -->

## ✨ Features

### 🦾 Iron Man Interface (The "Super-Hand")
Experience 6DoF (Six Degrees of Freedom) control without touching a screen:

| Gesture | Action | Result |
| :--- | :--- | :--- |
| **Hover** | Open Hands | **Idle / Focus** |
| **Grab** | One Hand Pinch | **Drag** objects through space |
| **Twist** | One Hand Pinch + Rotate | **Rotate** objects (Z-Axis Roll) |
| **Elastic Zoom** | **Double Pinch** (Both Hands) | **Stretch** to Zoom In, **Compress** to Zoom Out (Rate-based) |
| **Reset** | **Namaste** (Palms Together) | **Reset** position, scale, and rotation to center |

### 🧬 Particle Morphing
Seamlessly transform between mathematical and organic forms:
*   **Sphere**, **Heart**, **Flower**, **Saturn**, **Buddha**, **Fireworks**.

### 🎨 Customization
*   **Real-time Color Picker**: Paint the particles with any color.
*   **HUD Camera**: Integrated "Heads-Up Display" for immersive tracking.

## 🛠️ Technology Stack

*   **HTML5 / CSS3**: Single-file architecture.
*   **Three.js**: High-performance WebGL 3D rendering.
*   **MediaPipe Hands**: Google's real-time hand tracking ML solution.
*   **Vanilla JS**: No heavy frameworks, just pure performance.

## 🚀 How to Run

1.  **Clone the repository**:
    ```bash
    git clone https://github.com/MathewJoseph1993/AetherTouch.git
    cd AetherTouch
    ```

2.  **Serve the file**:
    Due to browser security restrictions with Webcams, you must run this over a local server.
    *   **VS Code**: Right-click `index.html` -> "Open with Live Server".
    *   **Python**: `python3 -m http.server 8000`
    *   **Node**: `npx serve .`

3.  **Grant Permissions**: Allow your browser to access the Webcam.

## 🎮 Controls Guide

### 1️⃣ Zooming (God Mode)
*   **Gesture**: Raise both hands and **PINCH** with both.
*   **Action**: 
    *   Pull hands apart: **Zoom IN** (up to 1000%).
    *   Push hands together: **Zoom OUT**.
    *   Release pinch: **Freeze** zoom level.

### 2️⃣ Moving & Rotating
*   **Gesture**: **PINCH** with one hand.
*   **Action**: Move hand to drag. Rotate wrist to roll the object.

### 3️⃣ System Reset
*   **Gesture**: **Namaste** (Bring palms together like a clap).
*   **Keyboard**: Press **SPACEBAR**.
*   **Effect**: Instantly centers and resets the object.

## 🤝 Contributing

Contributions are welcome! Please fork the repository and submit a pull request for any new shapes, gestures, or optimizations.

## 📄 License

This project is open-source and available under the [MIT License](LICENSE).

---
*Built with ❤️ and ☕ by [Mathew Joseph](https://www.linkedin.com/in/gtm-engineer-mathew/)*
