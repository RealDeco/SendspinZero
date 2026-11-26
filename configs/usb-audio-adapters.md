# USB Audio Adapter Compatibility

| Device | USB VID:PID | Mic / line in | Mic channels tested | Mic Sample rates | USB identification | USB capture | USB playback | ESP-IDF override fix |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Fun Generation UA-202 | `08bb:29c2` | line in / phono in (turntable) | 2 (1 OK) | 48 kHz | TI PCM2902C | 2 ch, 16-bit, up to 48 kHz | 2 ch, 16-bit, 32 / 44.1 / 48 kHz | Fix #1 needed |
| Dongle 1 (black, two jacks) | `1b3f:2008` | Mono mic | 1 (2 not OK) | 44.1 / 48 kHz | Generalplus USB Audio | 1 ch, 16-bit, 44.1 / 48 kHz | 2 ch, 16-bit, 44.1 / 48 kHz (published dump for this USB ID) | No fix needed |
| Dongle 2 (transparent) | `001f:0b21` | Mono mic | 1 (2 not OK) | 48 kHz | Bluetrum AB13X | 1 ch, 48 kHz (bit depth unverified) | 2 ch, 48 kHz reported on one variant | without fix #2 on S3 |
| Dongle 3 (one jack on cable) | `0666:0880` | Mono mic | 2 (1 not OK) | 44.1 / 48 kHz | SPACETOUCH USB Audio | 1 ch, 16-bit, 44.1 / 48 kHz | Playback tested on S31 (full format list unverified) | Fix #2 needed |
| Dongle 4 (Creative Play! 3) | `041e:324d` | Mono mic | 2 (1 not OK) | 44.1 / 48 kHz | Sound Blaster Play! 3 | 1 ch, 16/24-bit, 44.1 / 48 kHz | 2 ch, 16/24-bit, 44.1 / 48 / 96kHz Playback tested on S31| No fix needed |
| Dongle 5 (One jack on cable USB-C) | `0666:0880` | Mono mic | 2 (1 not OK) | 44.1 / 48 kHz | SPACETOUCH | 1 ch, 16-bit, 44.1 / 48 kHz | 2 ch, 16-bit, 44.1 / 48 kHz | Fix #2 needed |
| Dongle 6 (White dongle) | `001f:0b21` | Mono mic | 1 (2 not OK) | 44.1 / 48 kHz | Generic | 1 ch, 16-bit, 44.1 / 48 kHz | 2 ch, 16-bit, 44.1 / 48 kHz | No fix needed  |
| Dongle 7 (black and white, two jacks) | `1b3f:2008` | Mono mic | 1 (2 not OK) | 44.1 / 48 kHz | GeneralPlus | 1 ch, 16-bit, 44.1 / 48 kHz | 2 ch, 16-bit, 44.1 / 48 kHz | No fix needed |
| Dongle 8 (One jack on cable) | `3302:20c1` | Mono mic | 1 (2 not OK) | 44.1 / 48 kHz | TTGK Technology | 1 ch, 16/24-bit, 44.1 / 48 kHz | 2 ch, 16/24/32-bit, 44.1/48/96 kHz | No fix needed |


## ESP-IDF overrides

Add the relevant setting under `esp32.framework.sdkconfig_options`.

| Fix | Setting |
| --- | --- |
| #1 | `CONFIG_USB_HOST_CONTROL_TRANSFER_MAX_SIZE: "4096"` |
| #2 | `CONFIG_USB_HOST_HW_BUFFER_BIAS_PERIODIC_OUT: y` |

  ### Fix #2 and the ESP32-S3: speaker or mic, not both
  
  Some cards (like Dongle 3) declare a much larger USB packet for playback than they actually use (600 bytes,
  while 48 kHz / 16-bit stereo needs about 196). ESP-IDF reserves USB buffer memory (FIFO) for the declared
  size, so these cards need fix #2 to play at all.
  
  The ESP32-S3 has too little USB FIFO to hold that 600-byte playback buffer and a 2-channel mic stream at
  the same time. With fix #2 and the mic at 2 channels, ESPHome stops the build with *"The requested USB
  packets don't fit the FIFO split..."*. So on the S3, a card that needs fix #2 is **speaker only**: set the
  mic to 1 channel (`usb_mic_channels: "1"`) or remove the mic. The build then passes and the speaker works,
  but the mic won't, because these cards only send 2 channels.
  
  The ESP32-P4 and S31 have enough FIFO for both. On the S3, pick a card that doesn't need fix #2 if you want
  the mic too. Fix #1 is fine (the UA-202 does both on the S3).

<img width="300" alt="f6ecbb18-b2a6-4bdb-9260-e83e32ec90fe" src="https://github.com/user-attachments/assets/0226ea84-872c-4963-924d-2a53c0ac5d6c" />

<img width="300" alt="2aa68699-ce88-43b3-8f80-da0badb88686" src="https://github.com/user-attachments/assets/500c59d4-0922-4a33-9df0-13bb736c5ed8" />

<img width="300" alt="ca3efb3b-f072-488f-8b3e-7634fc1236b3" src="https://github.com/user-attachments/assets/467b62b1-1517-43af-838e-bff160ab8cf8" />

<img width="300" alt="993bf435-8d90-4a2b-bacf-6fb1eb3dd527" src="https://github.com/user-attachments/assets/bd460323-ee13-4a84-a185-c212610a9b85" />

<img width="300" alt="0e999505-ccaf-4d93-9b46-7ea6f3d08dba" src="https://github.com/user-attachments/assets/64e15d7f-8e0c-4ba7-bd15-b9f6b4542a6b" />

<img width="300" alt="93800e9a-4475-43db-83a1-08c08af2f8bc" src="https://github.com/user-attachments/assets/28e3a1e1-0b7d-4795-9469-b334c81c60f8" />



<img width="300" alt="8a27dbd5-ea2d-44af-b85f-f8ea3ea6605b" src="https://github.com/user-attachments/assets/d4f14e8b-0076-4a72-b60a-57ac85c415fe" />

<img width="300" alt="a14a3f2c-7f0e-44bd-89dd-48df5fb8b367" src="https://github.com/user-attachments/assets/00f274ca-2e68-43c8-8873-ce0fa230b2f6" />

<img width="300" alt="9dd2ef27-4cc2-4849-bb5d-c89844ab5d0d" src="https://github.com/user-attachments/assets/d96c30a5-c96c-46f4-b423-e179a68a9feb" />
