# Component Editor User Documentation
`In Beta Testing`
The Component Editor is a visual tool for creating and editing custom electronic components. Through it, you can define the appearance, pin layout, functional blocks, and related properties of components, and export them as JSON configuration files for use in simulators.

## 1. Interface Overview

The editor interface is mainly divided into the following areas:

### 1.1 Top Toolbar (Header)
Located at the top of the interface, provides global settings and file operation functions:
*   **Snap**: Turn on/off grid snap function. When turned on, dragging elements will automatically align to the grid.
*   **Grid Size**: Set the pixel size of the grid (only valid when Snap is enabled).
*   **Zoom**: Control the zoom ratio of the canvas.
    *   `+` / `-`: Zoom in/out.
    *   `Reset`: Reset zoom ratio to 100%.
*   **Import**: Import existing component configuration file (`.json`).
*   **Export**: Export the currently edited component as a JSON configuration file.
*   **Preview**: Open the component previewer in a new window to view the actual rendering effect of the component in the simulator.

### 1.2 Left Toolbar (Left Sider)
Provides shortcut buttons for adding various elements:
*   **Add Image**: Add an image. Supports uploading local images, will automatically compress and convert to WebP format.
*   **Add Pin**: Add a pin.
*   **Add Function**: Add a function block for the currently selected pin.
*   **Add Text**: Add a text label.

### 1.3 Canvas Area (Canvas)
Located in the center of the interface, is the main working area for editing components.
*   Displays the component's Base Frame, images, pins, function blocks, and text.
*   Supports grid background display (when Snap is enabled).
*   Click and drag the blank space to move the canvas view.

### 1.4 Right Panel (Properties & Element List)
Contains two parts:
*   **Element List**: Displays the hierarchical structure of all elements contained in the current component.
    *   Can view, select, and delete elements.
    *   Can lock/unlock element positions.
    *   Supports dragging to adjust the order of pins and function blocks.
*   **Properties Editor**: Displays and edits the detailed properties of the currently selected element.

### 1.5 Bottom Panel (Bottom Sider)
*   **Legend**: Displays the currently defined function types and their colors.
*   **Editor**: Click the edit button to customize function types (Label, Value, Color, Text Color).

---

## 2. Basic Operations

### 2.1 Add Elements
*   **Image**: Click the "Add Image" button on the left, select a local image file. The image will be centered automatically.
*   **Pin**: Click the "Add Pin" button to add a new pin at the default position.
*   **Function Block**: After selecting a pin, click the "Add Function" button to add a function definition block for the pin.
*   **Text**: Click the "Add Text" button to add a text label.

### 2.2 Select and Move
*   **Select**: Click elements on the canvas or items in the right list to select. Click blank space on the canvas to select the entire component (Base Frame).
*   **Move**: After selecting an element, hold down the left mouse button and drag.
    *   If Snap is enabled, it will automatically snap to the grid when moving.
    *   The position of the function block (Function) is relative to its pin (Pin), moving the function block actually adjusts its label's relative offset.

### 2.3 Adjust Size
*   **Component Size**: Select the component (Base Frame), modify Width/Height in the properties panel, or directly drag the lower right corner of the component on the canvas (need to confirm whether drag adjustment is supported).
*   **Image**: Select the image, drag the adjustment handles around the image (usually the lower right corner), or accurately input the size in the properties panel.

### 2.4 Delete Elements
*   In the right **Element List** panel, find the element to delete, and click the **trash icon** on the right.

### 2.5 Lock/Unlock
*   In the **Element List** panel, click the **lock icon** on the right of the element.
*   Locked elements cannot be dragged, preventing accidental operations.

### 2.6 Sort
*   In the **Element List** panel, drag pin (Pin) or function block (Function) items to adjust their display order.

---

## 3. Shortcut Operations

| Key | Function | Description |
| :--- | :--- | :--- |
| **Arrow Keys** | Fine-tune position | After selecting an element, press `↑` `↓` `←` `→` to move 0.5px |
| **Shift + Arrow Keys** | Quick fine-tune | After selecting an element, hold `Shift` + arrow keys to move 5px |
| **Mouse Wheel** | Zoom canvas | Scroll up to zoom in, scroll down to zoom out (10% - 300%) |

---

## 4. Property Details

### Component
*   **Name**: Component name.
*   **Width/Height**: Component's basic size (cm or px).

### Pin
*   **ID**: Pin's unique identifier.
*   **Layout**: Function block arrangement direction (Horizontal/Vertical).
*   **Line Type**: Connection line style (Solid/Dashed).
*   **Line Algorithm**: Connection line path algorithm (Direct/Bezier/Orthogonal).

### Function (Function Block)
*   **Name**: Function block display name.
*   **Type**: Function type (such as Digital, Analog, VCC, GND, etc.), determines the display color.

### Text
*   **Content**: Text content.
*   **Font Size**: Font size.
*   **Color**: Font color.
