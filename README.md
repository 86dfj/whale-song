# Whale Song

**Passive tick measurement for game servers — no injection, no memory reading, no game modification.**

Whale Song records one match's network traffic (with Windows' built-in packet capture), then estimates how fast the server sends state updates — a tick approximation.

> This repository hosts **binaries, documentation and issue tracking only**.
> The source code is not published.

---

## What it measures

Each game server sends state packets at some cadence. If that cadence is periodic, its spectrum shows a sharp peak, and the peak position is the frequency.

Whale Song reports, per match:

- **batches per second** — the server's state packet cadence
- **confidence** — `trusted` / `reference` / `undecidable`
- **variation check** — did the rate change mid-match
- **stalls** — when packets stopped, and for how long

## What it does NOT claim

- **batches ≠ engine tick.** Passive capture cannot separate "packets per second" from "simulation ticks per second".
- **Multiplexed flows are undecidable.** Several logical streams flattened into one flow are reported as `undecidable`.
- **Changes under ~10 seconds are invisible.**
- **Packet loss is over-reported.** It includes real network loss *and* the server sending less.

## Install

1. Download `WhaleSong-1.0.zip` from [Releases](../../releases)
2. Verify SHA-256 (see the release notes)
3. Extract anywhere and run `WhaleSong.exe` (Windows 10/11)

Interface is available in Chinese and English (toggle in the main window).
When the UI is English, a concise `report.en.md` is generated next to the Chinese report.

No Python installation required. The tool is **offline**: it never uploads anything by itself.

## Usage

1. Launch, choose an input method, press **Start**
2. Play one match
3. Press **Stop** — a report appears in 1–3 minutes

The in-app **Usage Guide** explains every button.

## Feedback

Open an issue, or attach a report file (no raw capture needed).

Report format: `report.md` + `tick.png` produced by the tool.

## Validation

| Test | Result |
|---|---|
| Loopback (synthetic 60/50/128 Hz) | error 0.0% |
| Ground truth (10% / 20% loss) | estimated 10.2% / 20.9% |
| Adversarial (6 fake-cadence traps) | all rejected |
| Regression suite | 17 checks |

## License

Documentation: CC BY-NC 4.0.
Binaries: free to use for personal, non-commercial purposes. Redistribution or modification without permission is not allowed. See [LICENSE.md](LICENSE.md).

## Links

- [中文说明](README.zh-CN.md)
- [Method](docs/method.md)
