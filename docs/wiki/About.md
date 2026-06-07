# About GhostESP

GhostESP: Revival is an open source firmware for ESP32 microcontrollers.

## Supported Hardware

The following ESP32 models and boards are officially supported:

### Display-Enabled Boards

- **CYD (Cheap Yellow Display) variants**
  - **CYD2USB** (USB-C)
  - **CYDMicroUSB**
  - **CYDDualUSB** (Both ports)
  - **AITRIP CYD** (ESP32-2432S028R)
  - **CYD 2.4″ variants**
  - **Compatibility Note**: All CYD variants supported
- **Waveshare LCD (7-inch)**: 800x480 resolution, using ESP32-S3
- **Crowtech LCD (7-inch)**: 800x480 resolution, using ESP32-S3
- **Sunton LCD (7-inch)**: 800x480 resolution, using ESP32-S3
- **ESP32-S3-Cardputer**: Compact design with built-in display and keyboard
- **ESP32-S3-Cardputer ADV**: Advanced Cardputer variant
- **MarauderV4 & MarauderV6**: 240x320 touchscreen models
- **BPM Circuits Feberis & Feberis Pro**: Flipper Zero GPIO add-on boards; Feberis Pro includes GPS support
- **AwokMini**: 128x128 display with joystick navigation
- **Awok ESP32 v5**
- **LilyGo T-Watch S3**
- **LilyGo TEmbed C1101**
- **LilyGo T-Display S3 Touch**
- **LilyGo T-Deck**


### Generic Development Boards

- **ESP32**
- **ESP32-S2** (WiFi only, no Bluetooth)
- **ESP32-C3**
- **ESP32-S3**
- **ESP32-C5**
- **ESP32-C6**

## Important Considerations

- **Performance** varies across ESP32 models and may impact certain features.
- **Hardware-specific limitations**: Certain features, like SD card support and touchscreen responsiveness, depend on board compatibility.
- **Firmware updates**: Beta development may include experimental features.

## Version Status

- **Current version**: v1.8 (Revival)
- **Framework**: ESP-IDF

### Recent Feature Additions

- **Complete NFC support** with PN532 including NTAG and MIFARE Classic
- **Enhanced dual ESP32 communication** with WebUI control
- **Advanced IR support** with FlipperZero .ir file compatibility and multiple protocols
- **802.15.4 packet capture** (ESP32-C5/C6)
- **Grid-based main menu layout** for better navigation
- **DHCP Starvation attack**
- **AirTag spoofing** and selection
- **Direct station deauthentication**
- **BLE Wardriving** with GPS logging
- **Terminal application** for keyboard-based command input
- **Fuel gauge support** (BQ27220)
- **Power saving optimizations** for extended battery life
- **Enhanced UI** with RGB565A8 icons and improved layouts

### Features Under Development

- **Additional board support** and hardware compatibility improvements
- **Enhanced SD card compatibility** for more board models
- **BLE feature improvements** for device discovery and interaction
- **Advanced touchscreen calibration** and gesture recognition
- **Extended wireless protocol support** and packet analysis

## Acknowledgments

GhostESP: Revival builds upon the work of numerous open-source projects and developers:

- **Spooky (Spooks4576)**: Original GhostESP developer
- **JustCallMeKoKo**: ESP32Marauder foundational development
- **Tototo31**: Large contributions including bug fixes, feature additions, and board support
- **thibauts**: CastV2 protocol insights
- **MarcoLucidi01**: DIAL protocol integration
- **SpacehuhnTech**: Reference deauthentication code
- **WillyJL**: Flipper BLE spam code, Flipper NDEF parser
- **FlipperZero Team**: IR protocol support and reference implementations

## Project Goals

GhostESP aims to provide:

- Comprehensive wireless testing capabilities
- A user-friendly interface
- Stable and reliable performance
- Educational value for security researchers
- Regular feature updates and improvements
