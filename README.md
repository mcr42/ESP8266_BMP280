# ESP8266_BMP280
## Pressure sensor with 2 BMP280 using an ESP8266

This project tries to connect 2 BMP280 to an ESP8266.

Datasheet for the BMP280 is here: https://www.bosch-sensortec.com/products/environmental-sensors/pressure-sensors/bmp280/#documents

My ESP8266 version reads ESP8266MOD from AI-Thinker, mounted to one of those white boards that are prepared for a Holtek HT7333 3,3V LDO.
However, I may use an external 3,3V regulator, as the board has no 3,3V output needed for the BMP280s, and I have those boards laying around anyway.

## BMP280

Rated 300..1100hPa (9000m above ... 500m below sea level)

Voltage: 1,8V typ, max 3.6V (so 3.3V should be fine)

The BMP280 has a combined I2C/SPI interface. By default it's I2C, until the CS is pulled low once, from then it's SPI until the next reset.
I'm going to use it in I2C mode.
The chip contains factory programmed calibration data, which is read only and never changes. These values are safe to be read on startup, and be used for calculation thereafter.
Bosch recommends to use their calculation code on https://github.com/BoschSensortec/BMP2-Sensor-API

## ESP8266MOD

According to [this guidehttps://blog.squix.org/2015/03/esp8266-module-comparison-esp-01-esp-05.html] my ESP8266 ist an ESP12 (or ESP12E), with Quickstart-Guides [here|https://www.instructables.com/Getting-Started-with-the-ESP8266-ESP-12/] (on my board GPIO5/4 are switched) and [here|https://bennthomsen.wordpress.com/iot/iot-things/esp8266-wifi-soc/esp8266-getting-started-with-arduino-ide/]

I'm not certain which I2C tutorial I will use, starting points may be
- https://diyi0t.com/i2c-tutorial-for-arduino-and-esp8266/ or
- http://wp.andreas.bieri.name/myblog/2016/07/08/meine-arduino-i2c-tests-blinkm-und-rtc-module/ 
