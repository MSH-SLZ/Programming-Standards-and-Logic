# DN-500BD
Denon's DB9 pins 2,3,5 and 7
2 - TX
3 - RX
5 - GND
7 - RTS
<br>
![pinout](/Device%20Configuration/Denon/dn500bd-pinout.png)

Default Baud Rate 115,200 N 8 1. **Do not Change. Does not work on other buad rates when powered off.**

Connect pin 7 to RTS of controller. Note that it is mis-labeled on the Denon. It should be the CTS pin.

RTS pin on Crestron DB9 is pin 7.
CTS pin on Crestron DB9 is pin 8.

Connect Denon DB9 pin 7 to Crestron DB9 pin 7.


## Update on 2-21-2019
Denon DN-500BD MKII
- RS232 does not work on other baud rates if the device is off. Thus use only 115200.
- configure SMW file as follows:
    - baud rate 115200, N, 8, 1
    - handshaking HW: NONE (no RTS/CTS), SW: none
- configure Denon DN-500BD MKII as follows
    - serial bit rate: 115200
