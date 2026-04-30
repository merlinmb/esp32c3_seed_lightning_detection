# ESP32-C3 Seed Lightning Detection

Firmware for a handheld lightning detector built around the Seeed Studio XIAO ESP32-C3, the Seeed round display, and a Grove AS3935 lightning sensor.

This project presents lightning activity on a compact circular UI with a distance readout, energy gauge, radar sweep, and recent strike history. It is intended for a dedicated handheld device rather than a general-purpose weather station.

## Homage

This repository is a firmware-focused homage to the original Flash Bee design by [gokux on Instructables](https://www.instructables.com/member/gokux/):

- [Flash Bee : Handheld Lightning Sensing and Ranging Device](https://www.instructables.com/Flash-Bee-Handheld-Lighting-Sensing-and-Ranging-De/)

The original project established the industrial design, handheld enclosure concept, and overall user experience for a portable lightning warning tool. This repository keeps that spirit while maintaining the firmware in a PlatformIO project.

## Current Firmware

The firmware currently provides:

- AS3935 initialization, calibration, and interrupt-driven strike detection
- Automatic sensitivity tuning for noise, watchdog, and spike rejection
- Circular display UI for distance, energy, strike count, and rolling energy history
- Touch gestures on the round display:
  - Hold for at least 2 seconds, then release: clear strike history
  - Hold for more than 5 seconds: reboot the device

## Hardware

This codebase is configured for:

- Seeed Studio XIAO ESP32-C3
- Seeed Studio Round Display for XIAO
- Grove AS3935 lightning sensor

Relevant project details:

- I2C bus uses `Wire.begin(6, 7)`
- AS3935 interrupt uses `D2` when available, otherwise GPIO `2`
- Round display touch controller uses CHSC6X on I2C address `0x2E`
- Round display touch interrupt uses `D7`

## Project Layout

- `src/main.cpp` contains the complete firmware logic and UI rendering
- `include/driver.h` selects the Seeed round display board profile
- `platformio.ini` defines the PlatformIO environment and library dependencies

## Build

From the project root:

```powershell
C:\Users\merli\.platformio\penv\Scripts\platformio.exe run
```

Or with a standard PlatformIO installation on `PATH`:

```powershell
platformio run
```

## Upload

```powershell
platformio run --target upload
```

To open a serial monitor:

```powershell
platformio device monitor
```

Default monitor speed is `115200`.

## Notes

- The UI is optimized for the 240x240 round display.
- The firmware depends on the libraries declared in `platformio.ini`, including Seeed's round display support and Seeed_GFX.
- If you are reproducing the complete handheld device, use the original Flash Bee article for enclosure, wiring, and assembly references.
