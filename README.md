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

|ESP32-PoE board Rev K EXT1 pin label|Description/Notes|ADC viability|Low-drive viability|
|-|-|-|-|
|+5V|Tied to 5V coming in on USB or created from PoE power. Draw no more than 4W from 5V and 3.3V combined (.8A on 5V)|na|na
|+3.3V|3.3V stepped down from 5V coming in on USB or created from PoE power. Draw no more than 4W from 5V and 3.3V combined (.5A on 3.3V [[sic]](https://www.olimex.com/Products/IoT/ESP32/ESP32-POE/resources/ESP32-POE-GPIO.png))|na|na
|GND|GND of MCU and USB. BE CAREFUL versus PoE minus. Do NOT power from both USB and PoE at the same time.|na|na
|ESP_EN|MCU reset, high to run|no|no
|GPIO0| HW pullup to 3.3V, must be high for proper MCU boot.|No, due to pullup|Yes, HW 10k pullup
|GPIO1/U0TXD|UART0 TxD, debug messages come out here|Maybe if debug output is stopped|No HW pulls, maybe not
|GPIO2| HW pullup to 3.3V, don't care on state if GPIO0 is high on boot **also UEXT pin 8**|Maybe, depends on BAT54 and RM3D | maybe
|GPIO3/U0RXD|UART0 RxD, used for programming|no|no
|GPIO4|MCU has internal pulldown, **also UEXT pin 3**. No HW pulls|Maybe, if un-muxed the MCU pulldown|No, has pulldown
|GPIO5| HW 10k pullup, **also UEXT pin 10**.|no|yes, 10k pullup


|ESP32-PoE board Rev K EXT2 pin label|Function|ADC viability|Low-drive viability|
|-|-|-|-|
|GPI39|+5V sense with divider, use atten 11dB and multiplier 1.67 to measure 5V rail.|no, already in use|no, pulls to middle
|GPI36| HW 10k pullup to 3.3V|no|yes
|GPI35|Could measure battery if solder-shorted, else no connections.|**yes**|no, no HW pulls
|GPI34| HW 10k pullup to 3.3V, BUT1 shorts to GND|no|yes, also BUT1 to GND
|GPIO33|Seems to be shorted to GPIO16|no|yes, but mirrors GPIO16
|GPIO32| no HW pulls, only to this pin|**yes**|no, no HW pulls
|GPIO16| HW 2.2k pullup to 3.3V for I2C-SCL, **also UEXT pin 5**|no|yes
|GPIO15| HW 10k pullup to 3.3V, **also UEXT pin 7**|no|yes
|GPIO14| **UEXT pin 9**, NO pulls, good ADC pin|yes|no, no HW pulls
|GPIO13| HW 2.2k pull to 3.3V for I2C-SDA, **also UEXT pin 6**|no|yes

|ESP32-PoE board Rev K UEXT pins not used by EXT1 or EXT2|Function|ADC viability|Low-drive viability|
|-|-|-|-|
|pin1|3.3V|no|no
|pin2|GND|no|no
|pin3|GPIO4, see EXT1||
|pin4|could drive GPI36 low (diode)|no|no
|pin5|GPIO16, see EXT2||
|pin6|GPIO13, see EXT2||
|pin7|GPIO15, see EXT2||
|pin8|GPIO2, see EXT1||
|pin9|GPIO14, see EXT2||
|PIN10|GPIO5, see EXT1||
