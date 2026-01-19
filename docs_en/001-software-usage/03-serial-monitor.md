# Serial Monitor User Guide

The Serial Monitor is a powerful serial communication debugging tool that supports data transmission/reception, real-time chart display, quick send, and many other features.

---

## Table of Contents

- [Basic Settings](#basic-settings)
  - [Port Selection](#port-selection)
  - [Baud Rate Settings](#baud-rate-settings)
  - [Advanced Serial Settings](#advanced-serial-settings)
  - [Connect/Disconnect Port](#connectdisconnect-port)
- [Data Display Area](#data-display-area)
  - [Display Mode Settings](#display-mode-settings)
  - [Search Function](#search-function)
  - [Data Export](#data-export)
  - [Clear Display](#clear-display)
  - [Line Chart Function](#line-chart-function)
- [Data Send Area](#data-send-area)
  - [Send Mode Settings](#send-mode-settings)
  - [Quick Send](#quick-send)
  - [Quick Send Editor](#quick-send-editor)
- [Shortcuts](#shortcuts)
- [FAQ](#faq)

---

## Basic Settings

### Port Selection

1. Click the **Port** dropdown box
2. Select the target serial device from the list
3. If the device is connected, it will display the device name (such as `COM3`, `/dev/ttyUSB0`, etc.)
4. The system will automatically identify and highlight the port matching the current development board

> **Tip**: If only one serial port is detected, the system will automatically select that port.

### Baud Rate Settings

1. Click the **Baud Rate** dropdown box
2. Select the appropriate baud rate

**Supported Baud Rates**:

| Common Baud Rates | High-Speed Baud Rates |
|-----------|-----------|
| 4800      | 460800    |
| 9600      | 921600    |
| 19200     | 1000000   |
| 38400     | 2000000   |
| 57600     | 3000000   |
| 115200    | 4000000   |
| 230400    |           |

> **Note**: The baud rate must match the target device's settings, otherwise garbled characters will appear.

### Advanced Serial Settings

Click the **gear icon** (⚙️) on the right side of the settings bar to expand the advanced settings panel:

| Parameter | Options | Default | Description |
|-----|--------|-------|------|
| **Data Bits** | 5, 6, 7, 8 | 8 | Number of data bits per character |
| **Stop Bits** | 1, 1.5, 2 | 1 | Stop bit length |
| **Parity** | None, Odd, Even, Mark, Space | None | Error detection method |
| **Flow Control** | None, RTS/CTS, XON/XOFF | None | Data flow control method |

> **Tip**: After modifying advanced settings, if the serial port is already connected, the system will automatically reconnect to apply the new settings.

### Connect/Disconnect Port

- Use the **switch button** on the right side of the settings bar to control the serial port connection
- **On**: Connect to the selected serial port
- **Off**: Disconnect the serial port

After successful connection, the window title will display the current serial port and baud rate information, for example: `Serial Monitor (COM3 - 115200)`

---

## Data Display Area

The data display area is located in the center of the interface and is used to display received and sent data.

### Data Type Identification

| Identifier | Description |
|-----|------|
| **RX** | Received data |
| **TX** | Sent data |
| **SYS** | System messages (such as connection status, signal settings, etc.) |

### Display Mode Settings

The right side of the data display area provides the following display control buttons:

| Icon | Function | Description |
|-----|------|------|
| **Hex** | Hexadecimal display | Display data in hexadecimal format (such as `FF A1 B2`) |
| ↵ | Auto wrap | Automatically wrap long data for display |
| ↓ | Auto scroll | Automatically scroll to the bottom when new data arrives |
| 🕐 | Show timestamp | Display receive/send time before each data entry |
| 👁 | Show control characters | Display control characters as visible symbols (such as `\r\n`, `\t`, etc.) |

### Search Function

1. Click the **magnifying glass icon** (🔍) to open the search box
2. Enter the keyword you want to search for
3. Matching content will be highlighted
4. Use the **Previous / Next** buttons to navigate between search results
5. The search box will display the current match position and total matches (such as `2/10`)

### Data Export

1. Click the **download icon** (⬇️) to export data
2. Select the save location and file name
3. Data will be saved in `.txt` format
4. The exported content will be formatted according to the current display settings (timestamp, Hex mode, control characters, etc.)

**Default file name format**: `log_YYYY_MM_DD_HH_mm_ss.txt`

### Clear Display

Click the **trash icon** (🗑️) to clear all display data.

> **Note**: Data cannot be recovered after clearing, please export important data before clearing.

### Line Chart Function

The serial monitor supports real-time data visualization:

1. Click the **line chart icon** (📈) to open the chart panel
2. The chart will automatically parse numeric data received

**Data Format Requirements**:
```
value1,value2,value3,...\r\n
```

- Each line of data ends with a newline character
- Multiple values are separated by commas
- Each value will be displayed as an independent line channel
- Supports up to 10 channels, colors will cycle if exceeded

**Chart Features**:
- Auto-scale time axis
- Real-time scrolling display
- Retain up to 1000 data points
- Support window size adjustment

---

## Data Send Area

The data send area is located at the bottom of the interface, and you can adjust the height by dragging the top edge.

### Send Mode Settings

The right side of the send area provides the following mode setting buttons:

| Icon | Function | Description |
|-----|------|------|
| **Hex** | Hex send mode | Send data in hexadecimal format (such as input `FF A1` will send bytes `0xFF 0xA1`) |
| ↵ | Enter to send | When enabled, press `Enter` key to send directly, when disabled need `Ctrl+Enter` to send |
| **R** | Add CR | Automatically add carriage return character `\r` when sending |
| **N** | Add LF | Automatically add line feed character `\n` when sending |

> **Tip**: Enabling both CR and LF will add `\r\n` at the end of the sent data, which is the most commonly used line terminator.

### Send Data

1. Enter the data to be sent in the input box
2. Select the send mode as needed
3. Click the **Send button** (✈️) or use the shortcut key to send

### Quick Send

The quick send bar is located at the top of the send area and displays preset quick send buttons:

**Default Quick Send Items**:

| Name | Type | Function |
|-----|------|------|
| **DTR** | Signal | Send DTR control signal |
| **RTS** | Signal | Send RTS control signal |
| **Send Text** | Text | Send preset text content |
| **Send Hex** | Hex | Send preset hexadecimal data |

Click the quick send button to immediately send the corresponding content.

### Quick Send Editor

1. Click the **Edit button** on the right side of the quick send bar to open the editor
2. Edit the quick send list in JSON format
3. Click **Save** to apply changes

**JSON Format Example**:
```json
[
  { "name": "DTR", "type": "signal", "data": "DTR" },
  { "name": "RTS", "type": "signal", "data": "RTS" },
  { "name": "Hello", "type": "text", "data": "Hello World!" },
  { "name": "0xFF", "type": "hex", "data": "FF FF 00 01 02" }
]
```

**Type Description**:

| type | Description |
|------|------|
| `signal` | Control signal (DTR or RTS) |
| `text` | Plain text, will add line terminator according to CR/LF settings |
| `hex` | Hexadecimal data, ignores CR/LF settings |

---

## Shortcuts

| Shortcut | Function | Condition |
|-------|------|------|
| `Enter` | Send data | "Enter to send" mode enabled |
| `Ctrl + Enter` | Send data | "Enter to send" mode disabled |

---

## FAQ

### Q: Serial port list is empty or device not found?

**A**: 
- Check if the device is properly connected
- Check if USB driver is installed
- Try re-plugging the device
- Some devices require dedicated drivers (such as CH340, CP2102, etc.)

### Q: Received data shows garbled characters?

**A**: 
- Check if baud rate settings match the device
- Check data bits, stop bits, parity settings
- Try using Hex mode to view raw data

### Q: Cannot send data?

**A**: 
- Confirm serial port is connected (switch is on)
- Check if device is working properly
- Check flow control settings

### Q: Line chart doesn't show data?

**A**: 
- Confirm the sent data format is correct (comma-separated values, ending with newline)
- Check if data contains valid numbers
- Make sure the chart panel is open

### Q: Configuration lost?

**A**: 
- Serial monitor automatically saves configuration (port, baud rate, advanced settings, etc.)
- Configuration is saved in the application's config file
- Configuration will be automatically restored after restarting the application

---

## Data Storage Description

The serial monitor uses an intelligent data grouping strategy:

- Continuously received data will be merged and stored, reducing the number of entries
- When the receive interval **exceeds 1 second**, a new data entry is created
- When a single data duration **exceeds 10 seconds**, a new data entry is created
- Sent data or system messages will immediately create independent entries

This design ensures data integrity while making it easy for users to view and analyze communication records.

---

## Version Information

- Supported operating systems: Windows, macOS, Linux
- Built on Electron and Angular
- Uses SerialPort library for serial communication
