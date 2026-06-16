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

The integrated **Flasher** tab uses `esptool-js` to program firmware directly to the ESP32-C3 via USB. 

### Prerequisites
1. Ensure the controller folder contains a subdirectory named `firmware/` containing three files:
   - `bootloader.bin` (Flashing offset: `0x0`)
   - `partitions.bin` (Flashing offset: `0x8000`)
   - `firmware.bin` (Flashing offset: `0x10000`)
2. Connect your ESP32-C3 Super Mini board to your computer via a USB-C data cable.
3. Open this web page in Chrome, Edge, or Opera.

### How to Flash
1. Navigate to the **Flasher** tab.
2. Select your preferred **Baud Rate** (921600 is recommended for fastest programming).
3. Click **Program Firmware**.
4. A browser dialog will appear asking you to select a serial port. Select the port corresponding to your device (usually listed as *USB JTAG/serial debug unit* or *ESP32-C3*) and click **Connect**.
5. The flasher will put the chip into ROM bootloader mode, fetch the binary files from the server, and write them sequentially.
6. The loader will automatically perform a hard reset to reboot the chip. Once complete, you will see a success message and your device will run the newly programmed firmware.

---

## 3. How to Host on GitHub Pages

You can easily host this Web Controller as a free, public tool for your users using GitHub Pages.

### Step 1: Create a GitHub Repository
1. Log into your GitHub account.
2. Create a new public repository (e.g., named `olobit-controller`).

### Step 2: Upload Files
Upload all contents of the `Webcontroller V1` directory to the repository:
- `index.html` (the controller page)
- `music.html` (the buzzer composer tool)
- `assets/` (the logo and image assets for the grid)
- `firmware/` (the folder containing the `.bin` files)

Ensure the file structure matches exactly, so that `firmware/` is in the same folder as `index.html`.

### Step 3: Enable GitHub Pages
1. In your GitHub repository, go to **Settings** > **Pages** (under the Code and automation section).
2. Under **Build and deployment**, select **Deploy from a branch**.
3. Under **Branch**, choose `main` (or `master`) and select `/ (root)` folder.
4. Click **Save**.

### Step 4: Access Your Tool
Within 1–2 minutes, GitHub will host the page. The URL will be in the format:
`https://<your-username>.github.io/<repository-name>/`

> [!IMPORTANT]
> The Web Serial API strictly requires a secure context (`HTTPS`) to run. GitHub Pages serves your site over HTTPS by default, which ensures that the connection and flashing tools work perfectly.
