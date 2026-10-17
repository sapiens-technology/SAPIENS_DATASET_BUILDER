# SAPIENS_DATASET_BUILDER_MULTIMODAL
Front-end web application for creating training datasets in the Sapiens standard.

# Sapiens Dataset Builder – Multimodal

A lightweight, zero-dependency, single-page web application designed for structuring, curating, and exporting multimodal prompt-response datasets for LLM (Large Language Model) and VLM (Vision-Language Model) fine-tuning.

---

## Table of Contents

- [Overview](#overview)
- [Key Features](#key-features)
- [Data Structure & Schema](#data-structure--schema)
- [User Guide](#user-guide)
  - [1. Creating & Editing Records](#1-creating--editing-records)
  - [2. Multimodal / File Path Handling](#2-multimodal--file-path-handling)
  - [3. Searching & Filtering](#3-searching--filtering)
  - [4. Inspecting & Deleting Records](#4-inspecting--deleting-records)
  - [5. Exporting Data](#5-exporting-data)
  - [6. Importing Data](#6-importing-data)
- [Keyboard Shortcuts & Productivity](#keyboard-shortcuts--productivity)
- [Technical Architecture](#technical-architecture)
- [Deployment & Local Setup](#deployment--local-setup)
- [Credits](#credits)

---

## Overview

**[Sapiens Dataset Builder - Multimodal](SAPIENS_DATASET_BUILDER_MULTIMODAL.html)** operates entirely in the browser client using native Web APIs. It requires no backend server, database configuration, or build steps. All records are automatically persisted in browser `localStorage`, preventing data loss between sessions or page reloads.

The application features a dark-mode cyberpunk aesthetic (pure black background, neon cyan accents, glowing borders, and smooth CSS3 keyframe animations).

---

## Key Features

- **Prompt-Response Pair Management:** Dedicated editors for multiline inputs (`input`) and model target outputs (`output`).
- **Multimodal Path Support:** Assign local file paths (images, audio, documents) or remote URLs (`file_path`) to any record.
- **Clipboard & File System Helpers:** Quick paste from clipboard or select files via the native file browser.
- **Client-Side Persistence:** Real-time synchronization with browser `localStorage`.
- **Search & Live Filtering:** Search through inputs, outputs, and paths instantaneously.
- **Flexible JSON Export:** Export with or without a root `"data"` object wrapper. Output files are automatically timestamped.
- **Safe JSON Import:** Append records from existing `.json` datasets with structural validation and confirmation previews.
- **Modal Confirmations:** Native HTML5 `<dialog>` elements styled with custom scale and backdrop blur animations for views and deletion confirmations.

---

## Data Structure & Schema

Each entry represents a training pair. The `file_path` key is optional and is omitted from the JSON record if left empty.

### Individual Record Format

```json
{
  "input": "Describe the contents of the provided image.",
  "output": "The image displays a high-resolution satellite scan of an urban coastline.",
  "file_path": "/datasets/images/satellite_0042.png"
}
```

### Export Formats

#### 1. Wrapped (Default)
When **Wrap with `"data"` key** is checked:
```json
{
  "data": [
    {
      "input": "Translate the sentence to French.",
      "output": "Traduisez la phrase en français."
    },
    {
      "input": "Identify the vehicle in the frame.",
      "output": "Autonomous delivery drone.",
      "file_path": "https://assets.example.com/frames/frame_01.jpg"
    }
  ]
}
```

#### 2. Raw Array
When unchecked:
```json
[
  {
    "input": "Translate the sentence to French.",
    "output": "Traduisez la phrase en français."
  }
]
```

---

## User Guide

### 1. Creating & Editing Records
1. Enter your prompt or question in the **Input** textarea.
2. Enter the target model response in the **Output** textarea.
3. *(Optional)* Add a local path or web URL in the **File Path** field.
4. Click **Save Record** (or press `Ctrl + Enter` / `Cmd + Enter`).
5. To edit an existing record, click the **Edit** button in the table row. The editor will populate with the record's data, scroll to the top, and change the save button to **Update Record**.
6. Click **Cancel** at any time to clear the form and exit edit mode.

### 2. Multimodal / File Path Handling
The bottom bar of the editor provides three helper tools for setting media paths:
- **Paste URL:** Reads the current text from your OS clipboard directly into the path field (requires clipboard permissions).
- **Browse File:** Opens your operating system file picker.
  - *Browser runtime:* Resolves to the selected file's name or relative path due to browser security sandboxing.
  - *Desktop runtime (e.g., Electron):* Extracts the absolute native file system path (`file.path`).
- **Clear:** Empties the file path input field.

### 3. Searching & Filtering
Use the search bar above the table to filter records in real time. Matching evaluates:
- Prompt text (`input`)
- Response text (`output`)
- Media path/URL (`file_path`)

The header counter updates dynamically to display matching vs. total sample counts (e.g., `4 / 12 SAMPLES`).

### 4. Inspecting & Deleting Records
- **View:** Opens an animated modal displaying the un-truncated input, output, and associated file path.
- **Delete (Single):** Prompts a confirmation dialog displaying a preview snippet of the item before deletion.
- **Delete All:** Clears the entire dataset from both memory and `localStorage` after an explicit confirmation.

### 5. Exporting Data
1. Toggle the **Wrap with `"data"` key** checkbox based on your desired schema.
2. Click **Download JSON**.
3. A file named `sapiens_dataset_YYYY-MM-DD_HH-mm-ss.json` will be generated and downloaded by your browser.

### 6. Importing Data
1. Click **Load JSON**.
2. Select any `.json` file from your device.
3. The parser accepts:
   - A plain JSON array of objects: `[ {...}, {...} ]`
   - An object with a root `data` array: `{ "data": [ {...}, {...} ] }`
4. A modal will display the number of valid detected records.
5. Click **Confirm & Append** to merge them into your existing dataset.

---

## Keyboard Shortcuts & Productivity

| Shortcut | Scope | Action |
| :--- | :--- | :--- |
| `Ctrl + Enter` / `Cmd + Enter` | Global | Save or Update current record |
| `Esc` | Modal Open | Closes modal with exit animation |

---

## Technical Architecture

| Layer | Implementation Details |
| :--- | :--- |
| **Runtime Environment** | Pure Client-side (HTML5, Vanilla ES6+ JavaScript, CSS3) |
| **Storage Mechanism** | `window.localStorage` under key `SAPIENS_DATASET_STORE` |
| **UI Components** | Custom-styled HTML5 `<dialog>` elements with manual animation listeners |
| **Data Parsing** | Native `FileReader` and `JSON.parse` / `JSON.stringify` |
| **Styling** | CSS Variables, CSS Grid, Flexbox, Custom Scrollbars |
| **Dependencies** | None (0 external libraries, frameworks, or fonts) |

---

## Deployment & Local Setup

### Running Locally
No web server is required. You can run the application directly from the file system:

1. Save the code into an `index.html` file.
2. Double-click `index.html` or open it with any modern web browser (Chrome, Firefox, Safari, Edge, Brave).

### Serving via HTTP (Optional)
If running inside a local development environment:
```bash
# Using Python 3
python -m http.server 8000

# Using Node.js npx
npx serve .
```
Navigate to `http://localhost:8000` in your browser.

---

## Credits

Produced by **SAPIENS TECHNOLOGY®️**. All rights reserved.

---

<div align="center">
  <sub>A SAPIENS TECHNOLOGY® PRODUCTION</sub>
</div>

## Contributing

We do not accept contributions that may result in changing the original code.

Make sure you are using the appropriate version.

## License

This is proprietary software and its alteration and/or distribution without the developer's authorization is not permitted.
