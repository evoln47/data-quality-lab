# Survey Data Quality Lab — Audited headline figures

Computed 2026-11-23 from the model code inside `index.html` itself. Method: the page's
`<script>` block was extracted and run headlessly in Node (vm module, no DOM), and the
script's own `auditFigures()` function produced every number below. The browser render
was then checked against these figures in headless Chromium screenshots at desktop and
phone widths; the §01 KPI row, the §02 table, and the §03 readout matched.

Defaults for every figure: speeder threshold 3.0 minutes, all five checks on where a
cleaned figure is named, provider prices $6.50 / $4.00 / $1.80, 2,400 raw completes per
provider, seed 20261123 (one stream per provider: 20261123, 20261124, 20261125).

## True values (attentive stratum mean, before any check)

| Provider | True value | Population value behind the stratum |
|---|---|---|
| Provider A | 37.25% | 38.0% |
| Provider B | 39.21% | 38.0% |
| Provider C | 37.92% | 38.0% |

The true value is a sampled mean over each provider's attentive respondents, so it moves
by sampling amounts between providers. The page's §05 notes state this.

## §01 default view (Provider B, all checks on, $4.00 per complete)

| Output | Figure |
|---|---|
| Completes surviving | 1,466 of 2,400 |
| Survival rate | 61.1% |
| Cost per usable complete | $6.55 |
| Headline, cleaned | 39.4% |
| Gap to the true value | +0.2 points |

Surviving composition at this setting: Attentive 1,424 (97.1%), Speeders 6 (0.4%),
Straightliners 0, Inattentive 36 (2.5%), Fabricated open-ends 0.

## Cleaning ladder by provider (threshold 3.0 minutes)

### Provider A (true value 37.25%)

| Level | Surviving | Survival | Headline | Gap | Cost per usable |
|---|---|---|---|---|---|
| Raw | 2,400 | 100.0% | 41.17% | +3.92 pts | $6.50 |
| Attention + speeder | 2,166 | 90.25% | 39.70% | +2.46 pts | $7.20 |
| Cheap + straightline + demographics | 2,005 | 83.54% | 38.15% | +0.91 pts | $7.78 |
| All five checks | 1,881 | 78.38% | 37.27% | +0.02 pts | $8.29 |

### Provider B (true value 39.21%)

| Level | Surviving | Survival | Headline | Gap | Cost per usable |
|---|---|---|---|---|---|
| Raw | 2,400 | 100.0% | 46.33% | +7.12 pts | $4.00 |
| Attention + speeder | 1,900 | 79.17% | 43.79% | +4.58 pts | $5.05 |
| Cheap + straightline + demographics | 1,659 | 69.13% | 41.71% | +2.50 pts | $5.79 |
| All five checks | 1,466 | 61.08% | 39.43% | +0.22 pts | $6.55 |

### Provider C (true value 37.92%)

| Level | Surviving | Survival | Headline | Gap | Cost per usable |
|---|---|---|---|---|---|
| Raw | 2,400 | 100.0% | 52.33% | +14.42 pts | $1.80 |
| Attention + speeder | 1,428 | 59.50% | 50.70% | +12.78 pts | $3.03 |
| Cheap + straightline + demographics | 1,082 | 45.08% | 45.29% | +7.37 pts | $3.99 |
| All five checks | 705 | 29.38% | 38.72% | +0.81 pts | $6.13 |

## §02 provider comparison (every check on, threshold 3.0 minutes)

| Provider | Price | Raw headline | Raw gap | Usable | Survival | Cost per usable | Cleaned headline | Cleaned gap |
|---|---|---|---|---|---|---|---|---|
| Provider A | $6.50 | 41.17% | +3.92 pts | 1,881 | 78.38% | $8.29 | 37.27% | +0.02 pts |
| Provider B | $4.00 | 46.33% | +7.12 pts | 1,466 | 61.08% | $6.55 | 39.43% | +0.22 pts |
| Provider C | $1.80 | 52.33% | +14.42 pts | 705 | 29.38% | $6.13 | 38.72% | +0.81 pts |

Accuracy bar behavior, verified from the same gaps: at the default bar of 2.0 points all
three providers meet the bar and Provider C takes the shaded cell at $6.13. At a bar of
0.5 points Provider C misses (gap +0.81) and the shaded cell moves to Provider B at
$6.55. That movement is the flip the section is built to show: the cheapest cost per
usable complete in the table stops being the cheapest cost among providers whose
headline sits within half a point of the truth.

## §03 coding example (computed from the 40 responses on the page)

| Step | Agreeing responses | Agreement rate |
|---|---|---|
| Step 0 · First pass | 22 of 40 | 55.0% |
| Step 1 · Codeframe clarified | 25 of 40 | 62.5% |
| Step 2 · Low-confidence routing | 28 of 40 | 70.0% |
| Step 3 · Disagreement sampling | 30 of 40 | 75.0% |

Program figures stated on the page, kept apart from the example: 55.0% and 75.3%.
