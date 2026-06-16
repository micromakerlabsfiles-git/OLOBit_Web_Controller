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

The integrated **Flasher** tab uses the official **ESP Web Tools** framework to download and flash firmware directly to the ESP32-C3 via USB using a `manifest.json` definition file.

### Prerequisites
1. Ensure the main controller folder contains the following files in the same directory as `index.html`:
   - `manifest.json` (Describes flashing offsets and binary paths)
   - `bootloader.bin` (Flashing offset: `0x0`)
   - `partitions.bin` (Flashing offset: `0x8000`)
   - `firmware.bin` (Flashing offset: `0x10000`)
2. Connect your ESP32-C3 Super Mini board to your computer via a USB-C data cable.
3. Open this web page in Chrome, Edge, or Opera.

### How to Flash
1. Navigate to the **Flasher** tab.
2. Click **Program Firmware**.
3. A modal popup managed by ESP Web Tools will appear. Follow the prompts by clicking **Connect**.
4. Select the serial port corresponding to your device (usually listed as *USB JTAG/serial debug unit* or *ESP32-C3*) and click **Connect**.
5. ESP Web Tools will fetch `manifest.json` and the `.bin` files from the server, put the chip into ROM bootloader mode, flash them sequentially, and automatically perform a reset once finished.

> [!IMPORTANT]
> Because ESP Web Tools relies on standard `fetch()` calls to load the manifest and binaries, running the HTML page directly using the `file://` protocol will fail due to browser security/CORS restrictions. 
> To test or run the controller locally:
> 1. Open a terminal in the `Webcontroller V1` directory.
> 2. Start a simple local server: `python -m http.server 8000` (or your preferred local dev server).
> 3. Open your browser and navigate to: `http://localhost:8000`.

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
- `manifest.json` (the flashing manifest)
- `bootloader.bin`, `partitions.bin`, `firmware.bin` (firmware files)

Ensure all files are placed directly in the repository root folder.

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
