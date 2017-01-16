---
title: "7 Segment Display with MAX7219 Backpack"
layout: text-width-sidebar

# Meta description for google and sharing
meta-description:  "Using a MAX7219-driven 8-digit 7 Segment LED display module on the microbit."

#############
## Options ##
#############

share: true
author: jez

#################################
##     Component Specific      ##
#################################

# About Box is on the left of the page
about: "Use a 7-segment display to show digits on the microbit"

# Type of component: internal or external
cats: external

# Name of Component for index page
simple-description: 7-Segment Display (SPI)

---

![microbit edge connector](images/7-segment-display-max7219.jpg){:.ui .image .small .floated .right}

This module will display 8 numerical digits on its display. Each digit is a 7-segment display comprised of 8 LEDs (7 for the number, and one for a decimal place).

It's possible to drive each of these component LEDs either directly, or through a shift register. However, these modules use the `MAX7219` driver chip to simplify the process.

The microbit tells the `MAX7219` chip which number to display over SPI. The chip then displays the digit.

Like the HT1633 8x8 module on this site, the LED displays are connected to a backpack containing the `MAX7219` chip and wiring.

{:.ui .dividing .header}
### Components

These 7-segment MAX7219 displays are available on eBay, Amazon and other sellers. Searching for `MAX7219 7-segment display` reveals the components. They're around £2 each.

Additionally, you will need a microbit breakout board to access the SPI pins of the microbit.

{:.ui .dividing .header}
### Electronics

#### Purpose of Each Pin

There are five wires to connect to the display module. Each of the pins do the following:

{:.ui .very .basic .table}
| Pin Name | Purpose |
|--- |--- |
| VCC | for power |
| GND | for ground |
| CS / Chip Select | Goes low when data is being transmitted to the device. Goes high at the end of transmission. `.write_digital()` is used for this. |
| DIN | Data transmitted over this wire. |
| CLK | Tells the microbit when to transmit data. |

#### Hookup Table

Connect the module to the microbit and its edge connector as below. Be aware the pin labels can change dependning on the manufacturer:

{:.ui .very .basic .table}
| My Module Label | Possible Label Names | microbit Pin | Micropython Doc Names for pin |
|--- |--- |--- |--- |
| VCC |  | 3v | |
| GND |  | GND | |
| DIN | SOMI, SDI, DI, DIN, SI, MRST. | `pin14` | MISO (master in, slave out) |
| CS | nCS, CSN, nSS, STE, SYNC | `pin0` | n/a, but frequently called _chip select_ |
| CLK | SCLK | `pin13` | Serial Clock |

* *Your module might also have a `DOUT` pin. Ignore it!*

To connect to these pins, you will need the microbit edge connector. Here's my module wired up to my microbit:

![microbit edge connector](images/7-segment-display-max7219.jpg){:.ui .image}

{:.ui .dividing .header}
### Code

#### Download the Module

Download the `Maxrix7seg` [module for the microbit from Github.](https://github.com/microbit-playground/matrix7seg/blob/master/matrix7seg.py). This contains the code used to communicate with the 7-segment display.

#### Import Module

The module is imported in the header of your Python script:

{% highlight python %}
from microbit import spi

# from matrix7seg.py import Matrix7seg class
from matrix7seg import Matrix7seg

# Initialise an instance of the Matrix7seg class
# and call it 'seg_display'.
# It's connected to default SPI pins. pin0 is chip select
# pin1 or pin2 etc could be used instead.
seg_display = matrix7seg(spi, pin0)
{% endhighlight %}

#### Add the `matrix7seg` Module

Once your script is complete and has been flashed, the `matrix7seg` module can be copied to the microbit:

1. Flash your script.
2. Click 'Files' within in the mu editor.
3. From the `/mu_code/` directory, copy drag the `matrix7seg.py` file across to the microbit.
4. Press reset on your microbit to reload the Python program with the `matrix7seg` module.

#### Using the Module

It's now possible to use the display module within the microbit:

{% highlight python %}
# Number must be 8 or fewer digits
seg_display.write_number(1234)

# Update display with '1234'
seg_display.show()
{% endhighlight %}

Each time `.write_number()` is used, `.show()` must be used to update the display.

#### Code Examples

##### `.write_number()`

![default display](images/7-segment-display-max7219-default.jpg)

{% highlight python %}
# display a number
seg_display.write_number(1234)
{% endhighlight %}

##### `.write_number(n, zeroPad=True)`

![zerofill](images/7-segment-display-max7219-zerofill.jpg)

{% highlight python %}
# empty 7-segments filled with 0
seg_display.write_number(1234, zeroPad=True)
{% endhighlight %}

##### `.write_number(n, leftJustify=True)

![go left](images/7-segment-display-max7219-left.jpg)

{% highlight python %}
# justify numbers to left
seg_display.write_number(1234, leftJustify=True)
{% endhighlight %}

#### Example Programs

##### Increment Numbers to 100

{% highlight python %}
# sequentially write numbers to 100
for i in range(100)
    seg_display.write_number(i)
    seg_display.show()
{% endhighlight %}

##### Show the Temperature
{% highlight python %}
# read and display the temperature every second
while True:
    seg_display.write_number(temperature())
    seg_display.show()
    sleep(1000)
{% endhighlight %}

##### G-Force Game

{% highlight python %}
# record total acceleration experienced by the microbit
# if it's the highest value recorded by the microbit,
# display the reading on the screen.
# importing as little as possible to save memory

from microbit import spi, accelerometer, sleep, pin0
from math import sqrt
from matrix7seg import Matrix7seg

def total_acceleration():
    """
    return total acceleration in milli-g across all 3 axes.
    """
    x = accelerometer.get_x()
    y = accelerometer.get_y()
    z = accelerometer.get_z()

    # root of sum of squares
    total = sqrt(x**2 + y**2 + z**2)
    return total

highest_reading = 0

segment = Matrix7seg(spi, pin0)

while True:
    reading = total_acceleration()
    if reading > highest_reading:
        highest_reading = reading
    segment.write_number(highest_reading)
    segment.show()
{% endhighlight %}
