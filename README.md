To use, make a file called secrets.yaml with sensitive info, based off secretsTemplate.yaml
MAKE SURE to have git IGNORE secrets.yaml, DO NOT commit it.


From esphome.io:

ESP32 pins

ADC2 pins are only usable when Wi-Fi is not configured on the device.

|Variant | ADC1 | ADC2|
|-|-|-|
|ESP32 | GPIO32 - GPIO39 | GPIO0, GPIO2, GPIO4, GPIO12 - GPIO15, GPIO25 - GPIO27 |
|ESP32-C3 | GPIO0 - GPIO4| GPIO5 |
|ESP32-S2 | GPIO1 - GPIO10 | GPIO11 - GPIO20 |
|ESP32-S3 | GPIO1 - GPIO10 | GPIO11 - GPIO20 |

ESP32-PoE should be ok to use non-PoE ethernet and USB, just not PoE power and USB power at the same time.

|ESP32-PoE board Rev K EXT1 pinout|Function|
|-|-|
|+5V|Tied to 5V coming in on USB or created from PoE power. Draw no more than 4W from 5V and 3.3V combined (.8A on 5V)
|+3.3V|3.3V stepped down from 5V coming in on USB or created from PoE power. Draw no more than 4W from 5V and 3.3V combined (.5A on 3.3V [[sic]](https://www.olimex.com/Products/IoT/ESP32/ESP32-POE/resources/ESP32-POE-GPIO.png))
|GND|GND of MCU and USB. BE CAREFUL versus PoE minus. Do NOT power from both USB and PoE at the same time.
|ESP_EN|MCU reset, high to run
|GPIO0|Has pullup to 3.3V
|GPIO1|U0TXD|Has pullup
|TODO|Continue
