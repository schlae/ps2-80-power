# IBM PS/2 Model 80 Power Supply Schematics

There are multiple types of power supplies for these machines. This one is for the one marked 72X6665 / PEC 3978. This is the red switch 225W model.

## Notes

The design is an LLC resonant converter. It has a rather interesting auxiliary bias supply to power the PWM controller, so technically it is two supplies in one box.

* Inrush current into the main reservoir capacitors is limited by R117/118 and RT1/RT2. The capacitors are tied in series (to handle the 220V input case) with balancing resistors.
* The bias supply uses a preregulator that detects ~180V Vp-p and, partway through every AC cycle, cuts off a triac connected in series with a plain-old linear transformer isolated power supply. This ensures that the VCC bias supply has roughly the same voltage regardless of whether it is connected to 120V or 220V.
* The PWM controller is a SG3524 with external transistors that drive an isolation transformer in order to control the BJTs in the main power stage on the non-isolated side. The output voltage trim is set by R77, which samples both the +5V and +12V rail.
* An overcurrent comparator monitors the ripple current through the main power transformer and latches off the PWM controller if it exceeds a threshold. It also monitors the current *difference* between the two Schottky diodes in the 12V secondary side, presumably to detect Schottky diode failures.
* Every voltage (+12, -12V, +5V) is monitored for overvoltage and undervoltage. Overvoltages cause the supply to latch off. Undervoltage just deasserts the power good. Trimmer potentiometer R50 adjusts the voltage reference used by the comparators.
* The power LED is driven by the power good signal.
* The HDD LED is driven by a signal from the planar (motherboard).

## License
This work is licensed under Creative Commons Attribution-ShareAlike 4.0 International.
(C) 2024 Tube Time.
