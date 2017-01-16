---
title: "Using a servo with the microbit"
layout: text-width-sidebar

# Meta description for google and sharing
meta-description:  "Use a servo in python with the microbit."

#############
## Options ##
#############

share: true
author: jez

#################################
##     Component Specific      ##
#################################

# About Box is on the left of the page
about: "Use a servo in python and PXT."

# Type of component: internal or external
cats: external

# Name of Component for index page
simple-description: Servo

acknowledgements: Servo teaser & diagram by [Upgrade Industries](https://www.upgradeindustries.com/licensing/)

date: 2016-12-23T10:20:00Z
---

The __Tower Pro SG90__ is a small, 9 gram servo that can run directly from the microbit power supply. This is a 180&deg; servo meaning it can turn from 0&deg; to 180&deg;. It has many applications: open a flap to dispense treats for to a dog, create a robotic walker, or to drive window wipers on a car.

{:.ui .dividing .header}
### Electronics

#### Which Wire is Which?

Most servos have three wires: GND, POWER, and SIGNAL.

Wire colours differ based on manufacturer. Here's the Tower Pro servo; look at the wire colours:

![SG90 Servo Wire Colours](images/servo.png){:.ui .image .centered}

Information about the wire colours can be found in the datasheet. This can be found by Googling _SG90 datasheet_:

![SG90 Data Sheet What Coloured Wires?](images/servo-data-sheet.png){:.ui .image .centered}

We now know how to connect the servo:

{:.ui .very .basic .small .table}
| Servo Wire Colour | Data Sheet Label | Connect to Microbit Pin |
| Red | VCC (+) | `3V` pin |
| Brown | Ground (-) | `GND` pin |
| Orange | PWM (Signal) | `pin0` |

The angle of the servo is set by a PWM pulse to the orange wire. This is connected to `pin0`.

{:.ui .dividing .header}
### Code

Servos are difficult to control in Python on the microbit. I've tried to make it easy below.

<div class="ui top attached tabular menu">
  <a class="item active" data-tab="first">Python</a>
  <a class="item" data-tab="second">MS Blocks</a>
</div>
<div class="ui bottom attached tab segment active" data-tab="first" markdown="1">

A module must be installed to tell Python how to use the servo. 

#### Steps

* Download the [Servo class](https://github.com/microbit-playground/microbit-servo-class/blob/master/) and save it in the `/mu_code` directory in your home folder.
* Upload the code below to your microbit.
* Upload the `servo.py` file to the microbit within mu.

There are [detailed instructions on adding a module to the microbit on this website](/howto/add-python-module-microbit-micropython).

#### Code
{% highlight python %}

from microbit import *

from servo import Servo

while True:
    Servo(pin0).write_angle(0)
    sleep(200)
    Servo(pin0).write_angle(90)
    sleep(200)
    Servo(pin0).write_angle(180)
    sleep(200)

{% endhighlight %}

The angle of the servo is controlled by `Servo(pin0).write_angle(30)`. If you want to control a servo attached to pin1 as well, it would be: 

{% highlight python %}
Servo(pin1).write_angle(30)
{% endhighlight %}

We can also make this a variable for ease of use:

{% highlight python %}
sv1 = Servo(pin0)
sv2 = Servo(pin1)

sv1.write_angle(180)
sv2.write_angle(0)
{% endhighlight %}

[There is additional detail about the `Servo` class on github](https://github.com/microbit-playground/microbit-servo-class)

</div>


<div class="ui bottom attached tab segment" data-tab="second">
<img src="images/servo-pxt.png" class="ui image">
</div>

### Experiment
* Play with the [sweep example](https://github.com/microbit-playground/microbit-servo-class/blob/master/examples/twist-example.py) to rotate the servo through 180&deg;

