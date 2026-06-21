# Format Converter (Local)

A single-file, browser-based tool that converts data files from one format to another using rule-based logic detected from a sample file — no backend, no build step, no data leaving your machine.

🔒 **100% local processing.** All parsing, format detection, mapping, and conversion run client-side in the browser. The only network activity is loading two small libraries (SheetJS and PapaParse) from a CDN the first time the page opens — after that, everything works fully offline.

---

## Features

- **7-step guided wizard**: Start → Target Format → Input File → Column Mapping → Output Settings → Preview → Download
- **Automatic format detection** from a sample file: date formats, decimal/thousands separators, currency symbols, text case, fixed-width padding, and exact blank/null value representation (including literal whitespace)
- **Per-target-column mapping** with five choices per column:
  1. Map to an input column
  2. Map from sample record (pick a real value already in the target file)
  3. Skip this column
  4. Leave blank
  5. Fill with a default value
- **Value recoding table** — recode specific values per column (e.g. `B → 1`, `S → 2`), unlimited rules
- **Output customization** — format (CSV/TSV/TXT/JSON/Pipe-delimited), separator, header row, trim/quote/case/decimal overrides
- **Live preview & conversion summary** before downloading
- **Profile persistence** via `localStorage` — saved mapping/rules/settings survive a browser restart; export/import as JSON backup
- Supports CSV, TSV, TXT, JSON, XLSX, and XLS for both the sample/target file and input file(s)

## Limitations

- PDF input is not supported (export to CSV/Excel first)
- Only the first sheet of a multi-sheet Excel workbook is read
- Requires internet access on first load to fetch the SheetJS and PapaParse libraries from a CDN

## Tech Stack

- Vanilla HTML/CSS/JavaScript — no framework, no build tools
- [SheetJS (xlsx)](https://cdnjs.cloudflare.com/ajax/libs/xlsx/) for Excel parsing
- [PapaParse](https://cdnjs.cloudflare.com/ajax/libs/PapaParse/) for CSV/TSV/TXT parsing
- Browser `localStorage` for profile persistence

## Usage

1. Download/clone this repo
2. Open `format-converter-local.html` directly in any modern browser (double-click it, or open via File → Open)
3. Follow the 7-step wizard

No installation, no server, no dependencies to manage.

## File Structure

```
.
├── format-converter-local.html   # the entire app — open this file
└── README.md
```

## License

Add your preferred license here (e.g. MIT).
