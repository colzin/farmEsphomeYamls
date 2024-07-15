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

|ESP32-PoE board Rev K EXT1 pin label|Function|
|-|-|
|+5V|Tied to 5V coming in on USB or created from PoE power. Draw no more than 4W from 5V and 3.3V combined (.8A on 5V)
|+3.3V|3.3V stepped down from 5V coming in on USB or created from PoE power. Draw no more than 4W from 5V and 3.3V combined (.5A on 3.3V [[sic]](https://www.olimex.com/Products/IoT/ESP32/ESP32-POE/resources/ESP32-POE-GPIO.png))
|GND|GND of MCU and USB. BE CAREFUL versus PoE minus. Do NOT power from both USB and PoE at the same time.
|ESP_EN|MCU reset, high to run
|GPIO0| HW pullup to 3.3V, must be high for proper MCU boot.
|GPIO1/U0TXD|UART0 TxD, debug messages come out here
|GPIO2| HW pullup to 3.3V, don't care on state if GPIO0 is high on boot.
|GPIO3/U0RXD|UART0 RxD, used for programming
|GPIO4|MCU has internal pulldown, also goes to UEXT pin 3. No HW pulls.
|GPIO5| HW 10k pullup, also goes to UEXT pin 10.


|ESP32-PoE board Rev K EXT2 pin label|Function|
|-|-|
|GPI39|+5V sense with divider, use atten 11dB and multiplier 1.67 to measure 5V rail.
|GPI36| HW 10k pullup to 3.3V
|GPI35|Could measure battery if solder-shorted, else NO connections. Open ADC pin!
|GPI34| HW 10k pullup to 3.3V, BUT1 shorts to GND
|GPIO33|Seems to be shorted to GPIO16
|GPIO16| HW 2.2k pullup to 3.3V for I2C-SCL, also on UEXT pin 5
|GPIO15| HW 10k pullup to 3.3V, also UEXT pin 7
|GPIO14| UEXT pin 9, NO pulls, good ADC pin
|GPIO13| HW 2.2k pull to 3.3V for I2C-SDA, also UEXT pin 6
