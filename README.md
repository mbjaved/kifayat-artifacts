# Kifayat artifacts

Small public files the Kifayat app reads, only when the user asks it to. They hold no personal data.

| Path | What | Read by |
|------|------|---------|
| `zakat/nisab.json` | Official zakat nisab notifications (and optionally the day's silver rate per tola), each with its source | Zakat tab > "Check for a new nisab" |

Each kind of file has its own folder. A file's format is fixed by its `version` field; a change that older apps can't read gets a new version number, not an edit in place.

## zakat/nisab.json

```
{"version": 1,
 "official": [{"islamic_year": "1447-1448", "amount": 540000, "notified_on": "2027-02-01",
               "silver_rate_tola": 10286, "source_name": "...", "source_url": "https://..."}],
 "silver": {"rate_tola": 9800, "on": "2026-11-15", "source_name": "...", "source_url": "https://..."}}
```

- Add a new year's notification to `official`; keep the older ones. `silver` is optional.
- The app drops any entry that is off (amount outside 50,000-10,000,000, a date in the future, a non-https source) and asks the user before using a figure.
