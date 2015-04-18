 TeensyLED Controller
 Copyright Brian Neltner 2015
 Version 0.2 - April 13, 2015

 This provides a basic library and example code for interacting
 with a RGBW LED light using Hue, Saturation, and Intensity (HSI)
 mode. This version has been updated to match the pinout of the RGBW
 driver board provided in the associated Eagle Design files included
 in this repository.

 Software Features:
 - HSI to RGBW library for interacting with LED sources.
 - PID based fader that follows a random walk through colorspace.
 - Outline (totally untested) start of DMX receiving software.

 Targeted features in this Eagle Board design, which is also released
 as open hardware under the same license as this software.

 - Teensy 3.1 socket.
 - RJ45-based DMX Connectors as per DMX-512A.
 - Fully isolated DMX-compatible RS485 Interface (ADM2582E).
 - Header to switch polarity of DMX signal for compatibility.
 - Accessible slider switch for connecting 120 ohm termination resistor.
 - 4x 700mA BJT based current sinks (670-730mA typical).
 - Current sinks capable of driving 700mA at up to 100nm pulse width.
   - 100nm pulse width allows 16-bit PWM at 150Hz, or 8-bit PWM at 39kHz.
 - 5-48VDC board compatibility, with the Vin routed directly to LED V+.
 - Built in high efficiency switching regulator to provide 3.7VDC.
 - Designed to fit into Hammond 1455C801 Extruded Aluminum Enclosure.
 - Solder lugs compatible with Keystone 5016 test points for:
   (a) V+ (voltage to the board)
   (b) GNDA (ground to the board)
   (c) VCC (voltage from 3.7V supply)
   (d) GND (ground for digital ICs)
   (e) VISO (isolated 3.3V for DMX)
   (f) DAC (12-bit Teensy 3.1 DAC output)
   (g) A0-A1 (2 10-bit ADCs)
   (h) A2 (1 10-bit ADC also usable for capacitive touch sensors)
 - Separate ground pours were used for the power ground, digital ground,
   and DMX ground.

 Major Design Considerations:
 - Heat dissipation at the BJTs is severe, with switching regulators
   generally being inappropriate for such high speed PWM capabilities.
   (a) Although the BJTs chosen are rated to 4.4W each, at 700mA and a
       typical minimum drop from the top of the BJT to ground of 3V for
       good regulation, power dissipation throughout the board is likely
       to be a bare minimum of 2.1W per channel fully on.
   (b) I think that if you operate the system in HSI mode, where the
       total current sent to the LEDs is limited to 700mA, split between
       the various channels to change colors, you can probably get away
       with as much as 4W from that subsystem. This is power lost in the
       current sink itself, the power of the LEDs is unimportant.
   (c) This limits the voltage you can have between the *bottom* of your
       LED chain (no matter how long it is) and ground to under *5VDC*.
   (d) I am thinking about a new design that will automatically regulate
       down the voltage at the top of the LEDs to the minimum needed
       for reliable regulation based on feedback, but this is a work in
       progress. Perhaps for version 2.0.
 - High current and high frequency PWM may radiate excessively for FCC.
 - High current and frequency PWM may introduce noise issues into board.
   (a) May severely degrade ADC measurements, especially from high-
       impedance sources.
   (b) May disrupt RS485 communication, this could render the board
       non-functional. As yet untested.
   (c) May put enough noise onto the power supply so as to severly
       hinder normal operation.
 - The best design practices I know for managing these I have used, but
   I am not an EE, I only play one on TV sometimes.

 This file is part of TeensyLED Controller.

 TeensyLED Controller is free software: you can redistribute it and/or 
 modify it under the terms of the GNU General Public License as published
 by the Free Software Foundation, either version 3 of the License, or
 (at your option) any later version.

 TeensyLED Controller is distributed in the hope that it will be useful,
 but WITHOUT ANY WARRANTY; without even the implied warranty of
 MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
 GNU General Public License for more details.

 You should have received a copy of the GNU General Public License
 along with Foobar.  If not, see <http://www.gnu.org/licenses/>.