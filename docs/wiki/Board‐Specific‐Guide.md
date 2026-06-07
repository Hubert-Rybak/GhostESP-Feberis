# Board-Specific Guide for GhostESP Firmware


```anything you read here may or may not be entirely accurate or up to date.``` 

This guide helps you identify your board type and start using GhostESP firmware.

## Identifying Your Board

### CYD (Cheap Yellow Display) Boards

CYD boards are recognizable by their yellow color and integrated display.

Features:
- Built-in display with touch functionality
- SD card slot
- RGB LED indicators
- Supported variants:
    - CYD2USB: USB-C only
    - CYDMicroUSB: Micro USB only
    - CYDDualUSB: USB-C and Micro USB (now supported)
    - AITRIP CYD: ESP32-2432S028R

Note: CYD boards using the ESP32-2432S028 (2.8 inches) are supported. The ESP32-2432S024 variant (2.4 inches) is not compatible.

For more help identifying your CYD, see the [CYD ID Guide](./CYD-ID-Guide.md).

### 7-Inch Display Boards

High-resolution display boards supported:
- Waveshare LCD: 800x480 resolution
- Crowtech LCD: 800x480 resolution
Both use the ESP32-S3.

### Awok and Marauder Boards

Supported variants:
- MarauderV6 and AwokDual: 240x320 touchscreen
- AwokMini: 128x128 display with joystick
- Awok V5

### BPM Circuits Feberis / Feberis Pro

BPM Circuits Feberis boards are Flipper Zero GPIO add-ons based on the classic ESP32.

Supported build artifacts:

- **Feberis:** `Feberis.zip`
- **Feberis Pro:** `FeberisPro.zip`
- **PC full-image flashing:** `Feberis-merged-gesp.bin` or `FeberisPro-merged-gesp.bin`

Feature notes:

- Both builds enable the onboard NeoPixel/RGB LED on GPIO25.
- Both builds enable GhostESP NFC/Chameleon-related features.
- Feberis Pro enables GPS on UART RX GPIO4 at 9600 baud.
- Feberis has GPS disabled.
- Display, keyboard, SD card, battery monitor, and infrared transmitter are not enabled for these builds.

First-install warning:

- If you are moving from stock BPM Circuits Marauder firmware to GhostESP, do **not** flash only `firmware.bin` as a FirmwareA-only update.
- Flash `bootloader.bin` at `0x1000`, `partitions.bin` at `0x8000`, and `firmware.bin` at `0x10000`, or flash the merged image at `0x0` from a PC.
- The stock Marauder Feberis OTA app slot is smaller than this GhostESP app image, so app-only flashing can boot loop until recovered with a full flash.

### Rabbit Labs GhostESP Board

- ESP32-C6 based
- Rabbit Labs GPS module port
- Three RGB LEDs
- Built-in SD card slot

### ESP32 Cardputer

A compact, keyboard-integrated board:
- Built-in display (240x135)
- Integrated keyboard
- SD card slot
- Terminal app for keyboard-based commands
- Infrared (IR) support with FlipperZero file compatibility

### LilyGo Boards

- LilyGo T-Watch S3: Smartwatch-style device with touchscreen and IR support (FlipperZero compatible)
- LilyGo TEmbed C1101: Compact embedded board
- LilyGo T-Deck

### Generic ESP32 Boards

Standard ESP32 models, with varying compatibility:
- ESP32 (standard model)
- ESP32-S2 (includes Flipper WiFi Devboard)
- ESP32-S3
- ESP32-C3
- ESP32-C5
- ESP32-C6

Feature notes:
- SD card support:
    - Full support: CYD boards, Cardputer
    - Not supported: Marauder V6, Awok Dual Touch, Awok Mini, Feberis, Feberis Pro
- Standby mode is available for non-touch displays.
- Power saving mode is available on Cardputer, S3TWatch, and LilyGo TEmbed C1101.

## Getting Started with GhostESP

1. Visit [The Flasher](https://flasher.ghostesp.net/).
2. Select your board type and follow the instructions.
3. For troubleshooting, use the [Discord community](https://discord.gg/5cyNmUMgwh).

## SD Card Compatibility

- Fully supported: CYD boards, Cardputer
- Not supported: Marauder V6, Awok variants, Generic ESP32 builds
- For updates on compatibility, check Discord announcements or the CHANGELOG.md

## Known Limitations

- No SD card support on Marauder V6, Awok variants, Feberis, or Feberis Pro
- ESP32S2 boards do not support Bluetooth
- Infrared (IR) functionality is available only on supported devices.

## Support and Community

- Join the [Discord Community](https://discord.gg/5cyNmUMgwh) for support and updates
- Visit the [GitHub Repository](https://github.com/jaylikesbunda/Ghost_ESP) for releases and reporting issues
- Use the [Web Flasher](https://flasher.ghostesp.net/) for firmware installation
