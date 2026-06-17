# OTA

## BLE OTA
The current version supports BLE OTA, limited to ESP32 chips with BLE support.
Usage:
1. For first-time use, install the "BLE OTA" library, add the "Start BLE OTA with one click" block to the project initialization section, then compile and flash this program.
2. In the device port selection menu at the top, click "Search BLE Devices". The software will search for devices that support BLE OTA, then you can select the target device.
3. Click the upload button to upload using BLE OTA.

> **Notes**
> 1. The new firmware updated through BLE OTA should also include BLE OTA functionality. Otherwise, subsequent BLE OTA updates will fail.  
> 2. For the ESP32 partition scheme, do not select a scheme without an OTA partition.  

> **Display Conditions for "Search BLE Devices"**  
> When the user selects an ESP32 development board and has installed the "BLE OTA" library, the "Search BLE Devices" option will appear in the device port selection menu at the top.


## WiFi OTA  
The current version supports WiFi OTA, limited to ESP32 chips with WiFi support.
Usage:
1. For first-time use, install the "WiFi OTA" library, add the WiFi connection code and the "Start WiFi OTA with one click" block to the project initialization section, then compile and flash this program.
2. In the device port selection menu at the top, click "Search WiFi Devices". The software will search for devices that support WiFi OTA, then you can select the target device.
3. Click the upload button to upload using WiFi OTA.

> **Notes**
> 0. The ESP32 must be on the same local network as the current computer, and device isolation must be disabled on the local network. The software discovers WiFi OTA devices through mDNS broadcasts.  
> 1. The new firmware updated through WiFi OTA should also include WiFi OTA functionality. Otherwise, subsequent WiFi OTA updates will fail.  
> 2. For the ESP32 partition scheme, do not select a scheme without an OTA partition.  

> **Display Conditions for "Search WiFi Devices"**  
> When the user selects an ESP32 development board and has installed the "WiFi OTA" library, the "Search WiFi Devices" option will appear in the device port selection menu at the top.
