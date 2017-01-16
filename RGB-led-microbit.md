---
title: "Using RGB LEDs with the microbit"
layout: text-width-sidebar

# Meta description for google and sharing
meta-description:  "Drive an RGB LED with the microbit"

#############
## Options ##
#############

share: true
author: jez

#################################
##     Component Specific      ##
#################################

# About Box is on the left of the page
about: "Connect a RGB LED to make any colour you wish!"

# Type of component: internal or external
cats: external

# Name of Component for index page
simple-description: RGB LEDs

acknowledgements: RGB LED teaser image by Oomlout (CC-BY-2.0). RGB spectrum image public domain.

date: 2016-12-23T10:20:00Z
---

An RGB LED is essentially a red, green and blue LED combined into one package. 

![RGB LED](images/RGB-LED-microbit-diagram.jpg){:.ui .image}

An RGB LED has four legs: an anode to drive each of the three component colours and a common cathode. The longest pin is the common cathode (**-**) and is used by all other LEDs in the package.

Each of the colours---red, green and blue---can be made my supplying current to the shorter pins. Usually the order of the pins is the same as the diagram above; but occassionally they can change, and sometimes it's even a common anode.

![RGB LED](images/RGB-LED-microbit-rgb.png){:.ui .centered .image}


Any coloured light can be made by varying how bright the red, blue and green LEDs are lit. This can be done with `pin0.write_analog(n)` where *n* is a value between 0 (off) and 1023 (on full). 


{:.ui .dividing .header}
### Electronics

220&#8486; resistors are placed before the each of the anode pins. 220&#8486; is a safe choice and will cover all RGB LEDs. You can consult the datasheet of the LED if you have it; you may not even need a resistor but it's better safe than sorry!

![RGB LED](images/RGB-LED-microbit-circuit.png){:.ui .image}

{% include box.html content="which-resistor" %}

{:.ui .dividing .header}
### Code

<div class="ui top attached tabular menu">
  <a class="item active" data-tab="first">Python</a>
</div>
<div class="ui bottom attached tab segment active" data-tab="first">

Code to show a yellow light for two seconds then show a red light slowly turning magenta

{% highlight python %}
from microbit import *

# assign colour names to each of the pins
red = pin0
blue = pin1
green = pin2

while True:
	
    # Make Yellow
    red.write_digital(1)
    green.write_digital(1)
    sleep(2000)			 # Show yellow for 2 seconds

    # Turn off Yellow
    red.write_digital(0)
    green.write_digital(0)

    # turn on red
    # slowly increment the intensity of blue to make magenta
    red.write_digital(1)
    for i in range(0,1023):
        blue.write_analog(i)
        sleep(10)

    # turn off pins before repeating
    red.write_digital(0)
    blue.write_digital(0)
{% endhighlight %}

</div>


{:.ui .dividing .header}
### Notes

* `pin0.analog_write(512)` is half as bright as `pin0.analog_write(1023)`.

{% include box.html content="digital-vs-analog" %}




### Experiment
* Use `random.randrange(start, stop, step)` to generate a random colour every few seconds
* Use three potentiometers to mix the colours