# Whale Song — Engineer Handoff

> Short version for other AI assistants / contributors.

## What it is
Windows tool that measures a game server's packet cadence (tick approximation) **passively**.
No injection, no memory reading, no game modification — only Windows built-in packet capture (pktmon) and timestamps.
One session = one capture (30–60 min) → `report.md`, `tick.png`, `report-brief.md`, `evidence.json`.

## Version
- 1.1.0 (build-20261023-c), package `WhaleSong-1.1.0.zip`
- GitHub: github.com/86dfj/whale-song (binaries + docs only, source is closed)
- Bilingual UI/report (Chinese default, English toggle)

## Pipeline
pktmon → network.etl → network.pcapng on stop → per-packet parse → group into UDP flows (5-tuple) → pick match segments → estimate tick/loss/jitter per segment → report + chart + evidence.
pktmon duplicates packets (2–6x), so packet counts are inflated; **tick is unaffected**.

## Algorithms
1. Spectral: FFT peak in 5–130 Hz; significance `snr` (random ≈10–14, >100 clear)
2. Windowed: 10 s windows, per-window tick/jitter/loss
3. Four estimators cross-checked; inconsistency downgrades to reference/undecidable
4. Harmonic parsing: main peak may be 2x/3x — use fundamental
5. One tick in two batches: lag-1 autocorr < -0.65 → real tick is half
6. Multiplexed flow: cadence flattened → undecidable; report gives inter-arrival peak as a *reference only*
7. Loss = missing share inferred from cadence (network loss + server batching), higher than in-game loss
8. Stall attribution: gaps ≥2 s, decide server-not-sending vs local link drop

## Segment rules (lobby vs match)
tick 10–130 Hz, loss <40%, continuous ≥60 s, periodic peak present.
Lobby heartbeats (1–5 Hz), loading screens, store traffic fail these. Risk: 60 s idle in lobby can be misread as a segment.

## Verdicts
- trusted: snr ≥100 and estimator diff <5%
- reference: snr 25–100 or flattened by jitter
- undecidable: snr <25 or multiplexed

## Game identification
DNS queries (strongest), TLS SNI, IP ranges; custom map `games.json` (domain keyword → game).
Community labels merge at ≥5 votes and ≥60% agreement; local entries are trusted.

## i18n
Single translation layer `i18n.en(text)` (longest-phrase replace + regex fallbacks), applied to report output, GUI widgets/dialogs, console stdout, chart labels.
**When changing Chinese copy, update `en_phrases.py` / `en_app_phrases.py`.** Never translate parser regexes or comparison keys.

## Validation
- loopback synthetic 60/50/128 Hz: 0.0% error
- induced 10%/20% loss: estimated 10.2%/20.9%
- 6 adversarial cadence traps rejected
- 17 regression cases pass in both languages

## Field data
VALORANT: inter-arrival peak 7.7 ms ≈130 (official 128; multiplexed → undecidable)
Delta Force: ~60 (Warfare) / ~120 (Space City)
Strinova: ~30
CS2: ~64

## Known pitfalls
- batches ≠ engine tick
- changes under 10 s invisible
- `settings.json` must be written without BOM
- locked `tick.png` breaks report regeneration
- embedded Python does not add the script dir to sys.path — app.py inserts it manually
- always package with `打包.py` (sets public channel, excludes author-only files)

## Principle
Slow is fine, few is fine, **fake is not**. Every number must be reproducible from the capture + scripts.
