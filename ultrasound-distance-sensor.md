---
title: "Ultrasound Sensor to Measure Distance"
layout: text-width-sidebar

# Meta description for google and sharing
meta-description:  "Use ultrasound to measure distance to an object on the microbit"

#############
## Options ##
#############

share: true
author: jez

#################################
##     Component Specific      ##
#################################

# About Box is on the left of the page
about: "Sensor sends an ultrasound pulse and listens for the echo. It returns the distance to a target by how long the echo took to return."

# Type of component: internal or external
cats: external

# Name of Component for index page
simple-description: Ultrasound

acknowledgements: Teaser image by Sparkfun (CC-BY). Sonar diagram by Georg Wiora CC-BY-SA-2.5

date:         2016-12-23T10:20:00Z
date-updated: 2016-12-23T10:20:00Z
---

Sonar uses sound to detect objects. It can be used to measure distance to an object.

#### How Sonar Works

![Example of Sonar](images/ultrasound-distance-sensor-sonar.svg){:.ui .image}

The distance from the sensor to the object can be calculated by measuring the time sound takes to return to the sensor after a pulse.


{:.ui .dividing .header}
### Component
A HC-SR04-compatible sensor module has a speaker and microphone; one sends an ultrasonic pulse of sound, the other receives it. By measuring the difference between the pulse and echo, the distance to the object can be calculated.

![HC-SR04](images/ultrasound-distance-sensor-HC-SR04.jpg){:.ui .image}

There are four pins:

* VCC: for 3v voltage
* Trig: triggers a pulse of ultrasound
* Echo: outputs high if the pulse of ultrasound is detected.
* GND: ground

Searching Amazon or eBay for `HC-SR04` will reveal many examples of these sensors. They're around £1 each.

{:.ui .dividing .header}
### Electronics

Hook up the sensor as follows:

{:.ui .celled .striped .table}
| HC-SR04 Sensor | Microbit Pin |
|----------------|--------------|
|  `VCC`         | `3v`         |
|  `GND`         | `GND`        |
|  `Trig`        | `PIN0`       |
|  `Echo`        | `PIN1`       |


{:.ui .dividing .header}
### Code

<div class="ui top attached tabular menu">
  <a class="item active" data-tab="first">PXT.io</a>
</div>
<div class="ui bottom attached tab segment active" data-tab="first">

The ultrasound sensor requires measurements in microseconds and so is only available in PXT.IO.

<img src="images/ultrasound-distance-sensor-pxt-example.png" class="ui image centered">

You will need to add the sonar package to the project.

</div>

{:.ui .dividing .header}
### Notes
* For use with Python, use an I2C ultrasound distance sensor. These are usually quite expensive.
