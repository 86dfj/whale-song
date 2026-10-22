# v1.0.0 — first public release

Whale Song 1.0: passive tick measurement for game servers.

## Download

`WhaleSong-1.0.zip` (45.8 MB)

SHA-256:

```
f7c0b75695f2207a1661b3abd1b4eded6621a937f7993e95cf289a352f939c78
```

Verify with:

```powershell
Get-FileHash .\WhaleSong-1.0.zip -Algorithm SHA256
```

## What's inside

- `鲸歌.exe` — launcher
- Built-in Python runtime (no installation needed)
- In-app usage guide explaining every button
- Bilingual interface: Chinese / English (toggle in the main window)

## What it measures

Per match: batches per second, confidence (`trusted` / `reference` / `undecidable`), rate-change check, stalls.

**batches ≠ engine tick** — passive capture cannot separate packet cadence from simulation rate.

## Validation

- loopback: error 0.0%
- ground truth: 10.2% / 20.9% estimated for 10% / 20% loss
- adversarial: 6 fake-cadence traps rejected
- regression: 17 checks

## Notes

- Windows 10/11, administrator required for capture
- The tool is offline: it never uploads anything by itself
- Personal, non-commercial use; see LICENSE.md
