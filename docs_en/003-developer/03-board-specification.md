# Board Configuration Specification 


## Board Configuration Library Structure
aily blockly libraries basically follow the google blockly library structure, using npm package management form to manage library versions and related necessary information. An aily blockly library structure is as follows:
```
board_name  
 |- board.json             // Board configuration file
 |- board.webp             // Board image
 |- package.json           // npm package management file
 |- example                // Example program folder
    |- <Example program list>
 |- template               // Initial template folder
    |- package.json
    |- project.abi
```

## board-name.json
Here is an Arduino UNO as a reference:
```json
{
    "name": "Arduino UNO",
    "version":"1.0.0",
    "description": "Arduino UNO standard compatible board",
    "compilerTool": "aily-builder",  // Default compiler tool used
    "type": "arduino:avr:uno",  // Type in arduino
    "mode": ["arduino", "micropython"],  // Supported development frameworks
    "compilerParam": "compile -v -b arduino:avr:uno",  // Compile command
    "uploadParam": "upload -v -b arduino:avr:uno -p ${serial}",  // Upload command
    "analogPins": [
        ["A0","A0"],["A1","A1"],["A2","A2"],["A3","A3"],["A4","A4"],["A5","A5"]
    ],
    "digitalPins": [
        ["0","0"],["1","1"],["2","2"],["3","3"],["4","4"],["5","5"],["6","6"],["7","7"],["8","8"],["9","9"],["10","10"],["11","11"],["12","12"],["13","13"],["A0","A0"],["A1","A1"],["A2","A2"],["A3","A3"],["A4","A4"],["A5","A5"]
    ],
    "pwmPins": [
        ["3","3"],["5","5"],["6","6"],["9","9"],["10","10"],["11","11"]
    ],
    "serialPort": [
        ["Serial","Serial"]
    ],
    "serialSpeed": [
        ["1200","1200"],["9600","9600"],["14400","14400"],["19200","19200"],["38400","38400"],["57600","57600"],["115200","115200"]
    ],
    "spi": [
        ["SPI","SPI"]
    ],
    "spiPins": {
        "SPI": [
            ["MOSI",11],["MISO",12],["SCK",13]
        ]
    },
    "spiClockDivide": [
        ["2 (8MHz)","SPI_CLOCK_DIV2"],["4 (4MHz)","SPI_CLOCK_DIV4"],["8 (2MHz)","SPI_CLOCK_DIV8"],["16 (1MHz)","SPI_CLOCK_DIV16"],["32 (500KHz)","SPI_CLOCK_DIV32"],["64 (250KHz)","SPI_CLOCK_DIV64"],["128 (125KHz)","SPI_CLOCK_DIV128"]
    ],
    "i2c": [
        ["I2C","Wire"]
    ],
    "i2cPins": {
        "Wire": [
            ["SDA","A4"],["SCL","A5"]
        ]
    },
    "i2cSpeed": [
        ["100kHz","100000L"],["400kHz","400000L"]
    ],
    "builtinLed": [
        ["BUILTIN_LED","13"]
    ],
    "interruptPins": [
        ["2","2"],["3","3"]
    ],
    "interruptMode": [
        ["LOW","LOW"],["RISING","RISING"],["FALLING","FALLING"],["CHANGE","CHANGE"]
    ]
}
```

### Compile and Upload Configuration
```json
    "compilerTool": "aily-builder",  // Compiler tool used, currently arduino-cli, no need to change
    "core": "arduino:avr@1.8.5",    // Board core and corresponding version number
    "type": "arduino:avr:uno",      // Board type
    "compilerParam": "compile -v -b arduino:avr:uno",  //Compile parameters
    "uploadParam": "upload -v -b arduino:avr:uno -p ${serial}",  //Upload parameters, where ${serial} is the serial port variable, will be replaced with the serial port selected by the user in actual use
```

#### Available Configuration
 ${serial} is the device serial port selected by the user  
 ${mac} is the device selected by the user for wireless download, can be bluetooth, can be wifi  
 ${usb} is the device selected by the user for usb download  

#### arduino-cli Reference
The current configuration is referenced from arduino cli configuration, see [arduino-cli documentation](https://arduino.github.io/arduino-cli)  

Commands you may use:
```bash
arduino-cli core list // List installed cores
arduino-cli board search // List available boards
```

### Pin Configuration
```json
"digitalPins": [
    ["0","0"],["1","1"],["2","2"],["3","3"],["4","4"],["5","5"],["6","6"],["7","7"],["8","8"],["9","9"],["10","10"],["11","11"],["12","12"],["13","13"],["A0","A0"],["A1","A1"],["A2","A2"],["A3","A3"],["A4","A4"],["A5","A5"]
]
```
These configurations are used when the block is loaded. Add ${board.varName} in the corresponding position. The usage in the library file block.json is as follows:
```json
[
  {
    "inputsInline": true,
    "message0": "数字引脚%1",
    "type": "io_pin_digi",
    "colour": "#00C48C",
    "args0": [
      {
        "type": "field_dropdown",
        "name": "PIN",
        "options": "${board.digitalPins}"
      }
    ],
    "output": "Any"
  }
]
```
When the library is loaded, the corresponding `${board.digitalPins}` will be automatically replaced with the `digitalPins` configuration in `board.json`.  

## package.json
Basically follows the npm package management specification. Note that the `boardDependencies` item contains the dependencies that the board needs for compilation, upload and other actions. The reference dependencies for different cores are as follows:
```json
// AVR core, such as Arduino UNO\MEGA\LEONARDO and other boards
{
    "@aily-project/compiler-avr-gcc": "7.3.0",
    "@aily-project/tool-avrdude": "6.3.0",
    "@aily-project/sdk-avr": "1.8.6",
    "@aily-project/tool-ctags": "5.8.0"
}
```  
```json
// Renesas RA4M1 core, such as Arduino UNO R4 series
{
    "@aily-project/compiler-arm-none-eabi-gcc": "7.2.1",
    "@aily-project/tool-bossac": "1.9.1",
    "@aily-project/sdk-renesas_uno": "1.3.2",
    "@aily-project/tool-ctags": "5.8.0",
    "@aily-project/tool-dfu-util": "0.11.0"    
}
```
```json
// ESP32 core
{
    "@aily-project/compiler-esp-x32": "14.2.0",
    "@aily-project/tool-esptool_py": "5.1.0",
    "@aily-project/sdk-esp32": "3.3.1",
    "@aily-project/tool-idf_esp32": "5.5.0",
    "@aily-project/tool-ctags": "5.8.0"
}
```
```json
// ESP32C3 core
{
    "@aily-project/compiler-esp-rv32": "14.2.0",
    "@aily-project/tool-esptool_py": "5.1.0",
    "@aily-project/sdk-esp32": "3.3.1",
    "@aily-project/tool-idf_esp32c3": "5.5.0",
    "@aily-project/tool-ctags": "5.8.0"
}
```
```json
// ESP32S3 core
{
    "@aily-project/compiler-esp-x32": "14.2.0",
    "@aily-project/tool-esptool_py": "5.1.0",
    "@aily-project/sdk-esp32": "3.3.1",
    "@aily-project/tool-idf_esp32s3": "5.5.0",
    "@aily-project/tool-ctags": "5.8.0"
}
```
```json
// ESP32C6 core To be updated
```
```json
// ESP32H2 core To be updated
```
```json
// ESP32S2 core To be updated
```
```json
// ESP32P4 core To be updated
```
```json
// RP2040, such as Raspberry Pi Pico To be updated
```
```json
// RP2350, such as Raspberry Pi Pico2  To be updated
```
```json
// SAM3X, such as Arduino Due To be updated
```

## Initial Project Template (template)
In each board package, there is a `template` directory, which stores the template project loaded after creating a new project.
You can modify `template\package.json` to add default loaded libraries, such as [Grove Beginner Kit's package.json](grove_beginner_kit\template\package.json)
```json
{
  "name": "project_",
  "version": "1.0.0",
  "description": "",
  "dependencies": {
    "@aily-project/board-grove_beginner_kit": "^1.0.0",
    "@aily-project/lib-core-io": "1.0.0",
    "@aily-project/lib-core-logic": "0.0.1",
    "@aily-project/lib-core-loop": "0.0.1",
    "@aily-project/lib-core-math": "0.0.1",
    "@aily-project/lib-core-text": "0.0.1",
    "@aily-project/lib-core-serial": "0.0.1",
    "@aily-project/lib-core-time": "0.0.1",
    "@aily-project/lib-core-variables": "1.0.1",
    "@aily-project/lib-dht": "1.0.0",
    "@aily-project/lib-bmp280": "0.0.1",
    "@aily-project/lib-u8g2": "1.0.0",
    "@aily-project/lib-core-tone": "0.0.1",
    "@aily-project/lib-lis3dhtr": "0.0.1"
  }
}
```

`template\project.abi` is the corresponding blockly workspace file. The default project.abi is usually as follows:
```json
{
  "blocks": {
    "languageVersion": 0,
    "blocks": [
      {
        "type": "arduino_setup",
        "id": "arduino_setup_id0",
        "x": 30,
        "y": 30,
        "deletable": false 
      },
      {
        "type": "arduino_loop",
        "id": "arduino_loop_id0",
        "x": 30,
        "y": 290,
        "deletable": false 
      }
    ]
  }
}
```
You can also write a pre-edited project into it, and after users create a new project using this board, this program will be automatically loaded.
