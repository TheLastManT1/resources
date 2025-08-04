# HTC HD Mini (photon)

## Patching Stock ROM

### What is patchable
- Weather
- Stocks

### Required tools
- Registry Editor (pick whichever is more convenient)
    - On device: [TRE](https://archive.org/download/tucows_32381_Tascal_RegEdit/reg050m.zip)
    - Via ActiveSync: [CeRegEditor](https://archive.org/download/ce-reg-edit-setup-0.0.5.0/CeRegEdit_Setup_0.0.5.0.exe)

### Steps

- Navigate to the HKEY_CURRENT_USER\Software\HTC\Manila key
- Create the following strings:
    - StockData.ServerURLOverride = http://[]()***\<your server address and port\>***/getstocks?imei=TEST&apptype=finance&src=HTC01
    - Weather.ServerURLOverride = http://[]()***\<your server address and port\>***/getstaticweather?locCode=%ls&ac=TR2cra9U&version=1&device=innovation
- Reboot and enjoy