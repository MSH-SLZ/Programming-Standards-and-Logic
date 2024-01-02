## Control Method
It is recommended to use Ethernet and Telnet to control a Biamp device.

## IP Address
Programming's default IP that will be used if none are provided is 192.168.1.141

## Serial Baud Rate
If serial control is to be used, please change the serial baud rate to 38400. This is default on the Audia.
It is NOT default on the Tesira. This lower baud rate will ensure that longer cable lengths can be used.

## Presets
* Startup
  - recalled when system is turned on
* Shutdown
  - recalled when system is turned off

## Instance Tags
| Instance Tag | Block Type | Description |
|-|-|-|
| LVM-PGM | Level Control | Program Volume, ganged if stereo|
| LVM-ATC | Level Control | VoIP or POTS Incoming Volume |
| LVM-VTC | Level Control | Video Conference Incoming Volume |
| LVM-WRLS | Level Control | Wireless Microphone Volume, multi-channel if needed |
| LVM-LECT | Level Control | Lectern Microphone Volume
| MTE-CMIC | Mute Control | Mute Ceiling Microphones
| MTE-PRV | Mute Control | Privacy Mute - Outgoing Audio to either VoIP or POTS |
| VCS | Voip Control Status | |
| VIDIALER | VoIP Dialer | |
| TCS | POTS/TI Control Status | |
| TIDIALER | POTS/TI Dialer | |

## Microphone LEDs and Mute
It is recommended that the microphones' LEDs be controlled and synced with the DSP. Use the Logic output of the mute block to control the microphone's LEDs
See below on how to control LEDs of microphones.
<br>
In the sample shown below the microphone itself is not muted. Audio will still pass from the microphone into the Tesira Forte or Server. The audio is muted downstream from the microphone. This allows for the AEC block to continually assess the audio from the microphone.

## Parlé Microphones
Biamp Parle microphones are normally RED. When the RD1 or RD2 logic is set to high, then it will be GREEN.
Here's a sample on how to setup your Tesira file.
### ![parle sample](parle-mute-sample.png)

## Shure MXA LEDs
Shure MXA LEDs can be controlled from the Tesira. This leads to a better software design because there's no reliance on the Crestron or other control system processor to keep the DSP and the microphone LEDs in sync.
### ![shure mute sample](shure-mute-sample.png)
### ![shure command strings](shure-command-strings.png)
For a list of control commands see [Shure MXA Publication](https://pubs.shure.com/command-strings/MXA-MUTE/en-US)
### ![shure command string properties](shure-command-strings-props.png)
