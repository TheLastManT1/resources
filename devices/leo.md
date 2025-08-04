# HTC HD2 (leo)

## Installing Custom ROM

### Fixes
- Weather
- Stocks
- YouTube

### Instructions

WIP

## Patching Stock ROM

### What is patchable
- Weather
- Stocks

### Required tools
- Registry Editor (pick whichever is more convenient)
    - On device: [TRE](https://github.com/htc-remanila/resources/raw/refs/heads/main/files/TRE.zip)
    - Via ActiveSync: [CeRegEditor](https://github.com/htc-remanila/resources/raw/refs/heads/main/files/CeRegEdit.exe)

### Steps

- Navigate to the HKEY_CURRENT_USER\Software\HTC\Manila key
- Create the following strings:
    - StockData.ServerURLOverride = http://[]()***\<your server address and port\>***/getstocks?imei=TEST&apptype=finance&src=HTC01
    - Weather.ServerURLGeoCodeOverride = http://[]()***\<your server address and port\>***/getweather?ac=TR2cra9U&lat=%s&lon=%s
    - Weather.ServerURLOverride = http://[]()***\<your server address and port\>***/getstaticweather?locCode=%ls&ac=TR2cra9U&version=1&device=innovation
- Reboot and enjoy