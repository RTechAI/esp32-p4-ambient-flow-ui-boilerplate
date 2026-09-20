# Ambient Flow — ESP32-P4 LVGL 9 Touchscreen UI/HMI Boilerplate

![Ambient Flow conceptual artwork](Splash%20esp32-p4-ambient-flow-ui-boilerplate.png)

An ESP32-P4 embedded UI/HMI boilerplate for the **Waveshare ESP32-P4-WIFI6-Touch-LCD-7B**: a 7-inch, 1024×600 MIPI DSI touchscreen using the EK79007 display controller and GT911 capacitive-touch controller. It is an ESP-IDF 5.5.4 project using LVGL 9.2.2.

This repository provides a ForgeUI One runtime baseline and a generated single-page Ambient Flow LVGL interface for building and evaluating ESP32-P4 touchscreen applications. **Ambient Flow is this project's visual theme: it does not implement airflow sensing, HVAC control, environmental monitoring, air-quality measurement, or building automation.**

## ForgeUI Ecosystem

ForgeUI is developed by [RTechAI](https://github.com/RTechAI).

The [ForgeUI website](https://forgeui.co.nz) is the official home of the ForgeUI embedded UI/HMI development ecosystem. ForgeUI Studio is the current visual embedded UI/HMI development environment for supported ESP32 hardware.

[ForgeUI Hosted Studio](https://studio.forgeui.co.nz) is the hosted, browser-based ForgeUI Studio application and is available for public registration.

RTechAI's GitHub organization hosts ForgeUI public repositories, hardware references, framework baselines, examples, and related open development work. This repository is a hardware-specific, theme-led ESP32-P4 boilerplate in that public reference work, retaining the earlier ForgeUI One runtime and ESP32-P4 UI Studio export lineage described below.

## Overview

The checkout contains a native C ESP-IDF firmware project that starts the Waveshare BSP display and touch stack, initializes the ForgeUI runtime, and renders a generated LVGL screen. The generated screen uses an Ambient Flow background asset and creates periodic clock and Wi-Fi-status update callbacks.

The enabled runtime configuration also includes ESP-Hosted Wi-Fi via the board's ESP32-C6, DS3231-backed retained time, and SD-card initialization. Audio support code and dependencies are present, but audio is disabled in the current project configuration.

## Hardware Target

| Item | Verified target |
| --- | --- |
| Board | Waveshare ESP32-P4-WIFI6-Touch-LCD-7B |
| SoC | Espressif ESP32-P4 |
| Display | 7-inch 1024×600 MIPI DSI, EK79007 |
| Touch | GT911 capacitive touch |
| Wireless path | ESP-Hosted over SDIO to the onboard ESP32-C6 through `esp_wifi_remote` |
| Runtime peripherals enabled | DS3231 RTC and SD card |

The configured boot order initializes hosted Wi-Fi before mounting SD storage because those paths share board resources.

## Software Stack

| Component | Locked version |
| --- | --- |
| ESP-IDF | 5.5.4 |
| LVGL | 9.2.2 |
| Waveshare board-support package | 1.0.2 |
| `esp_lvgl_port` | 2.7.2 |
| `esp_hosted` | 2.9.7 |
| `esp_wifi_remote` | 1.3.0 |

The complete resolved component set is recorded in [`dependencies.lock`](dependencies.lock).

## Ambient Flow UI and Demonstration Data

Ambient Flow refers to the pale-blue flowing-line visual treatment used by the generated UI asset. The checked-in generated screen contains no environmental, airflow, temperature, humidity, air-quality, or ventilation values.

Its time display is formatted from the runtime clock, with the configured DS3231 backend used for retained time and NVS as fallback. Its Wi-Fi text is updated from the runtime Wi-Fi status and assigned IP address. The local hero above is conceptual/generated artwork; it is neither a physical-hardware photograph nor proof of a running device.

## Hardware and Runtime Baseline

`main/` contains the ForgeUI One runtime modules and the generated Studio export. The active configuration enables:

- LVGL display/touch initialization through the Waveshare BSP
- ESP-Hosted/ESP32-C6 Wi-Fi support
- DS3231 RTC integration and NVS time fallback
- SD-card mount, read/write test, and ForgeUI storage helpers

Audio includes an available speaker-test implementation, but `FORGEUI_ENABLE_AUDIO` is set to `0`; it is not active in this baseline.

## Project Structure

```text
.
├── main/                         # Application, ForgeUI runtime, and generated UI export
│   ├── 90_Studio_Export.c         # Generated single-page LVGL UI
│   ├── 30_WIFI.c                  # ESP-Hosted Wi-Fi backend
│   ├── 20_RTC.c                   # DS3231/NVS time backend
│   └── 40_SD.c                    # SD-card storage backend
├── components/bsp_extra/          # Board-specific audio/BSP extension
├── docs/                          # Setup references and UI assets
├── dependencies.lock              # Resolved ESP-IDF component versions
├── sdkconfig.defaults             # ESP32-P4 project defaults
└── CMakeLists.txt                 # ESP-IDF project definition
```

## Build and Flash

Install and activate an ESP-IDF 5.5.4 environment, then from the repository root:

```bash
idf.py set-target esp32p4
idf.py build
idf.py flash monitor
```

Use the Waveshare ESP32-P4-WIFI6-Touch-LCD-7B target described above. No build or flash was performed as part of this documentation update.

## Historical ForgeUI Context

Source comments and the generated export identify this project as an earlier **ESP32-P4 UI Studio** export running on the **ForgeUI One** runtime. These are historical lineage references, not claims that the current Hosted Studio generated this checkout.

- [Historical ESP32-P4 UI Studio](https://github.com/RTechAI/esp32p4-ui-studio)
- [ForgeUI One](https://github.com/RTechAI/ForgeUI-One)

## Current ForgeUI Studio

The [ForgeUI website](https://forgeui.co.nz) is the official home of the ForgeUI embedded UI/HMI development ecosystem. ForgeUI Studio is the current visual embedded UI/HMI development environment for supported ESP32 hardware.

[ForgeUI Hosted Studio](https://studio.forgeui.co.nz) is the hosted, browser-based ForgeUI Studio application and is available for public registration.

## Related ForgeUI Projects

- [ForgeUI One](https://github.com/RTechAI/ForgeUI-One) — historical runtime lineage
- [Historical ESP32-P4 UI Studio](https://github.com/RTechAI/esp32p4-ui-studio) — historical export-tool lineage
- [ForgeUI P4](https://github.com/RTechAI/ForgeUI-P4) — ESP32-P4-focused ForgeUI work
- [ESP32-P4 LVGL Boilerplate 3](https://github.com/RTechAI/ESP32-P4-LVGL-Boilerplate-3) — related ESP32-P4/LVGL boilerplate

## About ForgeUI

[ForgeUI](https://forgeui.co.nz) is developed by [RTechAI](https://github.com/RTechAI).

ForgeUI Studio provides visual embedded UI/HMI development workflows for supported ESP32 hardware, while [ForgeUI Hosted Studio](https://studio.forgeui.co.nz) provides the hosted, browser-based Studio application.

RTechAI is the GitHub home for ForgeUI public repositories and reference work.

## License and Third-Party Software

ForgeUI-owned code in this repository is covered by the root [ForgeUI Source Available License](LICENSE). Third-party components retain their own licenses and notices; see [THIRD_PARTY_LICENSES.md](THIRD_PARTY_LICENSES.md) and the applicable component distributions. In particular, `components/bsp_extra/LICENSE` is Apache-2.0.

## Support

For ForgeUI public repositories and reference work, visit [RTechAI on GitHub](https://github.com/RTechAI). For the current Studio ecosystem, visit [forgeui.co.nz](https://forgeui.co.nz) or [ForgeUI Hosted Studio](https://studio.forgeui.co.nz).
