# dev-ideaspark-esp32

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

```c
#define USE_SPI
#define USE_DISPLAY
#define USE_DISPLAY_ST7789

#ifndef _USER_CONFIG_OVERRIDE_H_
#define _USER_CONFIG_OVERRIDE_H_

// Example GPIO configuration
#define GPIO_CONFIG           \
    GPIO(0, A3)               /* GPIO0 set to option a3 */
    GPIO(2, GPIO_SPI_DC),     /* GPIO2 for DC */       \
    GPIO(4, GPIO_DISPLAY_RST),/* GPIO4 for RST */      \
    GPIO(15, GPIO_SPI_CS),    /* GPIO15 for CS */      \
    GPIO(18, GPIO_SPI_CLK),   /* GPIO18 for SCLK */    \
    GPIO(23, GPIO_SPI_MOSI),  /* GPIO23 for MOSI */    \
    GPIO(32, GPIO_BACKLIGHT)  /* GPIO32 for Backlight */

// Replace with the module type (e.g., WEMOS, ESP32_DEVKIT)
#define MODULE                 ESP32_DEVKIT

#endif  // _USER_CONFIG_OVERRIDE_H_
```
