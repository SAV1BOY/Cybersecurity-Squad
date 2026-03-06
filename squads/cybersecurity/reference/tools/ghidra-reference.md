# Ghidra Reference

## Purpose

Operational reference for Ghidra, the NSA-developed open-source software reverse engineering framework. Covers setup, navigation, decompiler usage, scripting automation, collaborative analysis, and plugin development for malware analysis, vulnerability research, and binary auditing.

## Setup and Configuration

### Installation

```bash
# Prerequisites: JDK 17+
# Download from https://ghidra-sre.org/
unzip ghidra_<version>.zip
cd ghidra_<version>
./ghidraRun  # Linux/Mac
ghidraRun.bat  # Windows
```

### Project Organization

| Concept | Description |
|---------|-------------|
| Project | Container for multiple programs (binaries) |
| Program | Single binary under analysis |
| Tool | Analysis window (CodeBrowser, Debugger, etc.) |
| Shared Project | Multi-analyst collaborative project via Ghidra Server |

### Initial Analysis Options

When importing a binary, configure auto-analysis:

| Analyzer | Purpose | Enable For |
|----------|---------|------------|
| ASCII Strings | Find string references | Always |
| Aggressive Instruction Finder | Recover code in data sections | Packed/obfuscated binaries |
| Decompiler Parameter ID | Improve decompiler output | Always |
| Function Start Search | Find function entry points | Stripped binaries |
| Stack Reference Analysis | Resolve stack variable access | Always |
| Embedded Media | Find embedded files/resources | Malware analysis |
| PDB (Windows) | Load debug symbols | When PDB available |
| DWARF (Linux) | Load debug symbols | When DWARF present |

## Navigation and Analysis

### Key Shortcuts

| Shortcut | Action |
|----------|--------|
| `G` | Go to address |
| `L` | Rename label/function |
| `T` | Set data type |
| `;` | Add comment |
| `Ctrl+Shift+E` | Edit function signature |
| `D` | Disassemble at cursor |
| `P` | Create function at cursor |
| `X` | Show cross-references (xrefs) |
| `Ctrl+Shift+F` | Search memory for bytes |
| `Ctrl+E` | Search for strings |
| `Space` | Toggle listing/decompiler focus |

### Analysis Workflow

1. **Triage**: Check file headers, strings, imports/exports
2. **Entry Point**: Start at `main()` or `DllEntryPoint` or `_start`
3. **Import Analysis**: Review imported functions for capability indicators
4. **String Analysis**: Search for URLs, IPs, registry keys, file paths
5. **Cross-Reference**: Follow xrefs from interesting imports/strings
6. **Function Rename**: Name functions as behavior is understood
7. **Type Recovery**: Apply struct/enum types to improve decompilation
8. **Control Flow**: Use function graph view for complex logic

### Critical Windows API Indicators

| API Category | Functions | Indicates |
|-------------|-----------|-----------|
| Process | CreateProcess, ShellExecute | Execution |
| Registry | RegSetValue, RegCreateKey | Persistence |
| Network | WSAStartup, connect, send, recv | C2/Exfiltration |
| File | CreateFile, WriteFile, DeleteFile | File manipulation |
| Injection | VirtualAllocEx, WriteProcessMemory, CreateRemoteThread | Process injection |
| Crypto | CryptEncrypt, CryptDecrypt | Encryption/Ransomware |
| Anti-Debug | IsDebuggerPresent, CheckRemoteDebuggerPresent | Evasion |

## Decompiler

### Improving Decompiler Output

1. **Set function signatures**: Right-click function > Edit Function Signature
2. **Apply data types**: Import header files or create custom structures
3. **Retype variables**: Right-click variable > Retype Variable
4. **Split/merge variables**: Fix incorrect variable recovery
5. **Set calling convention**: Correct if auto-detection fails

### Structure Recovery

```c
// Create custom struct in Data Type Manager
// Right-click category > New > Structure

// Example: recovered C2 config structure
struct C2Config {
    char server_url[256];
    uint16_t port;
    uint32_t sleep_ms;
    uint32_t jitter_pct;
    byte encryption_key[32];
    uint8_t protocol_type;  // 0=HTTP, 1=DNS, 2=TCP
};
```

## Ghidra Scripting

### Java Script Example

```java
// FindSuspiciousStrings.java - Find potential IOCs in binary
import ghidra.app.script.GhidraScript;
import ghidra.program.model.data.*;
import ghidra.program.model.listing.*;

public class FindSuspiciousStrings extends GhidraScript {
    @Override
    public void run() throws Exception {
        DataIterator dataIterator = currentProgram.getListing().getDefinedData(true);
        while (dataIterator.hasNext()) {
            Data data = dataIterator.next();
            if (data.getDataType() instanceof StringDataType ||
                data.getDataType() instanceof UnicodeDataType) {
                String value = data.getValue().toString();
                if (value.matches(".*https?://.*") ||
                    value.matches(".*\\d{1,3}\\.\\d{1,3}\\.\\d{1,3}\\.\\d{1,3}.*") ||
                    value.matches(".*HKEY_.*") ||
                    value.contains("cmd.exe") ||
                    value.contains("powershell")) {
                    println(String.format("[IOC] %s: %s",
                        data.getAddress().toString(), value));
                }
            }
        }
    }
}
```

### Python (Jython) Script Example

```python
# list_functions_with_crypto.py
# Find functions that reference crypto-related APIs
from ghidra.program.model.symbol import SymbolType

crypto_apis = ["CryptEncrypt", "CryptDecrypt", "AES", "RSA",
               "BCryptEncrypt", "CryptHashData", "CryptDeriveKey"]

fm = currentProgram.getFunctionManager()
for func in fm.getFunctions(True):
    for ref in getReferencesFrom(func.getEntryPoint()):
        sym = getSymbolAt(ref.getToAddress())
        if sym and any(api in sym.getName() for api in crypto_apis):
            print("[CRYPTO] {} calls {} at {}".format(
                func.getName(), sym.getName(), ref.getToAddress()))
```

### Script Manager

Access via Window > Script Manager. Scripts are organized by category:
- Analysis, Binary, Data, Functions, Headless, Search
- Custom scripts go in `~/ghidra_scripts/`

## Headless Analysis

```bash
# Run analysis without GUI
analyzeHeadless /path/to/project ProjectName \
  -import /path/to/binary \
  -postScript FindSuspiciousStrings.java \
  -scriptlog /path/to/output.log

# Batch analysis
analyzeHeadless /path/to/project BatchProject \
  -import /path/to/samples/ \
  -recursive \
  -postScript ExportFunctions.py
```

## Collaborative Reverse Engineering

### Ghidra Server Setup

```bash
# Initialize server
cd ghidra_<version>/server
./svrInstall  # Linux
./ghidraSvr start
./ghidraSvr console  # For user management

# Analysts connect via File > New Project > Shared Project
# Changes are versioned and mergeable
```

### Collaboration Workflow

1. Create shared project on Ghidra Server
2. Check out files for exclusive edit or merge-on-commit
3. Use bookmarks and comments to communicate findings
4. Tag functions with analyst initials for attribution
5. Use version history for change tracking

## Cross-References

- See `frameworks/offense-layer.md` for vulnerability research methodology
- See `reference/tools/metasploit-reference.md` for exploit development post-RE
- See `data/registries/file-signatures-registry.md` for file type identification
- See `data/research/emerging-threats/ai-powered-attacks.md` for AI-assisted RE techniques
- See `lib/utilities/encoding-decoding-utility.md` for encoding analysis
