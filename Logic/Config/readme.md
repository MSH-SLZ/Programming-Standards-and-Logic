# About
The config file is a json file. You can learn more about JSON [here](https://www.w3schools.com/js/js_json_intro.asp). Json files can be edited using any text editor such as notepad.
However it is highly recommended to use VSCode. Since the schema.json file is written such that it can assist in validating and filling in the values needed to successfully edit the config.json file.

# How it's used.
The crestron program only look for the file name of config.json. Thus you can name your file with a version or any other prefix.
It must end in config.json.
The crestron program are written such that it will read the config.json file at bootup.
It is read only once and only at boot up.

# Editing the config.json file.
### Rooms
This section lists all the rooms. Typically there is only 1.
### Matrices
This section lists all the matrices of audio, video, or usb
### Sources
This section lists all the sources related to a matrix input
### Destinations
This section lists all destinations related to a matrix output
### RoutingRules
This section deals with how sources are routed to a destination when there are multiple matrices in the system.
### Displays
This section deals with displays.
### DSP
This section deals with audio DSP such as Biamp or Qsys. The fader section can also be used by the DMPS section to be referenced for control.
### Cameras
This section deals with controlled cameras
### Recorders
This section deals with recorders such as a hyperdeck.
### PresetRoutes
This section describes a preset route that will route a source to a destination.
Preset Routes are used by a room and touch panel menus
### Touchpanels
This section is related to touch panels
### DMPS
This section deals with the audio of the DMPS
