# Signal Deck — corrections and method notes

Standing method file for the scheduled refresh of `index.html`, published by GitHub Pages
at https://stevenchristiian.github.io/claudesignal/.

**Status of this file:** created 2026-09-21 06:00 UTC; last updated 2026-09-29 02:00 UTC. The routine prompt instructs the run to
read this file and the newest file in `notes/runs/` first. Before this date **neither existed** —
the `notes/` tree was absent from every branch of the repo, so the first several runs had to
back their baseline out of the deck prose itself. Everything below is reconstructed from the
Sept 16 and Sept 21 builds plus this run's own verification. Keep it current.

---

## 1. Repository and publishing

- Repo: `stevenchristiian/claudesignal`. Pages serves **`index.html` on `main`**, nothing else.
- **A snapshot file is not a publish.** On 2026-09-21 the repo contained
  `signal-deck-2026-09-21-0100utc.html`, a complete and more recent build uploaded as a *separate
  file* (commit `d8ff50c`). `index.html` was never updated, so the live site served the **Sept 16**
  deck for five days while a Sept 21 build sat beside it in the same directory. Two scores had
  moved in between (BTC -0.4 -> -0.3, ETH +0.3 -> +0.4) and the public page showed neither.
  **Always write the build into `index.html`.** Dated snapshots may be kept alongside it, but the
  run is not finished until `index.html` changes and the live bytes match.
- Always verify the publish by re-fetching the live URL and comparing the served bytes to the
  built file. Never report success on exit status alone. Pages takes ~1 minute; re-check.

## 2. Score baseline

As published 2026-09-29 02:00 UTC (**six holds; no score moved — third consecutive all-hold run**):

| Asset | Score | Held since |
|-------|-------|-----------|
| BTC   | -0.3  | Sept 20 (restored from -0.4 on the Sept 18 flow print) |
| ETH   | +0.4  | Sept 20 (restored from +0.3 on the Sept 18 flow print) |
| SOL   | +0.5  | Sept 22, 02:00 (remaining 0.1 restored on the completed $60.7M week to Sept 18) |
| BNB   | **0.0** | Sept 26 (0.1 restored on the relative branch). **Branch armed at -1.69pt; margin -0.9591pt on 2026-09-29, a 0.7309pt move, did not fire.** See §3. |
| XRP   |  0.0  | 14 consecutive runs |
| HYPE  | -0.1  | unchanged since the HIP-3 revenue cut |

Scale is **-2 to +2**. Move a score only when a written branch threshold below fires. Diff against
this table, **not** against the served page — the served page can be stale (see 1).

## 3. Live branch thresholds

- **BTC flow leg** — re-cut on one settled session below **-$300M**, or two consecutive sessions
  each below **-$150M**. Restored 2026-09-20 on the Sept 18 print of +$433.0M.
- **BTC Fed leg** — October priced **above 75%** on *two independently routed* instruments cuts
  0.1; **below 40%** on two restores it. Two routes currently used: Polymarket (prediction market)
  and centralbank.watch (fed funds futures-derived). Both must agree for the branch to fire.
  **2026-09-26: a named, dated instrument cleared the bar and the branch correctly did not fire — and that
  now needs a decision.** Both named routes **fell** (Polymarket 66.5 -> **64.5%**, centralbank.watch 69.5 ->
  **61.6%**) while **CME FedWatch read 75.8%** for a 25bp hike as of Sept 25 (77.5% on Sept 24). CME is not
  one of the two named routes, so per §5.5 it cannot fire the branch, and it did not. But this is no longer a
  technicality: **CME FedWatch and centralbank.watch are both fed-funds-futures-derived — i.e. not
  independently routed from each other — and they disagreed by 14.2pt on the same underlying.** One of them is
  mis-measuring, and the branch reads the lower one.
  Also **the route spread reversed for the first time**: sequence 1.4 -> 3.2 -> 2.2 -> 1.5 -> 4.9 -> 3.0 ->
  **2.9 with the lead changing hands**, Polymarket now the higher. Every prior run had centralbank.watch
  leading toward 75.
  **Open question for the user (do not decide it unilaterally): add CME FedWatch as a third route, replace
  centralbank.watch with it, or keep it excluded?** Until answered the branch reads the two named routes only.
  **2026-09-29 reading: Polymarket 68.5% (up 4.0pt), centralbank.watch 67.6% (up 2.2pt), CME FedWatch 72.3% (DOWN 3.5pt).**
  Higher named route **6.5pt short**, against 9.6 the day before — the largest move toward the bar in this series, and still
  not close. **The decisive change is on the unnamed route: CME has fallen BELOW the 75% bar for the first time**, and the
  CME-vs-centralbank.watch gap has closed **14.2 -> 10.4 -> 4.7pt**, entirely by CME coming down rather than the named routes
  rising. **This weakens the case that one instrument is mis-measuring** — a fast curve read at different moments now fits
  better than a measurement defect — so the route-set question is still open but **no longer urgent**. Named spread **0.9pt**
  with the **lead reversed again** (Polymarket higher): sequence 1.4 -> 3.2 -> 2.2 -> 1.5 -> 4.9 -> 3.0 -> 2.9 (*reversed*) ->
  2.9 -> 0.9 (*reversed back*) -> **0.9 (*reversed again*)**, three swaps in four runs. centralbank.watch **advanced its stamp
  to Sept 28** after three days on Sept 25 — §5.3's "lags, does not stick" confirmed again.
  **2026-09-28 reading: Polymarket 64.5% (unchanged), centralbank.watch 65.4% (up 3.8pt), CME FedWatch 75.8%.**
  Higher named route **9.6pt short**. Two things changed and both cut against the "one of them is mis-measuring"
  framing slightly: the **named-route spread collapsed to 0.9pt**, the closest in this series, with the **lead
  reversing back** to centralbank.watch (sequence 1.4 -> 3.2 -> 2.2 -> 1.5 -> 4.9 -> 3.0 -> 2.9 *reversed* -> 2.9 ->
  **0.9 reversed back**); and the CME-vs-centralbank.watch gap narrowed from **14.2pt to 10.4pt**. The decision is
  still open. Note the centralbank.watch move arrived **under an unchanged Sept 25 page stamp** — see §5.3.
- **ETH flow leg** — re-cut on two consecutive sessions each below **-$150M**.
- **ETH roadmap leg** — activation *and finality* on Sepolia Oct 6 adds 0.1; a slip, or a failure
  to finalise (including via the builder-griefing vector on enshrined PBS), cuts 0.1.
- **SOL flow leg** — the remaining 0.1 was **restored 2026-09-22** on the completed $60.7M week to
  Sept 18. Bar going forward: a weekly print **below $5M** re-cuts it. The instrument is the
  SoSoValue daily series (Farside's `/sol/` table agrees with it row for row — see 5.1).
  **Always confirm the week includes its Friday before comparing it to a bar.**
- **XRP** — a second cloture vote *passing* adds 0.2; the motion failing, or the window closing
  unused, cuts 0.1. **"The window closing unused" now has a date (fixed 2026-09-22): the Senate is
  due to leave Oct 1; reaching Oct 1 with no second cloture vote taken fires the 0.1 cut.** Before
  this it was an undated condition that could never fire, which is how a downside branch quietly
  becomes decorative.
- **BNB — branch WRITTEN 2026-09-23, live from the next run.** Sixteen runs with no numeric trigger
  was long enough. The old text ("a price response in either direction") fired on pure beta if read
  loosely: on Sept 21 all six set twenty-one-day highs and BNB rose +1.92%, which a naive absolute
  trigger reads as a move when BNB was in fact the *second weakest* of the six that day. So the
  branch is **relative**, as §3 proposed:

  > Compute BNB's return and the **median return of the other five** over a trailing **seven-day**
  > window of completed hourly candles. BNB **outperforming** that median by **more than 5
  > percentage points** adds 0.1; **underperforming** it by more than 5 points cuts 0.1. Re-arm after
  > either firing: a further move needs a fresh 5-point divergence measured from the new baseline.

  Rationale for the 5pt bar: the deck's noise floor is ~0.5pt on a 24-hour ordering, and a
  seven-day window is roughly an order of magnitude more variance, so 5pt is the smallest margin
  that is clearly not noise. **Do not apply this retroactively** — it is live from the run after it
  was written. Record the computed margin on every run whether or not it fires, so the bar can be
  re-tuned on evidence rather than on feel.

  **FIRED 2026-09-24, on its first live evaluation.** BNB +5.67% over the trailing seven days against
  a median of +14.65% for the other five (HYPE 17.03, SOL 15.66, XRP 14.65, ETH 10.27, BTC 10.23):
  margin **-8.99pt**, so 0.1 was cut and the branch **re-armed** from that baseline. Two things worth
  keeping. (a) **The margin cleared the bar by 1.8x**, which is mild evidence the 5pt bar is set
  conservatively rather than loosely — do not loosen it on one observation, but do keep recording the
  margin. (b) **The relative framing was vindicated against the absolute one within one day of being
  written:** BNB was *up* +5.67% on the week, so an absolute trigger fires nothing; what the branch
  caught is that BNB took a little over a third of the median peer's gain across a window containing
  both a broad rally and a sharp reversal. Note also that a 0.1 step does **not** cross a band —
  `macroWord()` maps [-0.2, +0.2] to "balanced" — so the card's plain-English label is unchanged at
  -0.1. Say so on the card rather than leaving a beginner hunting for a visible change.

  **DID NOT FIRE 2026-09-25, and the reason produced a new rule.** Margin **-5.61pt** against the -8.99pt
  baseline: a narrowing of 3.38pt, short of the fresh 5pt a further move needs. The score held and the
  branch stayed armed, now 1.62pt from a restore. **But the margin narrowed while BNB got worse.** BNB
  fell from +5.67% to +4.74%; the median fell from +14.65% (XRP) to +10.35% (BTC) because the HYPE spike
  of Sept 23 rolled out of the trailing window, taking HYPE from strongest to second weakest of the five.

  > **Always decompose a margin change into the subject's move and the median's move before describing
  > it.** A relative branch measured against a median can revert most of the way toward its trigger while
  > the asset it judges deteriorates, purely through what *leaves* the window. Never report "the margin
  > narrowed" as "the asset recovered".

  This also refines the open question of whether the seven-day window is too short. The reversion was
  **not** BNB recovering, so it is not evidence the window is reading a single bad week. It is evidence
  that a **median of five** is a noisy reference when one peer carries a rolling spike. Different
  diagnosis, different fix; do not change the window on this observation.

  **FIRED A RESTORE 2026-09-26 — and the branch is now demonstrated to be capable of firing backwards.**
  Margin **-1.69pt** against the -8.99pt baseline: a fresh **+7.30pt**, clearing the 5pt bar by 2.30, so 0.1
  was restored (score **0.0**) and the branch re-armed at -1.69pt. **The written rule fired and the score
  was moved, because a written rule is what moves scores here.** But read what fired it:

  | Component | Sept 25 | Sept 26 | Change |
  |-----------|---------|---------|--------|
  | BNB 7d return | +4.74% | **+1.76%** | **-2.98pt (worse)** |
  | Median of other five | +10.35% | **+3.46%** | **-6.89pt** |
  | Margin | -5.61pt | **-1.69pt** | +3.92pt |

  BNB **fell** over the week and remains the **second weakest of the six** on seven days. The entire
  narrowing came from the peer median, and the mechanism was roll-off: the **Sept 18 -> Sept 19** session
  left the trailing window, and it was broadly strong (+10.73% SOL, +8.27% XRP, +7.39% HYPE, +6.42% ETH,
  +6.00% BTC) while **BNB took +2.59% of it**. Dropping a day on which the subject badly lagged narrows a
  relative margin without the subject doing anything.

  > **The defect, stated generally: a trailing-window relative branch can fire in the direction opposite to
  > the subject's own movement, purely through roll-off.** Two consecutive runs saw the margin narrow while
  > BNB deteriorated; on the second it moved the score. A branch that restores a handicap on evidence
  > confirming the handicap is mis-specified.

  **DID NOT FIRE 2026-09-27 — and the SAME mechanism ran in the OPPOSITE direction, which settles the diagnosis.**
  Margin **-2.47pt** against the -1.69pt baseline: a move of only **-0.78pt**, far short of a fresh 5pt, so the score
  held and the branch stays armed at -1.69pt. Decomposition: **BNB was flat** (+1.76% -> +1.73%, -0.03pt) while the
  **peer median rose 0.73pt** (+3.46% -> +4.19%). And the driver was roll-off again — the session leaving the window
  (**Sept 19 -> Sept 20**) was broadly **weak**, median of the other five **-0.86%**, while **BNB gave up only
  -0.22%**, so BNB **outperformed the departing day by 0.64pt**. *Dropping a day the subject led widens a relative
  margin, exactly as dropping a day the subject lagged narrows it.*

  > **This is the mirror image of the 2026-09-26 firing, and two observations in opposite directions from one cause
  > make the defect structural rather than incidental.** The branch is substantially a function of *which day leaves
  > the window*, not of what the subject did inside it. **It therefore strengthens amendment option 2 specifically**
  > (measure the margin change only across days present in both windows), because option 2 is the only one of the
  > three that neutralises roll-off in **both** directions: option 1 (require the subject to contribute) would have
  > blocked the Sept 26 restore but says nothing about this run, and option 3 (a longer window) only dilutes the
  > effect. **Still the user's choice; the branch stands as written.**

  **BNB HAS NO FUNDAMENTAL OR ENFORCEMENT LEG AT ALL — found 2026-09-27, and it is the more basic defect.**
  A **US federal sanctions probe into Binance** (Manhattan US attorney + DOJ criminal division, reported Sept 22)
  arrived and **no written BNB branch could express it**, because every BNB branch is a price-divergence test.
  Four runs had been spent scrutinising the relative branch for mis-specification while the branch *set* had no leg
  for the category of news that actually turned up. **Generalise: audit what a branch set can express, not only
  whether its branches fired.** **Decision needed from the user:** does BNB get a regulatory/enforcement leg, and on
  what dated instrument? A charging decision, a plea, a monetary penalty above a threshold and a formal closure are
  all dated and checkable.

  **DID NOT FIRE 2026-09-28 — and the roll-off split was MEASURED for the first time, which defeats amendment option 1.**
  Margin **-3.3884pt** against the -1.69pt baseline: a move of **-1.6984pt**, short of a fresh 5pt, so the score held and
  the branch stays armed at -1.69pt. Decomposition: **BNB fell 1.78pt** (+1.73% -> **-0.05%**, its first negative week in
  this series) while the **peer median fell 0.86pt** (+4.19% -> +3.34%, BTC both runs). **The subject moved in the same
  direction as the margin** — which is exactly what option 1 would require before letting the branch fire. **It passes,
  and the move is still mostly roll-off.** Splitting the window three ways (the previous window was independently
  recomputed from this run's own candles and returned **-2.4669pt**, matching the recorded -2.47pt):

  | Window | Span | Margin | Step |
  |--------|------|--------|------|
  | Old 7d | Sep 20 01:00 -> Sep 27 01:00 | **-2.4669pt** | — |
  | **Overlap 6d** | Sep 21 01:00 -> Sep 27 01:00 | **-4.4129pt** | removing the departing day: **-1.9460pt (ROLL-OFF)** |
  | New 7d | Sep 21 01:00 -> Sep 28 01:00 | **-3.3884pt** | adding the new session: **+1.0246pt (NEW INFO)** |

  **The two components point in opposite directions and roll-off is 1.90x the new information.** And the direction
  agreement option 1 tests for is itself an artefact: **BNB was the best of the six on the only genuinely new day**
  (+0.04% against a peer median of -1.23%, **1.27pt ahead**) and its seven-day return *still* fell, because the day that
  dropped out was a **+1.82%** session for BNB against a peer median of +0.74%.

  > **Option 1 is empirically defeated.** It tests one roll-off-driven number (the subject's own window return) against
  > another (the margin). When the departing day dominates both, they move together and the filter passes while
  > measuring nothing. **Option 2 — measure the margin change only across days present in both windows — is the only
  > one of the three that addresses the cause.** Three consecutive runs are now roll-off-dominated (09-26 fired a
  > restore on it, 09-27 held on it, 09-28 measured it). **Compute the overlap-window margin every run** — it is what
  > makes the split measurable rather than arguable.

  **DID NOT FIRE 2026-09-29 — and the direction test flipped, which finishes off amendment option 1.**
  Margin **-0.9591pt** against the -1.69pt baseline: a move of **+0.7309pt**, far short of a fresh 5pt, so the score held and
  the branch stays armed at -1.69pt. Three-way split, computed as the 09-28 entry requires:

  | Window | Span | Margin | Step |
  |--------|------|--------|------|
  | Old 7d | Sep 21 01:00 -> Sep 28 01:00 | **-3.3884pt** | — (independently recomputed from this run's own candles; **matches the recorded -3.3884pt exactly**) |
  | **Overlap 6d** | Sep 22 01:00 -> Sep 28 01:00 | **+0.3145pt** | removing the departing day: **+3.7029pt (ROLL-OFF)** |
  | New 7d | Sep 22 01:00 -> Sep 29 01:00 | **-0.9591pt** | adding the new session: **-1.2736pt (NEW INFO)** |

  **Fourth consecutive roll-off-dominated run: opposite signs again, roll-off 2.91x the new information.** The departing
  session (Sep 21 -> Sep 22) was strong and BNB badly lagged it (**+1.92% against a peer median of +5.71%**), so dropping it
  narrowed the margin while BNB did nothing.

  > **The direction test flipped, and that settles amendment option 1.** BNB's own 7d return **fell 3.91pt** (-0.05% ->
  > -3.96%) while the margin **improved 2.43pt** (-3.39 -> -0.96): **opposite directions**, so option 1 would have BLOCKED
  > this run — having *passed* the previous run on a move that was 1.90x roll-off. **Two consecutive runs, opposite verdicts,
  > one cause.** A filter that blocks and passes on the same underlying phenomenon is not measuring that phenomenon; it is
  > measuring which day left the window, because the subject's own window return is itself roll-off-driven. **Option 2
  > (measure the margin change only across days present in both windows) remains the only one addressing the cause.**
  > Still the user's choice; the branch stands as written.

  **Do not patch this retroactively and do not un-fire the Sept 26 restore.** Amendment options, ranked, for
  the user to choose: (1) require the subject's own return to move in the same direction as the margin by
  some fraction of the divergence — targets the observed failure directly; (2) measure the margin change only
  across days present in *both* windows, so roll-off alone cannot fire it; (3) lengthen the window to 14 or 21
  days — blunter, and the 2026-09-25 diagnosis (roll-off of a peer spike, not a short window) argues it is
  treating the wrong cause. **Until the user chooses, the branch stands as written.**
- **HYPE, disclosure leg** — moves on a **disclosed fee split or protocol revenue term** on the
  Payward/Bitnomial HIP-3 deployment. As of Sept 21 the absence is confirmed by the counterparty, not
  merely unfound. This leg is **roughly a year long** (CFTC/SEC process estimated at 10-12 months),
  so it will not resolve on this routine's cadence. Kept, but it is not the working branch.
- **HYPE, revenue leg — WRITTEN 2026-09-23, live from the next run.** The -0.1 handicaps *protocol
  revenue erosion from HIP-3*, but until now the only branch named one deal and one disclosure, so
  evidence landing squarely on the thesis kept firing nothing (native lending drew **$269M on day
  one** on Sept 18; 2026 year-to-date on-chain revenue leads all of crypto at **$429M** through
  Sept 15). A branch that cannot fire is not doing work. So:

  > The instrument is **reported quarterly protocol revenue**, the series carrying $356.7M (Q3 2025)
  > and $201.8M (Q2 2026). A subsequently reported quarter **above $260M** restores 0.1 (erosion
  > arrested); a reported quarter **below $150M** cuts a further 0.1 (erosion deepening). Quarterly
  > prints only — the figure must be for a completed quarter and attributed to a named publisher.

  Rationale for the bars: $201.8M is the live level; ~$260M and ~$150M sit roughly 30% either side of
  it, wide enough that ordinary quarter-to-quarter variance does not fire the branch.

  **Tested and correctly refused to fire, 2026-09-24 — the "quarterly prints only" wording did real
  work on its first live run.** DefiLlama carries **$77.61M fees / $60.58M protocol revenue on a
  trailing 30 days**, plus annualised rates of **$919.22M / $694.51M**. The 30-day figure annualises
  to roughly **$181M a quarter**, which sits *inside* this branch's $150M-$260M corridor and is
  therefore exactly the kind of number that gets waved through as "close enough". It is not a reported
  completed quarter and was not substituted for one. **A trailing window and an annualised run rate
  are each a different series from a quarterly print**, in the same family of error as §5.5's
  YTD-vs-quarterly entry.
  **SERIES FILLED IN 2026-09-25, and it produced the sharpest wrong-object case yet.** An OAK Research
  report **dated Aug 27, 2026** carries the intervening quarters, so the full reported-quarterly series is
  **$356.7M (Q3 2025) -> $295M (Q4 2025) -> $217.5M (Q1 2026) -> $201.8M (Q2 2026)**, a ~43% decline in
  under a year, monotonic through every quarter in the series. **Q4 2025 at $295M is above the $260M
  restore bar and must not fire it.** The branch says a *subsequently* reported quarter, and Q4 2025 is
  **earlier** in the series than the Q2 2026 level the handicap is set against. Firing a restore on it
  would read confirmation of the erosion thesis as its refutation — it would **invert the signal**. The
  live instrument is **Q3 2026**, which ends Sept 30 and reports in October.
  **Generalise this, because it is a new shape.** The earlier near-misses (YTD cumulative, trailing
  30-day, annualised run rate) were the wrong *series* or the wrong *units*. This one is the **right
  series, right units, right side of the bar, and still the wrong object — because of its position in
  time.** A bar comparison needs three things checked, not two: the series, the units, and *which period
  the figure belongs to relative to the level the handicap is set against*.
  **Also not a disclosure (2026-09-25).** The standard HIP-3 configuration is now documented — a deployer
  stakes **500,000 HYPE**, users pay roughly **twice** native perp fees, fees split **50/50** between
  protocol and deployer, and a Growth Mode cuts protocol fees **90%**. That reads exactly like the
  disclosure leg firing. It is the **framework default applying to every builder**, not a term of the
  Payward/Bitnomial deal, which remains undisclosed. Cost of revenue has risen from under 6% of gross
  revenue (Q2 2025) to ~18%.
  **Object check built into this branch — the one that will break it if ignored:** the $429M figure is
  **2026 year-to-date on-chain revenue**, a different series from quarterly protocol revenue. Never
  compare a YTD cumulative to a quarterly level, and never difference them. See §5.5.

- **HORMUZ / macro — branch WRITTEN 2026-09-25, live from the next run.** Third run of asking, and the
  answer is to write it rather than leave the largest macro input on this deck unable to move any score.

  > **Instrument: the IMF PortWatch daily transit count for the Strait of Hormuz, against its 85/day
  > pre-crisis baseline** (portwatch.imf.org; MacroMicro mirrors the series). Observations carried: **6 on
  > Sept 6, 8 on Sept 13, 1 on Sept 20** — published at roughly weekly intervals in practice.
  > - **Above 20/day on two consecutive published observations** adds **+0.1 to BTC** (a phased reopening
  >   taking hold, which is the form currently under negotiation).
  > - **Above 40/day on two consecutive published observations** — roughly half the baseline — adds
  >   **+0.2 to BTC and +0.1 each to ETH and SOL**, superseding the step above rather than stacking on it.
  > - **Zero transits on two consecutive published observations** cuts **0.1 from BTC**.
  > - Re-arm after any firing: a further move needs a fresh threshold crossing from the new baseline.

  **Two rules built in deliberately.** (a) **Only the transit count fires this branch.** A reported
  agreement, ceasefire, road map or reopening *offer* fires nothing, however formal and however many
  publishers carry it — see §5.5 on a reported offer not being an agreement. Naming a numeric instrument
  is the entire point. (b) **Two consecutive observations, not one**, because the series is published
  weekly-ish and a single print of 1 or 8 is inside the noise of a near-total stoppage.
  **CORRECTION 2026-09-28 — the zero condition is TWO observations away, not one, and this file said otherwise.**
  The condition is **zero transits on two consecutive published observations**. The series is **6 (Sept 6), 8 (Sept 13),
  1 (Sept 20)** and **none of those is zero**, so firing requires **Sept 29 and Oct 6 both to read 0**. The 09-26 and
  09-27 run files and §9's open items all said "one observation from the zero condition", which would only hold if
  Sept 20 had read 0. **A very low reading was treated as satisfying a condition written for zero. 1 is not 0, and a
  branch that names a number means that number** — the same discipline as §5.2's reported-0.0-vs-blank rule, one level
  up: **a near-miss on a threshold is a miss.** Note this was **inherited from these notes and repeated**, not drafted
  fresh, and check 9 caught it only because its grep runs over published strings regardless of a claim's origin.
  **Re-derive inherited claims, not only new ones.**
  **The downside remains live rather than decorative**, but it needs two readings: Breadth is intended — a genuine reopening is a broad risk-on macro input,
  not an asset-specific one.

## 4. The calendar trap (found 2026-09-21 — the big one)

**US ETF sessions settle on trading days only. Crypto spot trades every day. Do not mix them.**

The Sept 21 01:00 UTC build carried, for both BTC and ETH, a watch item reading *"Farside has still
not posted the Sept 19 session two days on"* and *"the Sept 19 BTC and ETH rows have still not
settled."* **Sept 19 2026 was a Saturday and Sept 20 a Sunday.** No session settled, no row will
ever post, and the deck was waiting on data that cannot exist — which silently froze both flow legs
as "untested pending data" when they were untested *by construction*.

Farside itself is the proof: its table carries trading days only, skipping **Sept 5-7** (Sat/Sun +
Labor Day Monday Sept 7) and **Sept 12-13** (Sat/Sun) in exactly the same way.

**Rule:** before writing that a flow row is late, run `date -u -d "2026-09-DD" +%A` on it. A weekend
or US market holiday is not a data lag. The next settled session after Friday Sept 18 is Monday
Sept 21, which settles after the US close (~20:00-21:00 UTC) — well after an early-UTC build stamp.

## 5. Source traps

### 5.1 The SOL "vendor conflict" was a truncated week, not a conflict (resolved 2026-09-22)
**This entry replaces the 2026-09-21 version, which reached the wrong explanation.**

For the week ending Sept 18 2026, two figures circulated for US spot Solana ETFs:
- **$13.2M** — 24/7 Wall St (Sept 19) citing **SoSoValue**.
- **$60.7M** — Solana Compass (Sept 20) citing **CryptoBriefing**.

The Sept 21 run reconciled the $47.6M gap to "one disputed **Thursday** session that SoSoValue
records as flat," declared a live vendor dispute, stood on the SoSoValue series and held the score.
**That was wrong.** Farside now publishes a Solana table (`farside.co.uk/sol/`: BSOL, VSOL, FSOL,
TSOL, SOEZ, MSOL, GSOL) and it reads, for that week:

| Mon 14 | Tue 15 | Wed 16 | Thu 17 | Fri 18 | Total |
|--------|--------|--------|--------|--------|-------|
| 11.0 | 1.3 | 0.8 | **0.0** | **47.6** (BSOL) | **60.7** |

- Farside agrees with SoSoValue on **every overlapping day** (11.01 / 1.35 / 836,926 / no change).
  Same series, not rival measurements.
- The $47.6M is on **Friday Sept 18**, not Thursday. Farside puts 0.0 on the Thursday, exactly as
  SoSoValue does. Reporting independently describes "BSOL alone attracted $48M in a single **Friday**
  session."

So **$13.2M was a four-day partial week** (Mon-Thu), published Sept 19 before the Friday row was in
hand. The whole "conflict" was 5.2 operating at the *weekly* level.

**Rules this produces:**
1. **Count the days in a weekly figure before comparing it to a bar.** A five-session week that lists
   four sessions is incomplete, however authoritative the vendor. Sum the dailies and check the
   Friday is present.
2. **A clean arithmetic reconciliation is not a correct one.** $13.2M + $47.6M = $60.8M ≈ $60.7M held
   perfectly while the *day* was wrong and the *conclusion* was wrong. Reconciling the magnitude of a
   gap does not identify its cause. Ask which session, and check it.
3. **Prefer a fund-level table to a headline total.** Farside's per-fund rows made this visible in
   one read; two headline totals could not.
4. **Three routes now exist for SOL**: SoSoValue (the named instrument), Farside `/sol/`, and
   CryptoBriefing. Farside is the easiest to read directly — see the access note in 8.

### 5.2 Farside rows settle incrementally and get revised
On Sept 16 this deck read ETH Sept 15 as **-$49.5M** from three posted lines and published it as the
session total. Farside now carries Sept 15 at **-$142.0M** across seven lines. A ~3x revision.
An early read of a same-day or previous-day row can be materially incomplete. Re-read prior rows on
each run; do not assume a published row is final. (The revised -$142.0M still sits above the -$150M
bar, so no leg fired retroactively — but it could have.)

**Measured on 2026-09-22 (the cleanest example yet).** The 02:00 build published the Sept 21 rows as
floors and named the funds that had not posted. Re-read at 07:00, **five hours later**:

| Row | 02:00 | 07:00 | Change | Filled in |
|-----|-------|-------|--------|-----------|
| BTC Sept 21 | +$617.6M | +$999.0M | **+61.7%** | IBIT +$381.4M |
| ETH Sept 21 | +$147.1M | +$270.0M | **+83.6%** | ETHA +$110.1M, ETHB +$12.8M |

**Measured again on 2026-09-24, larger still, and now a pattern rather than an incident.** The Sept 22
rows published as floors at 02:00 on Sept 23 were re-read 24 hours later:

| Row | Published as floor | Settled | Revision | Filled in |
|-----|-------------------|---------|----------|-----------|
| BTC Sept 22 | +$364.4M | **+$714.7M** | **+96.1%** | IBIT +$350.3M |
| ETH Sept 22 | +$71.3M | **+$162.2M** | **+127.5%** | ETHA +$88.1M, ETHB +$2.8M |

So the measured series of revisions is now **+61.7%, +83.6%, +96.1%, +127.5%** — and a row has more
than doubled. Crucially, **the late funds were the same ones all three sessions**: IBIT on the Bitcoin
table, ETHA/ETHB on the Ethereum table. Three consecutive sessions makes this **predictive, not just
possible**: when IBIT or ETHA shows a blank, expect the row to roughly double, and write the floor
accordingly.

**2026-09-25 destroyed the "roughly double" rule. A floor can be 2.4% of the row.** The Sept 23 rows
settled and the revisions dwarf everything above:

| Row | Published as floor | Settled | Revision | Floor as % of settled | Filled in |
|-----|-------------------|---------|----------|----------------------|-----------|
| BTC Sept 23 | +$32.4M | **+$346.9M** | **+970.7%** (10.7x) | **9.3%** | IBIT +166.3, FBTC +143.2, ARKB +5.0 |
| ETH Sept 23 | +$2.5M | **+$104.5M** | **+4,080%** (41.8x) | **2.4%** | ETHA +50.8, FETH +41.3, TETH +4.0, ETHV +2.9, EZET +3.0 |
| SOL Sept 23 | +$5.5M | **+$13.7M** | +149.1% (2.5x) | 40.1% | VSOL +1.5, FSOL +6.7 |

So the measured series is now +61.7%, +83.6%, +96.1%, +127.5%, **+149.1%, +970.7%, +4,080%**.

**Why the spread is so wide, and this is the rule that replaces "roughly double".** The multiplier is not
a property of the series — it is a function of *which* funds are blank and how large they are. The Sept 22
BTC row had **only IBIT** missing and revised 96.1%; the Sept 23 BTC row had **seven** funds missing and
revised 970.7%.

> **Never apply a flat multiplier to a floor. Weigh the blank funds by their `Average` column.** IBIT
> averages **$96.0M** a session and FBTC **$16.3M** on the BTC table; ETHA averages **$24.2M** and FETH
> **$4.5M** on the ETH table. A BTC row missing IBIT and FBTC is missing ~$112M of expected flow on an
> average day, which against a +$32.4M floor is not a downward bias — it is the whole figure.
> **The publishable statement is that a row with IBIT or ETHA blank carries almost no information until
> those funds report**, not that it will roughly double.

**The weighted rule passed its first live test, 2026-09-26 — keep it, but it is an estimate, not a bound.**
The Sept 24 rows settled and the weighted-blanks prediction beat the doubling rule on both series:

| Series | Floor | Blanks (Average) | Weighted predict | Doubling | Actual | Weighted err | Doubling err |
|--------|-------|------------------|------------------|----------|--------|--------------|--------------|
| ETH Sept 24 | +$39.3M | ETHA $24.2M, ETHB $6.2M | **$69.7M** | $78.6M | **+$66.1M** | **+5.4%** | +18.9% |
| BTC Sept 24 | +$28.1M | IBIT $96.1M | **$124.2M** | $56.2M | **+$190.7M** | -34.9% | -70.5% |

Revision series is now +61.7%, +83.6%, +96.1%, +127.5%, +149.1%, +970.7%, +4,080%, **+578.6% (BTC Sept 24)**,
**+68.2% (ETH Sept 24)**. Two things to carry: the weighted figure **still understated BTC by 35%**, because
IBIT printed $162.6M against a $96.1M average (1.7x), so treat it as a central estimate and never as a floor
on the floor; and **ETH's prediction was close partly because ETHB reported an explicit `0.0`** rather than a
number, which is the dash-vs-zero distinction paying off in the estimate itself.

**The weighted rule's error range is 0.7% to 59.7% ON THE SAME DAY (2026-09-27) — and the reason refines it.**
The Sept 25 rows settled: **BTC +$37.5M floor -> +$134.5M** (+258.7%) and **ETH +$4.7M floor -> +$87.0M** (+1,751%).

| Series | Floor | Blanks (Average) | Weighted predict | Doubling | Actual | Weighted err | Doubling err |
|--------|-------|------------------|------------------|----------|--------|--------------|--------------|
| BTC | +$37.5M | IBIT $96.1M | **$133.6M** | $75.0M | **+$134.5M** | **-0.7%** | -44.2% |
| ETH | +$4.7M | ETHA $24.2M, ETHB $6.2M | **$35.1M** | $9.4M | **+$87.0M** | **-59.7%** | -89.2% |

Weighted beat doubling on both, a second consecutive run — **and its own one-day error range spans two orders of
magnitude.** The cause is one level down: **a fund's own print is itself a multiple of its average.** IBIT printed
**1.01x** its average, ETHA **2.08x**, ETHB **5.15x**.

> **Refinement to publish with any weighted estimate: it is most trustworthy when the blank is ONE LARGE fund with a
> stable average, and least trustworthy when the blanks are SEVERAL, or SMALL.** A $6.2M average carries far less
> information about tomorrow than a $96.1M one. Never quote a weighted figure without saying which case it is, and
> never treat it as a bound.

Revision series now: +61.7%, +83.6%, +96.1%, +127.5%, +149.1%, +970.7%, +4,080%, +578.6%, +68.2%, **+258.7%**, **+1,751%**.
**Averages shift as rows settle** — after Sept 25 the BTC table reads total **$84.9M**, ETHA **$24.3M**, ETHB **$6.4M**.
Re-read the `Average` row each run rather than reusing yesterday's.
**A floor can also hide an acceleration, not just a magnitude:** the settled ETH Friday (+$87.0M) came in **larger than
the settled Thursday** (+$66.1M), up 31.6% — invisible while Friday read +$4.7M.

**"Late at read time" is not "blank for N sessions" (2026-09-25, caught by check 9).** A draft read *"IBIT
shows no figure for a fourth consecutive session"*. False: IBIT was blank for exactly **one** session and
had posted for the other three. The true statement is that IBIT has been **the late line at this deck's
early-UTC read time on four consecutive runs**. The pattern is about read timing, not a persistently empty
cell — and this is the §5.2 reported-zero-vs-blank error in a new costume.

So the size of the incompleteness is not marginal: **a floor can be 60-128% low within one morning.**
Two rules follow. Publish an incomplete row as a floor *and name the missing funds* — doing that is
what let this run measure the gap instead of discovering it. And never let an incomplete row be the
thing that fires or withholds a branch if the missing fund could cross it on its own.

**A reported 0.0 is not a blank (2026-09-24).** Farside distinguishes a fund that reported no flow
(`0.0`) from one that has not reported at all (`-`), and the deck must too. A draft line reading "only
MSBT has reported" was wrong on the Sept 23 BTC row, where BITB, BTCO, GBTC and BTC all carry an
explicit 0.0; the true statement is that MSBT was the only fund **above zero**. Check 9 caught it.
Collapsing the two states overstates how incomplete a row is and mis-names which funds are missing.

### 5.3 centralbank.watch updates its table without advancing its stamp
**Cleanest instance yet, 2026-09-28.** Read **65.4 / 34.6 / 0.0** at 02:08 UTC with the page stamp still reading
**Sept 25** — the same stamp it displayed the day before against **61.6%**. So the figure moved **3.8pt under an
unchanged stamp**. Plausible mechanism: fed funds futures reopened on Globex around 22:00 UTC Sunday, so roughly four
hours of trading preceded the read while the page's stamp lagged. **The rule is unchanged and was load-bearing here:
quote the read and the time you took it, never the stamp.** A run that trusted the stamp would have reported the Fed
leg as frozen for a third day when one of its two instruments had moved almost 4 points toward the bar.
Read **57.9 / 42.1 / 0.0** on Sept 21 01:00 and **55.9 / 44.1 / 0.0** on Sept 21 06:00 — both
displaying the **same "Sept 18" stamp**. The stamp does not date the figure. Quote the read and the
time *you* took it. **Update 2026-09-22:** read **55.7 / 44.3 / 0.0** at 02:10 UTC with the stamp now
advanced to **Sept 21**. So the stamp is not permanently frozen — it lags, sometimes by days. The
rule is unchanged (quote your own read time), but do not describe the stamp as stuck. The page states the policy rate (3.88%) correctly throughout; that anchor being
right does not certify the meeting table.

### 5.4 Prefer the Polymarket API over the rendered page
`https://gamma-api.polymarket.com/events?slug=<slug>` returns per-outcome prices **with an
`updatedAt` timestamp** — a live, dated read instead of a scrape. Slug for the October meeting:
`fed-decision-in-october-20260617190323537`. Read each leg separately: "increase by 25 bps",
"no change", etc. Earlier builds appear to have crossed the *hike* and *no-change* legs (a "44.5%
Polymarket read" was logged as superseded when 44.5% is the current **no-change** price).

### 5.5 Object checks that keep recurring
- **A PERMISSION WINDOW IS NOT AN EVENT** (2026-09-29, new shape). Coverage said Solana faced "a crucial test on
  Sept 28, when the Alpenglow upgrade is scheduled to begin rolling out". What Sept 28 is, on Anza's own software
  schedule, is the date feature activations are **tentatively allowed to resume**. Alpenglow is live on **devnet and
  testnet only**; **mainnet activation has no date**. Nearest relative is the 09-28 "a target is not a schedule", but
  that was a *target* read as a *schedule*; this is **a window in which something becomes permitted** read as the thing
  happening. Both directions of the family are now recorded. Ask what the date is a date *of*.
- **Scheduled supply is not claimed supply** (2026-09-29, HYPE). The Oct 6 core-contributor tranche is **9.92M HYPE**,
  part of a ~238M allocation over **24 even monthly tranches** (238/24 = 9.917M, consistent), nominally **~$860M**.
  But the **Sept 6 tranche of the same size was claimed far under schedule** — reported ~**0.19%** of supply against an
  intended **2.32%**. Publish the schedule; never publish it as though it were the supply reaching the market.
- **A recurring-trap counter may only be incremented on a VERBATIM match with a confirmed date** (2026-09-29). A draft
  claimed "the seventh time this deck has recorded" the CLARITY August countdown pieces. The run's search returned a
  stale-looking bitcoinfoundation.org item with **a different headline**, and its date was never checked. **A
  same-domain, same-topic, same-vintage piece is a candidate, not an instance.** The 09-25 entry said to record the
  domain and the date; this adds the **headline**, or the series counts things that were never the same object. The
  claim was cut. (By contrast the HYPE Aug 24 "$1.2B unlock days away" trap **was** a verbatim match and **is**
  countable: fourth instance, all four on finance.yahoo.com — 09-26, 09-27, 09-28, 09-29.)
- **Do not retroactively bless an unsourced count because the series caught up to it** (2026-09-29, SOL). On 09-28 the
  circulating "eleven days" of Solana inflows matched **neither** the strict inflow count (6) nor the non-negative count
  (10). Adding Monday Sept 28 moves both up one: **strict 7, non-negative 11**. The number now reconciles with one
  convention. **It was still not a verified figure when it was published** — it was a figure a later session happened to
  meet. Record which convention a count uses; that is what makes it checkable.
- **The $258.4M "Sept 25 BTC ETF outflow" claim resurfaced — second recorded appearance** (2026-09-29; first 09-26).
  The Farside Sept 25 row settled at **+$134.5M** and has never been revised. Still unsourceable. **Published as an
  explicit refusal on the card** rather than ignored, so a later run does not rediscover it as news. Table wins.
- **Farside publishes NO `/xrp/` page** (2026-09-29, checked directly — the page loads and carries no table). Working
  slugs are **`/btc/`, `/eth/`, `/sol/`, `/hyp/`** and that is the complete set. So the **$75.59M** weekly US spot XRP
  ETF figure and the **eleven-week** streak in circulation cannot be read at fund level; attribute, never adopt.
  **There is no XRP flow instrument on this deck**, which is why no XRP flow branch exists. Stop looking.
- **A near-miss on a threshold is a miss** (2026-09-28). See the Hormuz correction in §3: a reading of **1** was
  repeatedly written up as satisfying a condition specified at **0**. **Read the branch's number, not its spirit.**
- **Subtract the underlying values, never the rendered ones** (2026-09-28). A draft said the BNB peer median "fell
  **0.85** points from +4.19% to +3.34%". Subtracting the *displayed* endpoints gives 0.85; the derived figure is
  **4.1935 - 3.3380 = 0.8555 -> 0.86**. This is distinct from the 09-27 self-flattering-rounding catch and more
  tempting, because **the arithmetic on the page's own two numbers checks out** — a reader verifying it finds 0.85.
  Publish the regenerated figure and accept that the rounded endpoints will not reproduce it exactly.
- **A right figure attached to the wrong session** (2026-09-28). **$4.77M** circulated as a HYPE ETF inflow "on
  September 25". Farside carries **Sept 24 at +$4.8M** and **Sept 25 at +$3.2M**: the figure is real, the series is
  right, the units are right — the **session** is wrong. Nearest relative is the 09-27 "real past event re-dated
  forward", but that was an *event*; this is a *datum*. The table wins.
- **A streak count can depend entirely on the dash-vs-zero rule** (2026-09-28). Two Solana streaks circulated, **six
  sessions** and **eleven days**. Sept 17 carries an explicit **0.0**, and zero is not an inflow, so the **inflow**
  streak is exactly **six** (Sept 18-25, +$235.7M); counting **non-negative** sessions reaches back to Sept 14 and
  gives **ten**; **eleven reconciles with neither**. The §5.2 reported-zero distinction is doing *arithmetic* work
  here, not descriptive work — the same datum supports 6 or 10 depending on how the 0.0 is classed.
- **Assets under management is not cumulative net flow** (2026-09-28). BSOL described as holding "more than **$1.36B**"
  against Farside's **$1,218.5M** cumulative net flow for that fund. Assets include price appreciation. File as
  scope, like the HYPE open-interest entries, not as a conflict.
- **A true, current, on-topic fact about the WRONG INSTITUTION** (2026-09-28, and this is a new shape). Coverage
  reported that the **House** cancelled its voting weeks of Sept 21 and Sept 28 — true, and irrelevant to the XRP
  branch: H.R. 3633 has **passed the House** and the pending action is a **Senate** cloture vote, so a House calendar
  change cannot move the Oct 1 date. **Every recency trap recorded before this was about the wrong *time*; this is the
  wrong *body*.** Ask which institution a calendar fact governs before letting it touch a dated branch.
- **A publicly confirmed rejection is not a delivered one** (2026-09-28, the mirror of the 09-23 offer entry).
  Trump on the record — *They made a proposal but I rejected it* — on the Iranian seven-day Hormuz plan, carried by
  France 24, Al Jazeera, NPR, CNBC, NBC, CNN and The Hill. **Iran's foreign minister says no rejection came through
  official channels**: *nothing has yet been conveyed to us from the mediators*. Both states are real; publish both.
- **A search summary's claim about its own SOURCING is a claim to verify** (2026-09-28). A first summary asserted "no
  public statement has come from US authorities" about that rejection. False — a targeted follow-up found the
  on-the-record quote across seven outlets. **Verify the sourcing characterisation, not only the facts.**
- **A URL date slug is a usable tiebreak** (2026-09-28). Three report dates circulate for the Binance Iran probe —
  **Sept 21, Sept 22, Sept 24**. The Bloomberg and CoinDesk items carry **`/2026-09-22/`** and **`/2026/09/22/`** in
  their own URLs, so Sept 22 stands, which is also what the deck already carried (§5.5, check the event against the deck).
- **A primary can carry LESS than its coverage, and that cuts both ways** (2026-09-28). The Bitget support notice
  (Sept 26) carries the phased withdrawal schedule **exactly** — BTC Sept 28 08:00, ETH Sept 29, USDT Sept 30, the
  rest Oct 2 — and states **no loss total** and **names no attacker**. So the **$387.5M** and the North Korea
  attribution are secondary-only *on that document* and must be published attributed. The primary-wins rule is not
  only about secondary sources *adding* specifics; it also tells you which specifics the primary will not stand behind.
- **A percentage of a "more than X" denominator is an upper bound** (2026-09-28). Bitget's revised **$387.5M** is
  **83.51%** of a protection fund the exchange values at "**more than** $464M", so **83.5% is a ceiling on the share,
  not the share**. Publishers also carry **84%** (a rounding) and **$388M** (the same loss, rounded). Compute it
  yourself and say which direction the bound runs.
- **A target is not a schedule** (2026-09-28). Ethereum mainnet Glamsterdam is now widely described as **targeted for
  Q4 2026**; this deck had been saying **unscheduled**. Both are true and the distinction is load-bearing: **no branch
  can read a target with no date and no slot.** Do not let a target quietly upgrade into a scheduled event.
- **Stolen assets on a ledger say nothing about the ledger** (2026-09-28). Bitget's revised estimate spans networks
  **including the XRP Ledger**. That is where assets were custodied, not a defect in the ledger.
- **A day count that moved two days in twenty-four hours** (2026-09-28). straits.live's front page read **Day 211**
  against **Day 209** the day before; true elapsed from Feb 28 is **212**. Previous instances were cross-publisher
  (09-25) and within one domain at one time (09-27); this one is **internally inconsistent across time on the same
  page**, which no daily counter can be. Day counts stay unpublished — the file now has three independent proofs.
- **BNB 88.2%** — a share of *tokenized stock DEX volume*, for **BNB Chain + Robinhood Chain
  combined**, in a largely **non-US** market. It is not a single-chain share and not a share of the
  RWA market. The **SEC Innovation Exemption (Sept 17)** names no blockchain and no company — do not
  score it against the 88.2%. **Superseded for most purposes 2026-09-22:** reporting dated Sept 21
  gives the like-for-like figure directly — tokenized stocks **$3.5B** of market value, **BNB Chain
  $1.0B = 32.7%**, Ethereum $770.1M, Solana $715.9M (market was $3.1B on Sept 6). Quote **32.7% of
  market value** when the question is "how much of the tokenized-stock market is BNB Chain", and keep
  the 88.2% only when the subject really is DEX volume across the two chains. The lead survives; the
  magnitude was never seven eighths.
  **ARITHMETIC CORRECTION 2026-09-24 — the deck was publishing a division that does not hold.** The
  card read "$1.0B of a $3.5B tokenized stock market, a 32.7% share". **$1.0B / $3.5B = 28.6%.** The
  publisher that reports the $3.5B market (The Coin Republic, Sept 21) says BNB Chain is the only
  chain above $1B and computes **about 28.5%**; the **32.7%** sits beside Ethereum at $770.1M and
  Solana at $715.9M and implies **~$1.14B**, which is consistent with "above $1B" but not with the
  rounded $1.0B it was paired with. Both readings can be true — what was wrong was **asserting the
  division**. Publish "above $1B (about 28.5% on that publisher's arithmetic)" or "32.7%, implying
  ~$1.14B", never the three numbers as one sentence.
  **The general rule, and it is new:** *do not combine two figures from different sentences or
  different sources into an arithmetic claim that neither source makes.* Each figure can be
  individually defensible and the derived ratio still false. Before publishing "X of Y, a Z% share",
  divide it yourself.
- **A real past event re-dated forward onto a day that does not exist for it** (2026-09-27, and this is a NEW shape).
  A summary asserted *"The Senate rejected the CLARITY Act on September 26, 2026, which caused a sharp 10% price
  drop."* **September 26 2026 was a Saturday**; the Senate took no vote, and the real cloture failure is **Sept 15,
  49-50**. Every recency trap recorded before this was either a *stale* item looking current or a *current* item
  making an old event look new. This one moves a genuine past event **forward** onto an impossible date.
  **Run `date -u -d` on any asserted event date before assessing the content** — §4's weekday rule disproves a claim
  about a vote just as cleanly as it disproves a claim about an ETF row, and it is the cheapest check available.
- **THE PRIMARY WINS — now a standing check, not a per-story correction** (2026-09-27). Coverage held that **ACI
  Worldwide**, "carrying about **9%** of Swift payment traffic", had **enabled XRP** as a settlement option
  (*"SWIFT Partner Picks Ripple As Preferred Settlement Route"*). The underlying release (**Sept 22**) extends ACI
  Connetic to support payments orchestrated through the Swift ledger, and says the ledger is ready for initial use
  with **17 banks across six continents** piloting. **It names no blockchain, no digital asset — no XRP, no Ripple,
  no RLUSD, no XRP Ledger — and carries no share-of-traffic figure.** Both specifics are secondary additions.
  **Why this entry matters more than the item:** the same rule was recorded against the **SEC Sept 17** story and had
  started to look like a quirk of that one story. It has now fired on a completely unrelated one. **Fetch the primary
  before publishing any specific that only secondary coverage carries** — the addition is usually the number.
- **A cumulative total is not a quarterly print** (2026-09-27). A **~$1.31B** cumulative protocol revenue figure for
  Hyperliquid is in wide circulation. The revenue branch is written against **reported quarterly** protocol revenue.
  Fourth member of this family, after the $429M YTD cumulative, the trailing-30-day figure and the annualised run rate.
- **A running day count can contradict itself INSIDE one domain** (2026-09-27). straits.live headlines **"Day 209"**
  on its front page while its `/today` page says **"210 days"**; the true elapsed count from Feb 28 is **211**.
  Previous instances of this trap were *between* publishers (207 vs 209 on 09-25). An internal contradiction is
  stronger evidence than a cross-publisher spread that the count is **computed, not observed**. Day counts stay unpublished.
- **A fresh timestamp on a static price is not a new observation** (2026-09-27). Polymarket's `updatedAt` advanced to
  02:02:49Z on an **unchanged** 64.5%. Over a weekend neither a prediction-market book nor a fed-funds curve can move,
  so record "unchanged, read at HH:MM" rather than letting an advancing stamp imply a fresh reading.
- **The settle/intraday trap has one genuine exception, and it must be earned** (2026-09-27). tradingeconomics'
  "Actual" is normally an in-progress read. On a Sunday build, Friday's session closed two days earlier, so that
  Actual **is** a completed settle. Check the calendar and say why; never assume it.
- **The HYPE supply figures are two different objects** (2026-09-27, unresolved). **~251M circulating (26% of max)**
  against this deck's **222,445,714 = 22.24% released to date** — circulating supply and cumulative released supply
  are not the same series. A companion claim that core-contributor allocations are **locked until 2027-2028** sits
  awkwardly beside the **Oct 6 core-contributor unlock** the deck carries. **Published none of it as fact.** Source it.
- **BNB search pollution** — queries return presale promotion for unrelated tokens. Filter hard.
- **HYPE open interest** is carried at four different published values ($14.3B The Block Sept 8;
  $8.1B Pluang Sept 20 also called a record; and two earlier). Publish attributed, adopt none.
- **ETH devnet trap** — a third-party GitHub "slips again" release ranks highly and reads like the
  downside branch firing; its nine failed devnets are **Devnet-1 to Devnet-9**, not Devnet-11.
  Devnet-11 *did* run the Glamsterdam transition on **Sept 16** across ~84,000 validators.
- **Oil figures** — EIA's "~$90/b for 2H26" is a **forecast average** and "$91 in August" a
  **monthly average**; neither is a spot print. tradingeconomics "Actual" during a live session is
  an **in-progress read, not a settle** (a fetch helper may wrongly call it a settle — it is not).
- **$13.2M collisions** — the SOL weekly figure is not the **-$13.2M BTC daily** print of Sept 11.
- **Liquidation totals have a window, not just a publisher** (2026-09-22). For the Sept 21 squeeze:
  **~$313M in one hour, 96% shorts** (CoinGlass, via Yahoo) and **$769.80M over 24h across 115,490
  traders, ~85% shorts** (a second publisher). Not a conflict — two windows. Always state the window.
- **"All-time high" is not a claim this deck can make** (2026-09-22). The tape method reads a
  21-day window, so a 21-day high is all it can verify. HYPE printed 96.07 on Sept 21, above the
  94.46 that reporting on Sept 19 called an ATH — publish it as a twenty-one-day high and attribute
  any ATH language to whoever made it.
- **Hormuz: relative and absolute claims can both be true** (2026-09-22). CENTCOM's "highest in six
  months" for crude/cargo/LNG and IMF PortWatch's **8 transits on Sept 13 against an 85/day
  pre-crisis baseline** do not contradict each other — one is a change against a collapsed base, the
  other a level. Do not let a relative improvement read as a normal strait. Also: the best transit
  count available is typically **a week or more old**; attach its date.
- **"Since October 2025" is attached to two different objects** (2026-09-22). Searching the Sept 21
  BTC ETF session returned, from several publishers at once, both *"single-day high since October
  2025"* and *"strongest **weekly** inflows since October 2025"* at **$1.92B** — and that weekly
  figure does not match the week this deck can verify from Farside rows (**+$6.1M** for Sept 14-18).
  When a superlative circulates with two different windows attached and the arithmetic does not
  reconcile, publish neither. Say what your own source supports: Farside's `Maximum` row carries a
  larger daily total at **$1,373.8M**, so Sept 21 was big and not a record.
- **Overlapping windows are not consecutive observations** (2026-09-22). The 02:00 build said "a
  third consecutive 24-hour window with every name up". A build five hours later is tempted to write
  "fourth" — but the two windows share nineteen hours, so it is not a new observation. Either compare
  like for like against the previous build, or wait a full window before extending a streak count.
- **HYPE open interest has a scope, not just a publisher** (2026-09-23). A fourth value appeared,
  **~$2.04B early Sept 22** — and it is *not* a rival measurement of the $14.3B and $8.1B already
  carried. $2.04B is open interest in **HYPE perpetual contracts**; the larger figures are
  **platform-wide** across all Hyperliquid perps. Same shape as the liquidation-window entry above:
  state the scope, and do not file a narrower object as a conflicting estimate of a wider one.
- **HYPE revenue: two series, never differenced** (2026-09-23). **$429M** = 2026 **year-to-date
  on-chain revenue** (leads all of crypto through Sept 15, more than the next two combined).
  **$356.7M -> $201.8M** = **quarterly protocol revenue** (Q3 2025 -> Q2 2026). A cumulative and a
  quarterly level. Subtracting one from the other produces a number that means nothing, and the
  revenue branch in §3 is written against the quarterly series specifically for this reason.
- **The SEC Sept 17 action, mis-reported a second way** (2026-09-23). Coverage this week described it
  as "a ruling that named BNB Chain as one of three networks set to gain". It **names no blockchain
  and no company** — see the 88.2% entry above. That is now two distinct ways this one story has been
  mis-repeated (first as a BNB market-share proof, now as a document that names BNB). When a
  secondary source adds a specific the primary does not contain, the primary wins and the addition is
  worth recording, because it will recur.
- **"2026 high" and the all-time Maximum row are different windows, and both can be true**
  (2026-09-23). Reporting called BTC's Sept 21 **+$999.0M** a 2026 high; Farside's `Maximum` row
  carries **$1,373.8M**. Unlike the Sept 22 "since October 2025" case, this is **not** a contradiction
  to publish-neither on — the Maximum row does not say which year its day falls in, so a 2026 high
  and a larger all-time day coexist happily. Rule: before declaring two superlatives in conflict,
  check whether their windows even overlap. Say what your source supports (Sept 21 was large, a larger
  day exists) and decline to certify the window you cannot see.
- **The settle/intraday trap fired twice in one run** (2026-09-23). (a) Fortune's Brent figure of
  **$99.27** is explicitly an intraday level "as of 6 a.m. Eastern", not a settle. (b) The WebFetch
  helper, reading tradingeconomics, asserted its live figure "represents a completed session close" —
  **exactly the failure the oil entry above warns about, now observed rather than predicted.** Do not
  let a fetch helper's characterisation stand in for your own: treat TE's headline number as an
  in-progress read for the current day and its "previous close" as the prior day's close. Published
  Brent as "about $99" with the move (fifth straight session lower) attributed, rather than a settle.
- **A reported offer is not an agreement** (2026-09-23). Iran was reported on Sept 22 to have offered,
  **through mediators**, to reopen the Strait of Hormuz within seven days if the US lifts its naval
  blockade. That is a proposal relayed by third parties; the strait is still shut. A de-escalation
  headline must not be published as de-escalation. The deck carried the item and a separate catalyst
  line stating the qualification, so the two cannot be read apart.
- **A figure can be the right series, right units, right side of the bar and still the wrong object —
  because of *when* it is from** (2026-09-25, and this is the sharpest wrong-object case the deck has
  produced). HYPE's revenue branch restores 0.1 on a *subsequently* reported quarter above $260M. The
  intervening quarters arrived and **Q4 2025 reads $295M**, clearing the bar. It must not fire: Q4 2025 is
  **earlier** in the series than the Q2 2026 level the handicap is set against, and the full series
  ($356.7M -> $295M -> $217.5M -> $201.8M) is a monotonic *decline*. Firing a restore would read
  confirmation of the thesis as its refutation. **Check three things against a bar, not two: the series,
  the units, and which period the figure belongs to relative to the level the handicap is set against.**
- **A framework default is not a deal disclosure** (2026-09-25). HYPE's disclosure leg needs a fee split
  on the **Payward/Bitnomial** HIP-3 deployment. Reporting gives the standard HIP-3 configuration instead:
  stake 500,000 HYPE, users pay ~2x native perp fees, fees split **50/50** protocol/deployer, Growth Mode
  cuts protocol fees 90%. That reads exactly like the branch firing. It applies to **every builder** and
  says nothing about that deal. When a branch names a counterparty, a parameter of the framework the
  counterparty will use does not satisfy it.
- **A branch's threshold can be cleared by a real, named, dated instrument that the branch does not name**
  (2026-09-26, and this is a sharper case than the unnamed-instrument one). **CME FedWatch read 75.8%** for an
  October 25bp hike, above the Fed leg's 75% bar, while both named routes read 64.5% and 61.6%. Unlike the
  2026-09-24 CoinDesk 73.1%, this figure names its instrument, carries a date, and is arguably the most cited
  route for the question. **It still must not fire a branch that names its routes.** The rule holds — but when
  this happens, say so on the card rather than quietly declining, and escalate the route set as an open
  decision. A branch whose named instruments diverge 14pt from an equivalently-derived one is not merely unfired.
- **A relative branch can fire in the direction opposite the subject's own move** (2026-09-26). See the BNB
  entry in §3. Roll-off of a strong day the subject lagged narrowed the margin 7.30pt and restored a handicap
  while BNB itself fell. Generalise: **before a relative branch fires, check that the subject moved the way the
  margin did.** If it did not, the firing is an artefact of the window, not a signal.
- **Three instruments for one geopolitical question, three baselines** (2026-09-26, Hormuz). **PortWatch daily
  transit calls: 1 on Sept 20 against 85/day** (the branch's instrument). **Kpler crude volume: 33.7M bbl for a
  partial week from Sept 20, 19 tankers of which 17 VLCCs, against 49.2M bbl for the full prior week.**
  **Reuters/US official: 9 commodity vessels and 8 exits on Sept 25, against ~125 large commercial vessels a day
  pre-crisis**, plus "highest daily crude volume since early July" on Sept 24 with **no figure attached**. None of
  these is a rival measurement of another: different units, different scopes, different baselines, different
  cadences. Only the transit count fires the branch. Two traps inside this: the 33.7M-vs-49.2M comparison is a
  **partial week against a full one** (§5.1 rule 1, and two search summaries drew opposite conclusions from it, so
  publish neither), and a **qualitative superlative with no number** is an attribution, not a datum.
- **An ETF flow figure that contradicts the table, and could not be sourced** (2026-09-26). A search summary
  asserted "spot Bitcoin ETFs recorded **$258.4M in net outflows on September 25**" against a Farside Sept 25 row
  of **+$37.5M**. A targeted search returned nothing carrying $258.4M; the nearest real figure is a **$236.5M
  outflow on Sept 1**. Not published. **When a flow figure contradicts the fund-level table, the table wins and
  the figure needs its own source before it is repeated** — and check whether it would even fire a branch (this
  one would not: the bar is one session under -$300M or two under -$150M).
- **A number rounded toward the argument it supports** (2026-09-26, check 9). A draft said the weighted-blanks
  prediction landed "inside 5%" of the settled ETH row. The actual overshoot is **5.45%** — just outside, on
  either denominator. The claim was flattering to the very method the paragraph was arguing for, which is exactly
  why it slipped through. **Add to check 9: for every margin that makes a case, recompute it and check the
  rounding does not favour the case.** This is a different failure from the count-and-ordinal family; the number
  was nearly right and directionally self-serving.
- **A superlative this deck CAN verify, and the test for it** (2026-09-26). Sept 25's Solana session of
  **+$86.7M equals the `Maximum` row of the Farside Solana table**, so it is the largest single session in that
  series *on the table publishing it*. Unlike "since October 2025" or "highest since January", this is
  publishable because **the bound and the observation come from the same source**. That is the test: not how long
  the window is, but whether the source of the bound is the source of the figure.
- **One fund is not the complex** (2026-09-26). Bitwise's chief executive described "more than $110M" for **BSOL**
  over the week to Sept 25; Farside's BSOL column sums to **$128.4M** and the **all-fund** week is **$188.1M**.
  Consistent, not conflicting — file as scope, like the HYPE open-interest entries.
- **A reported all-time high can sit just under this deck's own high** (2026-09-26). A **97.99** HYPE ATH is in
  circulation for the Sept 23 session; this deck's Coinbase 21-day high for that session is **98.01**. Same shape
  as the SOL 117.23 case of 2026-09-25 but inverted, and the resolution is identical: publish the deck's own
  figure and attribute the other.
- **Three different announcement dates for one event** (2026-09-26). The Payward/Bitnomial HIP-3 deployment is now
  carried at **Sept 21** (this deck, since that run), **Sept 23** and **Sept 24** by different publishers. Check the
  event against what the deck already carries, not the date against today.
- **The recency trap, inverted: a fresh date on an old event** (2026-09-25). A result asserted that "on
  September 24, 2026, Payward announced plans to offer US customers onchain perps via Hyperliquid using
  HIP-3 with Bitnomial." This deck has carried that deployment since **Sept 21**. A current-dated article
  restating a known arrangement is not a new announcement. Every earlier instance of this trap was a
  **stale** article looking current; this is a **current** article making an old event look new. Check the
  event against what the deck already carries, not only the date against today.
- **Name the maturity before quoting a yield superlative** (2026-09-25). Two Treasury superlatives were in
  circulation: the **10-year at 5.148%** is the highest since **2007** (19 years) and the **30-year at
  5.444%** the highest since **2004** (22 years). A headline reading "U.S. Treasury Yield Hits 22-Year
  High" names no maturity, and pairing that 22-year claim with the 10-year figure is wrong by three years
  and one instrument. Same family as the HYPE open-interest scope entries: state the object, not just the
  number.
- **The Hormuz day count disagrees across publishers** (2026-09-25). straits.live's live tracker read
  **Day 207** while globalsecurity.org headlined a **"Day 209 Update"** for Sept 24 — a three-day spread
  on a count that looks like a hard fact. The deck dropped the day number and published the status plus
  the transit count instead. **A running day count is a publisher's arithmetic, not an observation.**
- **A high from another venue is not comparable to this deck's tape** (2026-09-25). Reporting called
  **$117.23 on Sept 21** Solana's highest since January 2026. This deck's Coinbase 21-day high is
  **119.99**, and SOL's *current* close of 117.46 already exceeds that 117.23. Different venue, different
  window, and a nine-month superlative a 21-day tape cannot verify. Publish the deck's own high and
  attribute the rest (§6).
- **Article recency trap, second live example** (2026-09-23). A Solana ETF search returned "Solana ETF
  Inflows Fell 96% in a Week, From $153.87M to $6.18M" high in the results. Dated **Sept 8** — two
  weeks stale, and the week it describes has since been followed by the largest weekly inflow of the
  streak. Publishing it would have *inverted* the picture, not merely aged it.
- **Article recency trap, live example** (2026-09-22). A search for the CLARITY Act returned a Yahoo
  piece headlined "The Senate Has 5 Working Days Left" ranked near the top; it was published
  **Aug 2** and its "five working days" ran to the **Aug 7 recess**. Publishing it would have
  invented a September deadline. Check the date on every item — search rank is not recency.

- **HYPE open interest — the carried count is itself inconsistent, so stop numbering it**
  (2026-09-24). This entry's first bullet says four values are carried "($14.3B... $8.1B... and two
  earlier)" while the 2026-09-23 entry calls $2.04B "a fourth value". **The notes disagree with
  themselves about the count**, so a run cannot safely say "a fifth value". Drop the ordinal and
  publish the scope instead. A new value arrived 2026-09-24: **~$18B, reported Sept 23 as a record**,
  and it adds a *dimension* the earlier entries did not have — it is explicitly **bilateral**,
  "counting the combined value of long and short positions", which is roughly double a one-sided
  count. **So the axes are now three: publisher, scope (platform-wide vs HYPE perps alone), and
  counting convention (bilateral vs one-sided).** A bilateral platform-wide figure cannot be set
  against $14.3B or $8.1B without knowing their convention.
- **The recency trap is far more dangerous when the stale article is thematically right**
  (2026-09-24, and this is the sharpest instance yet). A search for the Sept 23 bond-driven crypto
  selloff returned **first** "Bitcoin Slides Under $77K as Crypto Liquidations Top $672M Amid Bond
  Sell-Off" — dated **May 18, 2026**, four months stale. It describes a bond-selloff-driven crypto
  slide "down 2% over the past 24 hours", which is almost exactly the live story. **Only the price
  ($76,770 against a live 84,100) gives it away.** Earlier instances of this trap described the wrong
  *event*; this one described the right *kind* of event at the wrong *time*, which no amount of
  reading-for-sense catches. **Check the date first, before judging whether the content fits** —
  fitting the story is evidence of nothing.
- **The CLARITY recency trap, third recorded instance** (2026-09-25), carried this time by
  **bitcoinfoundation.org** — the same Aug 3 "Countdown" headline about the **Aug 10** recess, still
  ranking seven weeks later, alongside the Aug 2 Yahoo "5 Working Days Left" piece in the same search.
  Recorded instances: **2026-09-22, 09-24, 09-25**. **Note what check 9 cut from the draft here:** it said
  "a third consecutive day, on a third domain". Neither ordinal survives — those dates are not
  consecutive, and the 09-24 run never recorded the domain, so "third domain" is uncheckable. **When
  logging a recurring trap, record the domain and the date every time, or a later run cannot count them.**
- **The HYPE unlock recency trap** (2026-09-26, **finance.yahoo.com**). A search for HYPE news dated
  "September 25 2026" returned *"Hyperliquid Sets New High With $1.2B Token Unlock Days Away"* — published
  **August 24, 2026**, about an **Aug 29** unlock and an **$83.27** all-time high. Publishing it would have
  invented an imminent $1.2B unlock. **Only the date and the stale price give it away**; the story shape fits the
  live situation perfectly. The real next unlock is **Oct 6, to core contributors, size behind a paywall**.
- **CLARITY recency trap, fourth recorded instance** (2026-09-26, **bitcoinfoundation.org** — the second time on
  that domain). Same Aug 3 "Countdown" headline about the Aug 10 recess. Recorded instances with domains:
  **09-22** (Yahoo), **09-24** (domain not recorded), **09-25** (bitcoinfoundation.org), **09-26**
  (bitcoinfoundation.org).
- **SOL recency trap, recurring on three domains at once** (2026-09-26). The Sept 8 "Fell 96%" piece returned
  **first** again, carried simultaneously by **247wallst.com, finance.yahoo.com and aol.com**. Now three weeks
  stale and followed by the largest weekly *and* largest daily prints in the series.
- **The SOL recency trap also recurred** (2026-09-25): "Solana ETF Inflows Fell 96% in a Week, From
  $153.87M to $6.18M" returned **first** again, still dated **Sept 8**, now two much larger weeks stale.
  Assume both this and the CLARITY trap recur on every relevant search.
- **The same CLARITY recency trap fired a second time** (2026-09-24). "CLARITY Act Countdown: Senate
  Has Days to Save Landmark Crypto Bill Before Recess", published **3 August 2026** about the
  **August 10** recess, ranking high seven weeks later. The Aug 2 Yahoo instance is already recorded
  above. Same bill, same shape, still ranking: **assume this one recurs on every CLARITY search.**
- **The SEC Sept 17 mis-report has now recurred on three consecutive runs** (2026-09-24). Coverage
  again claimed "the ruling named BNB Chain as one of three networks set to gain". It **names no
  blockchain and no company**. Confirmed again against the Sept 21 primary-ish source, which does not
  mention the SEC action at all. **Treat this as a standing correction, not a per-run discovery.**
- **A liveblog is not a single-timestamp source** (2026-09-24). One CoinDesk live-updates article
  carried both **73.1%** and **"more than 53%"** for October hike odds — two reads from different
  hours of the same day, in the same URL. Quote which entry, or quote neither.
- **Four instruments for one question is not a dispute — and the unnamed one is the dangerous one**
  (2026-09-24). October hike pricing read **64.5%** (Polymarket), **69.4%** (centralbank.watch),
  **66%** (CME FedWatch) and **73.1%** (CoinDesk, instrument unnamed). The 73.1% was both the closest
  to the 75% branch bar and the only one with no named instrument. **A branch that names its routes
  must not be fired by a figure that names no route**, however much closer to the bar it sits.

## 6. Tape method

- **Prices: Coinbase Exchange public API only** (`api.exchange.coinbase.com`), **completed candles
  only**. Hourly granularity 3600. The candle opening at `H` closes at `H+1`; at 05:56 UTC the last
  *complete* candle is the one opening 04:00. Exclude the in-progress hour.
- **Which field: highs come from `high`, everything else from `close`** (established 2026-09-22 —
  do not re-derive). A Coinbase candle is `[time, low, high, open, close, volume]`. The published
  "Close" and the 24h change use `close` (index 4); the 7-day and 21-day **high** columns use `high`
  (index 2), and the timestamp quoted beside a high is that candle's opening hour. A rebuild that
  used `close` for the highs returned 2,784.09 for ETH where the baseline says 2,807.10; switching to
  `high` reproduced all six of the previous build's highs exactly. 21 days of hourly candles needs
  paging — Coinbase caps a response at 300 candles, so fetch in two chunks with `start`/`end`.
- **The build stamp is the close time of the last completed candle.**
- State the **7-day and 21-day window** next to every drawdown. They often differ and the difference
  is load-bearing: on Sept 21 BTC set a fresh *seven-day* high (82,087.11) while its *twenty-one-day*
  high stayed 82,283.00 from Sept 3. Saying "fresh high" unqualified would have been wrong.
  The converse also happens: on **Sept 22 all six had the same print as their 7d and 21d high**, all
  set inside the Sept 21 session — then the qualification is unnecessary and saying so is the
  stronger claim. Check which case you are in; do not assume either.
- All six trade on Coinbase: BTC, ETH, SOL, BNB, XRP, HYPE — all `-USD`, all online.
- **Noise floor:** do not publish an ordering claim on a margin inside ~0.5pt; state the figures and
  decline the ranking. Precedent: HYPE/BNB reordered overnight on a 0.71pt margin.

### Pre-break levels (back-derived 2026-09-21 — store these, do not re-derive from prose)
The deck quotes every asset against a fixed "pre-break level" that exists **only in prose** — there
is no constant in the code. Back-derived from the Sept 21 01:00 build's own percentages:

| BTC | ETH | SOL | BNB | XRP | HYPE |
|-----|-----|-----|-----|-----|------|
| 77,277 | 2,507.8 | 101.29 | 721.2 | 1.3568 | 78.50 |

These reproduce that build's published figures to within 0.01pt. Consider promoting them to a
commented constant so no future run has to reverse-engineer them again.

## 7. Pre-publish checklist (run in order; audit a failing assertion before editing the file)

1. `node --check` the extracted inline script.
2. Evaluate the three arrays; assert **COINS 6 / MACRO_SNAPSHOT 6 / GLOBAL_CATALYSTS 21 /
   asset catalyst entries 18**.
3. **Zero apostrophes in single-quoted fields** (`id`, `symbol`, `name`, catalyst `date`/`text`,
   macro `label`/`value`/`cls`). Summaries are double-quoted, so apostrophes are legal there — but
   a double quote inside a summary is not. Assert both.
4. Every summary **over 200 chars**.
5. `cls` is only `ok` or `warn`.
6. Every `macroScore` within -2..+2.
7. **Blanked-array diff**: blank the three arrays in both old and new, diff, and assert the *only*
   differences are the as-of line. This catches design/JS drift — and it caught a real bug on the
   2026-09-21 run (see 8).
   **When the design change is intentional, swap this check, do not skip it** (established
   2026-09-22). On a run that deliberately changes layout the diff fails by construction and tells
   you nothing. Replace it with the stronger assertion it was standing in for: extract every
   computation and live-data block from both builds and require them **byte-identical** —
   `average`, `computeRSI`, `emaFull`, `computeMACD`, `computeTechnical`, `combine`, `sparkSVG`,
   `fmtPrice`, `fetchMarkets`, `fetchChart`, `loadAll`, `fmtUsd`, `pct`, `fetchRotationLive`,
   `loadRotation`, `ROTATION_ASOF`, `RIVALS` — plus a grep asserting the five rotation thresholds
   (`volShare < 55`, `bestMonet >= 1.0`, `bestTake > 2.5`, `lead.mcapRev * 0.5`, `bestTvl > 25`) are
   unchanged. A block extractor must stop at the *next* top-level declaration **or comment**; the
   first version of it ran past the end of a function and reported a new neighbouring comment as
   drift in `fetchChart`.
8. Stale-string checks scoped to the *previous build's* phrasing, not to generic words.
9. **Superlative / count / margin grep** over every published string; verify each claim against the
   tape. This caught a false "oldest high of the six" this run (see 8).
10. **Headless Chromium render**: `#macroGrid` 6, `#catalystsRow` 21, `#assetGrid` 6, and
    **zero uncaught JS exceptions**.

### Validator gotcha: `eval` of a `const` does not reach the outer scope (2026-09-23)
Check 2 extracts the three arrays and evaluates them. A **direct** `eval('const COINS = [...]')`
creates its own lexical environment, so `COINS` is undefined immediately afterwards and the check
reports a missing array on a perfectly good file. Rebind before evaluating —
`.replace('const NAME = [', 'globalThis.NAME = [')` — and use indirect eval `(0,eval)(...)`.
`node --check` passing while check 2 reports "X is not defined" is the signature of this, and it is
the harness, not the build. Four consecutive runs had a first-pass validation failure that was the
assertion's fault. Audit the assertion before touching `index.html`, every time.
**2026-09-24 broke that streak** — the rebinding and indirect-eval fixes were applied preventively and
checks 2-6 passed first time. The gotcha is now solved rather than merely known; keep the fix in the
validator and stop re-discovering it.

### Check 8 can fail on its own seeding — audit it too (2026-09-25)
Check 8 says stale-string checks must be scoped to the *previous build's phrasing*, **not to superseded
figures**. This run seeded it with the superseded figures (`+$32.4M`, `+$2.5M`, `96.1%`, `127.5%`) and it
failed on ten occurrences that were all deliberate: the build's whole subject was that those floors had been
superseded, so each is cited beside its replacement ("published it yesterday as a +$32.4M floor and it has
settled at +$346.9M"). **The assertion was wrong; `index.html` was not edited.** Fix: check genuine
*phrasings* for absence, and check superseded *figures* for **adjacency** to their replacement (the 8b
assertion) rather than for absence. A superseded figure is often load-bearing evidence, not staleness.

### Two more assertions were at fault, 2026-09-26 — and that is three runs in a row
**Check 7c** reported **1** `AS_OF` reference against a requirement of 3: the counter subtracted `ROTATION_ASOF`
from a raw substring count and got it wrong. Use a negative lookbehind — `(?<![A-Z_])AS_OF\b` — which returns
**3** (declaration, `.asOf` span injection, `${AS_OF}` in `renderCard()`). **Run the same assertion against the
previous build**: it returned 3 there too, which is the cheap way to separate a broken assertion from a real
regression. Do that before touching anything.

**Check 8b** flagged an orphaned `+$39.3M`: the assertion demanded the replacement as **`+$66.1M`** with a sign,
while the sentence cites *"against an actual **$66.1M**"*. **Adjacency assertions must match the bare figure, not
a signed form** — prose carries the sign inconsistently and has no reason not to.

**Neither failure led to an edit of `index.html`.** With 2026-09-24 and 2026-09-25, that is three consecutive runs
whose first-pass validation failure was the harness. **Treat a failing assertion as probably the harness until
proven otherwise** — this is no longer an occasional courtesy, it is the base rate.

### Check 8 failed on its own seeding AGAIN — and that is four consecutive runs of harness-fault (2026-09-27)
Check 8 flagged *"three days out"* and *"four days out"* as surviving from the previous build. **Both are generic
countdown phrases, not distinctive phrasings.** Every countdown on the page was correct for the new date (Sept 29 =
two days out, Sept 30 = three, Oct 1 = four), and the previous build's *pairings* were all absent. A rescoped pass
then flagged *"Sept 29, ahead of activation"* — also wrong, because that states an **unchanged standing fact** and
its recurrence is continuity.

> **Seed check 8 only with phrasings whose REFERENT has changed.** Never with a phrase that is merely re-computed
> (a countdown) or genuinely unchanged (a standing fact) — and, per 2026-09-25, never with a superseded figure,
> which belongs in the 8b adjacency assertion instead.

**`index.html` was not edited on either.** With 09-24, 09-25 and 09-26 that is **four consecutive runs** whose
first-pass validation failure was the harness. This is the settled base rate: **audit the assertion first, every time.**

### The self-flattering rounding catch fired on its first armed run (2026-09-27)
2026-09-26 added to check 9: *recompute every margin that makes a case and confirm the rounding does not flatter it.*
On the very next run it caught **"0.77 points over Bitcoin"** where the derived margin is **0.7629pt**, which rounds
to **0.76**. Tiny, and that is the point — **0.77 reads exactly as harmlessly as 0.76**, so nothing about the sentence
invites suspicion. **Only mechanical recomputation of every published margin catches this class.** Do not re-read the
sentence and ask whether it sounds right; regenerate the number.
Also corrected this run: **"the first time that has been true for several runs"** (on zero fresh highs) — an ordinal
the run notes cannot support, since 09-25 does not clearly record whether a fresh high was set. Rewritten to the
derivable fact. **The count-and-ordinal family remains check 9's main catch.**

### The 7b extractor missed `async function` — a FIFTH consecutive harness-fault run (2026-09-28)
Check 7b reported five blocks **missing**: `fetchMarkets`, `fetchChart`, `loadAll`, `fetchRotationLive`,
`loadRotation`. All five are declared **`async function`**, and the extractor matched only `^function NAME` or
`^const NAME =`. The same omission meant **`async function` was not recognised as a block *boundary* either**, so an
earlier block could have run past its end — the 2026-09-22 "must stop at the next top-level declaration **or
comment**" rule needs `async function` in both lists. Fixed; 7b then returned **17/17 identical, 0 drift**.
**`index.html` was not edited.** With 09-24, 09-25, 09-26 and 09-27 that is **five consecutive runs** of harness-fault.

> **Note the shape, because it differs from the previous four.** Those were mis-*seeded* assertions (check 8's stale
> strings, check 7c's counter) — assertions that **invented** a failure. This one was an **incomplete pattern in an
> extractor**, which could have **hidden** real drift instead. **A validator reporting "missing" rather than "changed"
> is reporting on itself**, and a byte-identity check that silently skips five of seventeen blocks is worse than no
> check at all. Assert the *count* of blocks matched, not only the absence of drift.

### A regex whose delimiter is the character it searches for is structurally blind (2026-09-29)
**Check 3** matched only **23** single-quoted fields where ~114 exist. Cause: the pattern required `: '` **with a
space**, but the build writes `date:'…'`, `text:'…'`, `cls:'…'` with **no space after the colon**. Fixed with
`:\s*'`, which returns **124** — *exactly the count the 09-28 run recorded*, which is the cheap way to confirm the
assertion and not the file was at fault. **Run a changed assertion against the previous build before touching
anything** (the 09-26 rule), or against the previous run's recorded count.

> **The deeper defect, and the fix to keep:** `'([^']*)'` **cannot detect the thing it is checking for.** A field
> containing an apostrophe terminates the match early, so the offending field is *silently skipped* rather than
> flagged. Check 3 now **also evaluates the arrays and inspects every field JS-side** (114 fields, 0 bad), which
> cannot be fooled this way. Same family as the 09-28 `async function` extractor: **a validator that can miss is
> worse than one that shouts.** Assert the *count* of fields inspected, not only the absence of violations.

### Check 8 mis-seeded again — a re-computed phrase with a CHANGING SUBJECT (2026-09-29)
Check 8 flagged *"the only one of the six to close higher over 24 hours"* as surviving. **Not stale.** It described
**BNB at +0.04%** in the previous build and **ETH at +0.28%** in this one. The 09-27 rule excludes countdowns and
standing facts from seeding; **this adds the third member: a phrase that is re-computed each run with a different
subject.** Verify by locating the phrase and checking *who* it now describes, not whether it recurs.
**`index.html` was not edited for either failure.** With 09-24, 09-25, 09-26, 09-27 and 09-28 that is **six
consecutive runs** whose first-pass validation failure was the harness. Audit the assertion first, every time.

### Do not pipe the Farside reader through `head` (2026-09-29)
`node farside.js | head -150` let SIGPIPE kill node after the third slug, so **`/hyp/` was silently never read** and
it looked like a Cloudflare failure. Redirect to a file and grep the file. All four slugs cleared on the **first
attempt** with a fresh context per slug — third consecutive clean run for the per-slug rule.

### Check 8 passed first pass for the first time (2026-09-28)
Seeded strictly per the 09-27 rule — only phrasings whose **referent had changed** (14 of them: "Neither named route
moved", "No asset on this deck set a fresh high", "a twelfth run", "a seventh consecutive run", "Brent last settled
$104.32", "mainnet remains unscheduled", and so on), with **countdowns, standing facts and superseded figures all
excluded**. 14/14 absent, no audit needed. **The rule works. Keep seeding it this way.**

### Check 9, 2026-09-28: three corrections, and one of them was THIS FILE'S
1. **"one observation from the zero condition"** (Hormuz) — **wrong, and inherited from these notes rather than
   drafted fresh.** Sept 20 read **1**, not 0, and the condition needs **two consecutive readings of 0**, so it is two
   observations away. See §3. **The important part is the provenance:** four earlier runs had re-read §3 and passed
   this along. Check 9 caught it only because **its grep runs over published strings regardless of where a claim came
   from**. *Re-derive inherited claims, not only new ones* — the count-and-ordinal family does not care who wrote it first.
2. **"the peer median fell 0.85 points from +4.19% to +3.34%"** — the derived figure is **0.8555 -> 0.86**. The 0.85
   comes from subtracting the **rounded endpoints**, which is why it survived drafting: the arithmetic on the page's
   own two numbers checks out. See §5.5.
3. **"uncarried through four builds"** (the HYPE Binance listing) — the listing was **Sept 24 11:00 UTC**, so the
   builds that followed are **09-25, 09-26, 09-27 = three**. Same convention the 09-27 run used for the BNB probe.

**98 claim-words were re-derived across 51 published strings.** Two of the three catches are counts or margins, which
keeps the standing pattern intact: **fluent prose hides an arithmetic count far better than it hides a wrong number.**
**New this run:** the pattern now extends to *inherited* counts. Grep the published strings, not the new sentences.

### Check 9 is the check that earns its keep (2026-09-24)
Check 9 corrected **four** drafted claims this run, the most of any run, and every one of them was a
sentence that read perfectly well:
1. *"only MSBT has reported"* — four funds carried an explicit `0.0`, which is a report (§5.2).
2. *"the three largest lines in the series"* — false by cumulative Total; ETHB is fifth, not third.
3. *"the one clearly separated ranking in that column"* — three of that column's margins clear the
   0.5pt noise floor, not one.
4. *"a fifth published value"* — the count is unverifiable because the notes disagree with themselves
   (§5.5).
The pattern: **fluent prose hides count and ordinal errors much better than it hides factual ones.**
Grep for the claim words, then re-derive each one from the source table — do not re-read the sentence
and ask whether it sounds right.

**2026-09-26: three corrections, and the pattern moved.** (1) *"inside 5%"* for a weighted prediction whose
overshoot is **5.45%** — **a number rounded toward the argument it supported**, which is a new failure mode and
the most dangerous kind, because self-serving rounding reads as confidence. (2) *"FBTC is most of what has
posted"* on a row where FBTC is the **only line above zero** and BITB posted an explicit **-$11.8M** — the
dash-vs-zero error in a third costume, now blurring a reported negative into absence. (3) *"four stablecoins"*
for a list containing "U", which is not verifiably one — softened to "dollar-referenced tokens". **Zero count or
ordinal errors this run, because the counts were re-derived from the tables before drafting rather than after.**
So: grepping the count words works and should continue, and the new item for the checklist is **recompute every
margin that makes a case and confirm the rounding does not flatter it**.

**2026-09-25: four more corrections, and the pattern is now firmly count-and-ordinal.** (1) *"IBIT shows no
figure for a fourth consecutive session"* — false; blank for one session, late at read time on four runs
(§5.2). (2) *"a third consecutive day, on a third domain"* — both ordinals uncheckable (§5.5). (3) *"every
quarter on record"* — only four quarters are in hand. (4) *"undoing most of the widening"* — 56% of it, so
literally true but marginal; softened. **Eight of the ten claims check 9 has corrected across two runs were
counts, ordinals or margins, and none were factual errors about a named figure.** Fluent prose hides an
arithmetic count far better than it hides a wrong number, so grep the count words hardest.

### One "as of" constant — the three-label trap is designed out (2026-09-22)
There used to be three separate as-of strings (the macro `<h2>`, the footer, and a `.sect-label`
inside a backtick template in the card renderer), and a run that updated only the visible heading
shipped a stale page. **They are now one `const AS_OF` at the top of the inline script**, injected
into the two `<span class="asOf">` placeholders by `renderMacro()` and interpolated directly in
`renderCard()`. To restamp a build, edit that one line.

Assert in validation: `const AS_OF = '` present, exactly **2** `class="asOf"` spans, at least **3**
`AS_OF` references in the script, and — in the headless render — that both spans contain the new
value. Both spans reading `—` means `renderMacro()` did not run.

`ROTATION_ASOF` (`'Sept 5, 2026'`) is **not** an as-of label. Do not touch it.

## 8. Build-script and tooling hazards (found 2026-09-21)

- **Python `re.subn` with a lambda does not expand backreferences.** Passing
  `lambda m: repl` inserts `\g<1>` *literally*. This corrupted all three as-of labels on the first
  build attempt; the blanked-array diff (check 7) caught it. Pass the replacement string directly so
  `re` expands it, or build the replacement by hand. Conversely, a replacement containing literal
  backslashes must be escaped. **This is why check 7 exists — do not skip it.**
- **"Zero page errors" must mean zero *uncaught JS exceptions*.** The page fetches live prices from
  CoinGecko, which returns **HTTP 429** from this environment under any load. Those are resource
  errors on an external API, present identically on the old published file, and are not defects in
  the build. Listen to Playwright's `pageerror` event for real faults; count 4xx/5xx responses
  separately.
- **`#assetGrid` renders 0 when CoinGecko 429s**, on *any* version of the file, because the asset
  cards are built from live data. A 0 there is an API-availability signal, not a broken build —
  re-run before concluding anything.
- **Farside is behind a Cloudflare JS challenge.** `curl` and WebFetch both get HTTP 403
  ("Just a moment..."). It loads fine in headless Chromium, which clears the challenge in ~6s —
  but allow up to ~60s and poll for `table tr` rather than waiting a fixed 9s, and set a realistic
  desktop `userAgent`; with the default Playwright UA the challenge did not clear at all
  (2026-09-22). Working pages: `/btc/`, `/eth/`, `/sol/`. There is a `Hyperliquid ETF Flow` link in
  the footer menu, but `/hype/` is a 404 — find the real slug before relying on it.
- **The Hyperliquid ETF slug is `/hyp/`, not `/hype/` — SOLVED 2026-09-26, stop looking.** Working Farside
  pages are `/btc/`, `/eth/`, `/sol/` and **`/hyp/`**. The Hyperliquid table carries three funds, **BHYP, THYP,
  HYPG**, averages **$3.7M a session** and **$349M cumulative**. There is no HYPE flow branch yet; see the open
  items.
- **Per-slug fresh contexts appear to be the fix (2026-09-27).** All four slugs — `/btc/`, `/eth/`, `/sol/`, `/hyp/` —
  cleared Cloudflare on the **first attempt** with a new context per slug and a realistic desktop UA. No warm-up load
  of `/btc/` was needed, unlike 2026-09-26. Keep the per-slug context rule.
- **Give each Farside slug its own browser context (2026-09-26).** `/btc/` cleared first attempt. `/eth/` cleared
  only after a warm-up load of `/btc/` in the same context. `/sol/` **failed three attempts inside a reused
  context and then succeeded on the first attempt in a fresh one**. Poll for `table tr` for up to 90s with a
  realistic desktop UA, and **build a new context per slug**.
- **Do not pass `--no-sandbox` (2026-09-26).** The first Farside reader passed it and the environment's auto-mode
  classifier blocked the call as TLS/auth weakening. Dropping the flag entirely worked — headless Chromium
  launches, trusts the agent-proxy CA via the `CACertificates` policy, and clears Cloudflare without it. The flag
  was never necessary.
- **SoSoValue does not clear.** `sosovalue.com/assets/etf/us-sol-spot` sits behind a harder
  Cloudflare challenge that did **not** clear in 60s of headless Chromium (2026-09-22). Read the
  SoSoValue series via Farside `/sol/` (rows agree) or via a citing publisher, and say which.
- **Playwright is not installed.** Not in the repo, not globally. `npm install playwright` into the
  scratchpad. Its bundled `chromium.executablePath()` reports **`chromium-1193`, which does not
  exist**; the installed browser is **`/opt/pw-browsers/chromium-1194/chrome-linux/chrome`** and must
  be passed as `executablePath` explicitly or every launch fails.
- **Playwright's Chromium does not trust the agent proxy CA** and fails every HTTPS request with
  `ERR_CERT_AUTHORITY_INVALID` — including, silently, the page's own live-price fetches. Importing
  the CA into the NSS store is *not* enough for Chromium 141 (it uses the Chrome Root Store). The
  fix that works is the supported enterprise policy: write
  `{"CACertificates": ["<base64 DER>", ...]}` from `/root/.ccr/agent-proxy-ca.crt` to
  `/etc/chromium/policies/managed/ccr-ca.json` (also `/etc/opt/chrome/policies/managed/`).
  Never disable TLS verification. This must be done **before** the validation render, or the render
  is not faithful to what a real visitor sees.

## 9. Open items (re-verify every run; correct them when they go stale)

- [x] **GitHub push blocker — CLOSED. Do not re-check it again.** Re-verified a **tenth** time 2026-09-29: pushed to
      `main` cleanly with the ambient credentials, no `claude/` branch fallback and no pull request needed. **The
      routine prompt still asks each run to re-verify this; the answer is settled and a future run should spend no
      time on it** beyond noting that the push succeeded. Two mechanical facts that are normal and are *not*
      blockers: the session starts checked out on a `claude/...` branch, and the local `main` ref can be stale on
      session start. On 2026-09-29 it was **not** stale — `HEAD`, `main` and `origin/main` all agreed at `d7a4203`.
      **Always `git fetch origin` before concluding anything about what is published.**
- [x] **The live URL matched the repo file byte for byte on session start** (2026-09-29, sha256 `b402911a…`
      identical, `AS_OF` reading Sept 28). Worth the one `curl` every run; it is how a five-day stale publish
      would be caught.
- [ ] **Oct 1 — XRP downside trigger, two days out. Still the most likely next score move, and it is a cut.** No
      second cloture vote scheduled; cloture failed **49-50** on Sept 15 over ethics drafting, not the whip count.
      Tillis motion to reconsider preserved. Senate out for nearly all of October and the first week of November;
      **Oct 1 is a recess date, not a funding one** — the CR signed Sept 2 funds the government to **Dec 11**, so no
      shutdown competes for floor time. Lame duck is the named realistic slot.
- [ ] **BTC Sept 28 is UNFINISHED — IBIT is the only blank.** Floor **-$23.8M**; weighted estimate **+$72.3M**
      (IBIT average $96.1M), which is the **one large blank with a stable average** case, the trustworthy one.
      **The seven-session inflow streak (Sept 17-25, +$2,978.3M) neither continues nor ends until IBIT reports.**
      IBIT would need **-$276.2M** alone to cross the -$300M bar, so the row neither fires nor withholds the branch.
- [ ] **BNB: AMENDMENT OPTION 1 IS NOW DEFEATED FROM BOTH SIDES (2026-09-29).** It **passed** on 09-28 (subject and
      margin moved together, on a 1.90x-roll-off move) and would have **BLOCKED** on 09-29 (subject fell 3.91pt while
      the margin improved 2.43pt). **Two runs, opposite verdicts, one cause** — the subject's own window return is
      itself roll-off-driven, so it carries no independent information. **Option 2 (overlap-window only) is the one to
      pick.** Four consecutive roll-off-dominated runs (09-26 fired on it, 09-27 held, 09-28 measured, 09-29 flipped
      the direction test). **User's choice. Decompose the margin AND compute the overlap-window margin every run.**
- [ ] **THE FED ROUTE SET — still open, but NO LONGER URGENT (2026-09-29).** CME FedWatch **fell 75.8% -> 72.3%** and
      is **below the 75% bar for the first time**; the CME-vs-centralbank.watch gap closed **14.2 -> 10.4 -> 4.7pt**,
      **by CME coming down**. The "one of them is mis-measuring" case is weaker than it was. Named routes: Polymarket
      **68.5%**, centralbank.watch **67.6%**, higher one **6.5pt short**. **Add CME as a third route, replace
      centralbank.watch with it, or keep it excluded?**
- [ ] **Fed route spread — reversed AGAIN.** Sequence: 1.4 -> 3.2 -> 2.2 -> 1.5 -> 4.9 -> 3.0 -> 2.9 (*reversed*) ->
      2.9 -> 0.9 (*reversed back*) -> **0.9 (*reversed again*, Polymarket higher)**. Three swaps in four runs.
- [ ] **THE BRANCH SETS CANNOT EXPRESS A LARGE DATED NON-PRICE EVENT — two assets.** BNB has no regulatory or
      enforcement leg (the US sanctions probe, Sept 22) and HYPE has no leg for an **exchange listing** (Binance spot,
      Sept 24). **Decision needed on both.** For BNB a charging decision, plea, penalty above a threshold or formal
      closure; for HYPE a listing is arguably not worth a branch at all, which is itself an answer worth writing down.
- [ ] **Sept 29 (today) — THREE unrelated things on one date. Do not blur them.** (a) **Glamsterdam client software
      deadline** — nothing slipped as of the 02:00 stamp; first place an Oct 6 slip becomes visible. (b) **Bitget
      reopens ETH withdrawals 08:00 UTC** (BTC reopened on schedule Monday; USDT Sept 30; the rest Oct 2 08:00) — a
      missed phase is the first sign the 83.5%-of-fund coverage is strained. (c) **Binance Funding accounts stop
      taking on-chain crypto deposits**; the Stocks Account rename completes **January 2027**, not today.
- [ ] **Sept 30 (tomorrow) — Q3 2026 ends**, the HYPE revenue branch's live instrument; reports in October. Above
      $260M restores 0.1; below $150M cuts a further 0.1. **Q4 2025's $295M is not it** (right series, right units,
      right side of the bar, wrong position in time). Neither is a **cumulative total ($1.31B)**, a trailing-30-day
      figure or an annualised run rate. **DefiLlama returned HTTP 403 to a direct fetch (2026-09-28)** — find another
      route or publish nothing rather than taking a figure from a search summary.
- [ ] **Hormuz — no new reading 2026-09-29.** Still **1 on Sept 20** against 85/day. Next PortWatch observation due
      **today**, published Tuesdays on a ~2-day lag, so an 02:00 UTC build cannot see it. Series **6 / 8 / 1** —
      **none is zero**, so the zero condition is **two** observations away at best. Kpler barrels and Reuters vessel
      counts publish daily but are different objects with different baselines and cannot substitute (§5.5).
- [ ] **Oct 6 — THREE unrelated things on one date.** (a) Glamsterdam on Sepolia, **13:53:36 UTC**, epoch 353024,
      slot 11296768: activation *and* finality adds 0.1 to ETH, a slip or failure to finalise cuts 0.1. (b) The
      **HYPE core-contributor tranche — NOW SIZED: 9.92M HYPE, ~$860M nominal**, one of 24 even monthly tranches of a
      ~238M allocation; **the Sept 6 tranche was claimed far under schedule (~0.19% vs an intended 2.32%)**, so
      scheduled and claimed supply are separate objects. (c) The **second** PortWatch observation after Sept 29.
- [ ] **Use the CURRENT Farside `Average` row on any weighted estimate.** Re-read 2026-09-29: BTC table total
      **$84.8M** (was 84.9), IBIT **$96.1M**, FBTC $16.3M; ETH total $25.5M, ETHA **$24.3M**, ETHB **$6.4M**,
      FETH $4.5M; SOL total $7.0M; HYP total **$3.7M**, cumulative **$349M**. And state which case the estimate is
      in: **one large blank with a stable average** (0.7% error on 09-27) versus **several or small blanks** (59.7%
      low the same day).
- [ ] **SOL Sept 18 row still has two blanks** — VSOL and FSOL, unchanged for a **ninth** consecutive run. That week
      can only be revised upward, which can only strengthen the $60.7M restore.
- [ ] **A SOL upside flow bar does not exist — decision needed.** The completed week to Sept 25 is **+$188.1M**,
      37.6x the downside bar, and the score cannot move on it. All seven funds were positive that week and BSOL took
      **$128.4M = 68.3%**. Note the **daily** superlative is publishable (Sept 25's +$86.7M equals the Farside
      `Maximum` row) while the **weekly** one is not (the table's bound is daily).
- [ ] **A HYPE flow branch is now writable — decision needed.** Farside `/hyp/` readable (BHYP, THYP, HYPG; Sept 28
      an **explicit 0.0** across all three; week to Sept 25 **+$9.3M**; **$3.7M** average a session; **$349M**
      cumulative).
- [ ] **Source the HYPE supply pair — now a TRIPLE.** ~**251M circulating (26% of max)**, a core-contributor lock to
      **2027-2028**, this deck's **222,445,714 = 22.24% released to date**, and now a **~238M core-contributor
      allocation over 24 monthly tranches** found 2026-09-29. Four figures, at least three different objects.
      **Still published as unresolved.**
- [ ] **Solana Alpenglow — mainnet has NO DATE.** Live on devnet and testnet; replaces TowerBFT with Votor, targets
      ~150ms finality against ~12.8s. **Sept 28 was the date feature activations were tentatively allowed to resume,
      not a launch (§5.5).** No branch can read it. Worth watching for a mainnet date appearing.
- [ ] **`7d high = 21d high for all six` HAS BROKEN (2026-09-29), as predicted.** BTC, ETH and BNB now differ (their
      Sept 21 21-day highs left the seven-day window); SOL, XRP and HYPE still match. **No name set a fresh 21-day
      high into this build** — SOL's 124.93 of Sep 27 08:00 is more than a day old.
- [ ] **Oct 27** — Hoodi Glamsterdam, provisional, contingent on Sepolia. **Oct 27-28 — FOMC**, the meeting the Fed
      branch prices. centralbank.watch carries the next meeting as **Oct 28** and the current rate as **3.88%**.
- [ ] **Stray snapshot** — `signal-deck-2026-09-21-0100utc.html` remains in the repo root, **nine runs** after it was
      first flagged. It was uploaded by the user, so no run has deleted it. Harmless (Pages serves `index.html`) but
      it is a stale build sitting beside the live one, and one like it caused a five-day stale publish. **Still needs
      a yes/no from the user.** This run does not create dated snapshots and no future run should.
- [ ] **Pre-break levels** live only in prose (see §6). Consider a commented constant. Used unchanged again this run
      and they continue to reproduce the published percentages exactly.

## 10. Design contract (standing user instruction, 2026-09-22)

The user amended the routine prompt with: *make the website easy to read for beginners, optimized for
phone or laptop depending where they open it, make the deck look clean, remove "not financial
advice".* That **overrides** the standing "do not touch the design, layout or disclaimer language"
clause in the prompt body, and it is standing — not a one-off for the 07:00 build.

What this means for future runs:

- **Do not restore the old layout, and do not re-add "not financial advice" or "not investment
  advice".** The honest framing stays, in plain words: one research read, it can be wrong, it does
  not know what you own, one input beside your own work. That text lives in the primer panel, the
  card footer note and the rotation note.
- **What must keep working:** the beginner primer, the plain-English band note under each score, the
  plain-English bar labels, the −2..+2 restatement, the glossary, and single-column collapse on a
  phone. These are the deliverable, not decoration.
- **Responsive floor to re-assert on every build:** no horizontal page scroll at **390 / 768 / 1440**,
  no element overflowing the viewport (the rotation table is the one allowed exception, inside
  `.rot-table-wrap`), and no interactive element under 32px tall. The render check in §7 does all
  three at once.
  **Re-asserted and passing 2026-09-29** at 390 / 768 / 1440: 0 horizontal scroll, 0 overflowing elements, 0
  interactive elements under 32px, `#macroGrid` 6 / `#catalystsRow` 21 / `#assetGrid` 6, **zero uncaught JS
  exceptions**, and both as-of spans reading the new stamp at every width. **The user re-stated the design
  instruction verbatim in the routine prompt again on 2026-09-29** (easy to read for beginners, optimised for phone
  or laptop, clean deck, remove "not financial advice"). It is the same standing contract recorded here on
  2026-09-22 and was already fully in force, so **no design change was needed and none was made** — checks 7, 7b and
  8c prove it together: the blanked-array diff shows the `AS_OF` line as the only difference outside the three
  arrays, all 17 computation and live-data blocks are byte-identical, and the banned phrases score zero while
  `primer`, `glossary`, `bar-sub`, `macroWord` and `rot-table-wrap` are all retained. **This is the third
  consecutive run on which the instruction was restated and the correct response was to verify, not to redesign.**
  **Re-asserted and passing 2026-09-28** at 390 / 768 / 1440: 0 horizontal scroll, 0 overflowing elements, 0
  interactive elements under 32px, `#macroGrid` 6 / `#catalystsRow` 21 / `#assetGrid` 6, **zero uncaught JS
  exceptions**, and both as-of spans reading the new stamp at every width. **The user re-stated the design
  instruction verbatim in the routine prompt again on 2026-09-28** (easy to read for beginners, optimised for phone or
  laptop, clean deck, remove "not financial advice"). It is the same standing contract recorded here on 2026-09-22 and
  was already fully in force, so **no design change was needed and none was made** — checks 7, 7b and 8c prove it
  together: the blanked-array diff shows the `AS_OF` line as the only difference outside the three arrays, all 17
  computation and live-data blocks are byte-identical, and the banned phrases score zero. **A future run should read a
  restatement of this instruction as confirmation that the contract is already satisfied, not as a request to redesign.**
  **Previously re-asserted and passing 2026-09-27** at 390 / 768 / 1440: 0 horizontal scroll, 0 overflowing elements, 0
  interactive elements under 32px, `#macroGrid` 6 / `#catalystsRow` 21 / `#assetGrid` 6, **zero uncaught JS
  exceptions**, and both as-of spans reading the new stamp at every width. The render also confirmed the
  beginner-facing band labels: **BNB 0.0, XRP 0.0 and HYPE -0.1 all read "balanced"**, since `macroWord()` maps
  [-0.2, +0.2] to that word. The user re-stated the design instruction in the routine prompt on 2026-09-27
  (easy to read for beginners, optimised for phone or laptop, clean, no "not financial advice"); it is the same
  standing contract recorded here on 2026-09-22 and was already in force, so **no design change was needed and
  none was made** — the byte-identity assertion in §7 proves it.
  **Previously re-asserted and passing 2026-09-26** at all three widths: 0 horizontal scroll, 0 overflowing elements, 0
  interactive elements under 32px, and `#macroGrid` 6 / `#catalystsRow` 21 / `#assetGrid` 6 with **zero uncaught
  JS exceptions**. The render also confirmed the plain-English band labels directly, which is worth doing whenever
  a score crosses or approaches a band edge: BNB at **0.0** and HYPE at **-0.1** both render as **"balanced"**,
  because `macroWord()` maps [-0.2, +0.2] to that word — so the BNB restore changed the number and no visible word.
  **Say that on the card when it happens**, or a beginner hunts for a change that is not there.
- **The design is still not the run's subject.** Refresh runs edit `MACRO_SNAPSHOT`,
  `GLOBAL_CATALYSTS`, the per-coin score/summary/catalysts and `AS_OF` — the byte-identity assertion
  in §7 is what proves the rest was left alone.
- **Netlify tags are gone (2026-09-22).** The `<head>` carried three Netlify meta tags and an
  advertising comment claiming the site was served from Netlify Edge; it is served by GitHub Pages,
  and the routine prompt says not to use Netlify for anything. Do not let them back in.
