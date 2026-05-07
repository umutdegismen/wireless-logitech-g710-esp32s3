# ESP32-S3 USB Keyboard to BLE Bridge (4-Slot)

This project transforms an **ESP32-S3** into a multi-slot Bluetooth LE bridge for wired USB keyboards. It is specifically optimized for the **Logitech G710**, featuring custom G-key mappings, media control, and intelligent power management.

## Features

- **4 BLE Slots:** Switch between four different host devices with unique identities.
- **Logitech G710 Mappings:** - **G1–G6** keys map to **F13–F18**.
    - **M1–M3 & MR** keys map to **F19–F22**.
- **Media Controls:** Full support for Volume Up/Down, Mute, Play/Pause, Stop, and Track Next/Previous.
- **Battery Monitoring:** Reports battery percentage to the host OS.
- **Power Management:** - **Eco Mode:** LED dims after 10 seconds of inactivity.
    - **Deep Sleep:** Auto-sleep after 30 minutes; wake via the BOOT button.

## Hardware Connections

### Pin Mapping
| Component | ESP32-S3 Pin | Notes |
| :--- | :--- | :--- |
| **USB VBUS Enable** | GPIO 12 | Powers the USB-A port |
| **Status LED (DIN)** | GPIO 5 | SK6812 GRBW (Neopixel) |
| **External BOOT** | GPIO 6 | Button to GND |
| **External RESET** | RST Pin | Hardware reset |
| **Battery ADC** | GPIO 3 | Voltage divider input |

### Battery Wiring (ADC)
To monitor battery levels, connect the **TP4056 BAT+** through a 100kΩ / 100kΩ voltage divider:
`TP4056 BAT+` ⮕ `100kΩ` ⮕ **GPIO 3** ⮕ `100kΩ` ⮕ `GND`

## Controls & Hotkeys

All commands use the **Insert** key as the modifier.

| Action | Keyboard Combo | BOOT Button |
| :--- | :--- | :--- |
| **Switch Slot** | `Insert + 1/2/3/4` | Short Press (Cycle) |
| **Pairing Mode** | `Shift + Insert + 1/2/3/4` | Long Press (1.5s) |
| **Factory Reset** | `Shift + Insert + 0` | — |

## LED Indicators

The bridge uses **Catppuccin** themed colors for slot identification:
* **Slot 1:** Blue (`0x04A5E5`)
* **Slot 2:** Orange (`0xFE640B`)
* **Slot 3:** Red (`0xD20F39`)
* **Slot 4:** Green (`0x40A02B`)

### Visual States
- **Solid Color:** Connected and active.
- **Breathing:** Pairing mode (visible to new devices).
- **Triple Blink:** Reconnecting to a saved host.
- **Dimmed Teal:** Eco Mode (Idle).

## Build & Flash

1. Open in **VS Code** with the **PlatformIO** extension.
2. Connect your ESP32-S3.
3. Run the **PlatformIO: Upload** task.

## License
MIT