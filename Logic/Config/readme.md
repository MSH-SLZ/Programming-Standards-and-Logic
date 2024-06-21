# About
The config file is a json file. You can learn more about JSON (here)[https://www.w3schools.com/js/js_json_intro.asp] It can be edited using any text editor such as notepad.
However it is highly recommended to use VSCode. Since the schema.json file is written such that it can assist in validating and filling in the values needed to successfully edit the config.json file.

# How it's used.
The crestron program only look for the file name of config.json. Thus you can name your file with a version or any other prefix.
It must end in config.json.
The crestron program are written such that it will read the config.json file at bootup.
It is read only once and only at boot up.
