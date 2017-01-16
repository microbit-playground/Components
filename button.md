---
title: "Using a Push Button &amp; Microbit"
layout: text-width-sidebar

# Meta description for google and sharing
meta-description:  "How to use a tactile push button switch in microbit electronic projects"

#############
## Options ##
#############

share: true
author: jez

#################################
##     Component Specific      ##
#################################

# About Box is on the left of the page
about: "Use buttons to provide external inputs to the microbit."

# Type of component: internal or external
cats: external

# Name of Component for index page
simple-description: Push Button

acknowledgements: SMD push button switch by Sparkfun (CC-BY-2.0)

date: 2016-12-23T10:20:00Z
---

A small push button can be used to provide an external input into your circuits.

![Push Button Diagram and Photograph](images/button-push-button.png){:.ui .image}

This is a small, SMD-mount tactile switch identical to the ones on your microbit.  These switches are normally open (or *NO*) and so must be pushed to close the circuit. It said to be momentary as it must be held to close.

{:.ui .dividing .header}
### Electronics

One of the button's pins is connected to 3V. The corresponding pin to `pin0` of the microbit. When the button is pressed, `pin0` reads `True` or `1`. 

![Push Button Diagram and Photograph](images/button-circuit-no-pull-down.png){:.ui .image .centered}

{:.ui .dividing .header}
### Code

<div class="ui top attached tabular menu">
  <a class="item active" data-tab="first">Python</a>
</div>
<div class="ui bottom attached tab segment active" data-tab="first">

Display a tick if button attached to `PIN0` is pressed

{% highlight python %}
from microbit import *

while True:
    # if pin1.read_digital() == 1
    if pin1.read_digital():
        display.show(Image.YES)
    else:
        display.show(Image.NO)
    sleep(10)

{% endhighlight %}

</div>



### Experiment
* Add multiple buttons
* Count button presses. It'll be wrong; why?

<div class="ui message">
  <div class="header">
    Pull-down Resistor?
  </div>
  <p>The microbit has internal pull-up and pull-down resistors. When a digital input is read by the microbit, the pull-down resistors are turned on so there is no need for an external one. </p>
  <p>This behaviour can be modified in PXT but not Python. </p>
</div>


