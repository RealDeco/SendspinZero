!!! ALBUM ART DISABLED UNTIL 2026.2.0 !!

---

# Minimalistic Sendspin Media Player for ESPHome / Home Assistant

A tiny Sendspin media player with **cover art display** and a **weather clock**, built around the **ESP32-S3 Zero**.

This project turns a small, inexpensive ESP32 board into a compact **audio receiver** for your amplifier, with a screen for album art, Song, Artist, and a weather clock when not playing.

---

## About the Project

This started as a fun experiment: I wanted to see if the little **ESP32-S3 Zero** would work with Sendspin. Since it has **2 MB of PSRAM**, I figured it *might* be possible—and it turns out, it is.

Once that worked, it hit me: instead of building yet another “Sendspin speaker”, why not make a **tiny receiver** for my amplifier?

So I:

* Replaced the **MAX98357** with a **PCM5102A DAC**
* Designed a custom case
* Added a display for **cover art** and a **weather clock**

…and this is the result 🙂

---

## Photos

<p float="left">
  <img src="https://github.com/user-attachments/assets/d5c4868f-853d-4685-beb3-79a2a368fe85" width="45%" />
  <img src="https://github.com/user-attachments/assets/234270a5-7343-45c7-a838-e55080f99edb" width="45%" />
</p>


---

## Cost

All parts were sourced from AliExpress and added up to **just over $10** the last time I checked.

---

## Parts List

* **1 × ESP32-S3 Zero**
  [https://www.aliexpress.com/item/1005009890203011.html](https://www.aliexpress.com/item/1005009890203011.html)

* **1 × PCM5102A DAC**
  [https://www.aliexpress.com/item/1005008130629022.html](https://www.aliexpress.com/item/1005008130629022.html)

* **1 × 1.54" LCD screen**
  [https://www.aliexpress.com/item/1005008703777053.html](https://www.aliexpress.com/item/1005008703777053.html)

---

## Diagram & Pins Used

<img width="100%" alt="Wiring diagram" src="https://github.com/user-attachments/assets/a2e1a7a3-8c68-4d39-9ab9-c8ddd73a0274" />

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

### Power (Both Modules, make two split cables)

* **GND**
* **3.3V**

---

