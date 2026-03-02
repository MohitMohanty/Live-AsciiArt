# 🎥 ASCII CAM — GPU-Accelerated Live Camera Feed

> Real-time webcam feed rendered entirely as characters, numbers & symbols — powered by WebGL fragment shaders on your GPU.

![WebGL](https://img.shields.io/badge/WebGL-GPU%20Accelerated-red?style=flat-square)
![FPS](https://img.shields.io/badge/Performance-60%20FPS-00ff41?style=flat-square)
![Zero Dependencies](https://img.shields.io/badge/Dependencies-Zero-blue?style=flat-square)

---

## ✨ What is this?

ASCII CAM converts your live webcam feed into a real-time stream of characters — every pixel becomes a letter, number, or symbol based on its brightness. Dark areas map to dense characters like `@`, `#`, `W`. Bright areas map to light ones like `.`, ` `.

It runs entirely in the browser. No libraries. No frameworks. Just raw WebGL and a camera.

---

## ⚡ How It Works

The rendering pipeline is fully GPU-driven:

1. **Webcam → GPU Texture** — Each frame, the raw video feed is uploaded to the GPU as a texture. This is the only work JavaScript does per frame.

2. **Fragment Shader** — A WebGL fragment shader runs on thousands of GPU cores in parallel. Each core handles one pixel, reads its brightness, and maps it to a character index.

3. **Character Atlas** — All characters are pre-baked into a single atlas texture sitting in GPU memory. Looking up which character to draw is instant.

4. **Single Draw Call** — The entire frame is rendered in one GPU draw call. No DOM manipulation. No HTML. No JS loops.

```glsl
// Core shader logic (simplified)
float lum     = dot(vid.rgb, vec3(0.299, 0.587, 0.114));
float charIdx = floor((1.0 - lum) * (uCharCount - 1.0));
float alpha   = texture2D(uAtlas, vec2((charIdx + posInCell.x) / uCharCount, posInCell.y)).r;
gl_FragColor  = vec4(color * alpha, 1.0);
```

---

## 🎛️ Features

| Feature | Description |
|---|---|
| **Multiple Charsets** | Detailed, Alphanumeric, Blocks, Symbols, Binary, Matrix Katakana |
| **Color Modes** | Green terminal, White, Amber, or full RGB (each char gets real pixel color) |
| **Font Size Slider** | Go from ultra-dense to chunky characters |
| **Mirrored Feed** | Front-facing camera is flipped naturally |
| **FPS Counter** | Live frame rate display |
| **60 FPS** | Locked smooth rendering via GPU parallelism |

---

## 🚀 Getting Started

No installation needed. Just open the HTML file in any modern browser.

```bash
git clone https://github.com/MohitMohanty/Live-AsciiArt
cd ascii-cam
open index.html
```

> Allow camera access when prompted. Your feed never leaves your device — everything is processed locally in the browser.

---

## 🛠️ Tech Stack

- **WebGL** — GPU rendering via fragment shaders
- **Canvas API** — Character atlas generation
- **MediaDevices API** — Webcam capture
- **Vanilla JS** — Zero dependencies

---

## 📸 Preview

| Green Mode | Color Mode | Matrix Mode |
|---|---|---|
| Classic terminal look | Full RGB per character | Japanese Katakana chars |



---

## 📄 License

 do whatever you want with it.
