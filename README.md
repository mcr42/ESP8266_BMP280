# ESP8266_BMP280
## Pressure sensor with 2 BMP280 using an ESP8266

This project tries to connect 2 BMP280 to an ESP8266.

Datasheet for the BMP280 is here: https://www.bosch-sensortec.com/products/environmental-sensors/pressure-sensors/bmp280/#documents

My ESP8266 version reads ESP8266MOD from AI-Thinker, mounted to one of those white boards that are prepared for a Holtek HT7333 3,3V LDO.
However, I may use an external 3,3V regulator, as the board has no 3,3V output needed for the BMP280s, and I have those boards laying around anyway.

## BMP280

Rated 300..1100hPa (9000m above ... 500m below sea level)
Voltage: 1,8V typ, max 3.6V (so 3.3V should be fine)
