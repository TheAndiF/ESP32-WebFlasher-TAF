# ESP32 WebFlasher-TAF

**Universal browser-based ESP32 firmware installer by TheAndiF**
*Choose firmware · Connect your ESP32 · Flash in your browser*

[![Launch WebFlasher](https://img.shields.io/badge/Launch-WebFlasher-0969da?style=for-the-badge&logo=googlechrome&logoColor=white)](https://theandif.github.io/ESP32-WebFlasher-TAF/)

**Direct link:** https://theandif.github.io/ESP32-WebFlasher-TAF/

[Deutsch](#deutsch) · [English](#english) · [Adding firmware projects](#adding-firmware-projects)

---

## Deutsch

Mit **ESP32 WebFlasher-TAF** lassen sich bereitgestellte ESP32-Firmware-Projekte direkt im Browser installieren. Eine separate Flash-Anwendung ist nicht erforderlich.

### In drei Schritten

1. **Software auswählen:** Wähle das gewünschte Firmware-Projekt in der Weboberfläche.
2. **ESP32 verbinden:** Schließe das Board per USB an. ESP Web Tools erkennt beim Verbindungsaufbau die Chipfamilie und prüft die angebotenen Firmware-Builds.
3. **Firmware flashen:** Starte die Installation und bestätige die Browserabfragen. Folge den Anweisungen bis zum Abschluss.

**[➡ WebFlasher jetzt öffnen](https://theandif.github.io/ESP32-WebFlasher-TAF/)**

### Aktuell verfügbare Firmware

| Software | ESP32 | ESP32-C3 | ESP32-S3 |
| --- | :---: | :---: | :---: |
| ESP32 UART Manager (v0.40.016) | ✅ | ⏳ Noch nicht verfügbar | ⏳ Noch nicht verfügbar |

> **Wichtig:** Automatische Chiperkennung bedeutet nicht, dass bereits für jeden Chip Firmware bereitsteht. Der WebFlasher bietet nur Builds an, die im Manifest des ausgewählten Projekts vorhanden sind. Die bestehende ESP32-Firmware darf **nicht** auf ESP32-C3 oder ESP32-S3 geflasht werden.

### Voraussetzungen und Sicherheit

- PC mit einem aktuellen **Chrome**- oder **Edge**-Browser mit Web-Serial-Unterstützung.
- USB-Datenkabel und Zugriff auf den seriellen Anschluss des Boards.
- Für den öffentlichen WebFlasher HTTPS verwenden (GitHub Pages).
- Vor dem Flashen wichtige Daten und Einstellungen sichern: Ein vollständiges Firmware-Image kann den Flash-Inhalt einschließlich Einstellungen überschreiben.
- Die Verfügbarkeit der Firmware für ein bestimmtes Board hängt nicht nur von der Chipfamilie, sondern ggf. auch von Pinbelegung und Hardwarekonfiguration ab.

## English

**ESP32 WebFlasher-TAF** provides a browser-based installation interface for supported ESP32 firmware projects. No separate desktop flashing tool is required.

### Three-step workflow

1. **Select firmware:** Choose the firmware project in the web interface.
2. **Connect your ESP32:** Attach the board over USB. ESP Web Tools detects the chip family when connecting and checks the manifest for compatible builds.
3. **Flash firmware:** Start the installation, confirm browser prompts, and follow the on-screen instructions.

**[➡ Launch WebFlasher](https://theandif.github.io/ESP32-WebFlasher-TAF/)**

### Current firmware availability

| Firmware | ESP32 | ESP32-C3 | ESP32-S3 |
| --- | :---: | :---: | :---: |
| ESP32 UART Manager (v0.40.016) | ✅ | ⏳ Not available yet | ⏳ Not available yet |

> **Note:** Chip detection does not imply that firmware is available for every chip. Only verified builds listed in the selected project's manifest can be installed. Never flash an ESP32 image onto an ESP32-C3 or ESP32-S3.

### Requirements and safety

- A recent desktop **Chrome** or **Edge** browser supporting Web Serial.
- A USB data cable and permission to access the board's serial port.
- HTTPS for production use (GitHub Pages).
- Back up important device data before flashing. Full flash images may overwrite settings and partitions.
- Firmware compatibility may also depend on board wiring, pins, or other hardware details.

## Adding firmware projects

The frontend reads project entries from `projects.json`. Each entry references a firmware manifest; ESP Web Tools selects a compatible build from that manifest once the device is connected.

1. Build and test **separate firmware images** for each supported chip and hardware configuration.
2. Publish the images in an accessible location (for example, under `firmware/<project>/<chip>/`). Verify URLs, image format, offsets and partition layout.
3. Provide an ESP Web Tools manifest containing a `builds` entry for each **actually available** `chipFamily` (`ESP32`, `ESP32-C3`, `ESP32-S3`).
4. Add a project entry to `projects.json` with `id`, `name`, `description_de`, `description_en`, `manifest` and `guide`.
5. Test the complete browser workflow on real hardware, including incompatible-chip behavior.

The existing root `manifest.json` and `firmware/uart_esp32_full.bin` are retained for backwards compatibility. The web interface reads the selected project's version from its manifest rather than using a hard-coded version label.

### Repository layout

```text
ESP32-WebFlasher-TAF/
├── index.html                 # Web interface
├── projects.json              # Firmware project directory
├── manifest.json              # UART Manager manifest (compatibility)
├── firmware/                  # Firmware images
├── anleitung/                 # Existing illustrated instructions
└── README.md
```

### Local preview

Run an HTTP server in the repository folder:

```powershell
python -m http.server 8000
```

Then open `http://localhost:8000/` to preview the interface. **Actual flashing** requires a compatible secure context, supported browser, serial permissions and real hardware; use the HTTPS GitHub Pages site for normal installation.

## Project links

- **[Open the WebFlasher](https://theandif.github.io/ESP32-WebFlasher-TAF/)**
- **[GitHub repository](https://github.com/TheAndiF/ESP32-WebFlasher-TAF)**
- **[ESP32 UART Manager](https://github.com/TheAndiF/ESP32-UART-Manager)**

---

Maintained by **TheAndiF** · ESP32 WebFlasher-TAF
