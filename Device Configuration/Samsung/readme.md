# Control Methods
The following can be used to control Samsung Displays
* Serial
    * MDC
    * Exlink
* Ethernet
    * MDC over IP
    * HTTP
* HDMI-CEC
* IR
    

# MDC (Multiple Display Control)
### About
MDC is Samsung display protocol that was established over a decade ago and has been in use.  
Most Samsung display that have RS-232 on their spec uses this protocol. It is bi-directional.  
One downside to this protocol is that it does not have a volume increment or decrement command.  
Most displays that have a RS-232 port that uses either a 3.5mm or DB9 connector uses this protocol. This protocol is also avaiable on ethernet using ip port 1515.  
### Serial Port Configuration
9600,N,8,1
### IP Port
1515
### Configuration
Press the Home button on the IR remote.
* Set the Device ID to 0, unless instructed otherwise by your programmer
* Set the Control Method to RS232 if using the serial port. Set to LAN if using ethernet
* Suggested settings:
    * Disable Power Save
    * Enable Auto Power On
    * Disable Auto Power Off
    * Enable Any-Net CEC

### Commands
A quick list of MDC commands [here](https://justaddpower.happyfox.com/kb/article/245-samsung-rs232-control-rs232c/)

# ExLink
### About
Exlink is another Samsung display protocol. This was in use many years ago. It is akin to IR commands over a serial port. Although it is also bidirectional there are no query commands. The display only responds with an acknowledge. So status of power or mute does not exist. There are increment, decrement, and discrete volume level commands available.  
### Serial Port Configuration
9600,N,8,1
## Commands
A quick list of Exlink commands [here](https://justaddpower.happyfox.com/kb/article/16-samsung-rs232-control-exlink/)

# HDMI-CEC
Some samsung displays can be controlled using CEC. Enable the Any-Net CEC on the displays. Displays can be turned ON using CEC. Some displays need to be sent HDMI input 1 then CEC power off in order to power off the display from CEC.

# HTTP Control
* Applicable to these models:
    * BE43T-H
    * BE50T-H
    * BE55T-H
    * BE65T-H
    * BE70T-H
    * BE75T-H
    * BE82T-H
    * LH43BETHLGFXGO
    * LH50BETHLGFXGO
    * LH55BETHLGFXGO
    * LH65BETHLGFXGO
    * LH70BETHLGFXGO
    * LH75BETHLGFXGO
    * LH82BETHLGFXGO

These series of display can be controlled using the ethernet. The display will kill its RJ45 port when powered off. Power ON requires a Wake-On-Lan mechanism.

### Configure the display to allow for external control.   
* Menu -> General -> Network -> Expert Settings -> IP Remote -> Enable.  
* During commissioning the token will need to be accepted the first time.  
Press and hold the display's power on button for 5 seconds to send a prompt to the display to accept or reject the token. Use an IR remote of the display to accept the token.

### Extron Programming
Put the Refresh Token command on a press-and-hold of the display's power on button. In the event that the token is not recognized.

# References
* Extron Driver Samsung BE75T-H v1.2 (smsg_10_4875_v1_1_1.pdf)
* A quick list of MDC commands [here](https://justaddpower.happyfox.com/kb/article/245-samsung-rs232-control-rs232c/)
* A quick list of Exlink commands [here](https://justaddpower.happyfox.com/kb/article/16-samsung-rs232-control-exlink/)
