# Board Adaptation Guide

[Board Repository](https://github.com/ailyProject/aily-blockly-boards)

## Development and Debugging

### Enable Developer Mode
Enable Developer Mode through `Menu > Settings > Developer Mode`. After that, a 🔁 icon will appear to the right of the `Library Manager` button at the lower-left corner of the Blockly workspace. This icon is used to manually reload the library after you modify its source code.

## Adaptation Based on Existing Boards
If your board is similar to an official Arduino board and uses avr, renesas, or esp32, you can find a similar configuration in the existing configs, copy it, and modify it on that basis.

### Arduino-Compatible Board Adaptation
The current version supports Arduino-compatible boards based on avr and renesas cores. Refer to the `arduino_uno` and `arduino_uno_r4` directories.

### esp32 Adaptation
This repository provides esp32-related templates. Determine your board's core model, then copy the corresponding folder, rename it to your board name, and update `package.json` and `board.json` accordingly.
`/template` is the initial project template. If your board includes some built-in libraries, you can add them to `/template/package.json` so they are automatically loaded when a user creates a new project.

### STM32 Adaptation
[Reference: STM32F103C8](https://github.com/ailyProject/aily-blockly-boards/tree/main/stm32f103c8)

### Raspberry Pi RP Series MCU Adaptation
[Reference: Raspberry Pi Pico 2 W](https://github.com/ailyProject/aily-blockly-boards/tree/main/raspberrypi_pico2_w)

### Custom Compile Parameter Adaptation
The board's compile parameters are configured through the `compilerParam` field in the template `board.json` file. If you have special compilation requirements, you can configure them in a similar way to the following examples, which use the same syntax as `arduino-cli`.
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

Available variables:

- `${serial}`
- `${baud}`
- `${file}`
- `${bootloader}`
- `${partitions}`
- `${boot_app0}`

String literal:

- `${"filename"}`

When `--use_1200bps_touch` and `--wait_for_upload` are required, wrap them in `[]` and place them at the beginning.

### Install a Library
You can place a library template or a library you created anywhere on your computer, such as `d:\arduino_test`.
Then open the project in aily blockly, open the terminal, and run:
```
npm i d:\arduino_test
```
This installs the board for the project.

### Reload the Library
Click the 🔁 icon to the right of `Project Management` to reload the project.

### Modify the Library
You can directly modify `node_modules\@aily-project\<board name>` in the project directory, then reload it in aily blockly for testing.
You can also modify the original board files under `d:\arduino_test`, then install the library again for testing.

## Adaptation Based on a New Chip
If you need to add a board for a chip that is not yet supported in the board repository, you may need to upload the corresponding compiler and tools. Since compilers and tools are usually binary executables, we cannot determine whether they are safe. Therefore, for adaptation to a completely new chip, please contact the official team and provide the source code and trusted sources of the relevant tools to avoid potential security issues.

## Submit a Library
You can first fork this project to your personal repository. Then place your newly created board configuration in it and submit a Pull Request.
Contact Naihe col to merge it, or wait for another project maintainer to merge it.
After the merge is completed, it will be published to npm, and all users will be able to use the board library you developed.
