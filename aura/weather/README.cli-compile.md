# Aura – CLI Compile Guide (arduino-cli)

Compile [/Aura](https://github.com/oernii/Aura) without Arduino IDE.

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
git clone git@github.com:oernii/Aura.git
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
cp lvgl/src/lv_conf.h ~/Arduino/libraries/
cp lvgl/src/lv_conf.h ~/Arduino/
```

---

## 6. Compile

> Sketch is located at `aura/weather/` inside the repo.

```bash
arduino-cli compile --fqbn esp32:esp32:esp32:PartitionScheme=huge_app \
  --libraries ~/Arduino/libraries aura/weather
```

---

## 7. Upload

> Replace `/dev/ttyUSB0` with your actual port.

```bash
arduino-cli upload --fqbn esp32:esp32:esp32:PartitionScheme=huge_app \
  --port /dev/ttyUSB0 aura/weather
```

---

## Auto-Reboot Every X Hours - seems to freeze sometimes
**1. Add the interval define near the top of the file** (with other `#define` config values):

```cpp
#define REBOOT_INTERVAL_HOURS 6
```
