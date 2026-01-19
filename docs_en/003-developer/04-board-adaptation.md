# Board Adaptation Guide  

## Development and Debugging Method  

### Enable Developer Mode
Through `Menu > Settings > Developer Mode`, enable developer mode. At this time, a 🔁 icon will appear to the right of the `Library Manager` button in the lower left corner of the blockly workspace, which is used to manually reload the library after modifying the library source code.

## Adapt Based on Existing Boards
If your board uses the same as Arduino official boards, using avr, renesas, or using esp32, you can find similar configuration files in existing configurations, copy and modify on this basis.  

### Arduino Compatible Board Adaptation  
The current version supports avr and renesas core Arduino compatible boards, refer to arduino_uno, arduino_uno_r4 directories  

### esp32 Adaptation
This repository has prepared three templates: esp32, esp32c3, esp32s3. Determine the core model of your board, then copy the corresponding folder, change it to your board name, and then modify the package.json and board.json files accordingly.
The `/template` is the project initial template project. If your board comes with some libraries, you can add them to `/template/package.json`, so that users will automatically load the corresponding libraries after creating a new project.  

### STM32 Adaptation  
To be written  

### Raspberry Pi RP Series MCU Adaptation  
To be written  

### Custom Compile Parameter Adaptation
The compile parameters of the board are configured in the `compilerParam` parameter in the template `board.json` file. If there are special compilation configuration requirements, you can use a similar method for configuration (the same usage as arduino-cli).
```
compile -b esp32:esp32:esp32c3 --build-property build.flash_mode=dio --build-property build.flash_freq=80m --build-property build.flash_size=4MB
compile -b arduino:avr:uno --build-property build.extra_flags=\"-DMY_DEFINE=\"hello world\"\""
compile -b arduino:avr:uno --build-property build.extra_flags=-DPIN=2 \"-DMY_DEFINE=\"hello world\"\"" /home/user/Arduino/MySketch` + "\n" +
compile -b arduino:avr:uno --build-property build.extra_flags=-DPIN=2 --build-property "compiler.cpp.extra_flags=\"-DSSID=\"hello world\"\"" /home/user/Arduino/MySketch` + "\n",
```

### Custom Upload Parameter Adaptation

```
avrdude -C${'avrdude.conf'} -v -V -patmega328p -carduino -P${serial} -b${baud} -D -Uflash:w:${file}:i;

esptool --chip esp32s3 --port ${serial} --baud ${baud} --before default_reset --after hard_reset write_flash -z --flash_mode keep --flash_freq keep --flash_size keep 0x0 ${bootloader} 0x8000 ${partitions} 0xe000 ${boot_app0} 0x10000 ${file}

bossac -d --port=${serial} -a -U -e -w ${file} -R
[--use_1200bps_touch, --wait_for_upload] bossac -d --port=${serial} -a -U -e -w ${file} -R

dfu-util --device 0x2341:0x0069,:0x0369 -D ${file} -a0 -Q
```

Replaceable variables:

- `${serial}`
- `${baud}`
- `${file}`
- `${bootloader}`
- `${partitions}`
- `${boot_app0}`

String constants:

- `${"filename"}`

When you need to use --use_1200bps_touch and --wait_for_upload: Wrap with "[]" and put at the front


### Install Library
You can first put the library template or your own created library in any location on the computer, such as `d:\arduino_test`.
Then open the project in aily blockly, open the terminal, and input:
```
npm i d:\arduino_test
```
You can install this board for this project.

### Reload Library
Click the 🔁 icon to the right of `Project Management` to reload the project.

### Modify Library
You can directly modify `node_modules\@aily-project\<board name>` in the project directory, and then reload in aily blockly to test;
You can also modify the original board files under `d:\arduino_test`, and then install the library again to test.

## Submit Library 
You can first fork this project to your personal repository. Then put your newly created board configuration in it, and then submit a Pull request.
Contact Naihe col to merge, or wait for other project administrators to merge.  
After the merge is complete, it will be pushed to the npm repository, and all users can use your developed library.
