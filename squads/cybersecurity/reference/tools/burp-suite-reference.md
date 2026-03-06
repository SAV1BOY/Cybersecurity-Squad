# Burp Suite Pro Complete Reference

## Purpose

Comprehensive operational reference for Burp Suite Professional, the industry-standard web application security testing platform. Covers scanner configuration, intruder attack modes, extension ecosystem, macro-based authentication handling, and API security testing workflows.

## Scanner Configuration

### Active Scan Settings

| Setting | Recommended Value | Rationale |
|---------|------------------|-----------|
| Scan Speed | Thorough | Maximizes coverage; use Fast only for time-constrained engagements |
| Audit Items | All except DoS-related | Avoids service disruption in production |
| JavaScript Analysis | Enabled | Catches DOM-based vulnerabilities |
| Consolidate Findings | By path + parameter | Reduces duplicate noise |

### Passive Scan Tuning

Passive scanning runs continuously on all proxied traffic:

- Enable all information disclosure checks
- Enable cookie attribute checks (Secure, HttpOnly, SameSite)
- Enable mixed content detection
- Enable cacheable HTTPS response detection
- Monitor for PII leakage patterns in responses

### Crawl Configuration

```
Max crawl depth: 12
Max link depth: 10
Crawl strategy: Fastest (for large apps), Most complete (for focused targets)
Form submission: Use configured credentials
Handle app logins: Via recorded macros or session rules
```

## Intruder Attack Types

### Sniper
Single payload set, one position at a time. Best for individual parameter fuzzing.

### Battering Ram
Single payload set, all positions simultaneously. Useful for CSRF token testing where the same value must appear in multiple places.

### Pitchfork
Multiple payload sets, one per position, iterated in parallel. Ideal for credential stuffing with username/password pairs.

### Cluster Bomb
Multiple payload sets, all combinations tested. Use for brute-force discovery but be aware of combinatorial explosion.

### Payload Types Reference

| Payload Type | Use Case |
|-------------|----------|
| Simple list | Custom wordlists, known values |
| Runtime file | Large files loaded on demand |
| Character substitution | Leet-speak / homoglyph attacks |
| Recursive grep | Extract tokens from responses for chained attacks |
| Extension-generated | Custom payloads from BApp extensions |

## Extension Ecosystem (Critical BApps)

### Must-Install Extensions

1. **Logger++** — Enhanced logging with grep/filter across all traffic
2. **Autorize** — Automated IDOR and authorization bypass testing
3. **Turbo Intruder** — High-speed HTTP fuzzing via Python scripting
4. **Param Miner** — Hidden parameter and header discovery
5. **JSON Web Token Attacker** — JWT manipulation and attack automation
6. **Retire.js** — Client-side library vulnerability detection
7. **Active Scan++** — Additional active scan checks (host header injection, SMTP injection)
8. **Backslash Powered Scanner** — Advanced server-side injection detection
9. **Collaborator Everywhere** — OOB interaction injection in all parameters
10. **SAML Raider** — SAML assertion manipulation

### Extension Development

```python
# Minimal Burp extension skeleton (Python/Jython)
from burp import IBurpExtender, IHttpListener

class BurpExtender(IBurpExtender, IHttpListener):
    def registerExtenderCallbacks(self, callbacks):
        self._callbacks = callbacks
        self._helpers = callbacks.getHelpers()
        callbacks.setExtensionName("Custom Extension")
        callbacks.registerHttpListener(self)

    def processHttpMessage(self, toolFlag, messageIsRequest, messageInfo):
        if not messageIsRequest:
            response = messageInfo.getResponse()
            analyzedResponse = self._helpers.analyzeResponse(response)
            # Custom analysis logic here
```

## Macro and Session Handling

### Authentication Macro Setup

1. Navigate to Project Options > Sessions > Macros
2. Record login sequence (GET login page, POST credentials, follow redirect)
3. Create Session Handling Rule:
   - Scope: Target domain only
   - Action: Check session validity via indicator (e.g., "Logout" link)
   - If invalid: Run macro to re-authenticate
4. Configure cookie jar to update from macro responses

### Multi-Step Authentication

For MFA or multi-page login flows:

- Chain multiple macros in sequence
- Use parameter derivation between macro steps (extract CSRF tokens, session IDs)
- Set inter-request delays if rate limiting is enforced

## API Testing Workflow

### OpenAPI/Swagger Import

1. Import API definition via Target > Import
2. Review auto-generated request templates
3. Configure authentication headers (Bearer tokens, API keys)
4. Run active scan against all endpoints

### GraphQL Testing

- Use InQL extension for schema introspection
- Test for query depth/complexity abuse
- Check for batching attacks
- Validate authorization on nested resolvers
- Test subscription endpoints for information disclosure

### REST API Checks

| Test | Method |
|------|--------|
| BOLA/IDOR | Swap IDs between user contexts using Autorize |
| Mass assignment | Send additional fields in POST/PUT bodies |
| Rate limiting | Turbo Intruder with throttle detection |
| Injection | Standard Intruder payloads against all parameters |
| Verb tampering | Replay requests with alternate HTTP methods |

## Collaborator and Out-of-Band Testing

Burp Collaborator detects blind vulnerabilities via DNS/HTTP/SMTP callbacks:

- Blind SSRF: Inject Collaborator URLs in URL parameters, headers, webhooks
- Blind XXE: External entity pointing to Collaborator
- Blind SQLi: DNS exfiltration via `xp_dirtree` or `LOAD_FILE()`
- Email header injection: Collaborator as recipient

Use private Collaborator server for sensitive engagements to avoid data leaving the network.

## Output and Reporting

### Export Formats

- HTML report (executive + technical)
- XML export (for custom processing pipelines)
- Issue JSON via REST API (Burp Suite Enterprise)

### Scan Quality Metrics

Track and report: total requests made, unique endpoints discovered, scan coverage percentage, false positive rate after triage.

## Cross-References

- See `reference/tools/nmap-reference.md` for network-layer reconnaissance preceding web testing
- See `frameworks/appsec-layer.md` for application security methodology
- See `checklists/web-app-assessment-quality.md` for assessment quality gates
- See `checklists/api-security-assessment-quality.md` for API-specific checks
- See `templates/reports/executive-summary-template.md` for report structure
