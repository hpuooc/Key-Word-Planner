# Key Word Planner

An interactive planner for High Point University's paid search buy. Open `index.html` in a
browser, or use the hosted page. Everything runs client side, no build step, no dependencies.

## What it does

- Check the search terms you want and the cart totals spend, impressions and clicks against a
  $10,000 monthly budget.
- Type any percentage in the Share column to control how much of a term's search volume you
  capture. The cost per click moves with it.
- Click any search term to preview the ad, rendered as a mock Google results page.
- Download the selected terms as CSV.

## How the pricing model works

Google reports a range for every search: the cheapest and the most that advertisers have paid
for a top-of-page click. Winning a small slice of a search is cheap. Winning most of it means
outbidding everyone else, so the price climbs toward the top of that range.

The planner prices each term as `low + (high - low) x share^curve`. The three buttons in the
cart set the curve:

| Button | Curve | Meaning |
|---|---|---|
| Best case | 2.2 | Clicks stay cheap until we chase the last few searches |
| Likely | 1.5 | Price rises steadily as we go after more of a search. Default |
| Cautious | 1.0 | Price rises in step with share from the very start |

Clicks assume 3.5 per 100 impressions on non-branded terms and 10 per 100 on searches for our
own name.

## Where the data comes from

Search volumes, competition and both bid figures: Google Keyword Planner, United States,
August 2025 through July 2026, pulled from HPU's Google Ads account 25 August 2026.

Ad copy is drawn from live highpoint.edu pages. Each preview names the page a claim came from.

## Constraints baked into the ad copy

These are not style preferences. Read the flag on any preview that shows one.

- **Nursing.** The BSN holds NC Board of Nursing full approval and is *pursuing* CCNE
  accreditation. Never write "accredited," "nationally accredited," "fully accredited,"
  "direct admit" or "guaranteed admission." Always name the inaugural 2024 cohort alongside
  the 100% NCLEX figure.
- **Engineering.** Only the B.S. in Computer Science carries an ABET accreditation statement.
  Mechanical Engineering and Mechatronics reproduce ABET curriculum criteria, which is not the
  same thing.
- **Business.** No AACSB or ACBSP accreditation. Do not imply one.
- **Placement.** Use 99% and 13 points above the national average. Do not use 99.2% or the
  14-point framing.
- **Pharmacy.** No licensure or pass-rate claims. **Optometry.** Do not advertise.

Two terms are marked do-not-run: `accelerated nursing programs` and `direct entry bsn`. HPU
offers neither, and bidding on them invites a misrepresentation complaint under 34 CFR 668.72.

## Bidding strategy

The audience section is a table of bid adjustments. Google only honors those under manual
bidding. Under Smart Bidding (Maximize Conversions, Target CPA, Target ROAS) it discards
location, demographic, audience and ad-schedule adjustments and decides on its own. Launch on
manual or enhanced CPC. Revisit once conversion volume can support Smart Bidding.

Verified against Google Ads Help, 31 August 2026:

- Search campaigns support affinity, detailed demographic, in-market and your-data segments.
- Search campaigns do **not** support custom segments or life events, so competitor-browsing
  audiences cannot be built here. Buy the comparison queries as keywords instead.
- Search demographic targeting covers age, gender and household income. Parental status is not
  in that table, so parents of teenagers are added as a detailed demographic audience segment.

## Editing

`index.html` is a single self-contained file. The two data structures near the top of the
`<script>` block are the ones worth knowing:

- `POOL` — one object per search term: volume, bid range, competition, default share, HPU
  program and landing page.
- `AD` — one object per term id: three headlines (30 character cap), two descriptions (90
  character cap), display path, final URL, claim source and an optional compliance flag.
