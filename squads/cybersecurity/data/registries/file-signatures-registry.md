# File Signatures (Magic Bytes) Registry

## Purpose

Reference for file type identification via magic bytes (file signatures). Covers common file types, polyglot file construction, malware disguise techniques, and forensic identification methods for digital forensics, malware analysis, and content-type validation.

## Common File Signatures

### Executables and Libraries

| File Type | Magic Bytes (Hex) | ASCII | Notes |
|-----------|-------------------|-------|-------|
| Windows PE (EXE/DLL) | `4D 5A` | MZ | DOS MZ header; PE header at offset in e_lfanew |
| ELF (Linux) | `7F 45 4C 46` | .ELF | Linux/Unix executables and shared objects |
| Mach-O (macOS) | `FE ED FA CE` | .... | 32-bit; `FE ED FA CF` for 64-bit |
| Java Class | `CA FE BA BE` | .... | Java bytecode |
| DEX (Android) | `64 65 78 0A` | dex. | Dalvik executable |
| WebAssembly | `00 61 73 6D` | .asm | Wasm binary |
| Windows Shortcut (LNK) | `4C 00 00 00` | L... | Often used in phishing |

### Archives and Compressed

| File Type | Magic Bytes (Hex) | ASCII | Notes |
|-----------|-------------------|-------|-------|
| ZIP | `50 4B 03 04` | PK.. | Also DOCX, XLSX, PPTX, APK, JAR |
| ZIP (empty) | `50 4B 05 06` | PK.. | Empty archive |
| RAR | `52 61 72 21 1A 07` | Rar!.. | RAR4: `00`; RAR5: `01` follows |
| 7-Zip | `37 7A BC AF 27 1C` | 7z... | |
| GZIP | `1F 8B` | .. | Often wraps TAR |
| BZIP2 | `42 5A 68` | BZh | |
| XZ | `FD 37 7A 58 5A 00` | .7zXZ. | |
| TAR | `75 73 74 61 72` (offset 257) | ustar | At offset 257 |
| CAB | `4D 53 43 46` | MSCF | Windows Cabinet |

### Documents

| File Type | Magic Bytes (Hex) | ASCII | Notes |
|-----------|-------------------|-------|-------|
| PDF | `25 50 44 46 2D` | %PDF- | Check for JavaScript, embedded objects |
| OLE2 (DOC/XLS/PPT) | `D0 CF 11 E0 A1 B1 1A E1` | .... | Old Office format; macro container |
| RTF | `7B 5C 72 74 66` | {\rtf | Can contain OLE objects |
| Office XML (DOCX etc) | `50 4B 03 04` | PK.. | ZIP with specific directory structure |

### Images

| File Type | Magic Bytes (Hex) | ASCII | Notes |
|-----------|-------------------|-------|-------|
| JPEG | `FF D8 FF` | ... | Trailer: `FF D9` |
| PNG | `89 50 4E 47 0D 0A 1A 0A` | .PNG.... | |
| GIF | `47 49 46 38` | GIF8 | `37 61` (87a) or `39 61` (89a) follows |
| BMP | `42 4D` | BM | |
| TIFF (LE) | `49 49 2A 00` | II*. | Little-endian |
| TIFF (BE) | `4D 4D 00 2A` | MM.* | Big-endian |
| WebP | `52 49 46 46 ?? ?? ?? ?? 57 45 42 50` | RIFF....WEBP | |
| SVG | `3C 73 76 67` or `3C 3F 78 6D 6C` | <svg or <?xml | XML-based; XSS risk |

### Multimedia

| File Type | Magic Bytes (Hex) | ASCII | Notes |
|-----------|-------------------|-------|-------|
| MP3 | `49 44 33` or `FF FB` | ID3 | ID3 tag or frame sync |
| MP4 | `66 74 79 70` (offset 4) | ftyp | At offset 4 |
| AVI | `52 49 46 46 ?? ?? ?? ?? 41 56 49 20` | RIFF....AVI | |
| MKV | `1A 45 DF A3` | .E.. | Matroska container |

### Forensic-Critical Signatures

| File Type | Magic Bytes (Hex) | Notes |
|-----------|-------------------|-------|
| SQLite | `53 51 4C 69 74 65 20 66 6F 72 6D 61 74 20 33 00` | Browser history, app databases |
| Windows Registry | `72 65 67 66` | Registry hive file |
| EVTX (Event Log) | `45 6C 66 46 69 6C 65 00` | Windows event log |
| Prefetch | `53 43 43 41` | Windows execution artifacts |
| LNK | `4C 00 00 00 01 14 02 00` | Shortcut files (evidence of access) |

## Polyglot Files

### Concept

A polyglot file is valid as multiple file types simultaneously. Attackers use polyglots to bypass content-type validation.

### Common Polyglot Combinations

| Polyglot | Technique | Attack Use |
|----------|-----------|-----------|
| JPEG + JavaScript | JS comment wrapping image data | Bypass CSP, XSS via image upload |
| PDF + JavaScript | JS in PDF stream object | XSS in PDF viewers |
| ZIP + JPEG | Append ZIP to valid JPEG | Bypass image-only upload filters |
| GIF + JavaScript | GIF header followed by JS | XSS via `GIF89a=1; alert(1)` |
| HTML + JPEG | HTML in JPEG comment field | MIME sniffing exploitation |

### Defense Against Polyglots

1. Validate magic bytes AND file structure (not just extension or Content-Type header)
2. Set `X-Content-Type-Options: nosniff` on all responses
3. Re-encode uploaded images (strips non-image data)
4. Serve user uploads from a separate domain (prevent same-origin exploitation)
5. Use content-disposition: attachment for downloads

## Malware Disguise Techniques

| Technique | Description | Detection |
|-----------|-------------|-----------|
| Extension masquerading | `invoice.pdf.exe` | Check actual magic bytes, not extension |
| Double extension | `report.docx.js` | Validate against magic bytes |
| Right-to-left override | `report[RLO]fdp.exe` appears as `report.exe.pdf` | Check for Unicode control characters |
| Steganography | Data hidden in image pixel data | Statistical analysis, file size anomaly |
| Archive nesting | ZIP in ZIP in ZIP (AV evasion) | Recursive extraction with depth limit |
| Encrypted archive | Password-protected ZIP/RAR | Cannot scan contents; block or sandox |

## Forensic Identification Commands

```bash
# Linux file identification
file suspicious_file
xxd suspicious_file | head -5
hexdump -C suspicious_file | head -5

# Extract strings
strings -a suspicious_file | head -50

# Check for embedded files
binwalk suspicious_file
foremost -i suspicious_file -o output_dir

# Validate specific format
pdfinfo suspicious.pdf
exiftool suspicious.jpg
olevba suspicious.doc
```

## Cross-References

- See `reference/tools/ghidra-reference.md` for binary analysis
- See `lib/utilities/encoding-decoding-utility.md` for encoding analysis
- See `lib/utilities/hash-comparison-utility.md` for file hash verification
- See `lib/patterns/input-validation-patterns.md` for upload validation
- See `data/research/emerging-threats/ai-powered-attacks.md` for AI-generated content
