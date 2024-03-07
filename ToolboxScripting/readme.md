# Sending a Program
```
[Variables]
lpz="C:\program.lpz"

[Load Onto Test]
Connect=auto 172.16.48.12;username admin;password password
Program01.ProgramSetSpecialLoadBehavior StartStopDependentPrograms , "false" , SendSigFile , "true", SendIpTable , "false"
Program01.ProgramSend |lpz|
```

# Sending a Touch Panel
```
[Variables]
tpFile="C:\tp.vtz"

[Load TPs]
Connect=auto 192.168.1.41;username admin;password admin
DisplayListSend |tpFile|
```

# Using Address Lists
```
[Variables]
tpFile="C:\tp.vtz"

[Load TPs]
Connect=addresslist:touchpanels
DisplayListSend |tpFile|

[AddressList:touchpanels]
auto 192.168.1.41;username admin;password admin
auto 192.168.1.41;username admin;password admin
```
# Sending a Config File
```
[Variables]
processorIP=auto 192.168.1.11;username admin;password admin
configFile="C:\config.json"

[Load Config]
//will put config.json into the user folder of the processor
Connect=|processorIP|
FileXferPutTo |config| "\user\"
```