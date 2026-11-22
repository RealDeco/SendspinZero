# USB Audio Adapter Compatibility

| Device | USB VID:PID | Mic / line in | Mic channels tested | Mic Sample rates | USB identification | USB capture | USB playback | ESP-IDF override fix |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Fun Generation UA-202 | `08bb:29c2` | line in / phono in (turntable) | 2 (1 OK) | 48 kHz | TI PCM2902C | 2 ch, 16-bit, up to 48 kHz | 2 ch, 16-bit, 32 / 44.1 / 48 kHz | Fix #1 needed |
| Dongle 1 (black, two jacks) | `1b3f:2008` | Mono mic | 1 (2 not OK) | 44.1 / 48 kHz | Generalplus USB Audio | 1 ch, 16-bit, 44.1 / 48 kHz | 2 ch, 16-bit, 44.1 / 48 kHz (published dump for this USB ID) | No fix needed |
| Dongle 2 (transparent) | `001f:0b21` | Mono mic | 1 (2 not OK) | 48 kHz | Bluetrum AB13X | 1 ch, 48 kHz (bit depth unverified) | 2 ch, 48 kHz reported on one variant | without fix #2 on S3 |
| Dongle 3 (one jack on cable) | `0666:0880` | Mic | 2 (1 not OK) | 44.1 / 48 kHz | SPACETOUCH USB Audio | 2 ch, 16-bit, 44.1 / 48 kHz | Playback tested on S31 (full format list unverified) | Fix #2 needed |
| Dongle 4 (Creative Play! 3) | `041e:324d` | Mic | 2 (1 not OK) | 44.1 / 48 kHz | Sound Blaster Play! 3 | 2 ch, 16/24-bit, 44.1 / 48 kHz | 2 ch, 16/24-bit, 44.1 / 48 / 96kHz Playback tested on S31| Fix #2 needed |

## ESP-IDF overrides

Add the relevant setting under `esp32.framework.sdkconfig_options`.

| Fix | Setting |
| --- | --- |
| #1 | `CONFIG_USB_HOST_CONTROL_TRANSFER_MAX_SIZE: "4096"` |
| #2 | `CONFIG_USB_HOST_HW_BUFFER_BIAS_PERIODIC_OUT: y` |

Fix #2 only works on S31, not S3.

<img width="300" alt="f6ecbb18-b2a6-4bdb-9260-e83e32ec90fe" src="https://github.com/user-attachments/assets/0226ea84-872c-4963-924d-2a53c0ac5d6c" />

<img width="300" alt="2aa68699-ce88-43b3-8f80-da0badb88686" src="https://github.com/user-attachments/assets/500c59d4-0922-4a33-9df0-13bb736c5ed8" />

<img width="300" alt="ca3efb3b-f072-488f-8b3e-7634fc1236b3" src="https://github.com/user-attachments/assets/467b62b1-1517-43af-838e-bff160ab8cf8" />

<img width="300" alt="993bf435-8d90-4a2b-bacf-6fb1eb3dd527" src="https://github.com/user-attachments/assets/bd460323-ee13-4a84-a185-c212610a9b85" />

<img width="300" alt="0e999505-ccaf-4d93-9b46-7ea6f3d08dba" src="https://github.com/user-attachments/assets/64e15d7f-8e0c-4ba7-bd15-b9f6b4542a6b" />
