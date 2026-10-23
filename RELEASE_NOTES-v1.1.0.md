# v1.1.0 — English UI & smoother capture

## What's new

- **Bilingual interface** — Chinese / English toggle in the main window
- **English summary** — `report.en.md` is generated when the UI is English
- **English launcher** — `WhaleSong.exe` (same program as `鲸歌.exe`)
- **QUICKSTART.txt** — three-step English quick start
- **Remember elevation** — optional: create a scheduled task so capture starts without a UAC prompt every time (revocable in Dev tools)
- **Capture status fix** — the app now detects a running capture reliably and shows elapsed time
- **Reference value** — when a flow is multiplexed and the tick is undecidable, the report now shows the raw inter-arrival peak as a *reference only*

## Download

`WhaleSong-1.1.0.zip` (45.9 MB)

SHA-256:

```
1CC1F8D520591E8286F65E18C74C0EAAE32FA23108DC64BBC50703F7F17D7FCF
```

Verify:

```powershell
Get-FileHash .\WhaleSong-1.1.0.zip -Algorithm SHA256
```

## Notes

- Windows 10/11, administrator required for capture
- The tool is offline: it never uploads anything by itself
- For China users: 蓝奏云链接见 B站/小黑盒帖子
- Personal, non-commercial use; see LICENSE.md

## Field test

Valorant (official 128 tick):
- captured 30:56, one 28:20 match segment
- verdict: undecidable (multiplexed flow)
- raw interval peak 7.7 ms ≈ 130/s — close to the official 128, reported as reference only
