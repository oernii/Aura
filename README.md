# Aura

* Forked from github.com/pocketscience/Aura/ (and that is from https://github.com/Surrey-Homeware/Aura) - see details there
* Use Arduino IDE 2
* Configure Arduino IDE 
  * for "esp32" board with a device type of "ESP32 Dev Module" and
  * set "Tools -> Partition Scheme" to "Huge App (3MB No OTA/1MB SPIFFS)"
* install arduino libs 
    - ArduinoJson 7.4.1
    - HttpClient 2.2.0
    - TFT_eSPI 2.5.43_
    - WifiManager 2.0.17
    - XPT2046_Touchscreen 1.4
    - lvgl 9.2.2
* copy 2 files to Arduino folder (overwrite):
 * cp TFT_eSPI/User_Setup.h ~/Arduino/libraries/TFT_eSPI/User_Setup.h
 * cp lvgl/src/lv_conf.h ~/Arduino/libraries/lvgl/src/

