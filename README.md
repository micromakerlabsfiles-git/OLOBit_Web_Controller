# 🎨 OLO Glyph V1 - First Release
**Now with Beautiful U8g2 Fonts, Responsive Touch, Background Stopwatch, Non-Blocking Casio-style Beeps, and Dynamic Glyph Animations.**

OLO Glyph V1 is an offline-focused character system and serial glyph display for ESP32-based devices (specifically the ESP32-C3 SuperMini). It transforms a 1.3" or 0.96" OLED screen into an interactive companion, featuring real-time weather indicators, alarms, a background stopwatch, 13 selectable clock faces (including a full-screen sweep second rectangular Analog face, retro Casio watch style, and 7 Segment font), and completely offline over Web Serial.

This document covers hardware assembly, software installation, and how to utilize the offline Web Controller.

---

## 🚀 Key Features in OLO Glyph V1

- **🌐 WiFi Connectivity & Local Dashboard:** The device connects to local WiFi (credentials stored in NVS, toggled ON/OFF dynamically on-screen). When active, it hosts a premium, local HTTP dashboard directly from program flash (PROGMEM) at `http://ologlyph.local/` for password-secured remote control over your local network. It also supports USB Web Serial sync.
- **📡 On-Device WiFi Status Page (PAGE 11):** Displays active connection state, dynamically assigned IP address, and supports double-tap to toggle the WiFi transceiver ON/OFF.
- **✨ Premium U8g2 Fonts:** Both the boot sequence and the Glyph mode render using high-resolution, elegantly centered fonts (`helvB14`, `helvB10`, etc.).
- **🖼️ Outer Rounded OLED Borders:** Elegant `0,0,128,64` rounded borders are drawn around the Clock, Weather, and Glyph screens. Inner layouts automatically adapt to stay inside these borders.
- **⚡ Non-Blocking Alarm System:** The alarm sound uses a non-blocking state machine (`updateAlarmAudio()`) powered by `millis()`. The device's touch sensor and screen updates remain 100% responsive and lag-free even while the alarm is ringing.
- **🛡️ Glitch-Free Timekeeping & Alarm Lock:** Hour chime and alarms are checked continuously in the loop (outside the 3-second throttle) to prevent missed chimes, while a state-based lock prevents duplicate alarm triggers in the same minute.
- **🎯 Snappy & Debounced Touch:** A 20ms software debounce algorithm eliminates touch stuttering. Long press triggers at `500ms`, and double-taps respond within a `250ms` window.
- **⏱️ Background Stopwatch:** Access the stopwatch by double-tapping the Clock screen. It tracks time with 10ms accuracy and continues running in the background.
- **🔊 Casio-Style Audio Beeps:** 
  - The hourly chime triggers a crisp double-beep (`beep-beep` at 3.5kHz).
  - Alarms and countdown completions sound like a digital wristwatch alarm.
  - Startup tune plays on the first booting text.
- **📝 Intelligent U8g2 Glyph Mode:**
  - **Always Center-Aligned:** Multi-line text is horizontally centered for all animations (including Scroll Left, Scroll Right, and Bounce Scroll) relative to the screen or scroll block width.
  - Automatically wraps text at 120 pixels width.
  - Automatically parses newlines (`\n`) for paragraph separation.
  - **Dynamic Font Downscaling:** If the custom text exceeds screen dimensions in the selected font size, it automatically steps down to smaller U8g2 fonts until it fits perfectly.
  - **Advanced Animations:** Static, Scroll Left, Scroll Right, Blink, **Bounce Scroll** (bounces horizontally or vertically depending on size), and **Typing Effect** (character-by-character render with a pulsing typing cursor). Fully controllable via serial.
  - **Double-Tap Lock Toggle:** Double-tapping the touch sensor on the Glyph Mode page toggles the continuous text locked mode (`continuousGlyphMode`). While locked, a single tap is disabled, and screensaver timeouts are suspended. While unlocked, single tapping navigates to the Clock screen. Long press in Glyph Mode is disabled to avoid OS confusion.
- **🎛️ Direct-Push Glyph Mode:** Sending text configurations pushes them directly to the display in RAM without writing to flash (NVS), preserving flash memory cycles and making live text pushes instantaneous.
- **💡 WS2812B NeoPixel Integration (GPIO 6):**
  - **10 Selectable LED Modes:** Solid, Breathing, Color Cycle, Blink, Heartbeat, Fade In, Glow Flicker, Sparkle Strobe, Color Breathe, and Alternating Complement. All effects run independently of screen animations.
  - **OLED Status Screen (PAGE 10):** Displays the LED status ("ON" or "OFF"). Double-tap the touch sensor on Page 10 to toggle the LED, and single-tap to cycle back to Glyph mode.
  - **Low Power/Sleep Mode Override:** Automatically turns off the NeoPixel when the device goes into sleep mode to conserve energy.
  - **State Memory Restore:** When toggled back ON, the LED automatically loads and recovers the previously saved brightness, color, and effect from NVS.
  - **Hourly Chime & Alerts Flash:** Allows configuration of separate effects and color overrides for chime alerts, hydration reminders, and alarms.
  - **Buzzer-Synced Ringtones/Melodies & Equalizer Animation:** Trigger Star Wars, Super Mario, or Rickroll from the dashboard. The LED pulses in real-time sync with note pitch. When playing, a full-screen **Music card** displays an elegant treble note surrounded by active bouncing equalizer graphics, locking out display navigation and touch input, automatically returning when the song concludes.

---

## 🎛️ Web Control Center Layout
The Web Controller has been redesigned into a responsive, premium two-column dashboard:
1. **Left Sidebar Panel (Connection & Diagnostics):**
   - **Glow status badge:** Visual indicator for connection status ("Connected" in green / "Disconnected" in pulsing orange).
   - **Serial actions:** Simple buttons for connecting/disconnecting, syncing parameters, saving configurations to device flash, and rebooting.
   - **Pin configuration info:** Displays the physical hardware pinouts at a glance.
   - **Firmware Installer:** Connect and flash the system binary directly through the browser.
   - **Serial Monitor Console:** Monospace cyberpunk terminal showing incoming and outgoing serial commands in real-time.
2. **Right Main Panel (Web Controller & Tabs):**
   - **Tabbed workspace:** Move between Live Control, Eye Physics, Clock & Alarms, Glyph Mode, Weather Setup, and Hardware Driver tabs.
   - **Offline overlay:** When disconnected, a blurred glass overlay prevents accidental configuration changes and invites you to connect the device.

---

## ⏱ Navigation & Clock Sub-menus
We have simplified the Clock mode submenu navigation to be consistent and intuitive:
- **From Clock screen (PAGE 1):**
  - **Single-Tap:** Cycle to Weather (PAGE 2) (or World Clock page 3 if already in sub-menu state).
  - **Double-Tap:** Enter the sub-menu loop starting at World Clock (PAGE 3).
- **From World Clock (PAGE 3):**
  - **Single-Tap:** Go to Alarm View (PAGE 5).
- **From Alarm View (PAGE 5):**
  - **Single-Tap:** Go to Timer Mode (PAGE 8).
  - **Double-Tap:** Enter Alarm Set (PAGE 6) edit mode.
- **From Alarm Set (PAGE 6):**
  - **Single-Tap:** Increment the value of the active field.
  - **Double-Tap:** Cycle edit fields (Hour -> Minute -> Enabled/Disabled).
  - **Long-Press:** Save settings to NVS and return to Alarm View (PAGE 5).
- **From Timer Mode (PAGE 8):**
  - **Single-Tap:** Go to Stopwatch (PAGE 9).
  - **Double-Tap:** Start / Stop the countdown timer.
  - **Long-Press:** Reset timer duration.
- **From Stopwatch (PAGE 9):**
  - **Single-Tap:** Exit the sub-menu and return to Clock (PAGE 1).
  - **Double-Tap:** Start / Stop timing.
  - **Long-Press:** Reset stopwatch time.

---

## ⚙️ Page Timing & Transitions
Page rotation behavior in OLO Glyph V1 is split into two systems for optimized user control:
1. **Screensaver Timeout (Default 10s, configurable down to 5s safety floor):** If the touch sensor is not interacted with for the screensaver timeout duration, the display automatically transitions back to the **Eyes screensaver (Page 0)** and resets the sub-menu state. This automatic switch is paused if Glyph Mode is locked (`continuousGlyphMode`), the Stopwatch is active, or the Timer is counting down.
2. **Manual Tap Navigation:** When awake, manual navigation is done via single taps in the following cycle order:
   `Glyph Mode (7) -> Time (1) -> Weather (2) -> LED Status (10) -> WiFi Status (11) -> Eyes Screensaver (0) -> Glyph Mode (7)`
   Any touch activity resets the screensaver timeout. Toggling features or entering sub-menus occurs via double-tap (e.g. toggling LED status on Page 10, toggling WiFi radio on Page 11, entering sub-menus from Clock on Page 1, or toggling Sleep mode on the Eyes screensaver Page 0).

---

## 🔌 Hardware Setup & Pins

Connect your components using this pin mapping for the ESP32-C3 SuperMini:

| Component | Pin Name | ESP32 GPIO |
| :--- | :--- | :--- |
| **OLED Display** | SDA | `GPIO 20` (default) |
| **OLED Display** | SCL | `GPIO 21` (default) |
| **OLED Display** | VCC | `3.3V` / `5V` |
| **OLED Display** | GND | `GND` |
| **Touch Sensor** | I/O (Touch pin) | `GPIO 1` |
| **Touch Sensor** | VCC | `3.3V` / `5V` |
| **Touch Sensor** | GND | `GND` |
| **Buzzer** | I/O | `GPIO 2` |
| **WS2812B NeoPixel** | DIN | `GPIO 6` |

---

## 💻 Software Setup

This project is configured as a **PlatformIO** environment:
1. Open the project folder in VS Code with PlatformIO installed.
2. The `platformio.ini` automatically downloads required dependencies:
   - `Adafruit GFX Library`
   - `Adafruit SSD1306`
   - `Adafruit SH110X`
   - `Arduino_JSON`
   - `U8g2_for_Adafruit_GFX` (for premium fonts)
   - `Adafruit NeoPixel`
3. Click the PlatformIO **Build** button or run the command `pio run` to compile.
4. Upload the generated binary to the device over USB.
