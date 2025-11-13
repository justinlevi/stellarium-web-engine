# Stellarium Web Engine - Quick Start Guide

Get the beautiful planetarium web app running in 5 minutes!

## Prerequisites

- Git
- Python 3 (for running a simple web server)
- A modern web browser (Chrome, Firefox, Safari, Edge)

## Step-by-Step Setup

### 1. Clone the Repository

```bash
git clone https://github.com/justinlevi/stellarium-web-engine.git
cd stellarium-web-engine
```

### 2. Start a Local Web Server

The application needs to be served via HTTP (not opened as a file) due to CORS restrictions and WASM loading requirements.

**Option A: Using Python 3 (Recommended)**
```bash
python3 -m http.server 8000
```

**Option B: Using Python 2**
```bash
python -m SimpleHTTPServer 8000
```

**Option C: Using Node.js (if you have it)**
```bash
npx http-server -p 8000
```

You should see output like:
```
Serving HTTP on 0.0.0.0 port 8000 (http://0.0.0.0:8000/) ...
```

### 3. Open the Application

Open your web browser and navigate to:

**Main Application:**
```
http://localhost:8000/apps/simple-html/stellarium-web-engine.html
```

**Debug/Test Page (alternative):**
```
http://localhost:8000/apps/simple-html/debug-page.html
```

### 4. Wait for Loading

The first time you open the app, it will:
- Download the WASM engine (~1.3 MB)
- Load star catalogs
- Initialize WebGL rendering
- Load asteroids, comets, and satellites data

You'll see loading progress in the top bar. After 5-10 seconds, you should see:
- A beautiful night sky with stars
- The Milky Way
- A landscape at the bottom
- Control buttons at the bottom

## Using the Application

### Interactive Controls (Bottom Bar)

Click the icons to toggle features:

1. **Constellations** - Show/hide constellation lines
2. **Atmosphere** - Toggle atmospheric effects
3. **Landscape** - Show/hide ground landscape
4. **Azimuthal Grid** - Show horizontal coordinate grid
5. **Equatorial Grid** - Show celestial coordinate grid
6. **Nebulae** - Display deep sky objects
7. **DSS** - Digital Sky Survey overlay

### Navigation

- **Click and drag** - Pan around the sky
- **Mouse wheel** - Zoom in/out
- **Click on objects** - Select stars, planets, galaxies (shows info card)

## Troubleshooting

### Problem: Blank page or Vue template syntax showing

**Symptoms:** You see `{{getProgress().title}}` or similar text

**Solution:** Make sure you're accessing via `http://localhost:8000` and not opening the file directly (file:/// URLs won't work)

### Problem: "Failed to load WASM"

**Solution:**
1. Make sure the web server is running
2. Check that you're in the project root directory when starting the server
3. Clear your browser cache and reload

### Problem: No stars visible

**Symptoms:** Black screen with UI but no stars

**Solution:**
1. Wait 10-15 seconds for data to load
2. Check browser console (F12) for errors
3. Make sure WebGL is enabled in your browser

### Problem: CORS errors in console

**Solution:** You must use a web server (step 2). Opening the HTML file directly won't work.

## What You're Seeing

When working correctly, you should see:
- **Night sky** with thousands of stars
- **Milky Way** band across the sky
- **Labeled objects** like Pleiades, Andromeda (M31), bright stars
- **Landscape** with trees at the horizon
- **Smooth rendering** at 60 FPS
- **Interactive controls** that respond immediately

## Advanced: Building from Source

If you want to modify the core engine (requires Emscripten):

```bash
# Install Emscripten (follow official docs)
# https://emscripten.org/docs/getting_started/downloads.html

# Build the WASM engine
make js

# Or debug build
make js-debug
```

This compiles the C/C++ engine to WebAssembly and copies files to:
- `build/stellarium-web-engine.js`
- `build/stellarium-web-engine.wasm`

## Project Structure

```
stellarium-web-engine/
├── apps/
│   ├── simple-html/          # Ready-to-use test pages (START HERE)
│   │   ├── stellarium-web-engine.html  # Main demo
│   │   └── debug-page.html             # Alternative UI
│   ├── test-skydata/         # Star catalogs and astronomical data
│   └── web-frontend/         # Full Vue.js production app
├── build/                    # Compiled WASM engine
└── src/                      # C/C++ source code
```

## Browser Compatibility

✅ **Supported:**
- Chrome/Chromium 80+
- Firefox 75+
- Safari 14+
- Edge 80+

❌ **Not Supported:**
- Internet Explorer (no WebAssembly support)
- Very old mobile browsers

## Need Help?

- Original project: https://github.com/Stellarium/stellarium-web-engine
- This fixed fork: https://github.com/justinlevi/stellarium-web-engine
- Report issues on GitHub

## Credits

- **Stellarium Labs** - Original creators
- **Fixed by Claude Code** - Vue/Vuetify compatibility restoration (Nov 2025)

---

**Enjoy exploring the universe!** 🌌✨
