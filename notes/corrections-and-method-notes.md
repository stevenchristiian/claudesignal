# Signal Deck — corrections and method notes

Standing method file for the scheduled refresh of `index.html`, published by GitHub Pages
at https://stevenchristiian.github.io/claudesignal/.

**Status of this file:** created 2026-09-21 06:00 UTC; last updated 2026-09-22 02:00 UTC. The routine prompt instructs the run to
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

As published 2026-09-22 02:00 UTC (SOL +0.1; five holds):

| Asset | Score | Held since |
|-------|-------|-----------|
| BTC   | -0.3  | Sept 20 (restored from -0.4 on the Sept 18 flow print) |
| ETH   | +0.4  | Sept 20 (restored from +0.3 on the Sept 18 flow print) |
| SOL   | **+0.5**  | **Sept 22** (remaining 0.1 restored on the completed $60.7M week to Sept 18) |
| BNB   |  0.0  | 14 consecutive runs |
| XRP   |  0.0  | 6 consecutive runs |
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
- **BNB** — no numeric branch. Held while fundamentals improve and the price will not pay for them
  in either direction. A price response in either direction is what would move it. **This needs a
  numeric definition (flagged 2026-09-22).** On Sept 21 every one of the six set a twenty-one-day
  high; read loosely, "a price response" fires on pure beta. BNB was the *second weakest* of the six
  that session (+1.92% against BTC +5.71%), which is evidence *for* the hold. Proposal: define it
  **relative** — BNB outperforming or underperforming the median of the other five by some margin
  over a stated window — not as an absolute move.
- **HYPE** — moves on a **disclosed fee split or protocol revenue term** on the Payward/Bitnomial
  HIP-3 deployment. As of Sept 21 the absence is confirmed by the counterparty, not merely unfound.
  **The branch is narrower than the thesis it serves (flagged 2026-09-22).** The -0.1 handicaps
  *protocol revenue erosion from HIP-3* ($356.7M in Q3 2025 -> $201.8M in Q2 2026), but the branch
  names one deal and one disclosure. Native lending launched Sept 18 and borrowed **$269M on day
  one** (65% LTV on HYPE, 50% on BTC) — squarely evidence on the thesis, and it fired nothing.
  Consider adding a revenue-level branch (e.g. a reported quarterly protocol revenue figure crossing
  a stated level). Until one is written, do **not** move the score on thesis evidence — write the
  branch first, then let it fire.

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
  RWA market. BNB Chain alone holds ~$1B issuance inside a ~$3.1B tokenized-stock market cap.
  The **SEC Innovation Exemption (Sept 17)** names no blockchain and no company — do not score it
  against the 88.2%.
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
- **Article recency trap, live example** (2026-09-22). A search for the CLARITY Act returned a Yahoo
  piece headlined "The Senate Has 5 Working Days Left" ranked near the top; it was published
  **Aug 2** and its "five working days" ran to the **Aug 7 recess**. Publishing it would have
  invented a September deadline. Check the date on every item — search rank is not recency.

## 6. Tape method

- **Prices: Coinbase Exchange public API only** (`api.exchange.coinbase.com`), **completed candles
  only**. Hourly granularity 3600. The candle opening at `H` closes at `H+1`; at 05:56 UTC the last
  *complete* candle is the one opening 04:00. Exclude the in-progress hour.
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
   differences are the as-of lines. This catches design/JS drift — and it caught a real bug this
   run (see 8).
8. Stale-string checks scoped to the *previous build's* phrasing, not to generic words.
9. **Superlative / count / margin grep** over every published string; verify each claim against the
   tape. This caught a false "oldest high of the six" this run (see 8).
10. **Headless Chromium render**: `#macroGrid` 6, `#catalystsRow` 21, `#assetGrid` 6, and
    **zero uncaught JS exceptions**.

### Three "as of" labels, not one
They live at three places and a run that updates only the visible heading will ship a stale page:
- the `<h2>` macro heading — `Sept 21, 2026 (06:00 UTC)`
- the footer disclaimer — `06:00 UTC on September 21, 2026`
- **a `.sect-label` inside a JS template literal** in `renderAssets` — `Sept 21, 2026, 06:00 UTC`.
  This one is easy to miss: it is inside a backtick string, not in the HTML body.

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

- [x] **GitHub push blocker — RESOLVED, reconfirmed 2026-09-22.** Earlier notes referenced a push
      blocker for this routine. It pushed to `main` cleanly on 2026-09-21 and again on 2026-09-22
      with the ambient credentials. **Two clean runs — treat this as settled and stop carrying it.**
      Note the session starts checked out on a `claude/…` branch that is even with `origin/main`;
      that is normal, not a blocker.
- [x] **Sept 21 (Mon) ETF session — SETTLED, both flow legs tested.** BTC +$617.6M, ETH +$147.1M.
      Neither re-cut bar fired. Both rows are **incomplete**: BTC missing IBIT, ETH missing ETHA and
      ETHB. **Re-read them next run** — they can be revised materially (see 5.2).
- [x] **SOL weekly print, week to Sept 18 — RESOLVED at $60.7M**, the restore fired (see 5.1).
- [ ] **SOL weekly print** for the week ending Sept 25, due ~Sept 26. Bar is now **below $5M
      re-cuts** (the restore is spent). **Count the sessions in the week before comparing it.**
      The week opened at +$26.0M on Sept 21, six of seven funds positive.
- [ ] **Oct 1 — XRP downside trigger.** The Senate is due to leave; reaching that date with no second
      cloture vote taken is "the window closing unused" and cuts 0.1. Nine days out as of Sept 22.
      Blocker is still the ethics text on crypto holdings by public officials, not the whip count;
      Tillis motion to reconsider still preserved; lame duck is the named realistic slot.
- [ ] **Oct 6, 13:53:36 UTC** — Glamsterdam on Sepolia, epoch 353024, slot 11296768. Activation
      *and finality* adds 0.1 to ETH; a slip or failure to finalise cuts 0.1. Buffer is seven days
      against the usual fourteen.
- [ ] **Oct 27** — Hoodi Glamsterdam, provisional, contingent on Sepolia.
- [ ] **HYPE** — still no disclosed fee split or protocol revenue term on the Payward/Bitnomial
      deployment; Payward explicitly declined to give one. Subject to regulatory approval.
      **Separately: the branch is narrower than the thesis — see 3.** Native lending (Sept 18,
      $269M day one) fired nothing.
- [ ] **BNB non-branch needs a numeric, relative definition — see 3.** Nearly fired on pure beta
      this run.
- [ ] **Fed routes are diverging.** Spread between Polymarket and centralbank.watch went 1.4pt
      (Sept 21) -> 3.2pt (Sept 22). Both still mid-band. Watch whether one route leads before either
      approaches 75 or 40.
- [ ] **Stray snapshot** — `signal-deck-2026-09-21-0100utc.html` remains in the repo root. Harmless
      (Pages serves `index.html`), left in place deliberately. **Recommendation: stop creating dated
      snapshots** — one of them caused a five-day stale publish. Decide and act.
- [ ] **Pre-break levels** live only in prose (see 6). Consider a commented constant. They were used
      unchanged again this run and continue to reproduce the published percentages.
