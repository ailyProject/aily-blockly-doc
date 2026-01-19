# Library Specification

## Library Structure
aily blockly libraries basically follow the google blockly library structure (currently using blockly version 11), using npm package management form to manage library versions and related necessary information. An aily blockly library structure is as follows:
```
library-name  
 |- block.json             // aily blockly block file
 |- generator.js           // aily blockly generator file
 |- toolbox.json           // aily blockly toolbox file
 |- package.json           // npm package management file
 |- src.7z                 // Arduino library source file, please use 7z extreme compression and put it in the library
 |- readme.md              // Description file, if you use open source libraries, please explain
```

## block.json
aily blockly json extends the original blockly json. Here is an example of the servo lib (servo library), the servo library json is as follows:  
```json
[
    {
        "inputsInline": true,
        "message0": "舵机%1移动到%2",
        "type": "servo_write",
        "args0": [
            {
                "type": "field_variable",
                "name": "OBJECT",
                "variable": "servo1",
                "variableTypes": [
                    "Servo"
                ],
                "defaultType": "Servo"
            },
            {
                "type": "field_number",
                "name": "ANGLE",
                "value": 0
            }
        ],
        "previousStatement": null,
        "nextStatement": null,
        "colour": "#03a9f4"
    },
    {
        "inputsInline": true,
        "message0": "舵机%1连接到引脚%2",
        "type": "servo_attach",
        "args0": [
            {
                "type": "field_variable",
                "name": "OBJECT",
                "variable": "servo1",
                "variableTypes": [
                    "Servo"
                ],
                "defaultType": "Servo"
            },
            {
                "type": "field_dropdown",
                "name": "PIN1",
                "options": "${board.digitalPins}"
            }
        ],
        "previousStatement": null,
        "nextStatement": null,
        "colour": "#03a9f4"
    }
]
```

### block Configuration  
The `blocks array` in the json file is the specific block configuration, you can refer to [blockly official documentation](https://developers.google.com/blockly/guides/create-custom-blocks/define-blocks) to understand the related configuration.  
A single block example is as follows:  

```json
{
    "inputsInline": true,              // block style, true input items are displayed in one line, false in multiple lines
    "message0": "舵机%1连接到引脚%2",   // block information, defines the content displayed on this block
    "type": "servo_attach",           // block type, this parameter must be unique
    "previousStatement": null,         // previous connection, configure the block type before this block  
    "nextStatement": null,             // next connection, configure the block type after this block  
    "colour": "#03a9f4",               // block color
    "args0": [                         // input items
        {
            "type": "field_variable",
            "name": "OBJECT",
            "variable": "servo1",
            "variableTypes": [
                "Servo"
            ],
            "defaultType": "Servo"
        },
        {
            "type": "field_dropdown",
            "name": "PIN1",
            "options": "${board.digitalPins}"
        }
    ]
}
```



## generator.js 
generator.js is responsible for converting blocks to code, each block has a corresponding generator function. For Arduino libraries, the generator function writing form can refer to:
```javascript
Arduino.forBlock['servo_attach'] = function(block, generator) {
  // Implementation code refer to blockly official documentation
  return ''
};

Arduino.forBlock['servo_write'] = function(block, generator) {
  // Implementation code refer to blockly official documentation
  return ''
};

```

### Add Additional Code
In generator.js, the code corresponding to the block is returned using return. For most Arduinos, in addition to the block corresponding code, you also need to add additional code. For example, calling the servo library requires adding a library reference and creating a Servo object:
```c++
#include <Servo.h>
Servo myservo;
```
At this time, you can add the following statement in the corresponding function in generator.js to add library reference and new object statements in other parts of the program:
```javascript
Arduino.forBlock['servo_attach'] = function(block, generator) {
  generator.addLibrary('#include <Servo.h>','#include <Servo.h>');
  generator.addObject('Servo myservo','Servo myservo');
  // Implementation code refer to blockly official documentation
  return ''
};
```

Available functions are:
```javascript
addMacro(tag, code);
addLibrary(tag, code);
addVariable(tag, code);
addObject(tag, code);
addFunction(tag, code);
addSetupBegin(tag, code);
addSetup(tag, code); //System default, not recommended for library use
addSetupEnd(tag, code);
addLoopBegin(tag, code);
addLoop(tag, code); //System default, not recommended for library use
addLoopEnd(tag, code);
```
Where tag is a tag to avoid duplicate code addition, code is the actual inserted code.
Using these functions, you can add corresponding code to the following positions in the program:

```c++
// [macro definition macro] Use generator.addMacro to add code to this part
#defined PIN 3
// [library reference library] Use generator.addLibrary to add code to this part
#include <Servo.h>
// [variable variable] Use generator.addVariable to add code to this
static const int servoPin = 4;
// [object object] Use generator.addObject to add code to this part
Servo servo1;
// [function function] Use generator.addFunction to add code to this part

void setup() {
// [initialization setup Begin] Use generator.addSetupBegin to add code to this part
    servo1.attach(servoPin);
    
// [initialization setup] Use generator.addSetup to add code to this part (System default, not recommended for library use)
    Serial.begin(115200);

// [initialization setup End] Use generator.addSetupEnd to add code to this part

}

void loop() {
// [main program loop Begin] Use generator.addLoopBegin to add code to this part

// [main program loop] Use generator.addLoop to add code to this part (System default, not recommended for library use)
    for(int posDegrees = 0; posDegrees <= 180; posDegrees++) {
        servo1.write(posDegrees);
        Serial.println(posDegrees);
        delay(20);
    }

    for(int posDegrees = 180; posDegrees >= 0; posDegrees--) {
        servo1.write(posDegrees);
        Serial.println(posDegrees);
        delay(20);
    }

// [main program loop End] Use generator.addLoopEnd to add code to this part

}
```

### Precautions
If you need to create functions in generator.js, please do not create global functions, use the following method to define functions in Arduino, for example:
```js
Arduino.newFunction = function(value) {
  return 'ok';
};
```

## toolbox.json 
Toolbox is the block menu presented on the left side of the blockly interface, an example is as follows:
```json
{
    "kind": "category",
    "name": "Servo",
    "contents": [
        {
            "kind": "block",
            "type": "servo_attach"
        },
        {
            "kind": "block",
            "type": "servo_write"
        }
    ]
}
```

## package.json
Version control file, using npm package management, an example is as follows:
```json
{
    "name": "@aily-project/lib-servo",  // Library package name starts with @aily-project/lib-
    "nickname":"Servo Driver Library",             // Name displayed in the library manager
    "author": "aily Project",
    "description": "Servo control support library, supports Arduino UNO, MEGA, ESP8266, ESP32 and other development boards", // Brief introduction, no more than 50 words
    "version": "0.0.1",
    "compatibility": {                  // Compatibility description, supported cores and voltages
        "type": [                       // If [], it is a universal library, compatible with all development boards
            "arduino:avr:uno",
            "esp32:esp32:esp32",
            "esp32:esp32:esp32c3",
            "esp32:esp32:esp32s3",
            "arduino:renesas_uno:nanor4",
            "arduino:renesas_uno:nanor4"
        ],
        "voltage": [3.3,5]
    },
    "keywords": [                       // keywords can assist in searching libraries, it is recommended to add category names, function names, etc.
        "aily",
        "blockly",
        "servo",
        "servo_attach",
        "servo_write",
    ],
    "scripts": {},
    "dependencies": {},                // This library depends on other libraries
    "devDependencies": {}
}
```

### Package Name Naming Convention
Libraries are named in the form of @aily-project/lib-xxxx, such as @aily-project/lib-servo.
If the library is a general library for most development boards, I call it a core library, named in the form of @aily-project/lib-core-xxxx, such as @aily-project/lib-core-io.

## Optimization/Simplification Scheme
Without ambiguity, simplify the library call as much as possible, so that users can use the library normally with as few operations as possible, for example:
0. If there is an input variable in toolbox, you can use shadow block to fill; you can also provide some commonly used block combinations, combined into program segments, for users to use directly.
1. Some pin functions need to be initialized, such as calling `digitalWrite(5,HIGH)`, the corresponding initialization is `pinMode(5,OUTPUT)`. It is recommended that when the block library calls digitalWrite, digitalRead related blocks, it can automatically add the corresponding pinMode code to the program setup part.
2. Some libraries need to be initialized, such as the servo library, you need to use `myservo.attach(9)` to specify the pin connected to the servo, and then use `myservo.write(val)` to control the servo rotation angle. This library is recommended to provide a simplified block while retaining the original attach, write blocks, allowing users to directly specify the servo on a certain pin to rotate to how many degrees.
3. For IIC devices, if there is only one IIC address, the IIC address is not displayed in the block; if there are multiple IIC addresses, field_dropdown should be used to provide a menu for users to select the address, and the default address should be placed in the first position of the menu.
4. When the Arduino library function parameter is a callback function, such as `button.attachDoubleClick(doubleClick)` in the onebutton library, doubleClick is a callback function, then a block with the main body as the doubleClick function should be created, and in generator.js, add the code `button.attachDoubleClick(doubleClick)` to the setup part of the program, and add `button.tick()` to the loop part of the program.

## Extension Writing  
Blocks are allowed to use extensions, and the usage method follows the blockly definition:
```json
    {
        "type": "blinker_init_wifi",
        "message0": "初始化Blinker WiFi模式 %1",
        "args0": [
            {
                "type": "field_dropdown",
                "name": "MODE",
                "options": [
                    [
                        "手动配网",
                        "手动配网"
                    ],
                    [
                        "EspTouch V2",
                        "EspTouchV2"
                    ]
                ]
            }
        ],
        "extensions": ["blinker_init_wifi_extension"],
        "previousStatement": null,
        "nextStatement": null,
        "colour": "#03A9F4",
        "inputsInline": false
    },
```
Extensions can be directly defined in generator.js. Please add a check statement before registration to avoid duplicate loading of extensions, for example:  
```js
// Avoid duplicate loading
if (Blockly.Extensions.isRegistered('blinker_init_wifi_extension')) {
  Blockly.Extensions.unregister('blinker_init_wifi_extension');
}

Blockly.Extensions.register('blinker_init_wifi_extension', function() {
// Implementation code
})
```

## Get Current Development Board Configuration in Library  
### Get in block.json
In the block.json file, you can get the currently loaded `board.json` configuration through ${board.name}.
For example, in serial_begin block:
```json
{
"inputsInline": true,
"message0": "初始化串口%1 设置波特率为%2",
"type": "serial_begin",
"colour": "#48c2c4",
"args0": [
    {
    "type": "field_dropdown",
    "name": "SERIAL",
    "options": "${board.serialPort}"
    },
    {
    "type": "field_dropdown",
    "name": "SPEED",
    "options": "${board.serialSpeed}"
    }
],
"previousStatement": null,
"nextStatement": null
}
```
Through `${board.serialPort}`, `${board.serialSpeed}`, you can get the available serial ports and baud rate configurations of the development board. After the library is loaded, it will automatically be replaced with:
```json
{
    "inputsInline": true,
    "message0": "初始化串口%1 设置波特率为%2",
    "type": "serial_begin",
    "colour": "#48c2c4",
    "args0": [
        {
        "type": "field_dropdown",
        "name": "SERIAL",
        "options": [
            ["Serial","Serial"]
        ]
        },
        {
        "type": "field_dropdown",
        "name": "SPEED",
        "options": [
            ["1200","1200"],["9600","9600"],["14400","14400"],["19200","19200"],["38400","38400"],["57600","57600"],["115200","115200"]
        ]
        }
    ],
    "previousStatement": null,
    "nextStatement": null
}
```

### Get in generator.js
In the generator.js file, you can get the currently loaded `board.json` configuration through window['boardConfig'].
You can use the following method to determine the development board configuration, and then load different content
```js
// Determine the development board core
if (window['boardConfig'].core.indexOf('esp32') > -1) {
}
// Determine the development board name
if (window['boardConfig'].name.indexOf('ai-vox') > -1) {
}
```

## src.7z Packaging Specification
src.7z stores the corresponding library source code, the corresponding src directory path is as follows:  
```
src  
 |- library1
    |- library1.h
    |- library1.cpp   
 |- library2           
 |- library3           
```
One blockly library can have multiple source code libraries.  
When packaging, just right-click in the src directory > `Compress to 7z file`. If the library is large, please use 7z extreme compression.
