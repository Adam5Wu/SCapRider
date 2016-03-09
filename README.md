# Table of Content
1. [Prologue](#prologue)
2. [Solution Space](#solution-space)
  1. [Battery-based Solutions](#battery-based-solutions)
  2. [SuperCapacitor-based Solutions](#supercapacitor-based-solutions)
3. [Current Design](#current-design)
  1. [Version History](#version-history)
  2. [Layout Software Used](#layout-software-used)
4. [License](#license)

---

# Prologue
You just set up a nice shiny surveillance IP camera, and now you have a 24x7 view to your important asset.
And your camera has motion detection with recording, and can even shoot you an email when something interesting happens.

Brilliant!

But the next question soon comes: you camera needs power to operate, constant power.
If power goes black or brown, or even flickers a bit, the camera will lose ability to view, record as well as detect events for a period of time.
And you won't get an email if this happens.

What about battery? Well, the power consumption of a camera is moderate at best, not something you can shovel a battery or two and forget about it for a couple of months.
The power should come from the wall.

OK, you are serious about the robustness of your surveillance, you got a backup generator.
But it still won't give you uninterrupted surveillance, because when power fails, backup generators need some time to kick in.
And you would still be blinded during generator startup, unless you do something about it.

You need an uninterruptible power supply (UPS).

Or to be more precise (and sounds classy), Under-Voltage Ride Through (UVRT).

---

# Solution Space
## Battery-based Solutions

## SuperCapacitor-based Solutions

---

# Current Design

## Version History
V1 was mostly based on diodes and relays.
It does not handle capacitor charging rate control, output voltage regulation, or MCU integration.
Those two functions were to be achieved by external COTS (Commercial Off-The-Shelf) modules, such as PT4115 constant current driver, and adjustable boost regulators.

There is also one design issue -- double-throw relays are usually break-before-make, so there exists a total disconnection state, when relay changes states from one to another. However, for electro-magnetic mechanical relays, if the voltage change is slow enough, the total disconnection state can be quite long, up to several minutes!

V2 is almost a complete redesign, after I gathered a hefty knowledge on SMPS and ESP8266.
It has built-in capacitor charging rate control, output voltage regulation, and MCU integration.
Only one mechanical relay is used, in order to reduce PCB footprint and increase reliability of controls.

There is a minor design flaw -- The current path control should draw voltage before indicator LED, not after, as LEDs are diodes, which incur voltage drops, and thus rendered the control signal unreliable.

V3 is currently being designed.
It is an improved version of V2, on the following aspects:
1. Completely eliminate mechanical relay use
2. Increased voltage hysteresis for super capacitor, from 4.3v-off-5v-on to 4.3v-off-8.8v-on
3. Configurable power out soft-start based on capacitor charge progress, keep power out off until capacitor reaches 8.8v
4. Ability to power off MCU circuits

## Layout Software Used
PCBWeb http://www.pcbweb.com/

---

# License
The circuit design and PCB layout is released under GPL license.
Proprietary licensed release is available upon request.

