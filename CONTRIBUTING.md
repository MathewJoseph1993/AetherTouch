# Contributing to AetherTouch 🌌

Thank you for your interest in contributing to **AetherTouch**! We welcome improvements, bug fixes, and new magical gestures.

## 🛡️ Branch Strategy & Protection

To ensure the stability of the `main` branch, we follow a strict **Feature Branch Workflow**:

1.  **`main` is Protected**:
    *   Direct pushes to `main` are restricted.
    *   All changes must come through a **Pull Request (PR)**.
    *   Force pushes are disabled to preserve history.

2.  **Feature Branches**:
    *   Create a new branch for every feature or fix.
    *   Naming convention: `feature/your-feature-name` or `fix/bug-description`.
    *   Example: `feature/voice-commands` or `fix/pinch-detection`.

## 🚀 Development Workflow

1.  **Clone & Branch**:
    ```bash
    git clone https://github.com/MathewJoseph1993/AetherTouch.git
    git checkout -b feature/my-cool-feature
    ```

2.  **Code & Test**:
    *   Run the app locally (`Live Server` or `python3 -m http.server`).
    *   Ensure gestures feel smooth and "magical" (60 FPS target).

3.  **Commit**:
    *   Write clear, descriptive commit messages.
    *   Example: `feat: add Vulcan salute gesture for live long and prosper`

4.  **Push & PR**:
    ```bash
    git push origin feature/my-cool-feature
    ```
    *   Open a Pull Request on GitHub targeting `main`.
    *   Request a review (or review it yourself if solo).
    *   Merge only when checks pass.

## 🎨 Coding Standards

*   **Architecture**: Keep it Simple (KISS). We use a **Single-File Architecture** (`index.html`) for portability and performance.
*   **Style**:
    *   **JS**: Vanilla JavaScript (ES6+). No frameworks unless necessary.
    *   **CSS**: Glassmorphism, neon accents, dark mode default.
    *   **3D**: Three.js for rendering.
*   **Performance**: Minimize garbage collection in the animation loop. Pre-allocate vectors where possible.

## 🤝 Community

*   Be kind and respectful.
*   "Any sufficiently advanced technology is indistinguishable from magic." - Keep the magic alive!

---
*Happy Coding!* 🦾✨
