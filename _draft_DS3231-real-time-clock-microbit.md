---
title: "DS3241 Real Time Clock on the Microbit"
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
about: "Use a RTC to record the time in Python"

# Type of component: internal or external
cats: external

# Name of Component for index page
simple-description: DS3231 RTC
---

``` 
Ignore this. 
All of it!
```

A Real Time Clock (RTC) allows the microbit to know the time. It has a small battery and can keep the time for years. The microbit can use this data for datalogging and other programs.

This page uses the `DS3231` chip. The module is a generic one from eBay.

{:.ui .dividing .header}
### Electronics

#### Hook Up

You must connect 4 of the wires from the  module to the microbit.

{:.ui .very .basic .small .table}
| Board Pin | Microbit Pin |
|--------|----------|
| `GND` | `GND` |
| `VCC` | `3V` |
| `SDA` | `PIN 20` |
| `SCL`  | `PIN 19` |

You'll need a microbit edge connector to access the microbit's 19 & 20 pins.

#### Find RTC address

Before beginning we need to obtain the I2C address of the device. Here are the results of the scan script on my module:

{% highlight python %}
>>> Scanning I2C bus...
Found:  [0xe]
Found:  [0x1d]
Found:  [0x57]
Found:  [0x68]
Scanning complete
Reference:  Magnetometer [0x0e] Accelerometer [0x1d]
{% endhighlight %}

There are two additional devices: `0x57` & `0x68` whereas only the RTC might be expected.

There are often two devices on each module. One is the DS3231 RTC and the other is EEPROM memory. On my devices, the RTC has the address `0x68`.


{:.ui .dividing .header}
### Code

This example uses a Python module to communicate with the RTC. Download it from https://github.com/switchdoclabs/RTC_SDL_DS3231/blob/master/SDL_DS3231.py. Flash your script in mu (as below) and then upload the module. There's more detail on the how to page.

The head of the main script file would look like this:

{% highlight python %}

# only import microbit I2C and display modules
from microbit import I2C, display

# Import SDL_DS3231 class and functions
# from the SDL_DS3231.py file uploaded to the microbit.
from ds3231 import DS3231

# Initialise an instance of the SDL_DS3231 class
# and call it rtc.
rtc = SDL_DS3231()

# or if the address of the module is different
# to `0x68`, this can be specified
# rtc = DS3231(addr=0x65)


{% endhighlight %}

#### Setting the Time
The time on the RTC must be set.

You will need only to update it for British Summer Time or if the battery is replaced.

{% highlight python %}

# 1:32pm and 20 seconds. 13th October 2016
rtc.set_datetime(
            seconds=20,
            minutes=32,
            hours=14,
            day=13,
            month=10,
            year=2016,
            )

{% endhighlight %}

#### Reading the Time

With the time set, it is possible to read the time from the RTC.

There are three functions for returning the time:

* `datetime_tuple()` --- a tuple of the time and date
* `datetime_string()` --- a string of the time and date
* `time_string()` ---  a string of the time, eg. 11:33

##### `datetime_tuple()`

Return the time and date as a tuple.

Format is (YYYY, MM, DD, HH, MM, SS)
{% highlight python %}
>>> rtc.datetime_tuple()
(2016, 10, 13, 14, 32, 20)
{% endhighlight %}


##### `datetime_string()`

Return the time & date as a string.

Format is YYYY-MM-DDTHH:MM:SS. This is useful for recording as a `.CSV` file and importing into excel.

{% highlight python %}
>>> rtc.datetime_string()
'2016-10-13T14:32:20'
{% endhighlight %}

##### `time_string()`

Return the time as a string.

Format is HH:MM.

{% highlight python %}
>>> rtc.time_string()
'14:32'
{% endhighlight %}


#### Final Code

{% highlight python %}

from microbit import i2c, display

from ds3231 import DS3231

# rtc with address 0x68
rtc = DS3231()

# set the time to 1:32pm and 20 seconds. 13th October 2016
rtc.set_datetime(
            second=20,
            minute=32,
            hours14,
            day=13,
            month=10,
            year=2016,
            )

# print tuple of date & time to the REPL window
rtc.datetime_tuple()

# print formatted string of date & time to the REPL
rtc.datetime_string()

# scroll time HH:MM on the microbit display
display.scroll(rtc.time_string())

# unpack tuple
year, month, day, hour, minute, seconds = rtc.datetime_tuple()

# Show ghost face if between 11pm and 7am
if hour > 23 and hour < 7:
    display.show(Image.GHOST)
else:
    display.show(Image.FABULOUS)
{% endhighlight %}


{:.ui .dividing .header}
### Notes

* There is 32k of EEPROM memory on many of these modules. It would be possible to log data to the memory. I've not quite managed to work out how to do this yet.

* There's also a thermometer. Again, I've not managed get it working!


AT24C32 Code

```
from microbit import i2c, sleep


def _bcd2bin(value):
    return value - 6 * (value >> 4)


def _bin2bcd(value):
    return value + 6 * (value // 10)


class DS3231():

    def __init__(self, addr=0x68):
        self._addr = addr
        self._at24c32_addr = at24c32_addr

    def datetime_tuple(self):
        buffer = bytearray(7)
        buffer = i2c.read(self._addr, 7)
        return (
            _bcd2bin(buffer[6]) + 2000,  # year
            _bcd2bin(buffer[5]),         # month
            _bcd2bin(buffer[4]),         # day
            _bcd2bin(buffer[2]),         # hour
            _bcd2bin(buffer[1]),         # minute
            _bcd2bin(buffer[0]),         # second
            )

    def time_string(self):
        year, month, day, hour, minute, second = self.datetime_tuple()
        return '%02d:%02d' % (hour, minute)

    def datetime_string(self):
        year, month, day, hour, minute, second = self.datetime_tuple()
        return '%02d-%02d-%02dT%02d:%02d:%02d' % (year, month, day, hour, minute, second)

    def set_datetime(self, year, month, day, hour, minute, second):
        buffer = bytearray(7)
        buffer[6] = _bin2bcd(year % 1000)
        buffer[5] = _bin2bcd(month)
        buffer[4] = _bin2bcd(day)
        buffer[2] = _bin2bcd(hour)
        buffer[1] = _bin2bcd(minute)
        buffer[0] = _bin2bcd(second)
        i2c.write(self._addr, buffer)
```
