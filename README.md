# Hacking Scroll Transition Effect

An immersive, scroll-driven visual effect that creates a digital "matrix dissolve" transition between stacked images, featuring procedural character scatter and clipping paths. Built with vanilla HTML, CSS, JavaScript, and powered by **GSAP**, **ScrollTrigger**, and **Lenis**.

---

## 🎬 What It Is

The **Hacking Scroll Transition Effect** is a premium, cyberpunk-inspired visual interaction designed for modern portfolios, landing pages, and storytelling sites. 

As the user scrolls, stacked images transition by clipping downwards. At the exact boundary of the clip-path transition, a procedural grid of digital characters appears, scatters organically, changes randomly in real-time, and then dissolves back into the ether. It simulates a digital "screen glitch" or a "matrix decryption" reveal of the underlying image.

### 🌟 Key Features
- **Deterministic Procedural Noise**: Uses a sine-based hashing algorithm (`hashFromPosition`) to ensure consistent, responsive scatter calculations across scroll frames without heavy performance overhead.
- **GSAP & ScrollTrigger Driven**: Precise scroll-position synchronization utilizing smooth scrubs.
- **Ultra-Smooth Scrolling**: Integrated with **Lenis Smooth Scroll** to standardize scroll performance across different devices and modern input hardware.
- **Dynamic CSS Masking**: Leverages hardware-accelerated `clip-path` polygon interpolation to cut away top images and seamlessly reveal underlying layers.
- **Zero-Dependency CDN Stack**: Runs natively in any web browser without needing a bundler, node modules, or compile steps.

---

## 🛠️ The Development Process & Mechanics

Developing this effect involved combining math, modern CSS clipping, and timeline scrubbing to create a cohesive digital illusion. Here is a breakdown of the key development layers:

### 1. The Stacked Layer Architecture
Images are stacked directly on top of each other using `position: absolute`. Their stacking order (`z-index`) is procedurally inverted upon initialization, ensuring that the earlier images sit on top of the newer images:
```javascript
stackedImages.forEach((img, i) => {
    img.style.zIndex = totalImages - i;
});
```

### 2. The Procedural Matrix Grid
Instead of static images or heavy video elements, a pure DOM-based grid of character cells is generated upon page load. The grid size adaptively matches the screen resolution:
- The screen width and height are divided into fixed-size grid cells (e.g., `16px`).
- Each cell is populated with random high-tech characters (`ZXCVBNM...`) and given a normalized `normalizedY` position from `0` to `1`.

### 3. The Scatter & Proximity Algorithms
To prevent the dissolve from looking like a uniform grid transition, we developed two dynamic formulas:
- **`hashFromPosition`**: Generates high-frequency pseudorandom noise based on the cell's `(row, col)` coordinate and a seed value. This determines each cell's unique activation frame and scatter displacement.
- **Proximity calculation**: In the active scroll region, cells calculate their absolute distance from the moving transition wave. Within a specific spread band, cells become visible and start swapping random characters to evoke active "hacking/decryption" noise.

```javascript
const rawDistance = Math.abs(cell.normalizedY - bandCenterY);
const scatterStrength = gsap.utils.clamp(
    dissolveMinScatterAtCenter,
    1,
    rawDistance / dissolveSolidCoreRadius
);
const scatteredDistance = cell.normalizedY - bandCenterY + cellScatterOffset[i] * scatterStrength;
```

---

## 🚀 How to Run Locally

### 1. Prerequisites
You only need a basic local web server (like VS Code **Live Server** extension) to view the project properly due to CORS rules on local images.

### 2. Setup
1. Clone this repository:
   ```bash
   git clone https://github.com/Praneeth2607/Hacking-scroll-effect.git
   cd Hacking-scroll-effect
   ```
2. Launch with a local server (e.g. `Live Server` in VS Code, or python: `python -m http.server 8000`).
3. Open in your browser and scroll!

---

## 🎨 Tech Stack
- **HTML5** & **CSS3** (Hardware-accelerated CSS Clip-Paths)
- **Vanilla JavaScript** (ES6+)
- **GSAP (GreenSock Animation Platform)** & **ScrollTrigger** (Animation Engine)
- **Lenis** (Smooth Scroll Engine)
