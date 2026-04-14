# Aura – CLI Compile Guide (arduino-cli)

Compile [Surrey-Homeware/Aura](https://github.com/Surrey-Homeware/Aura) without Arduino IDE.

---

## 1. Install arduino-cli

```bash
curl -fsSL https://raw.githubusercontent.com/arduino/arduino-cli/master/install.sh | sh
sudo mv bin/arduino-cli /usr/local/bin/
arduino-cli version
```

---

## 2. Initialize Config & Add ESP32 Board Support

```bash
arduino-cli config init
arduino-cli config add board_manager.additional_urls https://raw.githubusercontent.com/espressif/arduino-esp32/gh-pages/package_esp32_index.json
arduino-cli core update-index
arduino-cli core install esp32:esp32
```

---

## 3. Clone the Repo

```bash
git clone https://github.com/Surrey-Homeware/Aura.git
cd Aura
```

---

## 4. Install Required Libraries

```bash
arduino-cli lib install "ArduinoJson@7.4.1"
arduino-cli lib install "HttpClient@2.2.0"
arduino-cli lib install "WiFiManager@2.0.17"
arduino-cli lib install "XPT2046_Touchscreen@1.4"
arduino-cli lib install "lvgl@9.2.2"

# TFT_eSPI is bundled in the repo — copy it to Arduino libraries folder:
cp -r TFT_eSPI ~/Arduino/libraries/TFT_eSPI
```

---

## 5. Copy LVGL Config Files

```bash
cp lvgl/src/lv_conf.h ~/Arduino/libraries/lvgl/
```

---

## 6. Copy Sketch Folder to Arduino Directory

```bash
cp -r aura ~/Arduino/aura
```

---

## 7. Compile

```bash
arduino-cli compile \
  --fqbn esp32:esp32:esp32:PartitionScheme=huge_app \
  --libraries ~/Arduino/libraries \
  ~/Arduino/aura
```

---

## 8. Upload

> Replace `/dev/ttyUSB0` with your actual port.

```bash
arduino-cli upload \
  --fqbn esp32:esp32:esp32:PartitionScheme=huge_app \
  --port /dev/ttyUSB0 \
  ~/Arduino/aura
```

---

## Notes

- `PartitionScheme=huge_app` maps to **Huge App (3MB No OTA/1MB SPIFFS)** as required by the project.
- **TFT_eSPI** is included in the repo with its config pre-set — use that copy, not the library manager version.
- Find your upload port with: `arduino-cli board list`
- On some systems use `/dev/ttyACM0` instead of `/dev/ttyUSB0`.
- If you get permission errors on the port, add yourself to the `dialout` group:
  ```bash
  sudo usermod -aG dialout $USER
  ```
