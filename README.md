# ⚡ OmniRand Studio

> **An Advanced, Cryptographically-Secure Random Number Generator & Probability Suite.**  
> Built with **React 19**, **TypeScript**, **Tailwind CSS**, and the **Web Audio API**.

[![React](https://img.shields.io/badge/React-19-61DAFB?logo=react&logoColor=black)](#)
[![TypeScript](https://img.shields.io/badge/TypeScript-5.x-3178C6?logo=typescript&logoColor=white)](#)
[![Tailwind CSS](https://img.shields.io/badge/TailwindCSS-3.4-38B2AC?logo=tailwind-css&logoColor=white)](#)
[![CSPRNG Security](https://img.shields.io/badge/Security-CSPRNG%20RFC%204086-10B981?logo=shield&logoColor=white)](#)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

---

## 🌟 Overview

**OmniRand Studio** takes the classic *"Random Number Generator"* tier-1 challenge and transforms it into a production-grade, scientific and utility suite suitable for developer portfolios, technical interviews, and real-world statistical applications.

It provides hardware-level cryptographic randomness (**CSPRNG**), Gaussian (Normal / Bell Curve) and Uniform distributions, arbitrary negative and positive bounds, high-precision floating points, batch sampling without replacement, interactive real-time frequency histograms, tabletop RPG polyhedral dice rolling, 3D coin flipping, and synthesized procedural audio.

---

## ✨ Features & Specification Compliance

| Feature | Classification | Description |
| :--- | :--- | :--- |
| **Custom Minimum & Maximum** | *Core User Story* | Arbitrary upper and lower bounds with smart validation and automatic clamping. |
| **Instant Generation** | *Core User Story* | Mechanical rolling slot-counter animation, tactile audio tick feedback, and `Space` keybinding. |
| **Negative Number Support** | *Bonus Feature* | Complete negative range support (e.g., `-100` to `50`, `-25` to `-5`) with sign handling. |
| **Decimal Precision Engine** | *Bonus Feature* | Floating-point mode with adjustable precision slider from `1` to `6` decimal places. |
| **Cryptographic CSPRNG** | *Portfolio Grade* | Leverages `window.crypto.getRandomValues()` to eliminate modulo bias and achieve zero predictability. |
| **Statistical Visualizer** | *Portfolio Grade* | Real-time dynamic frequency distribution histogram plotting empirical entropy over time. |
| **Descriptive Statistics** | *Portfolio Grade* | Live calculation of Sample Mean ($\mu$), Median, Min, Max, Standard Deviation ($\sigma$), and Variance ($s^2$). |
| **Tabletop RPG Dice Studio** | *Portfolio Grade* | Visual roller for polyhedral dice ($D4$, $D6$, $D8$, $D10$, $D12$, $D20$, $D100$) with modifier calculation and *Natural 20* critical hit celebration. |
| **3D Physics Coin Flipper** | *Portfolio Grade* | 3D-styled animated coin flip with cumulative heads/tails streak analytics and sound synthesis. |
| **List Shuffler & Raffle Picker** | *Portfolio Grade* | Impartial multi-winner raffle drawing and unbiased Fisher-Yates list shuffling. |
| **Procedural Audio Synthesizer** | *Portfolio Grade* | Native Web Audio API sound generator (ticking rolls, harmonic chimes, coin rings) with zero asset latency and master mute toggle. |
| **Session History & Data Export** | *Portfolio Grade* | Chronological history log with instant copy-to-clipboard and export to **CSV** and **JSON**. |
| **Saved Configurations & Presets**| *Portfolio Grade* | One-click presets (Lottery 6/49, D20, Temperature, Binary, Normalized Floats) + custom user presets saved in `localStorage`. |

---

## 🔬 Mathematical Architecture & Implementation

### 1. Zero Modulo-Bias CSPRNG Float
Standard `Math.random()` relies on pseudo-random algorithms like `xorshift128+`, which are vulnerable to state reconstruction. OmniRand uses the Web Crypto API:
```typescript
const buffer = new Uint32Array(1);
window.crypto.getRandomValues(buffer);
// Division by 2^32 produces an exact uniform float in [0, 1) without modulo bias:
const uniformFloat = buffer[0] / 4294967296;
```

### 2. Gaussian / Normal Distribution (Box-Muller Transform)
To simulate natural distributions (Bell curve centered around the midpoint):
$$Z_0 = \sqrt{-2 \ln(U_1)} \cos(2\pi U_2)$$
Where $U_1, U_2 \in (0, 1)$ are independent uniform variables. The transform scales with mean $\mu = \frac{min + max}{2}$ and standard deviation $\sigma = \frac{max - min}{6}$, ensuring 99.7% of values land naturally within the requested bounds.

### 3. Unbiased Fisher-Yates Shuffle
For unique batch sampling (such as a 6/49 lottery draw) and the list shuffler, OmniRand implements the modernized in-place Fisher-Yates algorithm in $O(n)$ time complexity.

---

## ⌨️ Keyboard Shortcuts

| Shortcut | Action |
| :--- | :--- |
| `Space` | Trigger generation / Roll active generator |
| `M` | Mute / Unmute audio sound effects |
| `Esc` | Close any active modal or drawer |

---

## 🚀 Getting Started

### Prerequisites
- **Node.js**: `v20.x` or higher
- **npm**: `v10.x` or higher

### Installation
```bash
# Clone the repository
git clone https://github.com/your-username/omnirand-studio.git

# Navigate into project directory
cd omnirand-studio

# Install dependencies
npm install
```

### Development Server
```bash
npm run dev
```
Open your browser at `http://localhost:5173` to explore the app.

### Production Build
```bash
npm run build
```
Creates an optimized static bundle in the `dist/` directory ready for deployment on **Vercel**, **Netlify**, or **GitHub Pages**.

---

## 🛠️ Tech Stack

- **UI Framework**: [React 19](https://react.dev/)
- **Type Safety**: [TypeScript](https://www.typescriptlang.org/)
- **Styling**: [Tailwind CSS](https://tailwindcss.com/)
- **Icons**: [Lucide React](https://lucide.dev/)
- **Audio Engine**: Native Web Audio API
- **Particle Effects**: Canvas Confetti
- **Build Tooling**: [Vite](https://vitejs.dev/)

---

## 📄 License

This project is open-source under the [MIT License](LICENSE).
