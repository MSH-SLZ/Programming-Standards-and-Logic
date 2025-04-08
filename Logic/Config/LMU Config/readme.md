# Table of Contents
For Table of Contents click the hamburger on the top right of this preview window. 

## What is JSON?
JSON (JavaScript Object Notation) is a lightweight data-interchange format that is easy for humans to read and write, and easy for machines to parse and generate. It is commonly used for transmitting data in web applications (e.g., between a server and a client).

### Key Features of JSON:
- **Text-based format**: JSON is written in plain text, making it easy to read and debug.
- **Data structures**: JSON supports two primary data structures:
    - **Objects**: Collections of key-value pairs enclosed in curly braces `{}`. Each key is a string, and the value can be a string, number, boolean, array, object, or `null`.
    - **Arrays**: Ordered lists of values enclosed in square brackets `[]`. Values can be of any type, including other arrays and objects.

### Example of JSON:
```json
{
  "name": "John Doe",
  "age": 30,
  "isStudent": false,
  "courses": ["Math", "Science", "History"],
  "address": {
    "street": "123 Main St",
    "city": "Anytown",
    "state": "CA"
  }
}
```

### Common Uses of JSON:
- **API responses**: JSON is widely used to format data returned by web APIs.
- **Configuration files**: Many applications use JSON to store configuration settings.
- **Data storage**: JSON can be used to store data in databases, especially NoSQL databases like MongoDB.
## How do we utilize JSON within Crestron rooms?
We use JSON primarily as a configuration file, which can change elements of the UI, or even the system, without the need for constant recompiles.

While this offers us *some* flexibility, system design should remain consistent if you're planning to deploy to multiple rooms. Otherwise I'd recommend splitting rooms into 'Types'.

Ultimately the config file is a way to pass data from a file to the processor, **how that data is handled is defined by the programmer.** So for example if you were to add another display to the display array, but the programmer only supported n displays **you would need to recompile.**

Some settings you'll typically find in *most* of our config files:
* Site/Room Name
* Startup/Shutdown presets
* Audio Min/Max ranges
* Matrix Assignment
* Source Definitions/Assignments
* Destinations Definitions/Assignments
* Touch Panel Visibilities (Sources, Destinations, Faders)
* Fader Assignments
* Fader Min/Max
* Routing Rules
* Display Definitions


# LMU Config File

## Room 
```json
{
    "Room": {
        "Site": "LMU",
        "RoomName": "WHH 118",
        "HelpNumber": "x87777 option 1",
        "UseExternalDsp": true,
        "DisplayAutoOn": true,
        "Startup":{
            "PresetRoute":0,
            "DspPreset":0,
            "ProgramVolumeLevel":70,
            "MicVolumeLevel":70,
            "VtcVolumeLevel":70
        },
        "Shutdown":{
            "PresetRoute":1,
            "DspPreset":1,
            "ProgramVolumeLevel":70,
            "MicVolumeLevel":70,
            "VtcVolumeLevel":70
        },
        "Audio":
        {
            "ProgramVolume":{
                "DMAddress":1,
                "DSPFader":0
            },
            "MicVolume":{
                "DMAddress":-1,
                "DSPFader":-1
            },
            "AtcVolume":{
                "DMAddress":-1,
                "DSPFader":-1
            },
            "VtcVolume":{
                "DMAddress":-1,
                "DSPFader":-1
            },
            "PrivacyMute":{
                "DMAddress":-1,
                "DSPFader":-1
            }
        }
    }
}
```

### Site
Data type: String
Defines site name, as of today I don't believe this is displayed on the UI anywhere, leave alone.

### RoomName
Data type: String
Defines room name, this is shown on the top left within the header.

### HelpNumber
Data type: String
Defines help number shown when pressing the help button.

### UseExternalDsp
Data type: Boolean
If true will attempt to connect to IP defined within [DSP]

### DisplayAutoOn
Data type: Boolean
If true, will pulse the displays to turn on when 'Start' is pressed from the logo, this might not be fully defined within programming because displays grow/shrink. Don't rely on this.

### Startup / Shutdown
#### Preset Route
Data type: Integer
Valid range: 0-31
Will recall an index of [PresetRoutes](#presetroutes)

#### DspPreset
Data type: Integer
Valid range: 0-31
Sends defined value on startup / shutdown, I don't know if this fully works.

#### xVolumeLevel
Data type: Integer
Valid range: 0-100
Will send the value as a **PERCENTAGE** to said volume fader on startup / shutdown.

### Audio
#### xVolume
Program Volume is the right column on the UI shown 99% of the time.
Mic Volume isn't really used, not sure where it is on the UI.
ATC Volume isn't really used, probably within ATC subpages.
VTC Volume isn't really used, probably within VTC subpages.
Privacy is the privacy button underneath Program Volume.
##### DMAddress
Data type: Integer
Valid range: -1-31
Sets xVolume to a control point on the DMPS/DM. See [FaderMapping](#fadermapping)

##### DSPFader
Data type: Integer
Valid range: -1-31
Sets xVolume to a fader on the DSP. See [DSP.Faders[]]()


## DMPS
```json
{
    "DMPS":{
        "Note":[
            "DigitalOutputAudioSource:",
            "0 = no route",
            "1 = Digital Mixer 1",
            "2 = Digital Mixer 2",
            "3 = Audio Follows Video",
            "__Range",
            "-500 to 100 (-80db to +10db)"
        ],
        "DigitalOutputAudioSource":[3,3,3,3],
        "MasterRange": {"Min":-500, "Max":0 },
        "SourceRange": {"Min":-500, "Max":0 },
        "MicMasterRange": {"Min":-500, "Max":0 },
        "Mic1Range": {"Min":-500, "Max":0 },
        "Mic2Range": {"Min":-500, "Max":0 },
        "Mic3Range": {"Min":-500, "Max":0 },
        "Mic4Range": {"Min":-500, "Max":0 },
        "Mic5Range": {"Min":-500, "Max":0 },
        "Mic6Range": {"Min":-500, "Max":0 },
        "FaderMapping":[
            -1,-1,-1,-1,
            -1,-1,-1,-1,
            -1,-1,-1,-1,
            -1,-1,-1,-1
        ],
        "Presets":{
            "Startup":{
                "Program":{
                    "Master":    { "Level": 0, "Mute":0 },
                    "MicMaster": { "Level": -500, "Mute":0 },
                    "Source":    { "Level": 0, "Mute":0 },
                    "Mic1":      { "Level": -500, "Mute":0 },
                    "Mic2":      { "Level": -500, "Mute":0 },
                    "Mic3":      { "Level": -500, "Mute":0 },
                    "Mic4":      { "Level": -500, "Mute":0 },
                    "Mic5":      { "Level": -500, "Mute":0 },
                    "Mic6":      { "Level": -500, "Mute":0 }
                },
                "Aux1":{
                    "Master":    { "Level": -500, "Mute":0 },
                    "MicMaster": { "Level": -500, "Mute":0 },
                    "Source":    { "Level": -500, "Mute":0 },
                    "Mic1":      { "Level": -500, "Mute":0 },
                    "Mic2":      { "Level": -500, "Mute":0 },
                    "Mic3":      { "Level": -500, "Mute":0 },
                    "Mic4":      { "Level": -500, "Mute":0 },
                    "Mic5":      { "Level": -500, "Mute":0 },
                    "Mic6":      { "Level": -500, "Mute":0 }
                },
                "Aux2":{
                    "Master":    { "Level": -500, "Mute":0 },
                    "MicMaster": { "Level": -500, "Mute":0 },
                    "Source":    { "Level": -500, "Mute":0 },
                    "Mic1":      { "Level": -500, "Mute":0 },
                    "Mic2":      { "Level": -500, "Mute":0 },
                    "Mic3":      { "Level": -500, "Mute":0 },
                    "Mic4":      { "Level": -500, "Mute":0 },
                    "Mic5":      { "Level": -500, "Mute":0 },
                    "Mic6":      { "Level": -500, "Mute":0 }
                },
                "DigitalMix1":{
                    "Master":    { "Level": -500, "Mute":0 },
                    "MicMaster": { "Level": -500, "Mute":0 },
                    "Source":    { "Level": -500, "Mute":0 },
                    "Mic1":      { "Level": -500, "Mute":0 },
                    "Mic2":      { "Level": -500, "Mute":0 },
                    "Mic3":      { "Level": -500, "Mute":0 },
                    "Mic4":      { "Level": -500, "Mute":0 },
                    "Mic5":      { "Level": -500, "Mute":0 },
                    "Mic6":      { "Level": -500, "Mute":0 }
                },
                "DigitalMix2":{
                    "Master":    { "Level": -500, "Mute":0 },
                    "MicMaster": { "Level": -500, "Mute":0 },
                    "Source":    { "Level": -500, "Mute":0 },
                    "Mic1":      { "Level": -500, "Mute":0 },
                    "Mic2":      { "Level": -500, "Mute":0 },
                    "Mic3":      { "Level": -500, "Mute":0 },
                    "Mic4":      { "Level": -500, "Mute":0 },
                    "Mic5":      { "Level": -500, "Mute":0 },
                    "Mic6":      { "Level": -500, "Mute":0 }
                }
            },
            "Shutdown":{
                "Program":{
                    "Master":    { "Level": -500, "Mute":1 },
                    "MicMaster": { "Level": -500, "Mute":1 },
                    "Source":    { "Level": -500, "Mute":1 },
                    "Mic1":      { "Level": -500, "Mute":1 },
                    "Mic2":      { "Level": -500, "Mute":1 },
                    "Mic3":      { "Level": -500, "Mute":1 },
                    "Mic4":      { "Level": -500, "Mute":1 },
                    "Mic5":      { "Level": -500, "Mute":1 },
                    "Mic6":      { "Level": -500, "Mute":1 }
                },
                "Aux1":{
                    "Master":    { "Level": -500, "Mute":1 },
                    "MicMaster": { "Level": -500, "Mute":1 },
                    "Source":    { "Level": -500, "Mute":1 },
                    "Mic1":      { "Level": -500, "Mute":1 },
                    "Mic2":      { "Level": -500, "Mute":1 },
                    "Mic3":      { "Level": -500, "Mute":1 },
                    "Mic4":      { "Level": -500, "Mute":1 },
                    "Mic5":      { "Level": -500, "Mute":1 },
                    "Mic6":      { "Level": -500, "Mute":1 }
                },
                "Aux2":{
                    "Master":    { "Level": -500, "Mute":1 },
                    "MicMaster": { "Level": -500, "Mute":1 },
                    "Source":    { "Level": -500, "Mute":1 },
                    "Mic1":      { "Level": -500, "Mute":1 },
                    "Mic2":      { "Level": -500, "Mute":1 },
                    "Mic3":      { "Level": -500, "Mute":1 },
                    "Mic4":      { "Level": -500, "Mute":1 },
                    "Mic5":      { "Level": -500, "Mute":1 },
                    "Mic6":      { "Level": -500, "Mute":1 }
                },
                "DigitalMix1":{
                    "Master":    { "Level": -500, "Mute":1 },
                    "MicMaster": { "Level": -500, "Mute":1 },
                    "Source":    { "Level": -500, "Mute":1 },
                    "Mic1":      { "Level": -500, "Mute":1 },
                    "Mic2":      { "Level": -500, "Mute":1 },
                    "Mic3":      { "Level": -500, "Mute":1 },
                    "Mic4":      { "Level": -500, "Mute":1 },
                    "Mic5":      { "Level": -500, "Mute":1 },
                    "Mic6":      { "Level": -500, "Mute":1 }
                },
                "DigitalMix2":{
                    "Master":    { "Level": -500, "Mute":1 },
                    "MicMaster": { "Level": -500, "Mute":1 },
                    "Source":    { "Level": -500, "Mute":1 },
                    "Mic1":      { "Level": -500, "Mute":1 },
                    "Mic2":      { "Level": -500, "Mute":1 },
                    "Mic3":      { "Level": -500, "Mute":1 },
                    "Mic4":      { "Level": -500, "Mute":1 },
                    "Mic5":      { "Level": -500, "Mute":1 },
                    "Mic6":      { "Level": -500, "Mute":1 }
                }
            }
        }
    }
}
```

### DigitalOutputAudioSource
Data type: Integer[]
Valid range: 0-3
0 = No Route
1 = Digital Mixer 1
2 = Digital Mixer 2
3 = Audio Follows Video
Sets the DMPS Audio Outputs on program boot.

### xRange
Data type: Integers
Valid range -800-100
Sets the volume range if controlling one of these volume points.

### FaderMapping
Data type: Integer[]
Valid range: -1-72
```text
* 0 Program Master
* 1 Program Source
* 2 Program Mic Master
* 3 Program Mic 1
* 4 Program Mic 2
* 5 Program Mic 3
* 6 Program Mic 4
* 7 Program Mic 5
* 8 Program Mic 6

* 16 Aux1 Master
* 17 Aux1 Source
* 18 Aux1 Mic Master
* 19 Aux1 Mic 1
* 20 Aux1 Mic 2
* 21 Aux1 Mic 3
* 22 Aux1 Mic 4
* 23 Aux1 Mic 5
* 24 Aux1 Mic 6

* 32 Aux2 Master
* 33 Aux2 Source
* 34 Aux2 Mic Master
* 35 Aux2 Mic 1
* 36 Aux2 Mic 2
* 37 Aux2 Mic 3
* 38 Aux2 Mic 4
* 39 Aux2 Mic 5
* 40 Aux2 Mic 6

* 48 Digital Mix 1 Master
* 49 Digital Mix 1 Source
* 50 Digital Mix 1 Mic Master
* 51 Digital Mix 1 Mic 1
* 52 Digital Mix 1 Mic 2
* 53 Digital Mix 1 Mic 3
* 54 Digital Mix 1 Mic 4
* 55 Digital Mix 1 Mic 5
* 56 Digital Mix 1 Mic 6

* 64 Digital Mix 2 Master
* 65 Digital Mix 2 Source
* 66 Digital Mix 2 Mic Master
* 67 Digital Mix 2 Mic 1
* 68 Digital Mix 2 Mic 2
* 69 Digital Mix 2 Mic 3
* 70 Digital Mix 2 Mic 4
* 71 Digital Mix 2 Mic 5
* 72 Digital Mix 2 Mic 6
```
This ties a control of the audio list to the [fader list under DSP]()
The audio list is determined by the position in the array 0-15

### Presets
Data type: Integer
Valid range: -800-100
Sets the respective volume, to the level provided, and the mute provided to the DMPS.

## Matrices[]
```json
{
    "Matrices":[
        {
            "Id": 0, 
            "Label": "DM-Video",
            "IP":"",
            "Username":"",
            "Password":"",
            "Inputs":9,
            "Outputs":4,
            "InputLabels": [
                "1 HDMI","2 HDMI","3 HDMI", "4 HDMI",
                "5 HDMI","6 HDMI","7 DM","8 DM",
                "9 Air Media"
            ],
            "OutputLabels": [
                "1 HDMI","2 HDMI","3 DM","4 DM"
            ]
        },
        {
            "Id": 1, 
            "Label": "DM-Audio",
            "IP":"",
            "Username":"",
            "Password":"",
            "Inputs":14,
            "Outputs":5,
            "InputLabels": [
                "1 Analog 1",
                "2 Analog 2",
                "3 Analog 3",
                "4 Analog 4",
                "5 Analog 5",
                "6 HDMI 1",
                "7 HDMI 2",
                "8 HDMI 3",
                "9 HDMI 4",
                "10 HDMI 5",
                "11 HDMI 6",
                "12 DM 7",
                "13 DM 8",
                "14 AirMedia"
            ],
            "OutputLabels": [
                "Program",
                "Aux 1",
                "Aux 2",
                "Codec 1",
                "Codec 2",
                "Digital Mixer 1",
                "Digital Mixer 2"
            ]
        },
        {
            "Id": 2, 
            "Label": "DM-TX-7",
            "IP":"",
            "Username":"",
            "Password":"",
            "Inputs":2,
            "Outputs":1,
            "InputLabels":[
                "1 Laptop",
                "2 Doc Cam",
                "3 VGA"
            ],
            "OutputLabels": [
                "1 DM Out"
            ]
        }
    ]
}
```
### Object
#### ID
Data type: Integer
Friendly way to view order, don't think this affects static config.

#### Label
Data type: String
A way to describe the matrix. If using AVRouter, that name needs to match within that module.

#### IP/Username/Password
Data type: String
Not utilized in programming currently

#### Inputs
Data type: Integer
How many inputs are on the Matrix

#### Outputs
Data type: Integer
How many outputs are on the Matrix

#### InputLabels / OutputLabels
Data type: String[]
A friendly way to reference what is where, also to assign names TO the DMPS or DM

## Sources[]
```json
{
    "Sources": [
    {
        "ID": 0,
        "Label": "Room Computer",
        "Icon": "PC_Light",
        "Input": 3,
        "Matrix": 0,
        "ShowControls": "",
        "Message": "",
        "IrPort": "0",
        "DriverPath": ""
    },
    {
        "ID": 1,
        "Label": "Laptop",
        "Icon": "Laptop",
        "Input": 4,
        "Matrix": 0,
        "ShowControls": "",
        "Message": "",
        "IrPort": "0",
        "DriverPath": ""
    },
    {
        "ID": 2,
        "Label": "Apple TV",
        "Icon": "AppleTV_light",
        "Input": 5,
        "Matrix": 0,
        "ShowControls": "appletv",
        "Message": "",
        "IrPort": "0.1",
        "DriverPath": "",
        "DisableDestinations": [
            3
        ]
    },
    {
        "ID": 3,
        "Label": "Blu-ray",
        "Icon": "Blu-ray",
        "Input": 6,
        "Matrix": 0,
        "ShowControls": "bluray",
        "Message": "",
        "IrPort": "0.2",
        "DriverPath": "",
        "DisableDestinations": [
            3
        ]
    },
    {
        "ID": 4,
        "Label": "Presenter Camera",
        "Icon": "Camera",
        "Input": 2,
        "Matrix": 0,
        "ShowControls": "camerawithpreview",
        "Message": "",
        "IrPort": "",
        "DeviceIndex": 0
    },
    {
        "ID": 5,
        "Label": "Audience Camera",
        "Icon": "Camera",
        "Input": 1,
        "Matrix": 0,
        "ShowControls": "camerawithpreview",
        "Message": "",
        "IrPort": "",
        "DeviceIndex": 1
    }
  ]
}
```

### Object
#### ID
Data type: Integer
Valid range: 0-31
Friendly way to order the source list, useful when looking at [RoutingRules](#routingrules) or [PresetRoutes](#presetroutes)
#### Label
Data type: String
Friendly label, displayed on UI in source list.
#### Icon
Data type: String
Valid values:
```text
tbd, see VTPro in the interim
```
Changes source icon in source list.
#### Input
Data type: Integer
Valid range: 0 to Defined by the Matrix it's assigned to
What input this source exists on the Matrix, this **must** be in the bounds of the [Matrices[].Inputs](#matrices) it's assigned to. If 0 the source will clear.
#### Matrix
Data type: Integer
Valid range: 0 to max matrix count
Assigns source to [Matrices](#matrices)

#### ShowControls
Data type: String
Valid values:
```text
"" (Blank)
none
appletv
bluray
message
wireless
camerawithpreview
cameranopreview
cabletv
doccam
```
Ties source control to source button.
In no destination routing mode: selecting source will open control.
In multiple destination routing mode: control button will show below source.
#### Message
Data type: String
Defines the message text to show if [ShowControls](#showcontrols) is set to `message`
#### IrPort
Data type: String
Deprecated and done in programming, ignore.
#### DriverPath
Data type: String
Deprecated and done in programming, ignore.
#### DisableDestinations
Data type: Integer[]
Valid range: 0 to max destination count
When source is selected, it will disable the destinations within it. Useful for preventing VTC from routing to itself, among other things, or if you have multiple matrices and there's no valid path to certain destinations on the list.
#### DeviceIndex
Data type: Integer
Probably deprecated and done in programming, ignore.

## Destinations[]
```json
{
  "Destinations": [
    {
        "ID": 0,
        "Label": "Left Projector",
        "Icon": "Projector",
        "ShowVideoMute": false,
        "Output": 3,
        "Matrix": 0
    },
    {
        "ID": 1,
        "Label": "Right Projector",
        "Icon": "Projector",
        "ShowVideoMute": false,
        "Output": 4,
        "Matrix": 0
    },
    {
        "ID": 2,
        "Label": "Program Audio",
        "Icon": "Volume_light",
        "ShowVideoMute": false,
        "Output": 1,
        "Matrix": 1
    },
    {
        "ID": 3,
        "Label": "USB Capture",
        "Icon": "Camera",
        "ShowVideoMute": false,
        "Output": 1,
        "Matrix": 0
    }
  ]
}
```

### Object
#### ID
Data type: Integer
Valid range: 0-31
Friendly way to order the source list, useful when looking at [RoutingRules] or [PresetRoutes]
#### Label
Data type: String
Friendly label, displayed on UI in destination list.
#### #### Icon
Data type: String
Valid values:
```text
tbd, see VTPro in the interim
```
Changes source icon in source list.
#### ShowVideoMute
Data type: Boolean
Shows a individual video mute button under the destination button, **Not used, keep false.**
#### Output
Data type: Integer
Valid range: Defined by the Matrix it's assigned to
What output this source exists on the Matrix, this **must** be in the bounds of the [Matrices[].Outputs](#matrices) it's assigned to.
#### Matrix
Data type: Integer
Valid range: 0 to max matrix count
Assigns destination to [Matrices](#matrices)

## RoutingRules[]
```json
{
    "RoutingRules": [
        "Tie Source.0 Matrix.1.In.8",
        "Tie Source.1 Matrix.1.In.9",
        "Tie Source.2 Matrix.1.In.10",
        "Tie Source.3 Matrix.1.In.11",
        "Tie Source.4 Matrix.1.In.7",
        "Tie Source.5 Matrix.1.In.6",
        "Destination.2 Follow.0",
        "Destination.2 Follow.1"
    ]
}
```
Data type: String[]
Assume all are case sensitive. This isn't a list of all the rules, I don't have them all off hand would need to peek in code or look for examples, this is primarily what you'll ever use. 

**Uses Zero-based numbering (Numbers begin at 0)\***
\*Not for inputs/outputs
### Tie Source.x Matrix.y.In.z
Ties a source on the [[#Sources[]]] list to a [[#Matrices[]]]
Example: `Tie Source.3 Matrix.1.In.11` 
This ties Source 4 on the Source[] list (Bluray) to Matrix 2 on the Matricies[] list (DM-Audio) to Input 11 (HDMI 6).

### Tie Matrix.x.Out.y Matrix.z.In.a
Ties a [Matrices](#matrices) *OUTPUT* to a [Matrices](#matrices) *INPUT*
Example:
```text
(For the sake of the example, lets assume:
	Matrix 0 = DMPS Video
	Matrix 1 = DMPS Audio
	Matrix 2 = DM-TX)
	
"Tie Matrix.2.Out.1 Matrix.0.In.7",
"Tie Matrix.2.Out.1 Matrix.1.In.12",
```
The above would tie Matrix 3 (DM-TX) output 1 (DM Output) to Matrix 1 (DM-Video) on input 7 (DM) and on Matrix 2 (DM-Audio) on input 12 (DM) (Because the DMPS offsets audio)

When routing a source that exists on `Matrix.2` the AVRouter will now know that it needs to route input 7 on `Matrix.0` and/or input 12 on `Matrix.12`

### Destination.x Follow.y
Ties a destination to follow another destination
Example:
```json
{
    "Destinations": [
    {
        "ID": 0,
        "Label": "Left Projector",
        "Icon": "Projector",
        "ShowVideoMute": false,
        "Output": 3,
        "Matrix": 0
    },
    {
        "ID": 1,
        "Label": "Right Projector",
        "Icon": "Projector",
        "ShowVideoMute": false,
        "Output": 4,
        "Matrix": 0
    },
    {
        "ID": 2,
        "Label": "Program Audio",
        "Icon": "Volume_light",
        "ShowVideoMute": false,
        "Output": 1,
        "Matrix": 1
    }
  ],
    "RoutingRules": [
        "Destination.2 Follow.0",
        "Destination.2 Follow.1"
    ]
}
```

In the above `Destination.2 Follow.0` is setting Destination 3 (Program Audio) to follow Destination 1 (Left Projector) and 2 (Right Projector). Whenever one is routed it will route to Program Audio as well.

**I do not remember if follows can chain (like in addition if you had another destination following Program Audio)**

## PresetRoutes[]
```json
{
    "PresetRoutes":[
    { 
        "Id": 0, 
        "Label": "Startup",
        "Routes":[
            { "Source":0, "Destination":0, "AllDestinations": false},
            { "Source":0, "Destination":1, "AllDestinations": false},
            { "Source":0, "Destination":2, "AllDestinations": false},
            { "Source":4, "Destination":3, "AllDestinations": false}
        ]
    },
    { 
        "Id": 1, 
        "Label": "Shutdown",
        "Routes":[
            { "Source":-1, "Destination":1, "AllDestinations": true}
        ]
    }
  ]
}
```
### Object
#### ID
Data type: String
Friendly number descriptor.
#### Label
Data type: String
Friendly name/descriptor.
#### Routes[]
##### Object
###### Source
Data type: Integer
Index of a source in the [Sources](#sources) list.
###### Destination
Data type: Integer
Index of a destination in the [Destinations](#destinations) list.
###### AllDestinations
Data type: Boolean
If true will route to all destinations in [Destinations](#destinations) try not to have a true one of these if multiple routes needs to happen for obvious reasons.

## Displays[]
```json
{
    "Displays": [
    {
        "Id": 0,
        "Label": "Left Projector",
        "Icon": "Projector",
        "IsAProjector": true,
        "HasScreen": true,
        "note-driver":"this projector is controlled via roomview.",
        "DriverPath": "",
        "LampHoursVisible":false,
        "VideoMuteVisible":true
    },
    {
        "Id": 1,
        "Label": "Right Projector",
        "Icon": "Projector",
        "IsAProjector": true,
        "HasScreen": true,
        "note-driver":"this projector is controlled via roomview.",
        "DriverPath": "",
        "LampHoursVisible":false,
        "VideoMuteVisible":true
    }
  ]
}
```
### Object
#### ID
Data type: String
Friendly number descriptor.
#### Label
Data type: String
Friendly name descriptor. This gets shown on the UI within Display/Projector controls.
#### Icon
Data type: String
Changes the icon on the destination button.
#### IsAProjector
Data type: Boolean

Allows the below to be visible. (HasScreen, LampHoursVisible, VideoMuteVisible)
#### HasScreen
Data type: Boolean

If true, shows up/down relays for screen control in display/projector control.
#### DriverPath
Data type: String

Deprecated, used to use Crestron Certified Drivers but compile times were massive, just hard code displays/projectors.
#### LampHoursVisible
Data type: Boolean

If true, shows lamp hours in projector control.
#### VideoMuteVisible
Data type: Boolean

if true, shows video mute button in display/projector control. LMU typically wants this enabled whenever possible, even on displays, they also typically dislike if we mute on the Video Output leading into the display/projector, so please try to mute on the device itself.

## DSP
### IP
Data type: String

If [UseExternalDsp](#useexternaldsp) is enabled will use the IP when connecting to the DSP.

### Faders[]
These are visible on the Audio Controls popups
#### Object
##### ID
Data type: Integer

Friendly number descriptor. This doesn't really matter, the order is more important.
##### Label
Data type: String

Friendly name descriptor. This gets shown on the UI within audio controls.
##### HasLevel
Data type: Boolean

If true, shows the level slider.
##### HasMute
Data type: Boolean

If true, shows the mute button.
##### MuteType
Data type: Integer

Valid values:

0 = Speaker Mute Icon

1 = Microphone Mute Icon

Changes the icon of the mute button.
##### Level Control
Data type: String

Instance tag or Named Control of the level goes here.
##### Mute Control
Data type: String

Instance tag or Named Control of the mute goes here.
##### LevelIndex
Data type: Integer

Defines what index is the level is on in the block given.

For example if you had a level block with 5 inputs, and you needed to control volume slider 3 of that block, you would use index 3.
##### MuteIndex
Data type: Integer

Defines what index is the mute is on in the block given.

For example if you had a mute block with 5 inputs, and you needed to control mute 3 of that block, you would use index 3.

### Presets
I don't know exactly what these do, pretty sure it's deprecated, have it commented out in code. **Ignore.**

## Cameras[]
```json
{
    "Cameras":[
    {
        "Id":0,
        "Label":"Presenter Camera",
        "Location":"",
        "IP":"10.0.90.128",
        "PanSpeed": 20,
        "TiltSpeed": 20,
        "ZoomSpeed": 20,
        "PreviewType": "mjpeg",
        "PreviewSource":"rtsp://10.0.90.128/mediainput/h264/stream_3",
        "Username":"",
        "Password":"",
        "Preset": [
            "Preset 1",
            "Preset 2",
            "Preset 3",
            "Preset 4",
            "",
            ""
        ],
        "GroupTags":[]
    },
    {
        "Id":0,
        "Label":"Audience Camera",
        "Location":"",
        "IP":"10.0.90.127",
        "PanSpeed": 20,
        "TiltSpeed": 20,
        "ZoomSpeed": 20,
        "PreviewType": "mjpeg",
        "PreviewSource":"rtsp://10.0.90.127/mediainput/h264/stream_3",
        "Username":"",
        "Password":"",
        "Preset": [
            "Preset 1",
            "Preset 2",
            "Preset 3",
            "Preset 4",
            "",
            ""
        ],
        "GroupTags":[]
    }
  ]
}
```
### Object
#### ID
Data type: Integer

Friendly number descriptor. Like most other objects, order is more important.
#### Label
Data type: String

Friendly name descriptor. Will be shown on UI if more than one camera is selectable.
#### Location
Data type: String

Not sure what this is, I've never used it.
#### IP
Data type: String

If filled will attempt to connect to IP given.
#### xSpeed
Data type: Integer

Speeds of each respective motor function, range depends on the camera.
#### PreviewType
Data type: String

Valid values:
```text
image
mjpeg
h264
```
Will show one of the previews while hiding the rest on the camera page, typically we've used mjpeg in the past it's worked fine.
#### PreviewSource
Data type: String

Path of the stream, this should be from the camera itself.
#### Username
Data type: String

Username of the camera, not always needed.
#### Password
Data type: String

Password of the camera, not always needed.
#### Preset
Data type: String[]

Labels of the presets in order, will be shown on UI.
#### GroupTags
Not sure what this is, I've never used it.

## TouchPanels[]
```json
{
    "Touchpanels": [
    {
        "Id": 0,
        "Startup": {
            "Menu": -1,
            "Source": 0,
            "Camera": 0,
            "SourceGroup": -1,
            "AudioGroup": -1,
            "DestinationGroup": -1,
            "DisplayGroup": -1,
            "TechMenu": -1
        },
        "PageStyles": {
            "Volume": 1,
            "Routing": 2
        },
        "SourceVisibility": [
            true,true,true,true,
            true,true,true,true,
            true,true,true,true,
            true,true,true,true
        ],
        "DestinationVisibility": [
            true,true,true,false,
            true,true,true,true,
            true,true,true,true,
            true,true,true,true
        ],
        "FadersVisible": [
            false,true,true,true,
            true,true,true,true,
            true,true,true,true,
            true,true,true,true
        ],
        "CamerasVisible": [
            true,true,false
        ],
        "Menus": [
        {
            "Id": 0,
            "Label": " ",
            "Icon": "Camera_Dark",
            "Visible": false
        },
        {
            "Id": 1,
            "Label": " ",
            "Icon": "Mic_Dark",
            "Visible": true
        },
        {
            "Id": 2,
            "Label": " ",
            "Icon": "Projector_Dark",
            "Visible": true
        },
        {
            "Id": 3,
            "Label": " ",
            "Icon": "TV_Dark",
            "Visible": false
        },
        {
            "Id": 4,
            "Label": " ",
            "Icon": "Blank",
            "Visible": false
        },
        {
            "Id": 5,
            "Label": " ",
            "Icon": "Blank",
            "Visible": false
        },
        {
            "Id": 6,
            "Label": " ",
            "Icon": "Blank",
            "Visible": false
        },
        {
            "Id": 7,
            "Label": " ",
            "Icon": "Lights_Dark",
            "Visible": false
        },
        {
            "Id": 8,
            "Label": " ",
            "Icon": "Help_Dark",
            "Visible": true
        },
        {
            "Id": 9,
            "Label": " ",
            "Icon": "Power_Dark",
            "Visible": true
        }
      ]
    }
  ]
}
```
### Object
#### ID
Data type: Integer<br>

Friendly number descriptor.
#### Startup
I think this is deprecated, if not it 'selects' the indexes given on startup.
#### PageStyles
##### Volume
Data type: Integer

Deprecated, in other config files it would change the right bar pairing
```text
1 = program only
2 = program + privacy
3 = program + privacy + mute all mics
```
##### Routing
Data type: Integer
```text
1 = Single destination (No destination list)
2 = Multi destination
```

#### xVisibility
Data type: Boolean[]

If true will be shown on the respective list of [Sources](#sources) or [Destinations](#destinations) or [Faders](#faders) or [Cameras](#cameras)

Remember it's using Zero-Based numbering, so `DestinationVisibility[3]` is set to false, so that will hide 'USB Capture' which is 4th on the [Destinations](#destinations) list.

#### Menus[]
This is the menu list on the bottom left of the UI
##### Object
###### ID
Data type: Integer

Friendly number descriptor.
###### Label
Data type: String

Friendly name descriptor. No labels on these buttons on the UI, so does nothing.
###### Icon
Data type: String

Changes the icon of the button.
###### Visible
Data type: Boolean

Changes the visibility of the button.
