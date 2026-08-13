# 📘 OLO Bit OS V3 — Complete User Manual & Reference Guide

Welcome to **OLO Bit OS V3**, the flagship operating system for your **OLOBit** desk companion! This manual provides comprehensive user instructions for operating your device via capacitive touch gestures, navigating the on-device menu system, launching built-in retro games and productivity apps, pairing with your smartphone for notifications and Google Maps turn-by-turn navigation, and customizing every feature using the official Online Web Controller.

---

## 🌐 1. Online Web Controller (No Installation Needed)

You can configure and customize your OLOBit directly from your web browser without installing any software or drivers:

👉 **Official Web Controller:** [https://micromakerlabsfiles-git.github.io/OLOBit_Web_Controller](https://micromakerlabsfiles-git.github.io/OLOBit_Web_Controller)

### 🔌 How to Connect:
1. Connect your OLOBit to your computer using a standard **USB-C Data Cable**.
2. Open the [Online Web Controller](https://micromakerlabsfiles-git.github.io/OLOBit_Web_Controller) in **Google Chrome**, **Microsoft Edge**, or **Opera** (browsers supporting the Web Serial API).
3. Click **"Connect Device"** and select your OLOBit serial port (e.g. `USB-Enhanced-SERIAL CH343`, `CP2102`, or `USB JTAG/serial debug unit`).
4. The dashboard automatically syncs all saved preferences from your device's flash memory and synchronizes your device's clock to your exact local computer timezone.

---

## 🕹️ 2. On-Device Touch Gestures & Navigation

Your OLOBit is operated using a smart capacitive touch sensor positioned on the top/front of the casing.

### 👆 Gesture Reference Table
| Gesture | Context | Action Performed |
| :--- | :--- | :--- |
| **Single Tap** | **Idle Face View** | Cycle through enabled face animations and status clock pages. |
| | **Notification Active** | **Dismiss & Next**: Pops current message and loads next queued alert (e.g. `WHATSAPP (1/3)` $\rightarrow$ `(2/3)`). |
| | **Canvas Mode** | **Toggle QR Screen**: Switches between live Canvas Text and Canvas QR Code Page (when QR is enabled). |
| | **Menu Navigation** | Scroll downward to the next menu item. |
| | **Stopwatch / Timer** | Start or Pause timer countdown / stopwatch elapsed time. |
| | **Retro Games** | Jump (Dino / Flappy) or Change Direction (Snake). |
| **Double Tap** | **Idle Face View** | Trigger interactive expressive reaction animations. |
| | **Canvas Mode** | **Toggle QR View**: Fast-switch between Canvas Text and QR code screen. |
| | **Menu Navigation** | **Enter / Toggle**: Open selected submenu or toggle setting value. |
| | **Stopwatch** | **Reset**: Resets stopwatch time counter back to `00:00:00`. |
| | **Dice Roller App** | Re-roll the dice with rolling animation. |
| **Triple Tap** | **Any Screen** | Open on-device **Apps & Settings Menu**. |
| **Long Press (>0.6s)** | **Menu / Any App** | **Exit Mode**: Immediately exits the active game, app, menu, Canvas Mode, or QR Page back to home faces. |
| | **Navigation Overlay** | **Force-Exit Maps**: Dismisses turn-by-turn navigation and restores normal face animations. |
| | **Active Alarm** | **Snooze / Dismiss**: Silences active alarm buzzer immediately. |

---

## 📱 3. Built-In On-Device Apps & Menu System

Triple-tap the touch sensor from any screen to access the on-device **Menu System**.

### 📲 A. Productivity & Utility Apps
- **🎲 Dice Roller (`Apps → Dice Roll`)**: Digital 6-sided random dice. Single-tap or double-tap rolls the dice with real-time rolling physics animation.
- **⏱️ Focus Pomodoro Timer (`Apps → Focus Timer`)**: Countdown productivity timer (default 5–120 min configurable via Web Controller). Single-tap starts/pauses; alarm chimes when finished.
- **⏱️ Stopwatch (`Apps → Stopwatch`)**: Centisecond precision elapsed timer. Single-tap starts/pauses; double-tap resets back to zero.
- **📱 Standalone QR Code (`Apps → QR Code`)**: Full-screen, high-contrast QR code display optimized for phone camera scanning.
- **💻 Hardware Monitor (`Apps → Hardware / CPU-Z`)**: Live companion stats monitor displaying CPU temperature, GPU usage, and RAM consumption when connected to your PC companion app.

### 🎮 B. Built-In Retro Games
- **🐍 Snake Game (`Apps → Snake`)**: Classic retro snake game. Tap to turn 90° clockwise, eat food pellets, grow longer, and beat your high score.
- **🦖 Chrome Dino Runner (`Apps → Dino Run`)**: Endless desert obstacle runner. Tap to jump over oncoming cacti and flying obstacles.
- **🐤 Flappy OLO (`Apps → Flappy`)**: One-touch flight physics. Tap to flap wings and navigate through obstacle pipes.

### ⚙️ C. On-Device Settings Submenus
- **Watch Face Style**: Switch between **Classic Digital** (clean digital time with battery indicator) and **Casio Retro** (retro digital style with seconds counter, day, and date).
- **Time Format**: Switch between 12-Hour (`AM/PM`) and 24-Hour clock formats.
- **Hourly Chime**: Toggle hourly audio chime (`Westminster Abbey` or `Casio Double-Beep`).
- **System Sound**: Enable or mute all touch clicks and interface audio.
- **Screen Flip**: Invert OLED display orientation 180° for upside-down mounting.
- **Bluetooth Power**: Toggle BLE radio ON/OFF to conserve power.
- **About Device**: View firmware version, uptime, and hardware MAC address.

---

## 🧭 4. Smartphone Integration & Google Maps Navigation

Your OLOBit connects via Bluetooth Low Energy (BLE) to the **Chronos ESP32** companion app (available on iOS and Android).

### 🚀 Setup Steps:
1. Install **Chronos ESP32** from Google Play Store or Apple App Store.
2. Turn on Bluetooth on your phone and open the app.
3. Tap **Connect** and select your OLOBit (default name: `OLO-Bit-XXXX`, where `XXXX` is your unique MAC ID).
4. **Time & Weather Synchronization**: The app automatically syncs your phone's time, date, local city weather, and temperature forecasts.

### 🗺️ Google Maps Turn-by-Turn HUD Mode:
When you start driving, walking, or cycling navigation in Google Maps:
- OLOBit instantly transitions to **Navigation Overlay Mode**.
- Displays dynamic direction turn arrows (Left, Right, Straight, U-Turn, Roundabouts).
- Shows live remaining distance to your next turn (with visual progress bar) and total destination distance/ETA.
- When navigation ends, OLOBit automatically returns to your idle face animations.

---

## 💬 5. Smart Notifications & Queue System

- **Multi-App Support**: Streams incoming Phone Calls, SMS, WhatsApp messages, Instagram alerts, Telegram, Emails, and calendar reminders.
- **FIFO Message Queue**: Stores up to 10 incoming notifications. Displays queue index badge (e.g. `WHATSAPP (1/3)`, `MESSAGES (2/3)`).
- **Interactive Browsing**:
  - **Single-tap** to dismiss the current message and instantly load the next alert in the queue.
  - Messages auto-advance after a configurable duration (default: 4 seconds).
  - Incoming phone calls ring with live caller ID display.

---

## 🖥️ 6. Web Controller Feature Guide

The [Online Web Controller](https://micromakerlabsfiles-git.github.io/OLOBit_Web_Controller) provides visual controls across 6 comprehensive categories:

### 🖼️ A. Face Animations & GIFs Tab
- **Idle Face Animation Library**: Choose from 16+ built-in visual expressions (Default, Angry, UwU, Demon Slayer, Road Rage, Headlights, Sleepy, Heart, Laughing, Yelling, Car, Speed, etc.).
- **Cycle Selection**: Pick which face animations are included in the random idle rotation cycle.
- **Gesture Reaction GIFs**: Assign unique animations triggered by single-tap, double-tap, or long-press.
- **Playback Speed & Delays**: Adjust frame playback speed (1 to 200ms per frame) and cycle pause duration (500ms to 60s).
- **Pixel Inversion**: Toggle Positive Dark mode (black background) or Negative Light mode (white background).

### 🎵 B. Sound & Melodies Tab
- **Master Volume**: Set piezo buzzer output level from `0` (Mute) to `10` (Maximum volume).
- **Audio Toggles**: Enable or disable system feedback clicks and emotion sound effects.
- **Melody Packs**: 1-click apply themed startup audio packs (Modern Startup, Sci-Fi Boot, Retro Computer, Cyberpunk Login, Soft Desktop).
- **Emotion Audio Themes**: Apply sound styles (Cute Robot, Retro Arcade, Cyber Mech, 8-Bit Pip).
- **RTTTL Melody Composer & Studio**: Compose, preview, and assign custom musical ringtones and gesture chimes.

### ⏰ C. Time, Alarms & Chronos Tab
- **Time Format**: 12-Hour (`AM/PM`) or 24-Hour digital clock display.
- **Daily Alarm**: Set alarm time (`00:00` to `23:59`) and toggle alarm active. Silenced with a single tap.
- **Hourly Chimes**: Choose between `Westminster Classic` melodic chimes or `Casio Retro` double-beeps.
- **Do Not Disturb (DND)**: Schedule quiet hours (e.g. `22:00` to `07:00`) to silence all audio alerts automatically during sleep.
- **Hydration Reminders**: Set periodic water drink alerts (`15`, `30`, `45`, `60`, `90`, `120` minutes).
- **Focus Pomodoro Timer**: Set default countdown work sessions (1 to 120 minutes).
- **Screensaver / Sleep Mode**: Automatically dims and puts the device to sleep during inactivity (5, 10, 30, or 60 min timeouts). Wakes up instantly on touch.
- **Custom Bluetooth Name**: Rename your device to your personal handle (e.g. `Robin-OLOBit`).
- **Quote Categories**: Choose motivational quote libraries (All, Bible, Mahabharatham, Quran, Buddhist, Hustle/Work, IT/Coding, Craftsmanship, Positive).

### 📝 D. Canvas Mode & QR Code Tab
- **Live Canvas Text Overlay**:
  - Type custom announcement or desk status messages (up to 128 characters).
  - Choose from 10 typography fonts (Helvetica Bold/Regular, Times, Courier, Lucida, New Century).
  - Select Font Size (Tiny 8px, Small 12px, Medium 14px, Large 18px, XL 24px).
  - Choose Animation Styles: Scroll Left, Scroll Right, Bounce, Typewriter, Blinking, or Fixed Center.
- **Dynamic QR Code Generator**:
  - Select payload type: **🌐 Website URL**, **📝 Plain Text Message**, **📞 Phone Call**, or **📶 WiFi Network Credentials (SSID + Password)**.
  - Generates high-contrast, full-screen QR codes with maximized module scaling and broad quiet zones for instant camera scanning.
  - Push QR directly to the screen or toggle on-device page flipping via double-tap.

### 💡 E. Status NeoPixel RGB LED Tab
- **Power & Brightness**: Toggle RGB LED power and adjust illumination brightness (levels 0 to 10).
- **Color Palette**: Pick from vibrant preset colors (Red, Orange, Yellow, Green, Blue, Indigo, Violet, Warm White).
- **12 Dynamic Lighting Effects**: Solid, Breathing, Blinking, Heartbeat, Rainbow, Shimmer, Candle, Color Cycle, Strobe, Neon Pulse, Police, Firefly.

---

## 👑 7. Display Priority & UI Flow Hierarchy

OLOBit OS V3 features an intelligent priority overlay engine. Lower priority screens pause automatically and resume immediately when higher priority events are dismissed:

```
[ LEVEL 1 (Highest) ] 🚨 Active Alarms / Emergency Alerts
          ↓
[ LEVEL 2 ]           📞 Incoming Phone Calls & Notifications (FIFO Queue)
          ↓
[ LEVEL 3 ]           🗺️ Google Maps Turn-by-Turn Navigation HUD
          ↓
[ LEVEL 4 ]           🕹️ Active Apps / Retro Games / Menu System
          ↓
[ LEVEL 5 ]           📝 Live Canvas Text / Canvas QR Code Display
          ↓
[ LEVEL 6 ]           ⏰ Clock Faces / Weather Screens / Quotes
          ↓
[ LEVEL 7 (Lowest) ]  😴 Screensaver / Idle Face Animation Loop
```

---

## ❓ 8. Frequently Asked Questions (FAQ)

- **Q: Which web browsers support the Online Web Controller?**
  - *Answer*: Use **Google Chrome**, **Microsoft Edge**, or **Opera** on Windows, macOS, Linux, or ChromeOS. Safari and Firefox do not currently support the Web Serial API.
- **Q: How do I sync time accurately with my computer?**
  - *Answer*: Connecting to the [Online Web Controller](https://micromakerlabsfiles-git.github.io/OLOBit_Web_Controller) automatically detects your computer's local timezone (e.g. IST UTC+5:30) and sets the device clock instantly.
- **Q: How do I switch between Canvas Text and the QR Code on my desk?**
  - *Answer*: While in Canvas Mode, **single-tap or double-tap** the touch sensor to flip between your text message and the full-screen QR code page.
- **Q: How do I exit any app or game back to face animations?**
  - *Answer*: **Long-press (>0.6s)** the capacitive touch sensor at any time to exit immediately.

