# AI Function Usage Guide  

In the main interface, the toolbar is located at the upper right. Click the ![](../img/0102/ai-btn.webp) button to start the AI interaction function.  

## Mode Switching  

Click the mode switch button at the bottom of the AI interface to switch AI modes  
 ![](../img/0102/mode-btn.webp)  

In `Q&A Mode`, AI has read access to the project, can collect workspace information, and provide answers to user questions;
In `Agent Mode`, AI has read and write access to the project, can call preset tools and services to operate on the project, but will consume a large amount of tokens.

## Common Usage Methods

Switch to Agent mode to perform various functions such as project analysis, automatic programming, error fixing, library conversion, etc.

### Project Analysis
You can try entering your project requirements, which can be vague:
```
I want to develop an environmental data logger, help me design it.
```
Or specific requirements:
```
Use ESP32 combined with DHT22 to collect temperature and humidity data, and store it on a TF card. Collect data every 60 seconds, and record it in the file in the format of "system time + data", the format is "timestamp, temperature, humidity\n", such as: "123456,32,45\n"
```

### Automatic Programming
Directly describe the program you want, then wait for AI to write it for you
```
Help me write a serial port test program: use Arduino UNO R4 minima; 115200 baud rate communication; output a set of values every 500ms; 8 random values per set, values separated by commas, single value range within 0~255; each set ends with a newline; corresponding positions in each set should have continuity, not fluctuate too much.
```

### Error Fixing
When compilation or upload reports an error, click to view details, you can see the error content in the log, then double-click the error content to submit the error to the AI input box, send the error information, and AI will give processing suggestions or directly handle it for you.

### Library Conversion
If you have a library from arduino, micropython or other similar software that you want to use in this software, you can use AI to convert the library to this software's library, the prompt is as follows:
```
"C:\Users\coloz\Downloads\xxx-lib" is the arduino xxx library source code, please convert this library to an aily blockly library according to the specification
```
Then wait for the library conversion to complete and install it.

## AI Function Configuration  
Through the settings button in the upper right corner of the AI ASSISTANT interface, you can open the AI assistant settings page  
### Using External Models  
On the settings page, you can fill in your own LLM apikey to call more models. Theoretically supports all models with OpenAI interface style.
### Loop Count
Loop count is the maximum number of requests for a single agent operation, up to 100 times, usually no need to modify.
