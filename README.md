# PsychoMotion Studio Mobile (Capacitor + WebCodecs)

A 100% client-side, zero-python-dependency mobile motion graphics studio built with **HTML5 Canvas 2D**, **WebCodecs (H.264)**, **mp4-muxer**, and **Capacitor**.

Directly connected to the **OmniRoute AI Gateway** via Cloudflare Tunnel for instant script generation, conversational scene director chat, and procedural canvas coding.

---

## 🌟 Key Architecture & Features

1. **Zero-Python Client-Side Architecture**:
   - No local backend server needed. Runs 100% inside Android System WebView or standard mobile browsers.
   - All assets (fonts, SFX, BGM, and `mp4-muxer`) are bundled locally offline inside `www/`.

2. **Zero-Drop, Frame-Accurate MP4 (H.264) Export**:
   - Powered by modern **WebCodecs API** (`VideoEncoder`) and **`mp4-muxer`**.
   - Frame-by-frame offline rendering loop (at 720x1280 or 1080x1920 @ 60 FPS).
   - Zero dropped frames even on budget mobile processors.
   - Generates native `.mp4` (H.264 Baseline/Main) with hardware acceleration.

3. **Audio Routing with Web Audio API**:
   - `PsychoAudioEngine` synthesizes ambient drones and dynamic SFX (whoosh, sub impact, glitch, mystery bell) offline via `OfflineAudioContext`.
   - Audio buffer is encoded into AAC (`mp4a.40.2`) and muxed synchronously into the MP4 file.
   - Fallback to real-time `MediaRecorder` stream recording if WebCodecs is unavailable.

4. **Direct OmniRoute AI Integration**:
   - Direct `fetch` calls to:
     - **Endpoint**: `https://information-helps-renaissance-recipe.trycloudflare.com/v1`
     - **API Key**: `sk-97a9d81b5d3c4a0b-3b6992-b24ddd92`
     - **Model**: `free-is` (or customizable)
   - Built-in Settings Modal (⚙️) to view, edit, or test the AI connection with live status pings.
   - Persists configuration seamlessly across reloads in `localStorage`.

5. **2D Kinematics & Procedural Visuals**:
   - 23+ built-in character archetypes: Walking with thought bubbles, Meditating lotus with pulsing chakras, Overthinking vortex, Breakthrough burst, Digital trap, Reaching star, Floating brain, Dopamine gauge, etc.
   - Full live `customCode` evaluation pipeline with sandboxed `eval`/`Function` execution and live hot-reloading.

---

## 🚀 Exact Steps to Build the Android APK

### Option 1: Automatic Build via GitHub Actions (Recommended)
This repository includes a preconfigured GitHub Actions workflow in `.github/workflows/build-apk.yml`.
1. Push this repository to GitHub:
   ```bash
   git init
   git add .
   git commit -m "Initial commit: PsychoMotion Studio Capacitor Mobile App"
   git remote add origin https://github.com/lyla360/<repo-name>.git
   git push -u origin main
   ```
2. Go to your GitHub repository -> **Actions** tab.
3. Click on the **Build Android APK (Capacitor)** workflow and click **Run workflow**.
4. Once completed (~2 minutes), download the ready-to-install `MotionStudio-Android-APK` from the workflow summary!

### Option 2: Local Android Studio Build
If you have Android Studio & Android SDK installed:
```bash
# 1. Install dependencies
npm install

# 2. Add Android platform (first time only)
npx cap add android

# 3. Synchronize web assets to native Android project
npx cap sync android

# 4. Open in Android Studio
npx cap open android

# 5. Or build APK from command line
cd android
./gradlew assembleDebug
```
The resulting debug APK will be generated at:
`android/app/build/outputs/apk/debug/app-debug.apk`

---

## 📱 Local Web Testing
To preview the mobile web app locally:
```bash
python3 -m http.server 8080 --directory www
```
Open your browser at `http://localhost:8080` or `http://<your-ip>:8080` from your mobile device on the same Wi-Fi network.
