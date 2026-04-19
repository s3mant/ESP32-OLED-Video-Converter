# 🎬 ESP32 OLED Video Player (Pro Edition)

A comprehensive **web-based tool** for converting any video into a 1-bit (monochrome) animation that runs smoothly on a 128×64 OLED display (SSD1306 / SH1106) using an ESP32 microcontroller.

This project doesn’t just extract frames—it also includes advanced **image processing algorithms** typically found in professional tools (like Image2cpp), ensuring your videos and text remain sharp, maintain smooth gradients, and avoid turning into solid black silhouettes.

---

## ✨ Key Features (Pro Edition)

* 🧮 **Advanced Dithering Algorithms:** Supports **Bayer 8×8** (ultra-smooth for video), **Atkinson** (prevents heavy black blocking), and **Floyd-Steinberg**.
* 📏 **Smart Scaling & Panning:** Options include *Best Fit*, *Stretch*, *Fill/Cover* (fills screen without breaking aspect ratio), and *Custom* (manual W, H, X, Y control).
* 🖋️ **Sub-Pixel Thickness (Morphology):** Fine control to thin/thicken text and lines using decimal precision—preserves small details on OLED displays.
* 👁️ **NTSC Luminance Conversion:** Uses human visual perception formulas to accurately detect grayscale tones before converting to black and white.
* ⚡ **High-Performance ESP32 Code:** Generated code uses `millis()` (non-blocking) for stable FPS and includes **I2C overclocking (800 kHz)** for smooth playback without lag.
* 💾 **Auto-Save Settings:** All slider and dropdown settings are automatically saved locally in your browser.

---

## 🛠️ Hardware Requirements

1. **ESP32** (NodeMCU / WROOM)
2. **128×64 OLED Display** (SSD1306 or SH110X, I2C interface)
3. Jumper wires

### Standard Wiring Configuration

| OLED Pin | ESP32 Pin |
| :------: | :-------: |
|    VCC   |    3.3V   |
|    GND   |    GND    |
|    SDA   |  GPIO 21  |
|    SCL   |  GPIO 22  |

---

## 📦 Software Requirements (Libraries)

Make sure the following libraries are installed in Arduino IDE (via Library Manager):

* `Adafruit GFX Library`
* `Adafruit SSD1306` (for SSD1306 displays)
* `Adafruit SH110X` (for SH1106 displays)

---

## 🚀 How to Use

### 1. Extract Video via Web Converter

1. Open the Web Converter page (open `index.html` in your browser or use the GitHub Pages link).
2. Upload the video you want to display.
   *(Tip: Use the “Rotate 90°” button for vertical videos / reels.)*
3. Adjust **Dithering**, **Scaling**, and **Line Thickness** until the preview looks right.
4. Click **Start Frame-by-Frame Extraction** and wait for completion.

---

### 2. Upload to ESP32

1. Click **Copy Data Array**, then paste it into a new file/tab in Arduino IDE named `VideoFrame.h`.
2. Click **Copy Main.ino Code**, then paste it into your main Arduino sketch file.
3. In `Main.ino`, select your OLED type by uncommenting either:

   ```cpp
   #define PAKAI_SSD1306
   // or
   #define PAKAI_SH1106
   ```
4. ⚠️ **IMPORTANT:** Since video arrays consume large flash memory, go to:
   **Tools > Partition Scheme → select “Huge APP (3MB No OTA / 1MB SPIFFS)”**
5. Click **Upload** to your ESP32.

---

## 💡 Pro Tips for Image Settings

* **For real-life videos / landscapes:**
  Use **Bayer 8×8 dithering** → stable gradients, no flickering.

* **For text or simple cartoons:**
  Use **Solid Threshold** → if text looks broken, increase **Line Thickness toward White +** (e.g., 0.5–1.0).

* **To prevent dark objects merging (silhouette effect):**
  Use **Atkinson dithering** + slightly increase **Brightness**.
