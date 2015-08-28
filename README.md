# GENIE-LP20-calculator-printer-Arduino

Interfacing a GENIE LP20 calculator printing module with Arduino 
(in my particular case a an Arduino Nano w/ Atmega 328 - but this should not matter)

The printer has:
----------------
- a DC motor (5V, connected to pin2 via a darlington transistor & freewheeling diode)
- an electromagnet (5V coil, connected to pin3 via a darlington transistor & freewheeling diode)
- an encoder (connected to pin4 with a 20K pulldown resistor)
- power source for the encoder (requires external 220 OHM current limiting resistor)

The printer module works as follows:
-------------------------------------
First, the motor has to be switched on (and it takes a while until it spins at full speed).
Then, the encoder can be read out: It always gives 13 short LOW pulses and then one long LOW pulse for sync.
The coil can be switched on after any of those pulses, which will then print different characters.
If the coil is switched on for 20MS, the printhead will move to the next position (from right to left) on in order to print the next character.
If the coil is switched on for 50MS, the printhead will return home (right) after printing the character and the paper will feed one line.
The first three characters which can be printed (rightmost on the paper) are special characters (+,X,÷,DIAMOND,*,DELTA,G,M,C,SPACE,=,-,%,LINE_FEED).
After printing the three special characters, the printhead uses another print wheel and numbers and some other special characters can be printed (·,0,1,2,3,4,5,6,7,8,9,#,-,COMMA).
After printing, the motor should be switched off again.

Pinout of the printer module:
-----------------------------
- BLK:  Coil GND
- BLK:  Coil +5V
- RED:  Motor +5V
- YEL:  Motor GND
- GRE:  Encoder output - connected to Arduino and via 20K pulldown resistor to GND
- WHI:  +5V (encoder power supply)
- ORA:  +5V (encoder power supply)
- BLU:  via 220 OHM to GND (encoder power supply)
