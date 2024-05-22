# Crestron Systems
### Un-compiled Code
| extension | description |
| --------- | ----------- |
| .smw | Simpl Windows file for programming a control processor |
| _compiled.zip | a zip file. It contains all files necessary to upload and modify code to the control processor. IR, UMC, USP, and CLZs are included. It is created when a the control processor code is compiled |
| _archive.zip | a zip file. It is created when the programmer presses save. It contains IR, UMC, USP, and CLZ files. It contains all files to modify code. |
| .vtp | VT-ProE touch panel file |
| .vta | VT-ProE touch panel archive file. In addition to the vtp file, it also contains the theme file. |
| .umc | A Simpl Windows file. A umc file is a module file |
| .usp | Simpl+ module source code. |
|ir| IR driver file |
| .sln | a Visual Studio solution file that describes the C# project |
| .cs | a C# code file used to create clz module files |
| .json | a json (Java Script Object Notation) file. It is a text file. Used by programmers as data storage or configuration of a system. |
| .csv | a comma delimited text file. Used by programmers as data storage or configuration |

### Compiled Code
| extension | description | 
| --------- | ----------- | 
| lpz | 3 or 4 series compiled code. Use this to upload the program to a control processor. This is actually a zip file. It may contain the _archive.zip. Good for backup and re-upload |
| spz | 2 series compiled code. This is only good for backup and re-upload. Does not contain un-compiled source code |
| cpz | a 4 series Simpl# compiled code. This is only good for backup and re-upload. Does not contain un-compiled source code|
| vtz | touch panel code |
| c3p | an x-panel project |
| clz | a Simpl# module file. It is created and compiled using Microsoft's Visual Studio |

# AMX Systems

### Un-compiled Code
| extension | description |
| --------- | ----------- |
| axw | an exported AMX workspace. It is a zip file that contains all files described in the the apw. |
| apw | a Netlinx Studio workspace file. It describes what files are used and to which devices ir, tp4 or tp5 files are mapped to |
| axs | a main code or module code |
| axi | an include file of source code |
| src | a file usually extracted from the processor. This file usually contains the un-compiled source code. It is a zip file of the axs and axi files in a workspace | 
| tp4 | a touch panel file of the G4 series. Used by TPDesign4 application. Can be extracted from a touch panel |
| tp5 | a touch panel file of the G5 series. Used by TPDesign5 application. Can be extracted from a touch panel |
| irl | an ir file |
| irn | an ir file |

### Compiled Code
| extension | description | 
| --------- | ----------- | 
| tkn | a compiled file for the control processor |
| tko | a compiled file of module written in axs |
| jar | a compiled file of module written in java |


# Extron Systems
### Un-compiled Code
| extension | description | 
| --------- | ----------- | 
| gcpro |  a Global Configuration Professional file for control processors. Can be extracted from the processor. Contains the gdl touch panel file. |
| gcplus |  a Global Configuration Professional file for control processors. Can be extracted from the processor. Contains the gdl touch panel file. |
| gdl | a GUI Design file for touch panels |
| gc3 | a Global Configurator file for control processors. Can be extracted from the processor. Does not include the gui file. |
| gui | a GUI Configurator file for touch panels |