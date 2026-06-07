# Known issues in Ghost ESP


```anything you read here may or may not be entirely accurate or up to date.``` 


1. **Display Color Inversion**: A number of CYDs invert colors by default
2. **SD Card Support**: **Marauder V6**, **Generic ESP32** builds, **Awok variants**, **Feberis**, and **Feberis Pro** have no SD card support.
3. **Feberis / Feberis Pro first install**: If installing GhostESP over stock BPM Circuits Marauder firmware, do not flash only `firmware.bin` as FirmwareA. Flash `bootloader.bin`, `partitions.bin`, and `firmware.bin` together because the stock Marauder OTA app slot is smaller than the GhostESP app image.
4. **GPS Pin Limitations**: Some pins cannot be assigned as GPS input. Notably the Rabbit Labs Yapper board exhibits this behavior.
5. **ESP32-S2 Bluetooth**: ESP32-S2 boards do not support Bluetooth functionality due to lack of hardware.
6. **mDNS Compatibility**: `ghostesp.local` access requires mDNS support on your device/network. Use `192.168.4.1` as alternative.
7. **Battery Monitoring**: Battery status is not available on all devices. Ensure your board supports battery monitoring before relying on it.
8. **Web Flasher Cache**: Browser cache clearing may be required when using the web flasher for proper functionality.
9. **HTML Buffer Size**: Flipper Zero App HTML upload is limited to 2048 bytes maximum.
10. **Infrared Support**: IR functionality is limited to LilyGo S3TWatch, ESP32-S3-Cardputer, and LilyGo TEmbed C1101 devices only.
