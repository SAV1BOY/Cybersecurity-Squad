# Input Validation Patterns

## Purpose

Reference patterns for secure input validation. Covers allowlisting strategies, type coercion safety, boundary checking, context-appropriate encoding and escaping, and defense against injection attacks across all input vectors.

## Core Principles

### Validation Strategy Hierarchy

1. **Reject**: If input does not match expected format, reject immediately
2. **Sanitize**: Remove or neutralize dangerous content (only if rejection is impractical)
3. **Escape**: Encode for output context (always, even after validation)

### Allowlist vs Denylist

| Approach | Description | Effectiveness |
|----------|-------------|--------------|
| Allowlist (preferred) | Define exactly what IS allowed | High: new attacks automatically blocked |
| Denylist (fragile) | Define what is NOT allowed | Low: must anticipate all attack patterns |

**Rule**: Always validate against what you expect, not what you fear.

## Validation by Data Type

### String Validation

```python
# Length constraints (ALWAYS enforce)
if len(input_string) > MAX_LENGTH:
    reject("Input too long")

# Character allowlisting
import re
if not re.match(r'^[a-zA-Z0-9\s\-\.]{1,100}$', input_string):
    reject("Invalid characters")

# Email validation (simplified; use library for production)
if not re.match(r'^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$', email):
    reject("Invalid email format")

# URL validation
from urllib.parse import urlparse
parsed = urlparse(input_url)
if parsed.scheme not in ('https',):  # Only allow HTTPS
    reject("Invalid URL scheme")
if parsed.hostname in BLOCKLIST:     # SSRF prevention
    reject("Blocked destination")
```

### Numeric Validation

```python
# Type coercion safety
try:
    value = int(user_input)  # or float() with care
except (ValueError, TypeError):
    reject("Not a valid number")

# Boundary checking
if not (MIN_VALUE <= value <= MAX_VALUE):
    reject("Value out of range")

# Prevent integer overflow (language-dependent)
if value > sys.maxsize:
    reject("Value too large")
```

### Date and Time Validation

```python
from datetime import datetime
try:
    dt = datetime.strptime(input_date, "%Y-%m-%d")
    if dt < MIN_DATE or dt > MAX_DATE:
        reject("Date out of range")
except ValueError:
    reject("Invalid date format")
```

## Context-Specific Encoding and Escaping

### The Critical Rule

Validate input on entry. Encode output for context. These are separate concerns. Validation cannot replace output encoding.

### HTML Context

```python
# User input displayed in HTML body
import html
safe_output = html.escape(user_input)
# Converts < > & " ' to HTML entities

# Template engines with auto-escaping (preferred)
# Jinja2: {{ user_input }} auto-escapes by default
# React: JSX auto-escapes by default
```

### JavaScript Context

```javascript
// NEVER inject user input directly into JS
// BAD: var name = "{{ user_input }}";
// GOOD: Use data attributes + DOM API
// <div data-name="{{ user_input | escape }}">
// var name = element.dataset.name;

// If absolutely necessary, use JSON encoding:
var data = JSON.parse('{{ user_input | tojson }}');
```

### SQL Context (Parameterized Queries)

```python
# NEVER concatenate user input into SQL
# BAD:
cursor.execute(f"SELECT * FROM users WHERE id = {user_id}")

# GOOD: Parameterized queries (prepared statements)
cursor.execute("SELECT * FROM users WHERE id = %s", (user_id,))

# ORM usage (also safe)
user = User.objects.get(id=user_id)
```

### URL Context

```python
from urllib.parse import quote
safe_param = quote(user_input, safe='')
url = f"https://example.com/search?q={safe_param}"
```

### LDAP Context

```python
# Escape LDAP special characters
def ldap_escape(input_str):
    special_chars = ['\\', '*', '(', ')', '\x00']
    for char in special_chars:
        input_str = input_str.replace(char, f'\\{ord(char):02x}')
    return input_str
```

### OS Command Context

```python
# NEVER use shell=True with user input
# BAD:
os.system(f"ping {user_input}")
subprocess.call(f"grep {user_input} file.txt", shell=True)

# GOOD: Use array form (no shell interpretation)
subprocess.run(["ping", "-c", "4", validated_hostname], shell=False)

# BEST: Use language-native libraries instead of OS commands
import socket
socket.gethostbyname(validated_hostname)
```

## File Upload Validation

```python
# Multi-layer validation for file uploads
def validate_upload(file):
    # 1. Check file size
    if file.size > MAX_FILE_SIZE:
        reject("File too large")

    # 2. Check extension (allowlist)
    ext = os.path.splitext(file.name)[1].lower()
    if ext not in ALLOWED_EXTENSIONS:
        reject("File type not allowed")

    # 3. Check MIME type (from content, not header)
    import magic
    mime_type = magic.from_buffer(file.read(2048), mime=True)
    if mime_type not in ALLOWED_MIME_TYPES:
        reject("Invalid file content type")

    # 4. Check magic bytes
    file.seek(0)
    header = file.read(8)
    if not matches_expected_signature(header, ext):
        reject("File signature mismatch")

    # 5. For images: re-encode to strip embedded content
    if mime_type.startswith('image/'):
        file = reencode_image(file)

    # 6. Generate safe filename
    safe_name = generate_uuid() + ext
    return safe_name
```

## API Input Validation

### JSON Schema Validation

```json
{
  "$schema": "https://json-schema.org/draft/2020-12/schema",
  "type": "object",
  "properties": {
    "username": {
      "type": "string",
      "minLength": 3,
      "maxLength": 30,
      "pattern": "^[a-zA-Z0-9_-]+$"
    },
    "email": {
      "type": "string",
      "format": "email",
      "maxLength": 254
    },
    "age": {
      "type": "integer",
      "minimum": 13,
      "maximum": 150
    }
  },
  "required": ["username", "email"],
  "additionalProperties": false
}
```

### GraphQL-Specific Validation

- Query depth limiting (prevent nested query attacks)
- Query complexity analysis (prevent resource exhaustion)
- Field-level authorization (validate access per field)
- Input type enforcement via schema
- Introspection disabled in production

## Common Bypass Techniques to Defend Against

| Bypass | Defense |
|--------|---------|
| Double encoding (`%2527`) | Decode once, then validate; or validate at each decode step |
| Unicode normalization (`%EF%BC%9C` = `<`) | Normalize Unicode before validation |
| Null byte injection (`file%00.jpg`) | Strip null bytes; validate after filename parsing |
| Case variation (`<ScRiPt>`) | Lowercase/normalize before comparison |
| Whitespace injection (`java\tscript:`) | Strip/normalize whitespace |
| Protocol-relative URLs (`//evil.com`) | Validate scheme explicitly |

## Cross-References

- See `lib/patterns/authentication-patterns.md` for credential input handling
- See `lib/utilities/regex-security-patterns.md` for validation regex library
- See `lib/utilities/encoding-decoding-utility.md` for encoding reference
- See `data/registries/file-signatures-registry.md` for file magic bytes
- See `frameworks/appsec-layer.md` for application security methodology
