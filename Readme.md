# LOGITECH G710 USB Keyboard to BLE Bridge with ESP32-S3 (4-Slots) v1.2

This firmware transforms an **ESP32-S3** into a multi-slot Bluetooth LE bridge for wired USB keyboards. It is specifically optimized for the **Logitech G710**, providing custom G-key mappings, full media control support, and battery level reporting.

## Features

- **4 Switchable BLE Slots:** Seamlessly switch between 4 different host devices.
- **G710 Specific Mappings:** - **G1–G6** keys map to **F13–F18**.
    - **M1–M3 & MR** keys map to **F19–F22**.
- **Full Media Support:** Dedicated support for Volume Up/Down, Mute, Play/Pause, Stop, and Track navigation.
- **Battery Reporting:** Real-time battery percentage monitoring visible on the host OS.
- **Intelligent Power Management:** - **Eco Mode:** LED dims/shifts to teal after 10 seconds of inactivity.
    - **Deep Sleep:** Enters sleep mode after 30 minutes; wake via BOOT button.

## Hardware Configuration

### Pin Mapping
| Component | ESP32-S3 Pin | Notes |
| :--- | :--- | :--- |
| **USB VBUS Enable** | GPIO 12 | Powers the USB-A host port |
| **Status LED** | GPIO 5 | SK6812 GRBW (Neopixel) |
| **BOOT Switch** | GPIO 6 | External button to GND |
| **RESET Switch** | RST Pin | Hardware reboot |
| **Battery ADC** | GPIO 3 | 100kΩ / 100kΩ voltage divider |

### Battery Monitoring (ADC)
To monitor battery levels, use a voltage divider on **GPIO 3**:
`TP4056 BAT+` ⮕ `100kΩ Resistor` ⮕ **GPIO 3** ⮕ `100kΩ Resistor` ⮕ `GND`

## Controls & Hotkeys

All keyboard commands use the **Insert** key as the primary modifier.

| Action | Keyboard Combo | BOOT Button |
| :--- | :--- | :--- |
| **Switch Slot (Reconnect)** | `Insert + 1/2/3/4` | Short Press (Cycle) |
| **Pairing Mode** | `Shift + Insert + 1/2/3/4` | Long Press (1.5s) |
| **Factory Reset** | `Shift + Insert + 0` | — |

## LED Visual Indicators

The bridge uses **Catppuccin** themed colors to identify the active slot:
* **Slot 1:** Blue (`0x04A5E5`)
* **Slot 2:** Orange (`0xFE640B`)
* **Slot 3:** Red (`0xD20F39`)
* **Slot 4:** Green (`0x40A02B`)

### Patterns
- **Solid Color:** Connected and active.
- **Breathing:** Pairing mode (visible to new devices).
- **Triple Blink:** Reconnecting to a saved host.
- **Dimmed/Teal:** Eco Mode (Idle).

## Build & Flash

1. Open the project in **VS Code** with the **PlatformIO** extension.
2. Connect your ESP32-S3 via USB.
3. Run the **PlatformIO: Upload** task.

## License
MIT