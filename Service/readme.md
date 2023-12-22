# Service Information

## General Information
If you’re service ticket will require programming support or has a programming issue please retrieve the following. Otherwise you will have to make another site visit to gather this information. This is also the same process you would use to make a backup of the current control system.


## Onsite Data

### All Systems
1. IP address for all relevant devices (DSP, control system(s), touchscreen(s), etc.
2. Current firmware versions
3. Error logs if possible

### AMX Systems
1. Using Netlinx Studio refresh the online tree and save as CSV (Right Click on the Online Tree, select Online Tree Reporting)
2. Using Netlinx Studio retrieve the TKN and SRC from the processor
3. Using Netlinx Studio retrieve any other files such as JARs
4. Using FTP from windows explorer, FTP into the processor copy an IR files.
5. Using Netlinx Studio retrieve any Touch Panel connected to the system
6. Run Putty or Telnet, connect to the AMX processor using telnet. Run the command “program info”. Capture the resulting text to a notepad file. If using Putty, right click on the title bar, copy all to clipboard, open notepad and paste, save the notepad file. Do not use Netlinx Studio telnet window, as it does not capture everything if the text overflows.
### Crestron Systems
1. Currently loaded program (SPZ or LPZ)
2. System Info for the processor in question (not a screen shot, save as a text file)
3. System Info for the touch panel related to the processor in question. (not a screen shot, save as a text file)
4. Alternatively to the System Info, you can use the Information Gather Tool for each Crestron device. Info Gather tool can be found [here](https://www.crestron.com/Software-Firmware/Software/SW-INFOTOOL/3-5-2-821).

### Extron Systems
1. Extract the GCP programming. This applies to IPCP Pros
2. Extract the GC3 programming. This applies to many older GC products including MLCs.
3. Extract DSP configuration if present
