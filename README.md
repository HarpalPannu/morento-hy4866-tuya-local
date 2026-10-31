# MORENTO HY4866-WF Air Purifier for Tuya Local

Device profile for the **MORENTO HY4866-WF Smart Air Purifier** (`wqymg6ujqvmixp2i`) using the [Tuya Local](https://github.com/make-all/tuya-local) integration in Home Assistant.

## What This Fixes
- **Speed controls:** Maps firmware codes (`1F`, `2F`, `3F`, `4F`) to 25%, 50%, 75%, and 100% fan speed.
- **Timer options:** Correctly exposes `cancel`, `2h`, `5h`, and `8h`.
- **Clean entities:** Removes unsupported air quality enum and countdown timer sensors that show `unknown`.

## Installation
1. Copy `morento_hy4866_airpurifier.yaml` to:
   ```text
   /config/custom_components/tuya_local/devices/morento_hy4866_airpurifier.yaml
   ```
2. In Home Assistant, go to **Developer Tools** > **YAML** and click **Tuya Local** under *Integration Reload* (or restart Home Assistant).
3. Go to **Settings** > **Devices & Services** > **Tuya Local**, click **Configure** on your Air Purifier, and select the `MORENTO Air Purifier (HY4866-WF)` profile.

## Supported Entities
- **Fan:** Power & 4 Speeds (25%, 50%, 75%, 100%) + Presets (`manual`, `auto`, `sleep`)
- **PM2.5 Sensor:** Real-time air quality in µg/m³
- **Filter Life Sensor:** Remaining percentage (0–100%)
- **Timer Select:** `cancel`, `2h`, `5h`, `8h`
- **Child Lock:** Toggle switch
- **Filter Reset:** Push button
