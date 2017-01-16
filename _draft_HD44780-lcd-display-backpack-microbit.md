---
title: "8x8 LED Matrix"
layout: text-width-sidebar

# Meta description for google and sharing
meta-description:  "Connect a DS3231 RTC to the microbit and take time & date with python."

#############
## Options ##
#############

share: true
author: jez

#################################
##     Component Specific      ##
#################################

# About Box is on the left of the page
about: "Use 8x8 LED matrix with HK16K33 driver "

# Type of component: internal or external
cats: external

# Name of Component for index page
simple-description: HD44780 LCD + Backpack

acknowledgements: Messy LED Matrix image by Hypercoregz on Flickr (CC-BY). Teaser Image by Adafruit (CC-BY).
---

LCD displays are a good way to display information from the microbit; it is much easier to read than the scrolling display.

(picture)

As with the [8x8 matrix](/8x8-matrix-HT16K33), an I2C backpack is used for simplicitiy.


{:.ui .dividing .header}
### Component

#### HD44780 Display Module

The LCD screen above has two roads of 16 characters (16x2). There is a Hitachi HD44780 chip on the back of the module which drives the display. These are usually listed as `HD44780` LCDs.

#### Serial I2C Backpack

The backpack connects to the LCD module's 16 pins. The microbit communicates display information over two I2C wires as opposed to 4 or 8!

There are many available and are usually around £3. [Here's an example on eBay](http://www.ebay.co.uk/itm/1602-16x2-HD44780-Character-LCD-w-IIC-I2C-Serial-Interface-Adapter-Module-/221905369007?hash=item33aa9737af:g:W-4AAOSw0HVWEobg).

#### Solder Backpack to LCD

##### Contrast

The contrast is altered by `pin3` on the HD44780.


{:.ui .dividing .header}
### Electronics

A microbit edge connector is required to access the I2C pins on the microbit. These are `pin19` and `pin20` of the microbit.

{:.ui .basic .small .table}
| Backpack Pin | Microbit Pin |
|--------|----------|
| `GND` | `GND` |
| `VCC+` | `3V` |
| `DAT` or `SDA` | `PIN 20` |
| `CLK` or `SCA`  | `PIN 19` |

The I2C naming conventions are different than usual. SCL = CLK & SDA = DAT.

#### I2C Addresses

The I2C bus is accessed through `pin19` and `pin20`. There are already two components on the bus:

{:.ui .basic .small .table}
| Device | I2C Address |
|--------|----------|
| Accelerometer | `0x1D` |
| Magnetometer | `0x0E` |

Each slave on the bus must occupy a different address. Check the I2C address on the data sheet of your component and ensure they do not conflict with other components. On the Adafruit backpack it's possible to [change the I2C address](https://learn.adafruit.com/adafruit-led-backpack/changing-i2c-address) if required.

The is a [guide to scanning the I2C bus on this website](/howto/scan-i2c-bus).

{:.ui .dividing .header}
### Code

[Radomir Dopieralski](https://bitbucket.org/thesheep/) has written a Python module to control HT16K33-based backpacks. [Download the HT16k33 driver](https://bitbucket.org/thesheep/microbit-ht16k33/raw/a5b7961f0b57ba226ab98edc2c5f8d95d8954d00/ht16k33.py) and save it to your computer.

Upload the saved module to the microbit in mu. See [here for tutorial on how to add modules](/howto/add-python-module-microbit-micropython).

{% highlight python %}
from microbit import i2c, sleep

from ht16k33 import Matrix8x8

display = Matrix8x8(i2c)

# Run through each pixel individually and turn it on.
for x in range(8):
	for y in range(8):
		display.pixel(x, y, 1)
		display.show()
		sleep(50)

# Clear the display
display.fill(0x00)
display.show()
sleep(1000)

# Fill display
display.fill(0xff)
display.show()
sleep(1000)

# Cycle through the brightness levels
for x in range(15):
    display.brightness(x)
    sleep(50)

{% endhighlight %}

<div class="ui message">
  <div class="header">
    MAX7219 LED Driver
  </div>
  <p>The MAX7219 is an alternative driver that uses SPI. Multiple LED displays can be linked together. I've not managed to slim a module down yet for the microbit. </p>
</div>
