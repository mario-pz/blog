---
title: "traffic light circuit"
date: 2023-04-15
draft: false
categories:
  - "iot"
tags:
  - "rp2040"
  - "circuits"
---

# project: traffic light controller using a rp2040

![picture](https://media.discordapp.net/attachments/1104034184357494886/1104288967228137472/20230506_090854.jpg?width=1194&height=892)

# purpose

the purpose of this project is to create a simple traffic light controller using a rp2040 microcontroller and a few leds.
the traffic light controller will cycle through three different led colors (red, yellow, and green) 
in a repeating pattern to simulate a real traffic light.

# materials

* a rp2040 microcontroller loaded with circuit python
* breadboard
* 3 x 3mm leds (red, yellow, green)
* 3 x resistors (its better than nothing)
* 4 x male jumper wires

# circuit datagram

![datagram](https://media.discordapp.net/attachments/1104034184357494886/1104296506590253066/Screenshot_from_2023-05-06_09-32-51.png)

gpios are basically switches so it should be fine ¯\_(ツ)_/¯

# calculations 

we will apply ohm's law to find what resistance we need for each.

```
resistance (r) = (supply voltage - led forward voltage) / led forward current
```

* green -> 2.1V => (3.3 - 2.1) / 0.02 = 60Ω
* yellow -> 1.8~2.2V => (3.3 - 1.8) / 0.02 = 75Ω
* red -> 1.8v => (3.3 - 1.8) / 0.02 = 75Ω

# code

i choose to use gp0, gp1, and gp2 as my pins. you can easily change these pins by modifying the numbers

```py
# code.py
import time
import board
import digitalio


def main():
    green_led = digitalio.DigitalInOut(board.GP0)
    yellow_led = digitalio.DigitalInOut(board.GP1)
    red_led = digitalio.DigitalInOut(board.GP2)

    green_led.direction = digitalio.Direction.OUTPUT
    yellow_led.direction = digitalio.Direction.OUTPUT
    red_led.direction = digitalio.Direction.OUTPUT

    green_latency: float = 4.0
    yellow_latency: float = 1.0
    red_latency: float = 4.0

    while True:
        green_led.value = True
        time.sleep(green_latency)
        green_led.value = False
        yellow_led.value = True
        time.sleep(yellow_latency)
        yellow_led.value = False
        red_led.value = True
        time.sleep(red_latency)
        red_led.value = False


main()

```

and voila. just like that i made my first circuit project.

# references 

* https://www.waveshare.com/wiki/RP2040-Zero
* https://learn.adafruit.com/circuitpython-digital-inputs-and-outputs/digital-outputs
* https://learn.sparkfun.com/tutorials/rp2040-thing-plus-hookup-guide/hardware-overview
* i watched a lot of https://www.youtube.com/@EngineeringMindset
