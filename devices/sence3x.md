# HTC Sence 3.x Devices

## What is patchable
- Weather services

## What is the GOAL
- To make the system access your server

## How to
- Either hijack DNS or modify the request URL in the system

## What is the difference between these two methods?

### DNS override (authorized, network-level)
- Technical threshold: relatively higher — requires networking knowledge and control over DNS or DHCP settings.  
- Environment/equipment requirements: needs access to the network infrastructure (DNS server, DHCP, or local resolver).  
- Effect on devices: no modification to device firmware or OS; devices are unaffected at the system level.  
- Scalability: highly scalable — a single change applies to many devices at once, and new devices joining the network take effect immediately.  
- Use case: suitable for controlled lab, staging, or internal networks where you have explicit authorization.

### Modify request URL (device-level)
- Technical threshold: lower — can be implemented directly on the client or application level.  
- Environment/equipment requirements: minimal network infrastructure access required, but you must be able to modify each device’s configuration.  
- Effect on devices: involves changing each device’s settings (or its software); there is a risk of misconfiguration or damaging device software if done incorrectly.  
- Scalability: less scalable — each device needs to be updated individually.  
- Use case: suitable when you can safely update client configurations or for per-device customization in authorized environments.

---

> **Note:** Only perform DNS or endpoint modifications on networks and devices you own or have explicit permission to modify. Unauthorized tampering with DNS records, network traffic, or device configurations is illegal and unethical.

## Method one: Hijack DNS

### Who is this for
- Users with basic networking knowledge
- Network administrators or engineers who can modify DNS or endpoint settings in environments they control

### Requirement
- Device or system that could hijack DNS, such as OpenWRT router
- Backend server is listening 80 port

### Steps
- Find the DHCP/DNS setting, this usually can be find in network sub
- bind domain htc2.accu-weather.com with your server ip address
- Apply changes then enjoy it

## Method two: Modify the request URL in the system

> **Note:** This method has not been tested yet, but it should theoretically work.

### Who is this for
- Users with a device that has root access (required)  
- Familiarity with flashing ROMs, unbricking devices, and using ADB

### Required tools
- Device with root access (required)  
- Root-capable file manager on the device (e.g., Root Explorer, MiXplorer, MT Manager)  
- ADB environment on a host computer (recommended, optional)  
- Custom recovery with ADB shell support (e.g., TWRP) — optional but recommended

> **Note:** These operations can void warranties or render devices inoperable if done incorrectly. Only perform them on devices you own or have explicit permission to modify. Always back up important data before proceeding.

### Steps
- Find /system/framework/framework.odex file
- Make a backup such as cpoy it as /system/framework/framework.odex.bak
- Open /system/framework/framework.odex as text file
- Serach "htc2.accu-weather.com", then you should replace it with "<your server address>:<port>", but don't do it now
- Do remember the string you replace must has the same length with "htc2.accu-weather.com"(21 letters)
- Usually it would shorter then "htc2.accu-weather.com", you can add some path segment, such as "192.168.1.1:8080/abcd"
- Now you can replace
- Also update the backend route in `weather/weatherSence3x.py`:
  - Change:
    ```py
    @app.route("/widget/htc2/weather-data.asp", methods=["GET"])
    ```
  - To:
    ```py
    @app.route("/abcd/widget/htc2/weather-data.asp", methods=["GET"])
    ```

  This makes the service endpoint available at the new test path `/abcd/widget/htc2/weather-data.asp`.
- Then reboot

### Unbrick
- Only do this when your system brokedown, such as boot loop
- reboot device into recovery
- restore backup file in twrp or adb shell
