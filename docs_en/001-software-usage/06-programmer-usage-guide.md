# Programmer Usage Guide
The software integrates openocd/probe-rs, supporting DAPLink, J-Link, and ST-Link programmers.
DAPLink can be used directly. J-Link and ST-Link require driver replacement using Zadig before use.


### J-Link/ST-Link Driver Replacement Method
0. Download [Zadig](https://zadig.akeo.ie/).
1. Open Zadig with `Administrator privileges`.
2. Click the menu Options -> List All Devices.
3. In the dropdown list, you will see several entries related to J-Link/ST-Link. Please identify carefully:

J-Link Notes:
> Select the device named J-Link (Interface 0)
> Confirm its USB ID: VID is usually 1366

ST-Link Notes:
> Select the device named ST-Link Debug (Interface 0)
> Confirm its USB ID: VID is usually 0483

4. In the driver selection box on the right, select WinUSB, then click Replace Driver.
5. Wait for the replacement to complete.

Now reopen the software, and you will see the corresponding device and be able to use it to flash chips/development boards.

### Restoring J-Link Driver
Once replaced with WinUSB, Segger's official software (such as J-Flash, J-Link Configurator) will not recognize the device. If you want to switch back to the official tools, you need to uninstall the device in Device Manager and check "Delete driver", then re-plug the device to use the original driver.

### Known Issues
Some newer STM32 models cannot be flashed properly, such as the STM32F407. This may also be related to the debugger's own firmware.
