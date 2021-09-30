# ESP8266_BMP280
## Pressure sensor with 2 BMP280 using an ESP8266

This project tries to connect 2 BMP280 to an ESP8266.

Google says: The pressure in water increases by 1bar for every 10m depth.

Ambient pressure is 1 bar typically and changes with weather.

So for 10m of water we need to measure a pressure of up to 2 bar, and correct for ambient pressure variations.
(1 bar = 100kPa = 1000hPa).
The 1100hPa (=110kPa) is therefore sufficient to only measure 1m Water, for 10m we would need 2bar = 200kPa = 2000hPa. We will see how much depth the sensor is able to measure. 

## BMP280

Datasheet for the BMP280 is here: https://www.bosch-sensortec.com/products/environmental-sensors/pressure-sensors/bmp280/#documents

Rated 300..1100hPa (9000m above ... 500m below sea level) (or 1m of water @ sea level)

Voltage: 1,8V typ, max 3.6V (so 3.3V should be fine)

The BMP280 has a combined I2C/SPI interface. By default it's I2C, until the CS is pulled low once, from then it's SPI until the next reset.
I'm going to use it in I2C mode.
The chip contains factory programmed calibration data, which is read only and never changes. These values are safe to be read on startup, and be used for calculation thereafter.
Bosch recommends to use their calculation code on https://github.com/BoschSensortec/BMP2-Sensor-API

## ESP12E

My ESP8266 version is an ESP12E, mounted to one of those white boards that are prepared for a Holtek HT7333 3,3V LDO.
However, I may use an external 3,3V regulator, as the board has no 3,3V output needed for the BMP280s, and I have those boards laying around anyway.
ESP download tool says, the module has 32MBit (=4MB) Flash, but the bootloader says 8MBit (=1MB).
The pre-installed firmware is Espressif AT-Firmware 1.3.0.2.

![ESP12E.jpg](docu/ESP12E.jpg)

I found [A good german startup guide](http://stefanfrings.de/esp8266/), lots of details. (Especially how to trigger the bootloader was important.)
Quickstart-Guides [here](https://www.instructables.com/Getting-Started-with-the-ESP8266-ESP-12/) (on my board GPIO5/4 are switched) and 
[here](https://bennthomsen.wordpress.com/iot/iot-things/esp8266-wifi-soc/esp8266-getting-started-with-arduino-ide/). 
A good and detailed starter is 
Some quirks are discribed unter https://www.letscontrolit.com/wiki/index.php/Basics:_ESP8266_Types_and_Boards 

My MobaXTerm did not receive anything from the ESP32, but the Arduino IDE did.
The bootloader tells me the Flash has 40 MHz, but it also says it were 8MBit.
The ESP download tool disagrees, an says it were 32MBit. So maybe 80MHz are supported.

[Espressiv AT-Firmware Download](https://docs.espressif.com/projects/esp-at/en/release-v2.2.0.0_esp8266/AT_Binary_Lists/ESP8266_AT_binaries.html)

[Espressiv AT-Firmware Documentation](https://docs.espressif.com/projects/esp-at/en/release-v2.2.0.0_esp8266/AT_Command_Set/index.html)

## NodeMCU firmware

The AT firmware seems to be a client-based approach (it relies on commands coming in to do something). What I want is something that works on its own, so we need to switch to a different firmware. There's some cool projects laying around there, I found the NodeMCU being good documented and broadly supported. It also has a I2C software module (as there is no I2C hardware), so we can just hook up the sensor to any GPIO and are ready to go.
There's a lot of tutorial how to flash NodeMCU like [this one](https://www.best-microcontroller-projects.com/nodemcu-firmware.html) or [this one (German)](https://www.mikrocontroller.net/articles/ESP8266_nodeMCU_Lua).

[NodeMCU documentation](https://nodemcu.readthedocs.io)

[NodeMCU I2C module](https://nodemcu.readthedocs.io/en/release/modules/i2c/)

(In case it doesn't work, one might also try [MicroPython](https://micropython.org/download/esp8266/) .)
