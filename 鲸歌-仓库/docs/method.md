# Method

## Why passive capture

There are two ways to measure a server's update rate:

1. Read game memory / inject code — touches anti-cheat and modifies the game
2. Watch the network only — leaves the game untouched

Whale Song takes the second path.

## Principle

If state packets arrive at a periodic cadence, the sequence shows a sharp spectral peak:

- peak position → frequency (batches per second)
- peak width → jitter

To avoid relying on a single method, Whale Song runs four algorithms:

1. spectral peak detection
2. autocorrelation
3. inter-arrival statistics (median / mode)
4. cross-flow consistency check

When the methods disagree, the result is downgraded to `reference` or `undecidable`.

## Confidence levels

| Level | Condition |
|---|---|
| trusted | ≥3 methods agree and significance is high |
| reference | 2 methods agree, or sample is small |
| undecidable | flow too mixed, jitter too high, or not enough samples |

## Validation

| Test | Method | Result |
|---|---|---|
| Loopback | synthetic streams with known frequency | error 0.0% |
| Ground truth | 10% / 20% deliberate loss | estimated 10.2% / 20.9% |
| Adversarial | 6 fake-cadence traps | all rejected |
| Regression | 17 fixed cases | all pass |

## Known limits

- batches ≠ engine tick
- multiplexed flows are undecidable
- changes under ~10 s are invisible
- packet loss is over-reported (network loss + server sending less)
