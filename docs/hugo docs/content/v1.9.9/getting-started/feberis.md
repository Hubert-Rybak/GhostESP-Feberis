---
title: "BPM Circuits Feberis"
description: "Flash GhostESP on BPM Circuits Feberis and Feberis Pro boards"
weight: 16
toc: true
---

This page covers the BPM Circuits **Feberis** and **Feberis Pro** Flipper Zero add-on boards.

Use the board-specific artifacts from the `feberis` branch build:

- **Feberis:** `Feberis.zip`
- **Feberis Pro:** `FeberisPro.zip`
- **Full merged images for PC flashing:** `Feberis-merged-gesp.bin` and `FeberisPro-merged-gesp.bin`

> **Important:** when installing GhostESP over the stock BPM Circuits Marauder firmware for the first time, do **not** flash only `firmware.bin` into the FirmwareA slot. Stock Marauder Feberis builds use a smaller OTA app slot than this GhostESP build. Flash the bootloader, partition table, and firmware together, or use the merged image at offset `0x0`.

## Board feature notes

- Both builds target the classic **ESP32** with 4 MB flash.
- Both builds use **DIO** flash mode and **80 MHz** flash frequency.
- Both builds enable the onboard NeoPixel/RGB LED on **GPIO25**.
- Both builds enable GhostESP NFC/Chameleon-related features.
- **Feberis Pro** enables GPS on UART RX **GPIO4** at **9600 baud**.
- **Feberis** has GPS disabled.
- These builds do not enable an onboard display, keyboard, SD card, battery monitor, or infrared transmitter.

## Download the artifacts

1. Open the latest successful [Build Feberis firmware workflow run](https://github.com/Hubert-Rybak/GhostESP-Feberis/actions/workflows/build_feberis.yml?query=branch%3Afeberis).
2. Download the ZIP artifact for your exact board:
   - `Feberis-zip` contains `Feberis.zip`.
   - `FeberisPro-zip` contains `FeberisPro.zip`.
3. Extract the ZIP. You need these files for Flipper/manual flashing:
   - `bootloader.bin`
   - `partitions.bin`
   - `firmware.bin`

The separate merged BIN artifacts are only for full-image flashing from a PC. Do not put `Feberis-merged-gesp.bin` or `FeberisPro-merged-gesp.bin` into a Flipper FirmwareA slot.

## Flash with Flipper Zero ESP Flasher

1. Copy the three extracted files to the Flipper SD card:

   ```text
   SDCard/apps_data/esp_flasher/
   ```

2. Connect Feberis / Feberis Pro to the Flipper Zero GPIO header.
3. Put the board in the correct hardware mode:
   - **Feberis:** ESP32 mode.
   - **Feberis Pro:** ESP32 + GPS mode.
4. Open the Flipper ESP Flasher manual/options screen:

   ```text
   Apps -> GPIO -> ESP Flasher -> Flash ESP
   ```

5. Select the files and offsets exactly:

   | Slot | Offset | File |
   |------|--------|------|
   | Bootloader | `0x1000` | `bootloader.bin` |
   | Part Table | `0x8000` | `partitions.bin` |
   | FirmwareA | `0x10000` | `firmware.bin` |

6. Leave these slots unselected unless you specifically know you need them:
   - `FirmwareB`
   - `boot_app0`
   - `NVS`
   - `Custom`

7. Immediately before starting the flash, enter Feberis bootloader mode:
   1. Press and hold the **right** button.
   2. While still holding the right button, press and hold the **left** button.
   3. Release the **right** button.
   4. Release the **left** button.

8. Choose **FLASH - fast** and wait for completion.
9. Reboot the board and verify that GhostESP starts normally. If you use Feberis Pro GPS, run `gpsinfo` after the GPS has a clear view of the sky.

## Flash from a PC with esptool

Use this method if you have direct USB/serial access or need to recover from a bad app-only flash.

### Merged image method

Flash the merged image at offset `0x0`:

```bash
esptool.py --chip esp32 --port /dev/ttyUSBx --baud 460800 \
  write_flash --flash_mode dio --flash_freq 80m --flash_size 4MB \
  0x0 Feberis-merged-gesp.bin
```

For Feberis Pro, replace the filename with `FeberisPro-merged-gesp.bin`.

### Three-file method

Use the files extracted from `Feberis.zip` or `FeberisPro.zip`:

```bash
esptool.py --chip esp32 --port /dev/ttyUSBx --baud 460800 \
  write_flash --flash_mode dio --flash_freq 80m --flash_size 4MB \
  0x1000 bootloader.bin \
  0x8000 partitions.bin \
  0x10000 firmware.bin
```

## Updating after GhostESP is already installed

The safest repeat update is still the full three-file flash or merged-image flash, because it guarantees the bootloader and partition table match the app image.

An app-only `firmware.bin` update at `0x10000` is only appropriate if the GhostESP partition table is already installed and the new app image fits that partition. Do not use app-only flashing when moving from stock Marauder to GhostESP.

## Troubleshooting

**Board does not enter flashing mode**

- Re-run the right-button/left-button bootloader sequence immediately before pressing flash.
- Confirm the board is in ESP32 mode; Feberis Pro should be in ESP32 + GPS mode.
- Try a lower baud rate if fast flashing fails.

**Boot loop after flashing**

- Reflash using the full three-file method or the merged BIN at `0x0`.
- Make sure you did not flash only `firmware.bin` over the stock Marauder partition table.
- Make sure the artifact matches your board: `Feberis.zip` for Feberis, `FeberisPro.zip` for Feberis Pro.

**`SD Card init failed` / `sd_config` NVS errors on boot**

- Feberis and Feberis Pro do not expose an ESP32-connected SD card to GhostESP. The Flipper Zero SD card is separate.
- Affected builds may print default SD/MMC/SPI pin configuration and then `SD Card init failed with loaded pins`; this is not a flashing failure.
- Use a current Feberis artifact. Current builds skip SD initialization for these boards instead of probing non-existent SD pins.

**GPS does not show data on Feberis Pro**

- Confirm you flashed `FeberisPro.zip`, not `Feberis.zip`.
- Set the board to ESP32 + GPS mode.
- Move the GPS antenna to open sky and allow time for first fix.
- Check `gpsinfo`; this build listens on ESP32 UART RX GPIO4 at 9600 baud.

## References

- [Build Feberis firmware workflow](https://github.com/Hubert-Rybak/GhostESP-Feberis/actions/workflows/build_feberis.yml?query=branch%3Afeberis)
- [Sapsan: How to update your FEBERIS / NetNinja](https://sapsan-sklep.pl/blogs/artykuly/how-to-update-your-feberis-netninja)
