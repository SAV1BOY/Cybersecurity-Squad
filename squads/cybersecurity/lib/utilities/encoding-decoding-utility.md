# Encoding and Decoding Reference

## Purpose

Reference for encoding and decoding operations relevant to security testing, forensics, and vulnerability analysis. Covers Base64, URL encoding, HTML entities, Unicode normalization, and double encoding attacks for penetration testers and security analysts.

## Base64

### Standard Base64 (RFC 4648)

```
Charset: A-Z, a-z, 0-9, +, /
Padding: = (one or two)
Line breaks: Every 76 characters (MIME) or none (standard)
```

```bash
# Encode
echo -n "Hello World" | base64
# SGVsbG8gV29ybGQ=

# Decode
echo "SGVsbG8gV29ybGQ=" | base64 -d
# Hello World

# Encode file
base64 file.bin > file.b64
base64 -d file.b64 > file.bin
```

### Base64URL (RFC 4648 Section 5)

```
Charset: A-Z, a-z, 0-9, -, _  (replaces + and /)
Padding: Usually omitted
Used in: JWT, URL parameters, filenames
```

```python
import base64
encoded = base64.urlsafe_b64encode(b"data").rstrip(b"=")
decoded = base64.urlsafe_b64decode(encoded + b"==")
```

### Security Implications

- Base64 is encoding, NOT encryption (trivially reversible)
- Attacker can encode payloads to bypass naive filters
- PowerShell `-EncodedCommand` accepts UTF-16LE Base64 (common in malware)
- Base64 in URLs may indicate data exfiltration or C2 communication

```powershell
# Decode PowerShell encoded command
[System.Text.Encoding]::Unicode.GetString([System.Convert]::FromBase64String("encoded_string"))
```

## URL Encoding (Percent Encoding)

### Standard Encoding

```
Space  -> %20 (or + in form data)
<      -> %3C
>      -> %3E
"      -> %22
'      -> %27
/      -> %2F
?      -> %3F
#      -> %23
&      -> %26
=      -> %3D
```

### Double Encoding

```
# Single encoding:
<script> -> %3Cscript%3E

# Double encoding:
%3C -> %253C  (the % itself gets encoded)
<script> -> %253Cscript%253E

# Attack: if application decodes once, filter sees %3Cscript%3E
# Then a second decode layer produces <script>
```

```bash
# URL encode
python3 -c "import urllib.parse; print(urllib.parse.quote('<script>alert(1)</script>'))"
# %3Cscript%3Ealert%281%29%3C/script%3E

# URL decode
python3 -c "import urllib.parse; print(urllib.parse.unquote('%3Cscript%3E'))"
# <script>
```

### Security Testing with URL Encoding

| Test | Payload | Purpose |
|------|---------|---------|
| Standard | `<script>alert(1)</script>` | Baseline XSS |
| URL encoded | `%3Cscript%3Ealert(1)%3C/script%3E` | Bypass input filter |
| Double encoded | `%253Cscript%253Ealert(1)%253C/script%253E` | Bypass double decode |
| Mixed | `%3Cscript>alert(1)</script%3E` | Bypass partial filters |
| Unicode encoding | `%u003Cscript%u003E` | IIS-specific bypass |

## HTML Entity Encoding

### Named Entities

```
< -> &lt;        > -> &gt;
" -> &quot;       ' -> &apos; (or &#39;)
& -> &amp;        / -> &#47;
```

### Numeric Entities

```
< -> &#60;  (decimal)
< -> &#x3C; (hexadecimal)
< -> &#x3c; (hex, lowercase)
< -> &#0060; (decimal with leading zeros)
< -> &#x003C; (hex with leading zeros)
```

### HTML Entity Bypass Techniques

```html
<!-- Various ways to encode "javascript:" for XSS -->
&#106;avascript:           <!-- Partial entity encoding -->
&#x6A;avascript:           <!-- Hex entity -->
java&#x09;script:          <!-- Tab character injection -->
java&#x0A;script:          <!-- Newline injection -->
&#106;&#97;&#118;&#97;&#115;&#99;&#114;&#105;&#112;&#116;&#58;  <!-- Full encoding -->
```

## Unicode and Normalization

### Unicode Normalization Forms

| Form | Description | Security Relevance |
|------|-------------|-------------------|
| NFC | Canonical Decomposition + Composition | Standard normalized form |
| NFD | Canonical Decomposition | Decomposes characters |
| NFKC | Compatibility Decomposition + Composition | Maps visual equivalents |
| NFKD | Compatibility Decomposition | Most aggressive normalization |

### Homoglyph Attacks

```
Legitimate: apple.com
Homoglyph:  аpple.com  (Cyrillic 'а' U+0430 instead of Latin 'a' U+0061)

Common substitutions:
  a -> а (Cyrillic)
  e -> е (Cyrillic)
  o -> о (Cyrillic)
  p -> р (Cyrillic)
  c -> с (Cyrillic)
  l -> І (Cyrillic)
  0 -> О (Cyrillic Capital O)
```

### Unicode Security Issues

| Issue | Example | Risk |
|-------|---------|------|
| Normalization bypass | `%EF%BC%9C` (fullwidth `<`) normalizes to `<` | XSS after normalization |
| Right-to-left override | U+202E reverses text display | File extension disguise |
| Zero-width characters | U+200B, U+200C, U+200D, U+FEFF | Hidden content, watermarking |
| Overlong UTF-8 | `%C0%AF` = `/` (invalid UTF-8) | Path traversal bypass |

## Hex Encoding

```bash
# String to hex
echo -n "Hello" | xxd -p
# 48656c6c6f

# Hex to string
echo "48656c6c6f" | xxd -r -p
# Hello

# Hex dump of file
xxd file.bin | head
hexdump -C file.bin | head
```

## Multi-Layer Encoding Detection

### Analysis Workflow

```
1. Identify encoding type by pattern recognition
2. Decode one layer at a time
3. Check if result is another encoding
4. Repeat until plaintext is reached
5. Analyze final plaintext for malicious content

Example: Base64 -> URL encoded -> HTML entity
  Input: JTNDc2NyaXB0JTNF
  Base64 decode: %3Cscript%3E
  URL decode: <script>
  Final: XSS payload
```

### CyberChef Recipe (Conceptual)

```
Input -> From Base64 -> URL Decode -> HTML Entity Decode -> Output
```

## Cross-References

- See `lib/utilities/regex-security-patterns.md` for pattern matching encoded payloads
- See `lib/utilities/hash-comparison-utility.md` for hash encoding
- See `lib/patterns/input-validation-patterns.md` for encoding in validation
- See `data/registries/file-signatures-registry.md` for binary encoding
- See `reference/tools/burp-suite-reference.md` for encoding tools in Burp
