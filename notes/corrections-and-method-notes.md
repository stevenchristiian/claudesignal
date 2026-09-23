# Signal Deck — corrections and method notes

Standing method file for the scheduled refresh of `index.html`, published by GitHub Pages
at https://stevenchristiian.github.io/claudesignal/.

**Status of this file:** created 2026-09-21 06:00 UTC; last updated 2026-09-23 02:00 UTC. The routine prompt instructs the run to
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

As published 2026-09-23 02:00 UTC (six holds, no moves — second consecutive all-hold run):

| Asset | Score | Held since |
|-------|-------|-----------|
| BTC   | -0.3  | Sept 20 (restored from -0.4 on the Sept 18 flow print) |
| ETH   | +0.4  | Sept 20 (restored from +0.3 on the Sept 18 flow print) |
| SOL   | +0.5  | Sept 22, 02:00 (remaining 0.1 restored on the completed $60.7M week to Sept 18) |
| BNB   |  0.0  | 16 consecutive runs |
| XRP   |  0.0  | 8 consecutive runs |
| HYPE  | -0.1  | unchanged since the HIP-3 revenue cut |

Scale is **-2 to +2**. Move a score only when a written branch threshold below fires. Diff against
this table, **not** against the served page — the served page can be stale (see 1).

## 3. Live branch thresholds

- **BTC flow leg** — re-cut on one settled session below **-$300M**, or two consecutive sessions
  each below **-$150M**. Restored 2026-09-20 on the Sept 18 print of +$433.0M.
- **BTC Fed leg** — October priced **above 75%** on *two independently routed* instruments cuts
  0.1; **below 40%** on two restores it. Two routes currently used: Polymarket (prediction market)
  and centralbank.watch (fed funds futures-derived). Both must agree for the branch to fire.
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
  **Object check built into this branch — the one that will break it if ignored:** the $429M figure is
  **2026 year-to-date on-chain revenue**, a different series from quarterly protocol revenue. Never
  compare a YTD cumulative to a quarterly level, and never difference them. See §5.5.

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

So the size of the incompleteness is not marginal: **a floor can be 60-84% low within one morning.**
Two rules follow. Publish an incomplete row as a floor *and name the missing funds* — doing that is
what let this run measure the gap instead of discovering it. And never let an incomplete row be the
thing that fires or withholds a branch if the missing fund could cross it on its own.

### 5.3 centralbank.watch updates its table without advancing its stamp
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
- **BNB 88.2%** — a share of *tokenized stock DEX volume*, for **BNB Chain + Robinhood Chain
  combined**, in a largely **non-US** market. It is not a single-chain share and not a share of the
  RWA market. The **SEC Innovation Exemption (Sept 17)** names no blockchain and no company — do not
  score it against the 88.2%. **Superseded for most purposes 2026-09-22:** reporting dated Sept 21
  gives the like-for-like figure directly — tokenized stocks **$3.5B** of market value, **BNB Chain
  $1.0B = 32.7%**, Ethereum $770.1M, Solana $715.9M (market was $3.1B on Sept 6). Quote **32.7% of
  market value** when the question is "how much of the tokenized-stock market is BNB Chain", and keep
  the 88.2% only when the subject really is DEX volume across the two chains. The lead survives; the
  magnitude was never seven eighths.
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
- **Article recency trap, second live example** (2026-09-23). A Solana ETF search returned "Solana ETF
  Inflows Fell 96% in a Week, From $153.87M to $6.18M" high in the results. Dated **Sept 8** — two
  weeks stale, and the week it describes has since been followed by the largest weekly inflow of the
  streak. Publishing it would have *inverted* the picture, not merely aged it.
- **Article recency trap, live example** (2026-09-22). A search for the CLARITY Act returned a Yahoo
  piece headlined "The Senate Has 5 Working Days Left" ranked near the top; it was published
  **Aug 2** and its "five working days" ran to the **Aug 7 recess**. Publishing it would have
  invented a September deadline. Check the date on every item — search rank is not recency.

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
the harness, not the build. **Four consecutive runs have now had a first-pass validation failure that
was the assertion's fault.** Audit the assertion before touching `index.html`, every time.

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

- [x] **GitHub push blocker — RESOLVED. Re-verified a fourth time 2026-09-23 02:00; STOP CARRYING IT.**
      The routine prompt still asks each run to re-check this. It has now pushed to `main` cleanly on
      four consecutive runs with the ambient credentials, with no fallback to a `claude/` branch and no
      pull request needed. **This item is closed. A future run should not spend time on it** beyond
      noting that the push succeeded. The session starts checked out on a `claude/...` branch that is
      even with `origin/main`; that is normal and is not a blocker. The local `main` *ref* is stale on
      session start — on 2026-09-23 it pointed at `d8ff50c` while `origin/main` was `62cbf8e`. Always
      `git fetch origin` before concluding anything about what is published.
- [x] **Sept 21 (Mon) ETF session — FINAL.** BTC **+$999.0M**, ETH **+$270.0M**, SOL **+$26.0M**.
      Re-read 2026-09-23 and unrevised on a second reading, so that revision has settled. Closed.
- [ ] **Sept 22 (Tue) rows are FLOORS — re-read them first thing.** BTC **+$364.4M** with **IBIT
      blank**; ETH **+$71.3M** with **ETHA and ETHB blank**; SOL **+$28.9M** complete. These are the
      same funds that filled in late on Sept 21 and moved those rows 61.7% and 83.6% upward inside five
      hours, and IBIT alone was +$381.4M on Monday — larger than the whole Sept 22 BTC total posted so
      far. Neither can fire a branch by rising, but the published figures will be wrong if not re-read.
- [ ] **SOL Sept 18 row still has two blanks** — VSOL and FSOL, unchanged for a third consecutive run.
      That week can only be revised **upward**, which can only strengthen the $60.7M restore.
- [ ] **SOL weekly print** for the week ending Sept 25, due ~Sept 26. Bar is a weekly print **below
      $5M**. Two of five sessions are in at **+$54.9M** (Sept 21 +$26.0M, Sept 22 +$28.9M), ~11x the
      bar. **Count the sessions before comparing it** — §5.1 rule 1. Three sessions still to settle.
- [ ] **Sept 29 — Glamsterdam client software deadline, six days out.** The *earlier* date to watch and
      the first place an Oct 6 slip becomes visible. Positive datapoint 2026-09-23: a private rehearsal
      carried the testnet to a block gas limit near **200 million without losing finality**.
- [ ] **Oct 1 — XRP downside trigger, eight days out.** Reaching it with no second cloture vote taken
      is "the window closing unused" and cuts 0.1. **The date gained independent corroboration
      2026-09-23:** the Senate calendar allowed only **fourteen working days** from the Sept 14 return
      before the October recess, and the fourteenth working day from Sept 14 is **Oct 1**. Blocker is
      still the ethics text on crypto holdings by public officials, not the whip count; Tillis motion
      to reconsider still preserved; lame duck is the named realistic slot.
- [ ] **Oct 6, 13:53:36 UTC** — Glamsterdam on Sepolia, epoch 353024, slot 11296768. Activation *and
      finality* adds 0.1 to ETH; a slip or failure to finalise cuts 0.1. Seven-day buffer against the
      usual fourteen. Contingent on **Devnet-11** staying stable.
- [ ] **Oct 27** — Hoodi Glamsterdam, provisional, contingent on Sepolia.
- [ ] **Oct 27-28 — FOMC.** The October meeting the Fed branch prices. Background: September hiked 25bp
      to a **3.75-4.00%** target range (centralbank.watch's 3.88% is that midpoint), the dot plot median
      carries one more hike in 2026, and 16 of 19 members expect at least one more this year — which is
      consistent with October pricing near a coin flip. The committee is more agreed on *whether* than
      on *when*.
- [ ] **Two branches were WRITTEN 2026-09-23 and are live from the next run — check them explicitly.**
      (a) **HYPE revenue leg**: quarterly protocol revenue above $260M restores 0.1, below $150M cuts
      0.1. (b) **BNB relative branch**: BNB against the median of the other five over a trailing
      seven-day window, +/-5pt. See §3 for both, including the object check that will break the HYPE one
      if ignored. **Neither is retroactive.** Record the BNB margin every run whether or not it fires.
- [x] **Fed route spread — CLOSING THIS ITEM 2026-09-23.** Four readings: 1.4pt -> 3.2pt -> 2.2pt ->
      **1.5pt**. It oscillates inside two points with no direction, and has had enough chances to show
      a trend. Keep reading both routes every run (the branch requires both to agree), but stop
      carrying the spread as a watch item. Re-open only if one route leads the other toward 75 or 40.
- [ ] **Iran / Hormuz — no branch names this, and one may be warranted.** Iran was reported on Sept 22
      to have offered, through mediators, to reopen the strait within seven days if the US lifts its
      naval blockade. A *confirmed* reopening would be the single largest macro input on this deck —
      it would move oil, risk appetite and the Fed path together — and **no written branch on any of
      the six names it**, so it could resolve entirely without moving a score. Consider writing one,
      or decide deliberately that it stays a macro-snapshot item only. Current state: a proposal
      relayed by third parties; the strait is still shut; best transit count remains **8 on Sept 13
      against an 85/day pre-crisis baseline**, and that count is typically a week or more old.
- [ ] **Stray snapshot** — `signal-deck-2026-09-21-0100utc.html` remains in the repo root, **three runs
      after it was first flagged**. It was uploaded by the user, so no run has deleted it. Harmless
      (Pages serves `index.html`) but it is a stale build sitting beside the live one, and one like it
      caused a five-day stale publish. **Still needs a yes/no from the user.** This run does not create
      dated snapshots and no future run should.
- [ ] **Pre-break levels** live only in prose (see §6). Consider a commented constant. Used unchanged
      again this run and they continue to reproduce the published percentages exactly.

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
- **The design is still not the run's subject.** Refresh runs edit `MACRO_SNAPSHOT`,
  `GLOBAL_CATALYSTS`, the per-coin score/summary/catalysts and `AS_OF` — the byte-identity assertion
  in §7 is what proves the rest was left alone.
- **Netlify tags are gone (2026-09-22).** The `<head>` carried three Netlify meta tags and an
  advertising comment claiming the site was served from Netlify Edge; it is served by GitHub Pages,
  and the routine prompt says not to use Netlify for anything. Do not let them back in.
