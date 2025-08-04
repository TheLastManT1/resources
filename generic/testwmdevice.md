# How to test whether your HTC device, running Windows Mobile, is supported

## 1. Test Weather and Stocks

This is by far the simplest test you could do. The reason is that the registry keys haven't changed at all since the earliest versions of the OS, and the patches can be applied by simply adding registry values.

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
- Reboot and test

## 2. Test YouTube

If your device has a YouTube client as an app, it will definetly work, because the APIs used are the same across all versions. However, what we don't know is whether its going to play the videos without transcoding.

### Required tools
- None

### Steps

- Download the [test video](https://github.com/htc-remanila/resources/raw/refs/heads/main/files/testvideo.mp4)
- Transfer and play it on your device from the File Explorer
- If you can both see and hear the video, your device is capable of h264 main profile, so the status is "Working"
- If you don't, the backend will need to transcode the video first, so the status is "Requires specific option in the backend"