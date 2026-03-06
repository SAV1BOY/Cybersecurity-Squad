# HTTP Status Codes from a Security Perspective

## Purpose

Reference for HTTP status codes with emphasis on security implications. Covers information leakage through error responses, authentication and authorization flow analysis, and security-relevant response patterns for web application testing and incident analysis.

## Informational (1xx)

| Code | Name | Security Relevance |
|------|------|-------------------|
| 100 | Continue | WebSocket upgrade path; verify protocol switching |
| 101 | Switching Protocols | WebSocket/HTTP2 upgrade; ensure secure upgrade path |
| 103 | Early Hints | Preload resources; verify no sensitive resource hints |

## Successful (2xx)

| Code | Name | Security Relevance |
|------|------|-------------------|
| 200 | OK | Baseline success; check response body for data exposure |
| 201 | Created | Resource creation confirmed; verify authorization was checked |
| 204 | No Content | Common for DELETE; verify resource actually deleted |
| 206 | Partial Content | Range requests; can be used to probe file sizes |

### Security Notes for 2xx

- A 200 response to an unauthorized request indicates broken access control (BOLA/IDOR)
- 200 on sensitive endpoints without authentication = critical vulnerability
- Consistent 200 responses regardless of input may indicate a honeypot or WAF page

## Redirection (3xx)

| Code | Name | Security Relevance |
|------|------|-------------------|
| 301 | Moved Permanently | Verify HTTP->HTTPS redirect; open redirect check |
| 302 | Found | Authentication redirect flows; open redirect risk |
| 303 | See Other | POST-redirect-GET pattern; token in redirect URL? |
| 304 | Not Modified | Cache behavior; verify sensitive pages not cached |
| 307 | Temporary Redirect | Preserves method; body forwarding risks |
| 308 | Permanent Redirect | Preserves method; body forwarding risks |

### Redirect Security Analysis

```
Open Redirect Detection:
1. Test: GET /login?redirect=https://evil.com
2. If 302 Location: https://evil.com -> OPEN REDIRECT VULNERABILITY
3. Common bypass patterns:
   - //evil.com
   - /\evil.com
   - https://target.com@evil.com
   - https://target.com.evil.com
   - data:text/html;base64,...
   - javascript:alert(1) (307/308 redirect)
```

### Caching Security

- 301 responses are cached by browsers permanently; poisoning a 301 has lasting impact
- Verify `Cache-Control: no-store` on authenticated responses
- 304 on sensitive pages indicates potential cache poisoning vector

## Client Error (4xx)

| Code | Name | Security Relevance |
|------|------|-------------------|
| 400 | Bad Request | Input validation triggered; check error detail leakage |
| 401 | Unauthorized | Authentication required; user enumeration risk |
| 403 | Forbidden | Authorization denied; path exists but access blocked |
| 404 | Not Found | Resource does not exist; or intentionally masked 403 |
| 405 | Method Not Allowed | HTTP verb restricted; try other verbs (PUT, DELETE) |
| 407 | Proxy Authentication Required | Proxy detected; may reveal infrastructure |
| 408 | Request Timeout | Slow-loris detection; DoS indicator |
| 413 | Payload Too Large | Upload limit reached; probe for bypass |
| 414 | URI Too Long | URL length limit; may truncate security parameters |
| 418 | I'm a Teapot | Sometimes used by WAFs as a block page |
| 429 | Too Many Requests | Rate limiting active; brute force mitigation |
| 431 | Request Header Fields Too Large | Header injection limit |
| 451 | Unavailable For Legal Reasons | Geo-restriction or legal block |

### Authentication Enumeration via Status Codes

```
Vulnerability: Different responses reveal valid/invalid usernames

Secure Pattern:
  Invalid user + any password -> 401 "Invalid credentials"
  Valid user + wrong password -> 401 "Invalid credentials"
  (Same response, same timing)

Insecure Pattern:
  Invalid user -> 401 "User not found"           # LEAKS USER EXISTENCE
  Valid user + wrong password -> 401 "Wrong password"  # CONFIRMS USER EXISTS
  Valid user + wrong password -> 403              # DIFFERENT STATUS CODE

Also check:
  - Response time differences (slower for valid users = timing attack)
  - Response body length differences
  - Response header differences
```

### 403 vs 404 for Security Testing

```
403 Forbidden: Resource EXISTS but access denied
  -> Try different authentication, parameter tampering, verb tampering
  -> Path traversal: /admin/../admin
  -> Case variation: /Admin, /ADMIN
  -> Extension bypass: /admin.json, /admin/., /admin%20

404 Not Found: Resource does not exist (or properly masked 403)
  -> Consistent 404 for both = good security practice
  -> If 403 on some paths and 404 on others, 403 confirms path existence
```

## Server Error (5xx)

| Code | Name | Security Relevance |
|------|------|-------------------|
| 500 | Internal Server Error | Application error; check for stack traces |
| 501 | Not Implemented | Method not implemented; may reveal tech stack |
| 502 | Bad Gateway | Backend service error; reveals proxy architecture |
| 503 | Service Unavailable | Overloaded or maintenance; DoS success indicator |
| 504 | Gateway Timeout | Backend timeout; SSRF or DoS indicator |

### Information Leakage in Error Responses

```
CRITICAL: Stack traces in 500 responses reveal:
  - Framework and version (Spring, Django, Laravel, Express)
  - File paths on server
  - Database queries (SQL injection confirmation)
  - Internal IP addresses
  - Library versions (useful for CVE matching)

SECURE PRACTICE:
  - Generic error page for all 5xx in production
  - Detailed errors logged server-side only
  - Custom error pages that reveal nothing about stack
  - Correlation ID in response for support lookup
```

## Response Analysis for Penetration Testing

### Differential Analysis Pattern

```
1. Establish baseline response for normal request
2. Modify one parameter at a time
3. Compare: status code, response length, response time, headers
4. Differences indicate processing changes = potential vulnerability

Tool: Burp Suite Comparer for response differential analysis
```

### Security Headers to Check in Responses

| Header | Expected | If Missing |
|--------|----------|-----------|
| `Strict-Transport-Security` | max-age=31536000 | HTTPS downgrade risk |
| `X-Content-Type-Options` | nosniff | MIME type sniffing attacks |
| `X-Frame-Options` | DENY or SAMEORIGIN | Clickjacking risk |
| `Content-Security-Policy` | Restrictive policy | XSS risk |
| `X-XSS-Protection` | 0 (rely on CSP instead) | Legacy browsers at risk |
| `Referrer-Policy` | strict-origin-when-cross-origin | URL leakage |

## Cross-References

- See `reference/tools/burp-suite-reference.md` for web application testing
- See `lib/patterns/input-validation-patterns.md` for proper error handling
- See `frameworks/appsec-layer.md` for application security methodology
- See `checklists/web-app-assessment-quality.md` for assessment quality
- See `lib/utilities/encoding-decoding-utility.md` for URL encoding in bypass tests
