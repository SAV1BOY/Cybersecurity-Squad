# Timestamp Handling for Forensics

## Purpose

Reference for timestamp conversion, timezone normalization, and temporal analysis in digital forensics and incident response. Covers epoch time, common timestamp formats, NTP drift considerations, and timeline reconstruction techniques.

## Epoch Time Conversions

### Common Epoch Formats

| Format | Description | Example (2026-03-06 14:30:00 UTC) |
|--------|-------------|----------------------------------|
| Unix epoch (seconds) | Seconds since 1970-01-01 00:00:00 UTC | 1772975400 |
| Unix epoch (milliseconds) | JavaScript, Java | 1772975400000 |
| Unix epoch (microseconds) | Python datetime internal | 1772975400000000 |
| Unix epoch (nanoseconds) | Go time.Time | 1772975400000000000 |
| Windows FILETIME | 100-nanosecond intervals since 1601-01-01 | 133854402000000000 |
| Mac Absolute Time | Seconds since 2001-01-01 00:00:00 UTC | 794847000 |
| Chrome/WebKit | Microseconds since 1601-01-01 00:00:00 UTC | 13885440200000000 |
| LDAP/Active Directory | 100-nanosecond intervals since 1601-01-01 | 133854402000000000 |
| COCOA (macOS/iOS) | Seconds since 2001-01-01 | 794847000 |

### Conversion Commands

```bash
# Current Unix timestamp
date +%s

# Unix timestamp to human-readable
date -d @1772975400
# Fri Mar  6 14:30:00 UTC 2026

# Human-readable to Unix timestamp
date -d "2026-03-06 14:30:00 UTC" +%s

# Windows FILETIME to Unix (subtract 116444736000000000, divide by 10000000)
python3 -c "print((133854402000000000 - 116444736000000000) / 10000000)"
# 1772975400.0

# Mac Absolute Time to Unix (add 978307200)
python3 -c "print(794847000 + 978307200)"
# 1773154200 (Note: verify with actual date)

# Chrome timestamp to Unix
python3 -c "print((13885440200000000 - 11644473600000000) / 1000000)"
```

### Python Conversion Library

```python
from datetime import datetime, timezone, timedelta

# Unix epoch to datetime
ts = 1772975400
dt = datetime.fromtimestamp(ts, tz=timezone.utc)
print(dt.isoformat())  # 2026-03-06T14:30:00+00:00

# Datetime to Unix epoch
dt = datetime(2026, 3, 6, 14, 30, 0, tzinfo=timezone.utc)
ts = dt.timestamp()

# Windows FILETIME to datetime
EPOCH_DIFF = 116444736000000000
filetime = 133854402000000000
unix_ts = (filetime - EPOCH_DIFF) / 10000000
dt = datetime.fromtimestamp(unix_ts, tz=timezone.utc)

# LDAP timestamp (same as FILETIME)
ldap_ts = 133854402000000000
unix_ts = (ldap_ts - 116444736000000000) / 10000000

# macOS/iOS Cocoa timestamp
cocoa_ts = 794847000
unix_ts = cocoa_ts + 978307200
```

## Common Timestamp Formats in Logs

### Format Strings

| Format | Example | Source |
|--------|---------|-------|
| ISO 8601 | `2026-03-06T14:30:00.123Z` | Standard, SIEM preferred |
| RFC 2822 | `Fri, 06 Mar 2026 14:30:00 +0000` | Email headers |
| Syslog (RFC 3164) | `Mar  6 14:30:00` | Traditional syslog (no year!) |
| Syslog (RFC 5424) | `2026-03-06T14:30:00.123456+00:00` | Modern syslog |
| Apache Common Log | `06/Mar/2026:14:30:00 +0000` | Web server access logs |
| Windows Event Log | `3/6/2026 2:30:00 PM` | US locale, local time |
| MySQL | `2026-03-06 14:30:00` | Database logs |
| AWS CloudTrail | `2026-03-06T14:30:00Z` | ISO 8601 UTC |

### Dangerous Ambiguities

| Ambiguity | Example | Risk |
|-----------|---------|------|
| Missing year | `Mar 6 14:30:00` (syslog) | Year rollover causes misattribution |
| Missing timezone | `2026-03-06 14:30:00` | Assumed local time varies by system |
| Date format | `03/06/2026` vs `06/03/2026` | US (MM/DD) vs EU (DD/MM) |
| DST transitions | `2026-03-08 02:30:00 US/Eastern` | Ambiguous during spring-forward gap |
| 12-hour format | `2:30:00 PM` | AM/PM confusion in automated parsing |

## Timezone Normalization

### Forensic Standard

**Always normalize to UTC for timeline analysis.** Store original timezone offset for reference.

```python
from datetime import datetime
import pytz

# Convert local time to UTC
local_tz = pytz.timezone('US/Eastern')
local_dt = local_tz.localize(datetime(2026, 3, 6, 9, 30, 0))
utc_dt = local_dt.astimezone(pytz.utc)
print(f"Local: {local_dt}")  # 2026-03-06 09:30:00-05:00
print(f"UTC:   {utc_dt}")    # 2026-03-06 14:30:00+00:00
```

### Common Timezone Offsets

| Abbreviation | Offset | Region |
|-------------|--------|--------|
| UTC/GMT | +00:00 | Universal |
| EST/EDT | -05:00/-04:00 | US Eastern |
| CST/CDT | -06:00/-05:00 | US Central |
| PST/PDT | -08:00/-07:00 | US Pacific |
| CET/CEST | +01:00/+02:00 | Central Europe |
| IST | +05:30 | India |
| JST | +09:00 | Japan |
| AEST/AEDT | +10:00/+11:00 | Australia Eastern |

## NTP Drift Considerations

### Impact on Forensics

| Drift Amount | Impact |
|-------------|--------|
| <1 second | Negligible for most investigations |
| 1-60 seconds | May affect event ordering within tight windows |
| >60 seconds | Can invalidate timeline correlations |
| >300 seconds (5 min) | Critical: timeline reconstruction unreliable |

### Detection and Compensation

```bash
# Check NTP synchronization status
timedatectl status
chronyc tracking
ntpq -p

# Check time offset
chronyc sources -v
# Look for "offset" column; values >1s are concerning
```

### Forensic Timeline Adjustment

```
When building timelines from multiple sources:
1. Identify time source for each evidence item
2. Determine NTP sync status at time of events
3. Note maximum possible drift per source
4. Apply drift correction where measurable
5. Flag events within drift window as "approximately concurrent"
6. Document all time adjustments in forensic report
```

## Timeline Reconstruction

### Super Timeline Creation

```bash
# Using log2timeline (Plaso)
log2timeline.py timeline.plaso /path/to/evidence/
psort.py -o l2tcsv -w timeline.csv timeline.plaso

# Filter timeline
psort.py -o l2tcsv -w filtered.csv timeline.plaso \
  "date > '2026-03-01' AND date < '2026-03-07'"
```

### Timeline Correlation Pattern

```
1. Collect timestamps from all sources
2. Normalize all to UTC
3. Sort chronologically
4. Identify temporal clusters (events within seconds of each other)
5. Correlate across sources (same user, same IP, related resources)
6. Identify gaps (missing events that should exist)
7. Document the narrative timeline with supporting evidence
```

## Cross-References

- See `data/registries/windows-event-ids-registry.md` for Windows event timestamps
- See `data/registries/linux-log-sources-registry.md` for Linux log timestamp formats
- See `reference/tools/splunk-reference.md` for SIEM timestamp handling
- See `reference/tools/wireshark-reference.md` for packet capture timestamps
- See `frameworks/ir-layer.md` for incident response timeline requirements
