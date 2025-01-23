# dev-ideaspark-esp32

```
Chip is ESP32-D0WD-V3 (revision v3.0)
Features: WiFi, BT, Dual Core, 240MHz, VRef calibration in efuse, Coding Scheme None
Crystal is 40MHz
```

* The ESP32 1.9'' LCD board has all the features of the traditional ESP32 Devkit V1 module,with the same exact peripheral ports,offers seamless integration with a 1.9-inch LCD display, eliminating the need for frustrating wires and breadboards.Display features a high-resolution 170x320 full color with ST7789 driver and is compatible with I2C interfaces. Plus,It uses Type-c usb cable to connect. Say goodbye to messy setups and hello to hassle-free electronics with the ESP32 board
* Board is based on ESP32-WROOM-32 module integrated with Antenna switches, RF Balun, power amplifiers, low-noise amplifiers, filters, and management modules, and the entire solution occupies the least area of PCB. 2.4 GHz Wi-Fi plus BLE dual-mode chip, 16MB Flash with TSMC Ultra-low power consumption 40nm technology, power dissipation performance and RF performance is the best, safe and reliable, easy to extend to a variety of applications
* Board uses SPI to connect LCD: D23/GPIO23->MOSI, D18/GPIO18->SCLK, D15/GPIO15->CS, D2/GPIO2->DC, D4/GPIO4->RST,D32/GPIO32->BLK.With this board,it's easy to display a variety of information and data


|   Pin  |	    Connection    |	Tasmota GPIO Setting  |
| ------ | ------------------ | --------------------- |
| GPIO2  |	DC (Data/Command) |	SPI DC                |
| GPIO4  |	RST (Reset)	      | Display Rst           |
| GPIO15 |	CS (Chip Select)  |	SPI CS                |
| GPIO18 |	SCLK (Clock)      |	SPI CLK               |
| GPIO23 |	MOSI (Data)       |	SPI MOSI              |
| GPIO32 |	BLK (Backlight)   |	Backlight             |

https://www.amazon.com/dp/B0D6QXC813?ref=ppx_yo2ov_dt_b_fed_asin_title&th=1


## Tasmota custom `user_config_override.h`

* https://github.com/benzino77/tasmocompiler

```c
#define USE_SPI                    // Enable SPI support
#define USE_DISPLAY                // Enable display support
#define USE_DISPLAY_ST7789         // Enable ST7789 display support
#define USE_DHT                    // Enable support for DHT sensors (DHT11, DHT22, etc.)

#ifndef _USER_CONFIG_OVERRIDE_H_
#define _USER_CONFIG_OVERRIDE_H_

// GPIO Configuration
#define GPIO_CONFIG                                                      \
    GPIO(0, A3)                   /* GPIO0 is assigned to a virtual function (A3). This is a marker to signal that uDriver should be started. It has no effect on GPIO itself and can be assigned to reserved (red) GPIOs. */ \
    GPIO(2, GPIO_SPI_DC)          /* GPIO2 is used as the Data/Command pin for the SPI display. */ \
    GPIO(4, GPIO_DISPLAY_RST)     /* GPIO4 is used as the reset pin for the display module. */ \
    GPIO(15, GPIO_SPI_CS)         /* GPIO15 serves as the Chip Select pin for the SPI display. */ \
    GPIO(18, GPIO_SPI_CLK)        /* GPIO18 is the Clock pin for the SPI interface. */ \
    GPIO(23, GPIO_SPI_MOSI)       /* GPIO23 is the Master-Out-Slave-In (MOSI) pin for SPI communication. */ \
    GPIO(32, GPIO_BACKLIGHT)      /* GPIO32 controls the display backlight (on/off). */ \
    GPIO(14, GPIO_AM2301)          /* GPIO14 is configured for the DHT22 temperature and humidity sensor. */ \
    GPIO(13, GPIO_RELAY)          /* GPIO13 is configured for the relay control. */

#define MODULE                 ESP32_DEVKIT  // Set the device module to ESP32 DevKit.

#endif  // _USER_CONFIG_OVERRIDE_H_

// Define but do not activate Rule3
#ifndef USER_RULES
#define USER_RULES "Rule3 :H,ST7789,170,320,16,SPI,1,15,18,23,2,32,4,*,80 :S,2,1,3,0,80,30 :I 01,A0 11,A0 3A,81,55 36,81,00 21,80 13,80 29,A0 :o,28 :O,29 :A,2A,2B,2C :R,36 :0,C0,23,00,00 :1,A0,00,23,01 :2,00,23,00,02 :3,60,00,23,03 :i,21,20"
#endif

```

## References

* https://www.youtube.com/watch?v=xLC9bQUkEKM&t=29s
* https://tasmota.github.io/docs/Universal-Display-Driver/
* https://github.com/huyphamnhu/Tasmota-RGB565-Converter
