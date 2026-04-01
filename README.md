
<img width="1500" height="603" alt="Screenshot 2026-03-15 at 08 15 55 copy" src="https://github.com/user-attachments/assets/cf58463a-1112-4aff-8982-a297d2f72e1a" />


# Minimalistic Sendspin Media Player for Home Assistant

A tiny Sendspin media player with **cover art display** and a **weather clock**, built around the **ESP32-S3 Zero**.

This project turns a small, inexpensive ESP32 board into a compact **audio receiver** for your amplifier, with a screen for album art, Song, Artist, and a weather clock when not playing.

Each version could be made with either a Display, No Display, or a Big Button. this totals 9 variants:

<img width="1348" height="653" alt="ff08444c-edad-47c3-bce7-56dd34dd00ec" src="https://github.com/user-attachments/assets/e5c695af-840a-4180-949f-62e7d3e10bb6" />

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


### If you plan to put it in the box, do not solder pins to the DAC, zero and display, solder cords directly to boards or they won't fit.
### I reused the display from breadboard that had pins soldered on so had to bend 2 legs to make space for the jack.
![20260225_184128](https://github.com/user-attachments/assets/2a2601aa-c974-442e-9661-5e50fb09f139)



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

### And remember to solder the pads as on the on the back of the PCM5102A like in this image. and on the front, solder the bridge by SCK (some comes soldered, others unsoldered):
<img src="https://github.com/user-attachments/assets/17d6b71f-2928-4bff-ac34-9cff48638098" />

---

## Toslink (optical audio) version.

Toslink version without display, this is about the easiest project to make! and for under §10 :)

(for using with display or button, the pins are the same for those)

<img width="2544" height="1211" alt="Screenshot 2026-03-07 at 06 19 25" src="https://github.com/user-attachments/assets/f600ec5b-6d98-4597-b9a6-dfba106eeef2" />

Your Soundbar will love you for it ;) - 3D files for case is in [3D_Files](3D_Files)

## Pin Mapping (even easier)

### ESP32-S3 → toslink connector

| ESP32-S3 GPIO | TOSLINK PLUG |
| ------------- | ------------ |
| GPIO4         | VIN (DATA)   |
| 3.3V          | VCC          |
| GND           | GND          |

Pins on this specific toslink plug:
<img width="1741" height="774" alt="Screenshot 2026-03-08 at 08 25 18" src="https://github.com/user-attachments/assets/708cf545-3853-44d9-be97-c54bd7d5a25a" />

---

Links to parts, esp32-s3 zero is same as above, toslink connector that fits the 3D case:

single: https://www.aliexpress.com/item/1005011593001325.html

1-10pcs: https://www.aliexpress.com/item/1005008393864163.html

Cords: https://www.aliexpress.com/item/1005008202856228.html

and 1 M2.6x10 self tapping screw to hold the toslink plug in place

!IMPORTANT: remember to choose "Transmitting end" (A1)

---

## Coax (digital audio) version.

Coax version without display, this is about the easiest project of them all, just two cords and a resistor

(for using with display or button, the pins are the same for those)

<img width="1000" height="459" alt="Image" src="https://github.com/user-attachments/assets/0daa8227-f093-4db7-932d-d1da08eeb516" />

3D files for case is in [3D_Files](3D_Files)

## Pin Mapping

### ESP32-S3 → toslink connector

| ESP32-S3 GPIO | RCA PLUG     |
| ------------- | ------------ |
| GPIO4         | VIN (DATA)   |
| GND           | GND          |
---

Links to parts, esp32-s3 zero is same as above:

RCA female: https://www.aliexpress.com/item/1005010424983352.html

Cords: https://www.aliexpress.com/item/1005008202856228.html

---

## Button!

Instead of display or no display, there's now a 3rd option, a big nice button with light :)

Functionality: Single click_ start/stop playback, Double click: next song: Triple click: previous song.

Hold: switches from sendspin control to HA control or back, and light will change to orange'ish

In HA control mode the triggers are simply exposed to HA for use in automations. (single double, triple click)

![button-led](https://github.com/user-attachments/assets/58495e54-4e8d-465a-86ac-04d2dd644c3c)

3D files for case is in [3D_Files](3D_Files)

## Pin Mapping

### ESP32-S3 → Button (22mm 2 color)

| ESP32-S3 GPIO | BUTTON       |
| ------------- | ------------ |
| GPIO1         | 1            |
| GPIO2         | 3            |
| GPIO3         | 4            |
| GND           | 2 + 5        |

---

<img width="549" height="594" alt="Screenshot 2026-03-30 at 20 38 24" src="https://github.com/user-attachments/assets/43835fa0-46af-49d7-95a4-fb2c2d7c3063" />

Links to part:

This low profile button is a little expensive but also VERY nice :)

Inportant to select the correct size, and voltage:

22mm Bicolor (RG) Black 3-6V : https://www.aliexpress.com/item/1005004920346156.html

---
