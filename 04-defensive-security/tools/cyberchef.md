# CyberChef - Data Transformation Tool

## What is CyberChef?

**CyberChef** is a web-based tool for data manipulation, encoding, decoding, encryption, and analysis - often called the "Cyber Swiss Army Knife."

**Purpose**: Perform various "cyber" operations on data directly in browser.

**Operations Range:**
- Simple: Base64, URL encoding, ROT13
- Complex: AES encryption, RSA decryption, hash analysis

**Core Concept**: Operations execute in sequence as "recipes"

---

## CyberChef Workflow (4 Steps)

### 1. Define Objective
**Question**: "What do I want to accomplish?"

**Example**: "Found gibberish string during investigation - need to decode hidden message"

### 2. Input Data
**Action**: Paste or upload data into Input Area

**Example**: Enter the suspicious encoded string

### 3. Select Operations
**Action**: Choose appropriate operations (can be trial and error)

**Example Strategy:**
- Unknown encoding → Try common operations
- Research suggests encryption → Test ROT13, Base64, Base85, ROT47
- Iterate through encryption/encoding operations

### 4. Check Output
**Question**: "Did I achieve my objective?"

**Results:**
- ✅ Success → Decoded successfully
- ❌ Failure → Repeat with different operations

---

## CyberChef Interface (4 Areas)

### 1. Operations Area

**Purpose**: Repository of all available operations, organized by category.

**Features:**
- Search function for quick operation lookup
- Categories (Encryption, Encoding, Data format, etc.)
- Hover for operation description and examples

#### Common Operations

| Operation | Description | Example |
|-----------|-------------|---------|
| **From Morse Code** | Translates Morse to alphanumeric | `- .... .-. . .- - ...` → `THREATS` |
| **URL Encode** | Encodes special characters | `https://example.com` → `https%3A%2F%2Fexample%2Ecom` |
| **To Base64** | Encodes to ASCII Base64 | `This is fun!` → `VGhpcyBpcyBmdW4h` |
| **To Hex** | Converts to hexadecimal bytes | `This Hex conversion is awesome!` → `54 68 69 73 20 48 65 78...` |
| **To Decimal** | Converts to ordinal integer array | `This Decimal conversion is awesome!` → `84 104 105 115 32 68...` |
| **ROT13** | Caesar cipher rotation (default 13) | `Digital Forensics` → `Qvtvgny Sberafvpf` |

### 2. Recipe Area

**Purpose**: Heart of CyberChef - where operations are selected, arranged, and configured.

**Features:**
- **Save Recipe**: Store operation sequences for reuse
- **Load Recipe**: Recall saved recipes
- **Clear Recipe**: Remove all operations
- **BAKE! Button**: Execute recipe on input data
- **Auto Bake**: Automatically process without clicking BAKE!

**Workflow:**
1. Drag operations from Operations Area
2. Arrange in desired order
3. Configure arguments/options
4. Execute (BAKE!)

### 3. Input Area

**Purpose**: Space to input data for processing.

**Input Methods:**
- Paste text
- Type directly
- Drag and drop files

**Features:**
- **Add New Input Tab**: Work with multiple inputs simultaneously
- **Open Folder as Input**: Upload entire folder
- **Open File as Input**: Upload single file
- **Clear Input/Output**: Reset both areas
- **Reset Pane Layout**: Restore default window sizes

### 4. Output Area

**Purpose**: Display processed data results.

**Features:**
- **Save Output to File**: Export as .dat file
- **Copy Raw Output**: Copy to clipboard
- **Replace Input with Output**: Overwrite input with result (for chaining operations)
- **Maximize Output Pane**: Expand for better visibility

---

## Common Use Cases

### Encoding/Decoding
- Base64 encode/decode
- URL encode/decode
- Hex to ASCII
- Binary to text

### Cryptography
- Hash analysis (MD5, SHA-256)
- AES encryption/decryption
- RSA operations

### Data Formats
- JSON beautify/minify
- XML formatting
- CSV parsing

### Analysis
- Entropy calculation
- Character frequency
- Regular expressions

### Forensics
- Extract strings
- File carving
- Magic number identification

---

## Key Takeaways

- **CyberChef** = Swiss Army knife for data operations
- **4-step workflow**: Define objective → Input data → Select operations → Check output
- **Recipes** = sequences of operations (saveable and reusable)
- **Auto Bake** enables real-time processing
- **Trial and error** often needed for unknown encodings
- **Web-based** = no installation required
- **Chaining operations** = complex transformations possible