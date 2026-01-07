# AetherTouch 🌌✋

> **"Any sufficiently advanced technology is indistinguishable from magic."** - Arthur C. Clarke

**AetherTouch** is a futuristic, touchless interactive particle system that allows you to manipulate 3D objects using hand gestures, inspired by the holographic interfaces seen in movies like *Iron Man*.

<!-- TODO: Add a demo GIF or screenshot here -->

## ✨ Features

### 🦾 Iron Man Interface (The "Super-Hand")
Experience 6DoF (Six Degrees of Freedom) control without touching a screen:

| Gesture | Action | Result |
| :--- | :--- | :--- |
| **Hover** | Open Hands | **Zoom In/Out** (Scale the universe) |
| **Grab** | Pinch (Thumb+Index) | **Drag** objects through space |
| **Twist** | Pinch + Rotate Wrist | **Rotate** objects (Z-Axis Roll) |
| **Steer** | Two Fists (Closed) | **Tilt/Steer** the entire system |

### 🧬 Particle Morphing
Seamlessly transform between mathematical and organic forms:
*   **Sphere**: The classic starting point.
*   **Heart**: Parametric romance.
*   **Flower**: Rose curve mathematics.
*   **Saturn**: Planetary rings.
*   **Buddha**: Point cloud visualization.
*   **Fireworks**: Explosive radial bursts.

### 🎨 Customization
*   **Real-time Color Picker**: Paint the particles with any color.
*   **Neon Glass Aesthetics**: Premium dark-mode UI with glassmorphism.

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
    Due to browser security restrictions with Webcams, you must run this over a local server (not just double-clicking `index.html`).
    
    *   **VS Code**: Right-click `index.html` -> "Open with Live Server".
    *   **Python**: `python3 -m http.server 8000`
    *   **Node**: `npx serve .`

3.  **Grant Permissions**: Allow your browser to access the Webcam when prompted.

4.  **Enjoy**: Hold up your hands and become a wizard!

## 🎮 Controls

*   **One Hand**: 
    *   Open Palm: Idle / Focus.
    *   Pinch: Grab & Move.
    *   Pinch & Twist: Rotate.
    *   Fist: Collapse/Tension.
*   **Two Hands**:
    *   Spread/Close: Zoom In/Out.
    *   Two Fists (One up, One down): Steer/Tilt.

## 🤝 Contributing

Contributions are welcome! Please fork the repository and submit a pull request for any new shapes, gestures, or optimizations.

## 📄 License

This project is open-source and available under the [MIT License](LICENSE).

---
*Built with ❤️ and ☕ by [Mathew Joseph](https://www.linkedin.com/in/gtm-engineer-mathew/)*
