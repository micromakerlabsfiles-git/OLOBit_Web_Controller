# OLO Bit - User Quick Start, Flasher & Web Controller Guide

Welcome to the **OLO Bit Web Controller & Flasher Hub**! This guide contains quick-start setup instructions, I2C pin layout schematics, flashing instructions, and a detailed reference to the device's internal setting keywords.

---

## 1. User Quick Start Guide

### Hardware Pin Connections (ESP32-C3 Super Mini)
If you are building your own OLO Bit or troubleshooting hardware pins, connect the components to your **ESP32-C3 Super Mini** according to this layout:

| Component | Pin Function | ESP32-C3 Super Mini GPIO Pin |
|---|---|---|
| **OLED Display** | I2C SDA (Data) | **GPIO 20** |
| | I2C SCL (Clock) | **GPIO 21** |
| | Power Supply | 3.3V / GND |
| **Passive Buzzer** | Audio Output | **GPIO 2** |
| | Ground | GND |
| **Touch Button** | Capacitive Touch Input | **GPIO 1** |
| **NeoPixel RGB LED** | RGB Data In (DIN) | **GPIO 6** |
| | Power Supply | 5V (or 3.3V) / GND |

*Note: All pins are dynamic. If your custom device uses different GPIO lines, you can remap them anytime via the **Hardware** tab in the controller.*

### Quick Launch
1. Connect the OLO Bit hardware to your computer using a **USB-C Data Cable**.
2. Open the `index.html` page in **Google Chrome**, **Microsoft Edge**, or **Opera** (these browsers support the Web Serial API).
3. Connect and manage settings directly from the dashboard!

---

## 2. Web Serial Flasher Guide

If you need to install or update the device operating system, you can flash it directly from this web page without installing Arduino IDE or PlatformIO.

1. Locate the **SELECT DISPLAY TYPE FOR FIRMWARE** dropdown on the connect screen.
2. Select your OLED display type:
   * **SH1106 OLED (128x64)** - Default display driver.
   * **SSD1306 OLED (128x64)** - Alternate display driver.
3. Click the red **Install/Update Firmware** button (powered by ESP Web Tools).
4. Select the serial port labeled *USB JTAG/serial debug unit* or *ESP32-C3* and click **Connect**.
5. The installer will automatically flash the partition tables, bootloader, and default OLO Bit OS firmware binary, then reset the device.

---

## 3. Web Controller Tab walkthrough

Once connected, the screen scrolls down to show the full dashboard control panel. Always click **Save All Settings** at the top after making modifications to write settings to persistent flash memory (NVS).

*   **🖼️ GIFs Tab**: Set default/idle animations, upload custom animations, customize touch gestures, select active startup animations, and set positive or inverted pixel color modes.
*   **🎵 Audio Tab**: Customize tap sounds, melody notifications, boot-up startup chimes, and compose custom RTTTL melodies.
*   **⏰ Chronos Tab**: Configure time formatting (12H/24H), sync timezone, set focus timers, enable hydration alerts, configure daily alarms, adjust hourly chimes, set Do Not Disturb (DND) silences, and customize boot screen text.
*   **📝 Canvas Tab**: Type a custom text message, select a font size and layout style, and slide/scroll/blink live announcements onto your display instantly.
*   **⚙️ Hardware Tab**: Map internal pins to match customized boards, select driver modes, and invert the display orientation.

---

## 4. Useful Settings Keywords & Value Reference

The settings on OLO Bit can be modified either via the physical device screen menu or over USB Serial. Below is a list of all useful configuration keywords, ranges, and index values:

### LED Settings
| Setting Menu Name | Internal Variable / Key | Value Options | Description |
|---|---|---|---|
| **LED Power** | `led_enabled` | `0` = Disabled<br>`1` = Enabled | Turns the NeoPixel RGB LED on or off |
| **LED Effect** | `led_effect` | `0` = Static Color<br>`1` = Breathing animation<br>`2` = Rainbow Wave<br>`3` = Color Cycle animation<br>`4` = Blink/Flash | Sets the RGB animation pattern |
| **LED Color** | `led_color` | **0** = Red<br>**1** = Green<br>**2** = Blue<br>**3** = Yellow<br>**4** = Cyan<br>**5** = Magenta<br>**6** = White<br>**7** = Orange | Sets the default active RGB color |
| **Brightness** | `led_brightness` | `0` to `10` | Adjusts brightness level (0 = dimmest, 10 = brightest) |

### Watch Face Styles
| Key | Value Options | Watch Face Layout Style |
|---|---|---|
| `watch_face` | `0` | **Classic Digital** (Standard font) |
| | `1` | **Casio Retro** (Segmented digital font layout) |
| | `2` | **Analog** (Analog hand clock layout) |
| | `3` | **7-Segment** (Big block clock digits) |

### Hourly Chime Styles
| Key | Value Options | Chime Audio Melody Style |
|---|---|---|
| `chime_style` | `0` | **Classic Westminster** chime chimes |
| | `1` | **Casio Retro Double-Beep** tone chimes |

### Water Reminder Intervals
| Key | Value Options (in minutes) | Water Intake Periodic Alert Interval |
|---|---|---|
| `water_reminder_interval` | `15` \| `30` \| `45` \| `60` \| `90` \| `120` | Reminds the user to drink water at set interval |

### Font Configurations (Canvas & Boot Title)
| Font Key | Value Options | Font Family Style |
|---|---|---|
| `boot_font`<br>`canvas_font` | `0` | **Helvetica Bold** |
| | `1` | **Times Bold** |
| | `2` | **Courier Bold** |
| | `3` | **New Century Bold** |
| | `4` | **Lucida Regular** |

### Canvas Layout Styles
| Key | Value Options | Live Scroll Direction / Animation |
|---|---|---|
| `canvas_anim` | `0` | **Scroll Left** (standard scroll) |
| | `1` | **Scroll Right** |
| | `2` | **Bounce Scroll** (bounces side to side) |
| | `3` | **Typewriter Effect** (characters appear one by one) |
| | `4` | **Blinking / Flash** (text blinks continuously) |
| | `5` | **Fixed** (static text layout) |

---

## 5. Serial Communication Protocol

The OLO Bit communicates via plain-text messages over standard UART USB serial at **115200 baud**. 

*   Commands sent to the device are formatted as: `key:value` (e.g., `watch_face:1`).
*   To fetch settings, send: `set:get`.
*   To save modifications to NVS flash, send: `set:save`.
*   To restart the device, send: `set:reset`.
*   To restore default factory state, send: `set:clear_nvs`.