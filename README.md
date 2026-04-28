
# Minimalistic Sendspin Media Player for Home Assistant

<img width="1500" height="603" alt="Screenshot" src="https://github.com/user-attachments/assets/cf58463a-1112-4aff-8982-a297d2f72e1a" />

A tiny Sendspin media player with **cover art display** and a **weather clock**, built around the **ESP32-S3 Zero**.

This project turns a small, inexpensive ESP32 board into a compact **audio receiver** for your amplifier, with a screen for album art, **song**, **artist**, and a weather clock when not playing, OR a Button to control with, or with nothing so you can hide it behind the tv/stereo.

Each version can be built with one of these options:

* Display
* No display
* Big button

That gives a total of **9 variants**:

<img width="1348" height="653" alt="Variants" src="https://github.com/user-attachments/assets/e5c695af-840a-4180-949f-62e7d3e10bb6" />

---

## About the Project

This started as a fun experiment: I wanted to see if the **ESP32-S3 Zero** would work with Sendspin. Since it has **2 MB of PSRAM**, I figured it *might* be possible—and it turns out, it is.

Once that worked, I thought: instead of building yet another “Sendspin speaker”, why not make a **tiny receiver** for my amplifier?

So I:

* Replaced the **MAX98357** with a **PCM5102A DAC**
* Designed a custom case
* Added a display for **cover art** and a **weather clock**

…and this is the result 🙂

---

## Photos

<p align="center">
  <img src="https://github.com/user-attachments/assets/d5c4868f-853d-4685-beb3-79a2a368fe85" width="45%" />
  <img src="https://github.com/user-attachments/assets/234270a5-7343-45c7-a838-e55080f99edb" width="45%" />
</p>

---

## Cost

All parts were sourced from AliExpress and added up to **just over $10** (last checked).

---

## Parts List

* **1 × ESP32-S3 Zero**
  [https://www.aliexpress.com/item/1005009890203011.html](https://www.aliexpress.com/item/1005009890203011.html)

  (be sure you select esp32-s3, not esp32-c3 which the page defaults to.)

* **1 × PCM5102A DAC**
  [https://www.aliexpress.com/item/1005008130629022.html](https://www.aliexpress.com/item/1005008130629022.html)

* **1 × 1.54" LCD screen**
  [https://www.aliexpress.com/item/1005008703777053.html](https://www.aliexpress.com/item/1005008703777053.html)

---

## Diagram & Pins Used

<img width="100%" alt="Wiring diagram" src="https://github.com/user-attachments/assets/a2e1a7a3-8c68-4d39-9ab9-c8ddd73a0274" />

### ⚠️ Assembly Notes

* If you plan to mount everything inside the case, **do NOT solder header pins** to the DAC, ESP32, or display.
  → Solder wires directly to the boards instead, otherwise they won’t fit.

* If your display already has pins:
  → You may need to **bend two pins** slightly to make room for the audio jack.

<img src="https://github.com/user-attachments/assets/2a2601aa-c974-442e-9661-5e50fb09f139" />

---

## Pin Mapping

### ESP32-S3 → PCM5102A

| ESP32-S3 GPIO | PCM5102A Pin |
| ------------- | ------------ |
| GPIO4         | LRCK         |
| GPIO5         | BCK          |
| GPIO6         | DIN          |

### ESP32-S3 → Display

| ESP32-S3 GPIO | Display Pin |
| ------------- | ----------- |
| GPIO7         | SCL         |
| GPIO8         | SDA         |
| GPIO9         | RST         |
| GPIO10        | DC          |
| GPIO11        | BL          |

### Power (both modules)

* **GND**
* **3.3V**

### Important DAC Setup

Make sure to:

* Solder the pads on the **back of the PCM5102A** (as shown below)
* Solder the bridge near **SCK on the front** (some boards come pre-soldered)

<img src="https://github.com/user-attachments/assets/17d6b71f-2928-4bff-ac34-9cff48638098" />

---

## Toslink (Optical Audio) Version

This version has **no display** and is the easiest build—**under $10** 🙂

(For display or button versions, pin usage is the same)

<img width="2544" height="1211" alt="Toslink version" src="https://github.com/user-attachments/assets/f600ec5b-6d98-4597-b9a6-dfba106eeef2" />

Your soundbar will love you for it 😉
3D files are in [`3D_Files`](3D_Files)

### Pin Mapping

### ESP32-S3 → Toslink Connector

| ESP32-S3 GPIO | TOSLINK    |
| ------------- | ---------- |
| GPIO4         | VIN (DATA) |
| 3.3V          | VCC        |
| GND           | GND        |

<img width="1741" height="774" alt="Pins" src="https://github.com/user-attachments/assets/708cf545-3853-44d9-be97-c54bd7d5a25a" />

### Parts

* Single: [https://www.aliexpress.com/item/1005011593001325.html](https://www.aliexpress.com/item/1005011593001325.html)
* 1–10 pcs: [https://www.aliexpress.com/item/1005008393864163.html](https://www.aliexpress.com/item/1005008393864163.html)
* Cables: [https://www.aliexpress.com/item/1005008202856228.html](https://www.aliexpress.com/item/1005008202856228.html)

- 1 × M2.6×10 self-tapping screw

⚠️ **Important:** Select **"Transmitting end" (A1)**

---

## Coax (Digital Audio) Version

Simplest version of all: **just two wires and a resistor**.

<img width="1000" height="459" alt="Coax version" src="https://github.com/user-attachments/assets/0daa8227-f093-4db7-932d-d1da08eeb516" />

3D files are in [`3D_Files`](3D_Files)

### Pin Mapping

### ESP32-S3 → RCA Connector

| ESP32-S3 GPIO | RCA        |
| ------------- | ---------- |
| GPIO4         | VIN (DATA) |
| GND           | GND        |

### Parts

* 1 pcs. 332-470ohm resistor [https://www.aliexpress.com/item/1005005252979796.html](https://www.aliexpress.com/item/1005005252979796.html)

* RCA female: [https://www.aliexpress.com/item/1005010424983352.html](https://www.aliexpress.com/item/1005010424983352.html)
* Cables: [https://www.aliexpress.com/item/1005008202856228.html](https://www.aliexpress.com/item/1005008202856228.html)

---

## Button Version

Instead of a display, you can use a **large illuminated button**.

### Controls

* **Single click** → Play / pause
* **Double click** → Next track
* **Triple click** → Previous track
* **Hold** → Toggle Sendspin / Home Assistant control mode

In HA mode, clicks are exposed for automations.

<img src="https://github.com/user-attachments/assets/58495e54-4e8d-465a-86ac-04d2dd644c3c" />

3D files are in [`3D_Files`](3D_Files)

### Pin Mapping

| ESP32-S3 GPIO | Button |
| ------------- | ------ |
| GPIO1         | 1      |
| GPIO2         | 3      |
| GPIO3         | 4      |
| GND           | 2 + 5  |

<img width="549" height="594" src="https://github.com/user-attachments/assets/43835fa0-46af-49d7-95a4-fb2c2d7c3063" />

### Part

**22mm Bicolor (RG) Black 3–6V**
[https://www.aliexpress.com/item/1005004920346156.html](https://www.aliexpress.com/item/1005004920346156.html)

---

## SendspinZero-Control (Knob + Button + Display)

This version uses a combo board with a **rotary encoder + button + display i found cheap on aliexpress**.

<img width="2395" height="722" src="https://github.com/user-attachments/assets/31692617-ce55-4ee5-8284-0439f045655c" />

3D files are in [`3D_Files`](3D_Files)

### Additional Pins

(Same as display version + these)

| ESP32-S3 GPIO | Combo Board |
| ------------- | ----------- |
| GPIO12        | TRA         |
| GPIO13        | TRB         |
| GPIO43 (TX)   | PSH         |
| GPIO44 (RX)   | KO          |

(TX = GPIO43, RX=GPIO44 on the zero board)

<img width="663" height="573" src="https://github.com/user-attachments/assets/e70dc743-2b43-4fc2-916d-d06a073357b1" />

### Part

ESP32-S3 Zero and PCM5102A as above +

[https://www.aliexpress.com/item/1005009900611104.html](https://www.aliexpress.com/item/1005009900611104.html)

---

## Display + Button Version

<img width="1727" height="716" src="https://github.com/user-attachments/assets/c1b9a7c7-e729-4363-bc9f-79d61cc3c463" />

3D files are in [`3D_Files`](3D_Files)

### Pin Mapping

Same as SendspinZero-Display + SendspinZero-Button

### Parts

same components as the other versions (esp32-s3 + PCM5102A DAC + Button) +

* 1.9" screen: [https://www.aliexpress.com/item/1005007098895718.html](https://www.aliexpress.com/item/1005007098895718.html)

---

## Speaker amplifier version

<img width="1536" height="1024" src="https://github.com/user-attachments/assets/7088001b-3a60-41a7-8856-7a2b5ccdfa96" />

<img width="2233" height="891" src="https://github.com/user-attachments/assets/13aa64f8-b2fb-4f75-b916-e04134e37608" />


NO 3D files made for this device.

This is the only device with amplifier onboard, it's mono so for stereo speakers you need a module for each speaker and have them playing as stereo in MA.

### Pin Mapping
(remove two pins from the spacer and solder the boards together)

| ESP32-S3 GPIO | MAX98357    |
| ------------- | ----------- |
| VCC (5V)      | VCC         |
| GND           | GND         |
| *not used*    |             |
| *not used*    |             |
| GPIO2         | DIN         |
| GPIO3         | BCLK        |
| GPIO4         | LRC         |

### Parts

same esp32-s3 zero as the other versions +

* MAX98357: https://www.aliexpress.com/item/1005007003802663.html


---
