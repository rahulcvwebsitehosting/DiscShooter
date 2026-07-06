<div align="center">
  <br/>
  <h1>🎯 Gesture AR Shooter</h1>
  <p><b>A browser-based augmented reality shooting gallery controlled by your hands via webcam</b></p>
  <br/>
  <p>
    <img src="https://img.shields.io/badge/Three.js-r128-000000?style=flat-square&logo=three.js&logoColor=white" alt="Three.js"/>
    <img src="https://img.shields.io/badge/MediaPipe-Hands-FF6F00?style=flat-square&logo=google&logoColor=white" alt="MediaPipe Hands"/>
    <img src="https://img.shields.io/badge/Vite-6.x-646CFF?style=flat-square&logo=vite&logoColor=white" alt="Vite"/>
    <img src="https://img.shields.io/badge/TypeScript-5.8-3178C6?style=flat-square&logo=typescript&logoColor=white" alt="TypeScript"/>
    <img src="https://img.shields.io/badge/license-MIT-green?style=flat-square" alt="License"/>
  </p>
  <br/>
</div>

---

## ✨ Features

- **🖐️ Gesture-Controlled** — No controller, no keyboard. Just your hands.
- **👐 Dual-Hand Support** — Aim and shoot independently with both hands simultaneously.
- **⚡ Real-Time Tracking** — Powered by Google MediaPipe Hands for low-latency hand landmark detection.
- **🎮 Progressive Difficulty** — Enemies get faster as you level up (15% per level).
- **🔥 Combo System** — Chain hits for score multipliers up to 5×.
- **💎 Bonus Targets** — Gold orbs worth 500 points (regular discs are 100).
- **❤️ Lives System** — 3 lives. Miss a disc? Lose a life. Click **End Game** anytime to see your score card.
- **📊 End Game Score Card** — Full stats: final score, level, accuracy, best combo, hits/shots, time played. Play Again restarts fresh.
- **🎨 Immersive VFX** — Particle explosions, shard debris, screen shake, muzzle flash, and dynamic reticle feedback.
- **🔊 Procedural Audio** — Synthesized sound effects via Web Audio API (no audio files needed).
- **⚡ Optimized for Low-End Devices** — Lite hand model (modelComplexity: 0), 320×240 camera, adaptive AI throttling, object pooling, capped pixel ratio.
- **📱 Responsive** — Works on desktop and mobile browsers.
- **📡 Offline-Ready** — Service Worker caches assets for low-network environments.

---

## 🧠 How It Works

The app uses your webcam feed as the game background. MediaPipe Hands tracks 21 landmarks per hand in real time:

1. **Aim** — Extend your index finger toward a target. A reticle follows your fingertip with magnetic aim-assist.
2. **Shoot** — Pinch your thumb to your index finger (hammer action). The game detects the gesture using a normalized distance metric with hysteresis and debounce.
3. **Score** — Hit blue torus discs (+100) or gold icosahedron bonus orbs (+500). Build combos for multipliers.

### Architecture

The application runs two concurrent loops:

| Loop | Frequency | Purpose |
|---|---|---|
| **Render Loop** | ~60 FPS (`requestAnimationFrame`) | 3D rendering, entity updates, VFX, hand smoothing, aiming |
| **AI Loop** | ~45 FPS (adaptive) | Sends video frames to MediaPipe, receives hand landmarks, trigger detection |

Communication happens through a shared state object — the AI loop writes raw hand data; the render loop reads smoothed positions.

---

## 🚀 Getting Started

### Prerequisites

- [Node.js](https://nodejs.org/) (v18+)

### Installation

```bash
# Clone the repository
git clone https://github.com/rahulcvwebsitehosting/DiscShooter.git
cd DiscShooter

# Install dependencies
npm install

# Start the development server
npm run dev
```

The app will be available at `http://localhost:3000`.

> **No server needed** — You can also open `index.html` directly in a modern browser. The app uses an [Import Map](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/script/type/importmap) to load Three.js from CDN when Vite isn't running.

### Production Build

```bash
npm run build
npm run preview
```

---

## 🎮 Controls

| Gesture | Action |
|---|---|
| ☝️ Point index finger | Aim (reticle follows fingertip) |
| 👍 Pinch thumb to index | Shoot |
| 👐 Use both hands | Dual-wield — each hand aims & fires independently |

**Game Rules:**
- **Endless mode** — Play as long as you want. Click **End Game** (top-right) to finish and see your score card.
- You have **3 lives** (shown as hearts). Each disc that escapes off-screen costs 1 life. At 0 lives, the hearts turn black but you keep playing.
- Chain **5 consecutive hits** for a score multiplier. Keep the streak alive!

**Tips:**
- Keep your hand within the camera frame for best tracking.
- A well-lit background improves detection accuracy.
- Gold orbs move faster but are worth 500 points.
- Wait for the reticle to glow before pulling the trigger — it means you're locked on.

---

## 🛠️ Tech Stack

| Technology | Role |
|---|---|
| [Three.js](https://threejs.org/) (r128+) | 3D rendering, scene management, VFX |
| [MediaPipe Hands](https://developers.google.com/mediapipe/solutions/vision/hand_landmarker) | Real-time hand landmark detection (21 landmarks) |
| [Vite](https://vitejs.dev/) | Build tool and dev server |
| Web Audio API | Procedural sound synthesis |
| Service Worker | Offline caching |

---

## 📁 Project Structure

```
DiscShooter/
├── index.html          ← Main application (HTML + CSS + JS module)
├── sw.js               ← Service Worker for offline caching
├── vite.config.ts      ← Vite configuration
├── tsconfig.json       ← TypeScript configuration
├── package.json        ← Dependencies and scripts
├── metadata.json       ← AI Studio deployment metadata
└── README.md           ← You are here
```

The entire game logic lives in `index.html` as a single-file application — no build step needed for the core code.

---

## 🤝 Contributing

Contributions, issues, and feature requests are welcome! Feel free to check the [issues page](https://github.com/rahulcvwebsitehosting/DiscShooter/issues).

---

## 📄 License

This project is licensed under the MIT License.
