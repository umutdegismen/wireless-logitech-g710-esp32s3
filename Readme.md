# LOGITECH G710 USB Keyboard to BLE Bridge with ESP32-S3 (4-Slots) v1.3

This firmware transforms an **ESP32-S3** into a multi-slot Bluetooth LE bridge for wired USB keyboards. It is specifically optimized for the **Logitech G710**, providing custom G-key mappings, full media control support, and intelligent power management.

## Changelog

### v1.3
- **Removed** battery level monitoring (hardware ADC circuit removed from GPIO 3).
- **Removed** GPIO 12 VBUS enable (keyboard VBUS now powered directly from MT3608).

### v1.2
- Added battery level reporting via BLE Battery Service.
- Added external SK6812 GRBW LED support on GPIO 6.
- Added external BOOT micro switch on GPIO 5.
- Added external RESET micro switch on RST pin.
- Device name updated to `Logitech G710 - PC1/2/3/4`.

### v1.1
- Added G1–G6 key mappings to F13–F18.
- Added M1–M3 & MR key mappings to F19–F22.
- Added full media key support (Volume, Mute, Play/Pause, Stop, Track navigation).
- Fixed keyboard backlight button interference (Alt key ghost press resolved).

### v1.0
- Initial release: USB to BLE bridge with 4 switchable slots.

## Features

- **4 Switchable BLE Slots:** Seamlessly switch between 4 different host devices.
- **G710 Specific Mappings:**
    - **G1–G6** keys map to **F13–F18**.
    - **M1–M3 & MR** keys map to **F19–F22**.
- **Full Media Support:** Dedicated support for Volume Up/Down, Mute, Play/Pause, Stop, and Track navigation.
- **Intelligent Power Management:**
    - **Eco Mode:** LED dims/shifts to teal after 10 seconds of inactivity.
    - **Deep Sleep:** Enters sleep mode after 30 minutes; wake via BOOT button.

## Hardware Configuration

### Pin Mapping
| Component | ESP32-S3 Pin | Notes |
| :--- | :--- | :--- |
| **Status LED** | GPIO 6 | SK6812 GRBW (Neopixel) |
| **BOOT Switch** | GPIO 5 | External button to GND |
| **RESET Switch** | RST Pin | Hardware reboot |

### Power
| Component | Connection | Notes |
| :--- | :--- | :--- |
| **Battery** | TP4056 BAT+ / BAT- | LiPo 3.7V |
| **Charger** | TP4056 IN+ / IN- | USB 5V input |
| **Switch** | TP4056 OUT+ → Switch → MT3608 IN+ | On/Off control |
| **Boost Converter** | MT3608 OUT+ → ESP32 5V pin | 3.7V → 5V |
| **Keyboard VBUS** | MT3608 OUT+ → USB-A breakout VBUS | Direct 5V to keyboard |
| **Keyboard Data** | USB-A breakout D+/D- → ESP32 USB port | Via OTG adapter |

## Controls & Hotkeys

All keyboard commands use the **Insert** key as the primary modifier.

| Action | Keyboard Combo | BOOT Button |
| :--- | :--- | :--- |
| **Switch Slot (Reconnect)** | `Insert + 1/2/3/4` | Short Press (Cycle) |
| **Pairing Mode** | `Shift + Insert + 1/2/3/4` | Long Press (1.5s) |
| **Factory Reset** | `Shift + Insert + 0` | — |

## LED Visual Indicators

The bridge uses **Catppuccin** themed colors to identify the active slot:
* **Slot 1 (PC1):** Blue (`0x04A5E5`)
* **Slot 2 (PC2):** Orange (`0xFE640B`)
* **Slot 3 (PC3):** Red (`0xD20F39`)
* **Slot 4 (PC4):** Green (`0x40A02B`)

### Patterns
- **Solid Color:** Connected and active.
- **Breathing:** Pairing mode (visible to new devices).
- **Triple Blink:** Reconnecting to a saved host.
- **Dimmed/Teal:** Eco Mode (Idle).
- **LED Off:** Deep Sleep.

## Build & Flash

1. Open the project in **VS Code** with the **PlatformIO** extension.
2. Connect your ESP32-S3 via the COM port (left USB-C).
3. Run the **PlatformIO: Upload** task.

## Notes

- On deep sleep, press the external **BOOT** button (GPIO 5) to wake.
- If pairing issues occur, run factory reset (`Shift + Insert + 0`) and remove old bonds on the host.
- The keyboard's own backlight buttons function normally and do not interfere with BLE output.

## License
MIT
