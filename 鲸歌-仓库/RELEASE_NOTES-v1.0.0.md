# v1.0.0 — first public release

Whale Song 1.0: passive tick measurement for game servers.

## Download

`WhaleSong-1.0.zip` (45.8 MB)

SHA-256:

```
A383D9AF388BA823CEA5F61927208FE52AE1D9B726EF75BF630E7C494623C85A
```

Verify with:

```powershell
Get-FileHash .\WhaleSong-1.0.zip -Algorithm SHA256
```

## What's inside

- `鲸歌.exe` — launcher
- Built-in Python runtime (no installation needed)
- In-app usage guide explaining every button

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
