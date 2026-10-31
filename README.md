# MORENTO HY4866-WF Air Purifier - Tuya Local Device Definition

Custom device configuration for the **MORENTO HY4866-WF Smart Air Purifier** (Product ID: `wqymg6ujqvmixp2i`) for the [Home Assistant Tuya Local](https://github.com/make-all/tuya-local) integration.

---

## Background & Problem Solved

When added to Home Assistant via Tuya Local, this air purifier auto-detects as `ap402_airpurifier`. However, the standard `ap402` profile causes several issues:
1. **Broken Speed Control:** `ap402` maps fan speeds to string names (`Low`, `Medium`, `High`, `Turbo`). The MORENTO HY4866-WF firmware uses `1F`, `2F`, `3F`, and `4F` on DPS 4. This results in percentage controls showing raw strings and fan speed commands failing.
2. **Incorrect Timer Steps:** The stock profile exposes `[cancel, 2h, 4h, 6h, 8h]`, but this purifier only supports `cancel`, `2h`, `5h`, and `8h`.
3. **Dead Sensors:** Removes unused DPS 19 (Time Remaining) and DPS 21 (Air Quality enum) which perpetually report `unknown` on this hardware.

This profile fixes all speed steps, timer options, and entity mappings.

---

## Device Specifications

- **Brand:** MORENTO
- **Model:** HY4866-WF
- **Product ID:** `wqymg6ujqvmixp2i`
- **Protocol:** Tuya Local 3.5

---

## Supported Entities & DPS Mapping

| DPS ID | Type | Home Assistant Entity | Values / Description |
|---|---|---|---|
| **1** | Boolean | `fan` (Power) | `true` (On) / `false` (Off) |
| **3** | String | `preset_mode` | `auto`, `sleep`, `manual` |
| **4** | String | `fan` (Speed Percentage) | `1F` (25%), `2F` (50%), `3F` (75%), `4F` (100%) |
| **2** | Integer | `sensor.pm2_5` | Real-time PM2.5 in µg/m³ |
| **5** | Integer | `sensor.filter_life` | Filter life remaining (0–100%) |
| **18** | String | `select.timer` | `cancel`, `2h`, `5h`, `8h` |
| **7** | Boolean | `lock.child_lock` | Child lock toggle |
| **11** | Boolean | `button.filter_reset` | Filter life reset button |
| **22** | Bitfield | `binary_sensor.problem` | Fault / diagnostic status |

---

## Installation

### Method 1: Drop into `custom_components/tuya_local/devices/`

1. Copy [`morento_hy4866_airpurifier.yaml`](./morento_hy4866_airpurifier.yaml) into your Home Assistant directory:
   ```text
   /config/custom_components/tuya_local/devices/morento_hy4866_airpurifier.yaml
   ```
2. In Home Assistant, navigate to **Developer Tools** > **YAML** > click **Tuya Local** under Integration Reload (or restart Home Assistant).
3. In **Settings** > **Devices & Services** > **Tuya Local**, click **Configure** on your air purifier.
4. Select `MORENTO Air Purifier (HY4866-WF)` from the device profile dropdown and click **Submit**.

---

## Contributing to Upstream Tuya Local

This file is structured for direct inclusion in the upstream [make-all/tuya-local](https://github.com/make-all/tuya-local) repository. Pull requests and device requests can submit this file directly to `custom_components/tuya_local/devices/`.
