# SAPIENS_DATASET_BUILDER
Front-end web application for creating training datasets in the Sapiens standard.

# Sapiens Dataset Builder — Documentation

**[Sapiens Dataset Builder](https://github.com/sapiens-technology/SAPIENS_DATASET_BUILDER/blob/main/SAPIENS_DATASET_BUILDER.html?raw=true)** is a self-contained, client-side web application designed for creating, inspecting, curating, and exporting paired prompt-response datasets (Input/Output). It is engineered for AI practitioners, researchers, and developers preparing fine-tuning and alignment data for Large Language Models (LLMs).

---

<a href="https://github.com/sapiens-technology/SAPIENS_DATASET_BUILDER/blob/main/SAPIENS_DATASET_BUILDER.html?raw=true" download="SAPIENS_DATASET_BUILDER.html">
    Download SAPIENS Dataset Builder
</a>

---

## 📌 Table of Contents

1. [Overview & Architecture](#-overview--architecture)
2. [Key Features](#-key-features)
3. [User Interface Overview](#-user-interface-overview)
4. [Step-by-Step Usage Guide](#-step-by-step-usage-guide)
   - [Creating Records](#1-creating-records)
   - [Editing Records](#2-editing-records)
   - [Viewing and Deleting Records](#3-viewing-and-deleting-records)
   - [Real-Time Searching & Filtering](#4-real-time-searching--filtering)
   - [Importing JSON Files](#5-importing-json-files)
   - [Exporting Datasets](#6-exporting-datasets)
   - [Clearing the Entire Database](#7-clearing-the-entire-database)
5. [Supported Data Formats](#-supported-data-formats)
6. [Keyboard Shortcuts](#-keyboard-shortcuts)
7. [Storage & Persistence](#-storage--persistence)
8. [Security & Sanitization](#-security--sanitization)

---

## 🚀 Overview & Architecture

- **Zero External Dependencies:** Built with vanilla HTML5, modern CSS3, and ES6+ JavaScript. Operates entirely without external libraries, npm packages, or external CDNs.
- **Single-File Distribution:** The entire application (markup, presentation, and logic) is contained within a single `.html` file.
- **Client-Side Processing:** All operations occur locally in the user's browser runtime. No data is transmitted to external servers.
- **Cyberpunk Dark Theme:** Aesthetic styled with a pitch-black background (`#000000`), deep navy card surfaces (`#090a0f`), neon cyan primary accents (`#00f0ff`), and alert crimson highlights (`#ff2a5f`).

---

## ⚡ Key Features

- **Code-Grade Text Areas:** Dual editor inputs configured with `wrap="off"` and custom-styled horizontal and vertical scrollbars, making it easy to paste preformatted source code or multi-line system prompts.
- **Rapid Keyboard Workflow:** Create or update records instantly with the `Ctrl + Enter` (or `Cmd + Enter`) shortcut.
- **Compact Viewport Table:** A scrollable table container designed to display 4 rows simultaneously, maximizing editor real estate.
- **Smooth Animated Dialogs:** Uses the native HTML5 `<dialog>` API enhanced with scale-in, scale-out, and backdrop-blur keyframe transitions.
- **Real-Time Substring Filtering:** Searches across both input and output fields on keystroke, displaying relative match counters.
- **Structured JSON Import/Export:** Capable of reading and producing both raw arrays of objects and objects wrapped under a `"data"` key.
- **Timestamped File Naming:** Automatically names exports using the format: `sapiens_dataset_YYYY-MM-DD_HH-MI-SS.json`.

---

## 🖥 User Interface Overview

```text
┌──────────────────────────────────────────────────────────────────┐
│ SAPIENS DATASET BUILDER                          [ 0 SAMPLES ]   │
├──────────────────────────────────────────────────────────────────┤
│ [ Editor Card ]                                                  │
│   Input:  [ .................................................. ] │
│   Output: [ .................................................. ] │
│                                      [ Cancel ] [ Save Record ]  │
├──────────────────────────────────────────────────────────────────┤
│ [ Toolbar ]                                                      │
│   [ Load JSON ] [x] Wrap with "data" key  [ Download JSON ]      │
│   [ Filter input / output...                     ] [ Delete All ]│
├──────────────────────────────────────────────────────────────────┤
│ [ Records Table ]                                                │
│   # | Input               | Output              | Actions        │
│   1 | Sample prompt...    | Sample response...  | [V] [E] [D]    │
└──────────────────────────────────────────────────────────────────┘
```

---

## 📖 Step-by-Step Usage Guide

### 1. Creating Records
1. Enter your prompt or question sample into the **Input (Prompt / Question Sample)** textarea.
2. Enter the expected target response into the **Output (Expected Response)** textarea.
3. Click **Save Record** or press `Ctrl + Enter` (`Cmd + Enter` on macOS).
4. The record is appended to your local database and the table refreshes immediately.

### 2. Editing Records
1. Locate the record in the table and click the **Edit** button.
2. The record’s data will be loaded into the top editor textareas, the page will smoothly scroll to the top, and the save button will display **Update Record**.
3. Modify the content as needed and click **Update Record** (or press `Ctrl/Cmd + Enter`).
4. To discard modifications without saving, click **Cancel**.

### 3. Viewing and Deleting Records
- **Full View Modal:** Click **View** on any row to open the inspection dialog. This allows reading long, formatted prompt-response pairs with line breaks preserved (`white-space: pre-wrap`).
- **Single Record Deletion:** Click **Delete**. A confirmation modal will appear featuring a snippet preview of the selected record to prevent accidental data loss. Click **Delete Record** to confirm.

### 4. Real-Time Searching & Filtering
- Enter search terms into the **Filter input / output...** input field in the toolbar.
- The table will update on each keystroke to display only matching rows.
- The top-right badge will show the matching ratio (e.g., `3 / 15 SAMPLES`).

### 5. Importing JSON Files
1. Click the **Load JSON** button.
2. Select any standard `.json` file from your device.
3. The parser inspects the file schema (accepting raw arrays or `{ "data": [...] }` envelopes).
4. A confirmation dialog will report the number of valid records found.
5. Click **Confirm & Append** to add them to your existing database.

### 6. Exporting Datasets
1. Configure whether the output should be wrapped under a root `"data"` property using the **Wrap with `"data"` key** checkbox.
2. Click **Download JSON**.
3. The browser will download the formatted file named according to the generation timestamp:
   ```text
   sapiens_dataset_YYYY-MM-DD_HH-MI-SS.json
   ```

### 7. Clearing the Entire Database
1. Click the red **Delete All** button on the right side of the toolbar.
2. Review the confirmation dialog.
3. Click **Confirm & Clear** to wipe all stored entries from the application.

---

## 📦 Supported Data Formats

The app imports and exports using two standard dataset schemas:

### Schema 1: Direct Array (Flat)
*(Generated when **Wrap with `"data"` key** is unchecked)*

```json
[
  {
    "input": "Explain quantum entanglement in simple terms.",
    "output": "Quantum entanglement occurs when two particles become interconnected..."
  },
  {
    "input": "Write a Python function to compute the Fibonacci sequence.",
    "output": "def fibonacci(n):\n    a, b = 0, 1\n    for _ in range(n):\n        yield a\n        a, b = b, a + b"
  }
]
```

### Schema 2: Wrapped Object
*(Generated when **Wrap with `"data"` key** is checked)*

```json
{
  "data": [
    {
      "input": "Explain quantum entanglement in simple terms.",
      "output": "Quantum entanglement occurs when two particles become interconnected..."
    }
  ]
}
```

> **Import Note:** The import engine automatically detects both structures, validates that entries contain `input` and/or `output` fields, and converts missing fields into empty strings safely.

---

## ⌨️ Keyboard Shortcuts

| Shortcut | Scope | Action |
| :--- | :--- | :--- |
| `Ctrl + Enter` / `Cmd + Enter` | Global | Save new record or commit updates to the active record |
| `Esc` | Active Modal | Closes the open modal with a smooth exit animation |

---

## 💾 Storage & Persistence

- **Key:** Data is serialized into a JSON string and persisted using the browser's `localStorage` API under the key:
  ```javascript
  const STORAGE_KEY = 'SAPIENS_DATASET_STORE';
  ```
- **Capacity:** Standard browser storage quotas provide between **5 MB and 10 MB** of free storage per domain, accommodating thousands of prompt/response pairs.
- **Privacy Guarantee:** All parsing, filtering, and storage functions execute strictly within the browser sandbox; no telemetry or user data leaves your machine.

---

## 🛡 Security & Sanitization

To prevent **Cross-Site Scripting (XSS)** vulnerabilities when rendering user input, imported code samples, or raw Markdown syntax inside table cells, all text rendering is sanitized through an HTML entity escape routine:

```javascript
function escapeHTML(str) {
    return str
        .replace(/&/g, "&amp;")
        .replace(/</g, "&lt;")
        .replace(/>/g, "&gt;")
        .replace(/"/g, "&quot;")
        .replace(/'/g, "&#039;");
}
```

---

<div align="center">
  <sub>A SAPIENS TECHNOLOGY® PRODUCTION</sub>
</div>

## Contributing

We do not accept contributions that may result in changing the original code.

Make sure you are using the appropriate version.

## License

This is proprietary software and its alteration and/or distribution without the developer's authorization is not permitted.
