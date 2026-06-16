# OLO Bit Web Controller - Technical Manual & Flasher Guide

Welcome to the OLO Bit Web Controller! This static HTML application allows users to configure and program their OLO Bit devices directly from modern web browsers (Chrome, Edge, or Opera) using the Web Serial API.

---

## 1. Hardware Pin Connections (ESP32-C3 Super Mini)

To build your own OLO Bit device using an **ESP32-C3 Super Mini** development board, connect the components according to the default configuration table below:

| Component | Pin Function | ESP32-C3 Super Mini GPIO Pin |
|---|---|---|
| **OLED Display** | I2C SDA (Data) | **GPIO 20** |
| | I2C SCL (Clock) | **GPIO 21** |
| | VCC / GND | 3.3V / GND |
| **Passive Buzzer** | Audio Output | **GPIO 2** |
| | Negative Pin | GND |
| **Touch Button** | Touch Input | **GPIO 1** (pulls HIGH on touch) |
| **NeoPixel LED** | RGB DIN (Data) | **GPIO 6** |
| | VCC / GND | 5V (or 3.3V) / GND |

---

## 2. Web Serial Firmware Flasher

The integrated flasher on the main page of the controller uses the official **ESP Web Tools** framework to download and flash firmware directly to the ESP32-C3 via USB.

### Prerequisites
1. Connect your ESP32-C3 Super Mini board to your computer via a USB-C data cable.
2. Open this web page : https://micromakerlabsfiles-git.github.io/OLOBit_Web_Controller/ in Chrome, Edge, or Opera.

### How to Flash
1. On the main connection screen, click **Flash Firmware**.
2. A modal popup managed by ESP Web Tools will appear. Click **Connect**.
3. Select the serial port corresponding to your device (usually listed as *USB JTAG/serial debug unit* or *ESP32-C3*) and click **Connect**.
4. ESP Web Tools will fetch `manifest.json` and the `.bin` files from the server, put the chip into ROM bootloader mode, flash them sequentially, and automatically perform a reset once finished.

---