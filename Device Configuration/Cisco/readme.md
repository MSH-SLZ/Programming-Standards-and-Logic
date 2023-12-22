# Codec Configuration
- Video Monitors = Single or Dual. I do not recommend leaving this on Auto.
-  Serial Port Mode = On
- Serial Port Baud Rate = 38400
- Serial Port Login Mode = Off
    - If you are controlling a Cisco RoomKit over RS-232 and it responds to every command with an "Unknown Command" error message then you may need to create an account for the control system and turn login mode on.
- Network Services H323 = On (this is so you can dial to an IP address, by default it is off. It should be changed if necessary by their network IT personnel).
- Experimental Run Startup Wizard = Off (use the web portal and search for “wiz” in the configuration settings)
- Proximity Mode = Off
    - This is in the API but I’m not sure if it is in the Web portal.
    - Use keyword “ultra” for ultrasound in the configuration search and just set the Ultrasound Max Level to 0 and Mode to Static instead of Dynamic.
    - This will kill any “chirps” audio output by the Codec that can sometimes be heard when using with the Biamp DSP.
- Peripherals Touch Panels = Not Set (range is Minimum 1, 0-5, or Not Set).
- Peripherals ControlSystems = 1 (or more)

# Other Settings
- It is 99% preferred to control the codec over serial port.
- SX20s use USB to Serial Port adapters to be controlled over serial. Trendnet TU-S9 serial adapter have been confirmed to work with the SX20.
- When used with a DSP, Line Inputs should not be used. These are reinforced on the codec’s audio output by default. These are intended for use with presentation sources thus they are mixed in with the codec’s audio output in either the embedded HDMI audio or the analog audio outputs.
- When used with a DSP, Mic Inputs should be used.
- Mix the Program Audio with Mic Audio in the DSP before sending to the Mic Input of the cisco codec
- Change the Mic Input used with the DSP to a Line Mode in the codec’s configuration.
- When designing for dual screens. Output 1 of the codec is by default where the Far End and self-view appears. Output 2 is where presentation and self-view full screen appears.
- Cisco SX Cameras need to be connected to the codec’s LAN 2 or LAN 3. If more than 3 cameras need to be paired use an Ethernet switch or segregate part of a managed switch. These cameras auto IP from the SX80.
- Codec’s LAN PORT 1 is for the outside world or corporate network.
- Codec’s LAN PORT 2 and LAN PORT 3 is for the codec’s peripherals such as camera and cisco touch panels.
- A user account may need to be created for the control system with permissions for RoomControl, Integrator, and User.

# Spark Room Kit
Overall this is like an SX20 with a built in camera.

1. The unit will accept serial port. The unit must have software version CE 9.2 or higher. I tested with a CE 9.2.5
2. To use serial port, you must attach a USB to Serial device onto the USB A port of the unit. Not the small USB micro B port with the wrench icon. I’ve tested [TRENDNET TU-S9](https://www.amazon.com/TRENDnet-Converter-Installation-Universal-TU-S9/dp/B0007T27H8/ref=sr_1_1_sspa?ie=UTF8&qid=1535567810&sr=8-1-spons&keywords=tus9&psc=1) and it is working.
3. The baud rate is 115200 fixed. This cannot be changed. Please consider cable length into your designs due to this baud rate. At this baud rate it is preferred your COM port be no more than 6ft from the USB-Serial device. You can use an IP-to-Serial device such as a MOXA or C2N-IO to extend your com ports.
4. In the unit’s web portal Serial Port Login Mode OFF is preferred
5. There’s no pan-tilt camera control since the camera is fixed. There is zoom
6. The mic input is the same as the SX20. 4 conductor 3.5mm.  I found this nifty little [adapter](https://www.soundcontrol.net/products/rm-p20-adaptor/).
7. The HDMI input is Input 2. Other codecs the presentation input is usually Input 3.
8. The unit has a built in microphone. Microphone 1. If you intend to use a DSP. I suggest disabling it in the unit’s configuration via its web portal.
9. The unit does have 2 LAN ports. One of the ports has an icon of the touch panel. This is not PoE. The cisco touch 10 requires PoE/PoE+.
10. Crestron’s Module [“Cisco SX80 v2.3.9 for 3-Series (w/Cisco firmware CE 8.x or higher)”](http://applicationmarket.crestron.com/cisco-sx80-v2-3-9-for-3-series-w-cisco-firmware-ce-8-x-or-higher/) will work with this unit.
11. However, the hang-up all input of the module does not hang-up a call dialing in progress. The command to hang-up all calls can be used “xcommand call disconnect\x0D\x0A” to disconnect a call in progress.


 # In Room Controls
- Setup > Configuration > SerialPort
    - xConfiguration SerialPort LoginRequired: On
    - xConfiguration SerialPort Mode: On
- Setup > Configuration > Peripherals
    - xConfiguration Peripherals Profile ControlSystems: ControlSystems 1
- Security > Users
    - Create a user account for the control system, provide RoomControl, Integrator, and User permissions. Put the login credentials in the Cisco Room Device Crestron module.

Additionally, I don’t believe that the Cisco Touch 10 Room Control Processor module (v1.0) handles authentication. So I also included the Cisco Room Devices 3.1 module to perform the initial login and registration with the codec.
