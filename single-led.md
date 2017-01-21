---
title: "Light an external LED on the microbit bit"
layout: text-width-sidebar

# Meta description for google and sharing
meta-description:  "Use electronics and breadboard to light a single LED with the micro:bit."

#############
## Options ##
#############

share: true
author: jez

#################################
##     Component Specific      ##
#################################

# About Box is on the left of the page
about: "Light a Single External LED."

# Type of component: internal or external
cats: external

# Name of Component for index page
simple-description: LEDs

acknowledgements: Teaser image by Adafruit (CC-BY).

date:         2016-12-23T10:20:00Z
date-updated: 2016-12-23T10:20:00Z
---

It's possible to use the external pins on the micro:bit to control external LEDs.

{:.ui .dividing .header}
### Electronics

Electric current can only flow _one way_ through a _light emitting diode_ (LED). It must flow through its anode (**+**) and out its cathode (**-**) to light.

The anode has a longer leg and often has a bend in it.

![Single LED](/components/images/single-led.png){:.ui .image}

A 220&#8486; resistor is added to reduce the voltage; without it the LED would blow.

{% include box.html content="which-resistor" %}

{:.ui .dividing .header}
### Code

<div class="ui top attached tabular menu">
<a class="item active" data-tab="first">Python</a>
<a class="item" data-tab="second">MS Blocks</a>
</div>


<div class="ui bottom attached tab segment active" data-tab="first" markdown="1">

#### Flash a Single LED

{% highlight python %}
from microbit import *

while True:
    pin0.write_digital(1)
    sleep(500)
    pin0.write_digital(0)
    sleep(500)
{% endhighlight %}

#### Fade an LED

{% highlight python %}
from microbit import *

fade_amount = 5   # How much to change brightness each iteration
speed = 10        # speed brightness changes
brightness = 0

while True:
    brightness = brightness + fade_amount
    if (brightness <= 0) or (brightness >= 1023):
        fade_amount = -fade_amount
    else:
        pin0.write_analog(brightness)
    sleep(speed)
{% endhighlight %}

Creates a lot of flickering in Python; not quite sure yet.

</div>
<div class="ui bottom attached tab segment" data-tab="second" markdown="1">
#### Flash a Single LED
<img src="images/single-led-pxt.png" class="ui image">
</div>

### Experiment
* Remove the resistor; what happens?
* Reverse the polarity of the LED; what happens?
* Make the LED flash when the button is pushed.
