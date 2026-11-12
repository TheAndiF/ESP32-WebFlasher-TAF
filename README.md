# ESP32 WebFlasher-TAF

Universal browser-based firmware installation interface. The chip is detected by **ESP Web Tools 10** after a serial connection is established. The project provides only firmware variants actually listed in the selected project's manifest.

## Current compatibility

| Firmware project | ESP32 | ESP32-C3 | ESP32-S3 |
|---|---|---|---|
| ESP32 UART Manager v0.40.016 | Yes (`nodemcu-32s` image) | Not yet available | Not yet available |

Do **not** flash the existing ESP32 image onto ESP32-C3 or ESP32-S3. This repository does not compile firmware. Hardware-specific images must be built and tested in their respective source repositories.

## Adding another firmware project

1. Build and verify each supported chip-specific image, including correct flash offsets and partitions.
2. Publish the images under `firmware/<project>/<chip>/` or as accessible URLs. For paths relative to the manifest, confirm they resolve on GitHub Pages.
3. Create a manifest with a separate ESP Web Tools `builds` entry per supported `chipFamily` (`ESP32`, `ESP32-C3`, `ESP32-S3`). Include **only** builds with existing, verified files.
4. Add an object to `projects.json` with `id`, `name`, `description_de`, `description_en`, `manifest` and `guide` (`uart` for the current screenshots, otherwise `none`).
5. Test the browser in Chrome or Edge on desktop, including an unsupported-chip case. Selecting a firmware opens a manifest specific to that project; ESP Web Tools checks chip compatibility after connection.

`manifest.json` and `firmware/uart_esp32_full.bin` are intentionally retained for backwards compatibility. To preserve existing URLs, keep the root `manifest.json` as the UART Manager manifest until the firmware publishing workflow is migrated. Firmware version is read dynamically from the project manifest; no version number is hardcoded in the interface.

**Warning:** Flashing a full image may erase settings and partition data. Make a backup before installation.

## Local test

Serve the repository root using an HTTP server (opening `index.html` directly with `file://` does not work for `fetch`):

```powershell
python -m http.server 8000
```

Open `http://localhost:8000/`. Actual flashing requires a compatible secure context, supported browser, serial permissions and real hardware. Production hosting uses HTTPS via GitHub Pages.
