# Components Section

Repository for the microbit playground [components section](https://microbit-playground.co.uk/components/).

This repository is checked out at build time. There is a `draft` branch and a `publish` branch. All changes should be made to the `draft` branch and merged into publish with a squash.

### Contributing
See [the page on the website](https://microbit-playground.co.uk/about/how-to-contribute). Submissions are welcome.

Submit an issue if you have an idea for an article.

##### A Contribution Should...
* Not contain fixes or additions to existing articles; please use 'Issues'.
* Be a pull request to the `draft` branch.
* Have a `720x420px` `.png` teaser image in `/teaser/`.
* all filename prefixed by the name of the name of the main of the `.md` file.
* Update the _Image Licensing_ section of this README.
* Licensed images used are mentioned in the `YAML` frontmatter of the `.md` file in the `acknowledgements` field if required.
* Nothing too spammy or marketty or Google juicy.

###### Optional
* For public attribution on the website, add your name and details to the author repository.

###### A Brief Note
Github is very rude! I do not mean the people but github.com.  Picture the scene: you spend an age writing an article and are filled with pride and goodness about helping kids & adults learn. When I review and start to edit it, __rejected__ or __changes requested__ appears!

Perhaps this works fine in some areas but I know there is an emotional attachment when writing learning resources.

So please, do please translate these message from robot into Human.

### Files in Repository
The website's pages are generated from `.md` files in the main directory. The name of each `.md` file has a corresponding image in `/teaser/` of the same name.

* `/images/` -- Images used in the article.
* `/teaser/` -- Directory for teaser images & video.
* `/teaser/tiny` & `/teaser/card` -- Generated images sizes.
* `/KITCHENSINK.md` -- Examples for fomatting.

### Licensing
#### Contributions
Each submission is covered by the CC-BY-NC 3.0 licence. You retain copyright but allows the website to use it (but not make money).

#### Images


| Image Name          |  Author          |   Licence         |
|---------------------|------------------|-------------------|
| [sonar-sensor]      | Sparkfun         | CC-BY-NC-SA 3.0   |
| [sonar-diagram]     | Georg Wiora      | CC-BY-SA 2.5      |
| [HT16K33] _all_     | Adafruit         | CC-BY-SA 2.5      |
| 7seg-spi            | Jez              | CC0               |
| soil-moisture       | SparkFun         | CC-BY-NC-SA 3.0   |
| soil-dupont         | Adafruit         | CC-BY-SA 2.5      |
| [servo]             | Upgrade Ind.     | [^1]              |
| [PWM servo diag]    | Upgrade Ind.     | [^1]              |
| [reed]              | SparkFun         | CC-BY-NC-SA 3.0   |
| [potentiometer]     | SparkFun         | CC-BY-NC-SA 3.0   |
| pot-diag            | Jez              | CC0               |
| [neop-teaser]       | Adafruit         | CC-BY-SA 2.5      |
| [neop-video]        | Adafruit         | CC-BY-SA 2.5      |
| neop-connected      | Jez              | CC0               |
| neop-diag           | Jez              | CC0               |
| button _all_        | SparkFun         | CC-BY-NC-SA 3.0   |
| button-diag         | Jez              | CC0               |
| pir-sensor          | PD               | Public Domain     |

* All Fritzing diagrams CC0 by Jez.
* All PXT screenshots CC0 by Jez.

[sonar-sensor]: https://www.sparkfun.com/products/13959
[sonar-diagram]: https://commons.wikimedia.org/wiki/File:Sonar_Principle_EN.svg
[HT16K33]: https://learn.adafruit.com/adafruit-led-backpack/1-2-inch-7-segment-backpack
[neop-teaser]: https://learn.adafruit.com/adafruit-neopixel-uberguide
[neop-video]: https://learn.adafruit.com/adafruit-neopixel-uberguide
[reed]: https://www.sparkfun.com/products/8642
[potentiometer]: https://www.sparkfun.com/products/9288
[PWM servo diag]: https://www.upgradeindustries.com/licensing/
[servo]: https://www.upgradeindustries.com/licensing/

* [^1]: Upgrade industries Licence:
```
Photographs may be used when UPGRADE INDUSTRIES is credited and linked within visible range of the image on screen so as to be obvious of the source.
```