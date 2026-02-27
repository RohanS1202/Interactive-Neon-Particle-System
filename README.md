# 🖐️ Interactive Neon Particle System

A real-time, browser-based 3D particle experience driven entirely by hand gestures. Built with **Three.js** for rendering and **Google MediaPipe** for computer vision.

![HTML5](https://img.shields.io/badge/html5-%23E34F26.svg?style=for-the-badge&logo=html5&logoColor=white)
![Threejs](https://img.shields.io/badge/threejs-black?style=for-the-badge&logo=three.js&logoColor=white)
![JavaScript](https://img.shields.io/badge/javascript-%23323330.svg?style=for-the-badge&logo=javascript&logoColor=%23F7DF1E)

<br>

![Interactive Particle Demo](./demo.gif) 

<br>

##  Features

* **Real-Time Hand Tracking:** Uses your webcam to instantly track hand and finger movements via MediaPipe AI directly in the browser.
* **Dynamic Morphing Shapes:** Interpolates 6,000 particles smoothly between mathematical templates (Sphere, Heart, Flower, Saturn, Fireworks).
* **Gesture Controls:**
  * **Fingers Up:** Count your fingers (0-4) to change the current particle shape.
  * **Pinch (Thumb + Index):** Control the overall scale and expansion of the system.
  * **Move Left/Right:** Sweeping your hand across the camera dynamically shifts the particle colors across the HSL spectrum.
  * **Interactive Force Field:** Waving your hand through the center of the screen physically repels and pushes the particles away.
* **Post-Processing Pipeline:** Utilizes Three.js `UnrealBloomPass` to create a glowing, neon aesthetic.
* **Modern Glassmorphism UI:** Features a sleek, responsive HUD overlay with a dedicated start screen to handle modern browser autoplay policies.

## 🚀 How to Run

Because this project requests access to your webcam and loads external shader modules, **it must be run on a local web server**. Simply double-clicking the `index.html` file will result in CORS/security errors in modern browsers.

### Method 1: VS Code (Recommended)
1. Install the [Live Server](https://marketplace.visualstudio.com/items?itemName=ritwickdey.LiveServer) extension in Visual Studio Code.
2. Open `index.html`.
3. Click **"Go Live"** in the bottom right corner of your editor.

### Method 2: Python
If you have Python installed, open your terminal in the project directory and run:
```bash
# Python 3
python -m http.server 8000

```

Then open `http://localhost:8000` in your browser.

### Method 3: Node.js

If you have Node.js installed, you can use `http-server`:

```bash
npx http-server

```

## 🧠 How it Works

1. **Rendering:** Three.js utilizes a `BufferGeometry` array to manage the $X,Y,Z$ positions of 6,000 points. This is significantly faster than rendering 6,000 individual meshes.
2. **Math:** Target shapes are generated using parametric math equations. For example, the heart shape relies on $x=16\sin^3(t)$.
3. **Tracking:** MediaPipe detects 21 3D landmarks on the hand.
We use specific landmarks to trigger events:
* **Distance:** $\sqrt{\Delta x^2+\Delta y^2}$ between Landmark 4 (Thumb tip) and Landmark 8 (Index tip) controls the scale.
* **Shape Logic:** Simple geometric comparisons (e.g., if the Y coordinate of a fingertip is higher than its corresponding knuckle) to count raised fingers.


4. **Physics:** The animation loop utilizes a simple *lerp* (linear interpolation) function to smoothly move particles from their current position to their target position, creating a fluid swarming effect.

## 📄 License

This project is licensed under the MIT License - feel free to use, modify, and distribute it as you see fit!
