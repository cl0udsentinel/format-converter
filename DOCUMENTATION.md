# Format Converter Pro — Documentation

## Overview

Format Converter Pro is a **browser-based, fully local** data file conversion tool. All processing happens entirely in your browser — no data is uploaded to any server. Files are read via JavaScript File APIs, processed locally, and downloaded directly to your device.

---

## Table of Contents

1. [Quick Start](#quick-start)
2. [Features](#features)
3. [Step-by-Step Guide](#step-by-step-guide)
4. [Supported File Formats](#supported-file-formats)
5. [Feature Deep Dives](#feature-deep-dives)
6. [Keyboard Shortcuts](#keyboard-shortcuts)
7. [Troubleshooting](#troubleshooting)
8. [Technical Architecture](#technical-architecture)
9. [Privacy & Security](#privacy--security)

---

## Quick Start

1. Open `format-converter-pro.html` in any modern browser (Chrome, Firefox, Safari, Edge)
2. Click **"Start new conversion"** or select a **built-in template**
3. Upload a **target/sample file** with the desired output format
4. Upload your **input file(s)** to convert
5. Map columns, set transforms/filters, configure output settings
6. Validate, preview, and download

---

## Features

### Core Features
- **Rule-based column mapping** — Auto-map by similarity or manual selection
- **Format detection** — Automatically detects dates, numbers, text patterns from sample data
- **Multiple input files** — Batch process files with the same mapping
- **Profile saving** — Save conversion configurations for reuse

### Pro Features (v4+)
| # | Feature | Description |
|---|---------|-------------|
| 1 | **Data Validation** | Pre-conversion quality checks: duplicates, type mismatches, blank values, date ranges |
| 2 | **Transform Rules** | Find/replace (regex), substring, conditional logic, math operations, prefix/suffix |
| 3 | **Row Filtering** | Include/exclude rows based on column conditions |
| 4 | **Split Output** | Split large outputs by row count or column value |
| 5 | **Encoding Support** | Auto-detect and convert between UTF-8, Shift_JIS, EUC-JP, UTF-16 |
| 6 | **Undo/Redo** | 50-step history with Ctrl+Z / Ctrl+Y |
| 7 | **Template Library** | Built-in templates + import/export profiles |
| 8 | **Diff Preview** | Side-by-side comparison of original vs converted data |
| 9 | **Auto-Save Draft** | Automatic recovery of interrupted sessions |
| 10 | **Keyboard Shortcuts** | Full keyboard navigation support |

---

## Step-by-Step Guide

### Step 1: Start
Choose from:
- **🆕 Start new conversion** — Begin from scratch
- **📂 Import a profile backup** — Load previously exported profiles JSON
- **Built-in templates** — Salesforce Contact, QuickBooks Journal, Shopify Product
- **Saved profiles** — Previously saved conversions in this browser

### Step 2: Target Format
Upload a sample file representing your desired output format:
- Must include a **header row**
- Include **2+ data rows** for format detection
- Supported: CSV, TSV, TXT, JSON, XLSX, XLS

The app auto-detects:
- **Date formats** (YYYY-MM-DD, DD/MM/YYYY, Unix timestamps, etc.)
- **Number formats** (decimals, thousands separators, currency, negatives in parentheses)
- **Text patterns** (case, fixed length, padding)
- **Null representations** (N/A, NULL, blank, etc.)

### Step 3: Input File(s)
Upload one or more files to convert:
- Files are **batched** together
- Select **input encoding** (auto-detect or manual: UTF-8, Shift_JIS, EUC-JP, UTF-16)
- Preview first 10 rows

### Step 4: Column Mapping
For each target column, choose the source:
| Action | Description |
|--------|-------------|
| **Map to input column** | Link to a column from input file(s) |
| **Map from sample record** | Use a value from the target sample |
| **Skip this column** | Exclude from output |
| **Blank** | Output empty values |
| **Default value** | Use a fixed value for all rows |

Auto-mapping uses Levenshtein similarity (≥60% match threshold).

### Step 5: Transform & Filter

#### Transform Rules (applied per column, in order)
| Transform | Use Case |
|-----------|----------|
| **Find & Replace** | Clean data: "N/A" → "", regex replacements |
| **Substring** | Extract codes: "INV-2024-001" → "2024" (start:4, length:4) |
| **Conditional** | If status="A" then "Active" else "Inactive" |
| **Math** | Convert units: multiply by 1000, round, absolute value |
| **Prefix/Suffix** | Add currency symbols, IDs |

#### Filter Rules (applied per row)
| Operator | Example |
|----------|---------|
| equals | Status = "Active" |
| notEquals | Status ≠ "Deleted" |
| contains | Email contains "@company.com" |
| greaterThan | Amount > 1000 |
| regex | SKU matches /^[A-Z]{3}-\d{4}$/ |
| empty / notEmpty | Check for blank values |

**Logic**: All filter rules must pass (AND). Include rules require match; Exclude rules reject match.

### Step 6: Output Settings

#### Format Options
- **Output format**: CSV, TSV, TXT, JSON, Pipe-delimited
- **Separator**: Comma, Pipe, Tab, Semicolon
- **Header row**: Include/exclude
- **Output encoding**: UTF-8, Shift_JIS, EUC-JP, UTF-16

#### Formatting Overrides
- Trim whitespace
- Skip empty rows
- Quote text values
- Override date format (e.g., `DD/MM/YYYY`)
- Override decimal places
- Override text case (UPPER, lower, Title)
- Replace empty values with custom string

#### Value Recoding
Map specific input values to output values:
- "B" → "1" (Buy)
- "S" → "2" (Sell)
- "US" → "United States"

#### Split Output
- **By row count**: Max N rows per file (creates `output_1.csv`, `output_2.csv`, ...)
- **By column value**: Split by Region, Department, etc. (creates `output_North.csv`, `output_South.csv`, ...)

### Step 7: Validation
Runs automated quality checks:
- **Duplicate rows** based on key columns
- **Blank values** per column (with percentage)
- **Type mismatches** (text in number columns, invalid dates)
- **Date range issues** (outside 1900-2100)

Results shown as: 🔴 Error | 🟡 Warning | 🟢 Info

### Step 8: Preview
- **Standard view**: First 10 rows of converted output
- **Diff view** (toggle): Side-by-side original vs converted, with changed values highlighted

### Step 9: Download
- Download converted file(s)
- Profile automatically saved to browser storage
- Options: Convert another file with same profile, start new conversion, or view saved profiles

---

## Supported File Formats

### Input Formats
| Format | Extension | Notes |
|--------|-----------|-------|
| CSV | `.csv` | Comma-separated, with header |
| TSV | `.tsv` | Tab-separated |
| TXT | `.txt` | Delimited text |
| JSON | `.json` | Array of objects `[{"col":"val"}, ...]` |
| Excel | `.xlsx`, `.xls` | First sheet only |

### Output Formats
| Format | Extension | Encoding Support |
|--------|-----------|-----------------|
| CSV | `.csv` | ✅ All |
| TSV | `.tsv` | ✅ All |
| TXT | `.txt` | ✅ All |
| JSON | `.json` | UTF-8 only |
| Pipe-delimited | `.txt` | ✅ All |

### Encoding Support
| Encoding | Detection | Conversion |
|----------|-----------|------------|
| UTF-8 | ✅ | ✅ |
| Shift_JIS (Japanese) | ✅ | ✅ |
| EUC-JP | ✅ | ✅ |
| UTF-16 | ✅ | ✅ |

---

## Feature Deep Dives

### Fixed-Length Text Padding (Issue Fix)
When the target format has fixed-length text fields (e.g., "silver   " with 3 trailing spaces), the converter:
1. **Detects** the fixed length from sample data
2. **Pads** shorter values with trailing spaces to match target length
3. **Truncates** longer values (unless quote-text mode is enabled)

### Date Format Handling
The converter recognizes and converts between:
- `YYYY-MM-DD`, `DD/MM/YYYY`, `MM-DD-YYYY`
- `DD MMM YYYY` (e.g., "15 JAN 2024")
- Unix timestamps (seconds and milliseconds)
- Loose parsing for ambiguous formats

Custom formats use tokens: `YYYY`, `YY`, `MM`, `M`, `DD`, `D`, `HH`, `mm`, `ss`, `A` (AM/PM)

### Number Format Handling
Detects and preserves:
- Decimal places
- Thousands separators
- Currency symbols ($, €, £, ₹)
- Negative numbers in parentheses
- Zero-padding

---

## Keyboard Shortcuts

| Shortcut | Action |
|----------|--------|
| `Ctrl + Enter` | Next step |
| `Ctrl + Shift + Enter` | Run validation / confirm download |
| `Ctrl + Z` | Undo |
| `Ctrl + Y` | Redo |
| `Esc` | Go back |

---

## Troubleshooting

### Common Issues

**"No columns detected"**
→ Ensure the first row contains column headers, not data.

**"Type mismatch errors in validation"**
→ Check that mapped columns contain the expected data type. Use transform rules to clean data before conversion.

**"Special characters corrupted"**
→ Try manually selecting the input encoding (Step 3) instead of auto-detect.

**"Scroll jumps when selecting in Step 4"**
→ Fixed in v4+. If persists, try using keyboard (Tab/Arrow keys) instead of mouse.

**"Profile not showing after restart"**
→ Profiles are stored in browser localStorage. They persist per browser but don't sync across devices. Use Export/Import to transfer.

**"Draft recovery prompt keeps appearing"**
→ Click "Discard draft" or clear browser localStorage for this site.

### Browser Compatibility
- ✅ Chrome 80+
- ✅ Firefox 75+
- ✅ Safari 13.1+
- ✅ Edge 80+

Requires JavaScript enabled. No browser extensions needed.

---

## Technical Architecture

### Data Flow
```
User Files → FileReader API → PapaParse/XLSX → JavaScript Objects → 
Transform Pipeline → Validation → Formatting → Output Generator → 
Blob → Download
```

### Storage
| Data | Location | Persistence |
|------|----------|-------------|
| Saved profiles | `localStorage` | Until manually cleared |
| Draft recovery | `localStorage` | 7 days max |
| Undo history | Memory (RAM) | Lost on page reload |

### Libraries Used
- **SheetJS (xlsx)** — Excel file parsing
- **PapaParse** — CSV/TSV parsing
- **encoding-japanese** — Character encoding detection/conversion

### No Server Required
The entire application is a single HTML file (~94 KB) that runs client-side. No build step, no dependencies to install, no backend API.

---

## Privacy & Security

- **100% local processing** — Files never leave your browser
- **No external API calls** — Except CDN libraries (loaded once)
- **No tracking** — No analytics, cookies, or telemetry
- **Storage is local** — Data saved only in your browser's localStorage
- **Share carefully** — Exported profiles JSON may contain sample data snippets

---

## Version History

| Version | Date | Changes |
|---------|------|---------|
| v1 | — | Initial release |
| v2 | — | Bug fixes |
| v3 | — | Format detection improvements |
| v4 | — | Scroll fix, fixed-length padding |
| **v5 (Pro)** | 2026 | All 10 features: validation, transforms, filters, split output, encoding, undo/redo, templates, diff preview, auto-save, keyboard shortcuts |

---

## License

MIT License — Free for personal and commercial use.

---

*Generated for Format Converter Pro v5*
