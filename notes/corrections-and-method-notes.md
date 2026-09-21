# Signal Deck — corrections and method notes

Standing method file for the scheduled refresh of `index.html`, published by GitHub Pages
at https://stevenchristiian.github.io/claudesignal/.

**Status of this file:** created 2026-09-21 06:00 UTC. The routine prompt instructs the run to
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

As published 2026-09-21 06:00 UTC (this run — six holds, no moves):

| Asset | Score | Held since |
|-------|-------|-----------|
| BTC   | -0.3  | Sept 20 (restored from -0.4 on the Sept 18 flow print) |
| ETH   | +0.4  | Sept 20 (restored from +0.3 on the Sept 18 flow print) |
| SOL   | +0.4  | Sept 16 (raised from +0.3; half the earlier flow cut restored) |
| BNB   |  0.0  | 13 consecutive runs |
| XRP   |  0.0  | 5 consecutive runs |
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
- **SOL flow leg** — a weekly ETF print **above $50M** restores the remaining 0.1; **below $5M**
  re-cuts it. **The instrument is a SoSoValue weekly print** — see 5.1.
- **XRP** — a second cloture vote *passing* adds 0.2; the motion failing, or the window closing
  unused, cuts 0.1.
- **BNB** — no numeric branch. Held while fundamentals improve and the price will not pay for them
  in either direction. A price response in either direction is what would move it.
- **HYPE** — moves on a **disclosed fee split or protocol revenue term** on the Payward/Bitnomial
  HIP-3 deployment. As of Sept 21 the absence is confirmed by the counterparty, not merely unfound.

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

### 5.1 The SOL weekly ETF figure has two publishers that disagree (found 2026-09-21)
For the **same week ending Sept 18 2026**, same instrument (US spot Solana ETFs):
- **$13.2M** — 24/7 Wall St (Sept 19) citing **SoSoValue**. Internally reconciles: Sept 14 $11.01M
  + Sept 15 $1.35M + Sept 16 $836,926 + Sept 17 *no change* = $13.20M.
- **$60.7M** — Solana Compass (Sept 20) citing **CryptoBriefing**, "strongest of the run", with
  ~$47.6M on the Thursday.

They reconcile: **$13.2M + $47.6M = $60.8M**. The entire gap is one Thursday (Sept 17) session that
SoSoValue records as flat. Not a week-definition difference, not rounding — **one disputed session
between two vendors.**

This *matters to the score*: $13.2M fires nothing, $60.7M clears the $50M restore bar. **Resolution:
the SOL branch is written against a SoSoValue weekly print**, and the $153.87M / $6.18M / $10.30M
readings behind it are the same series. Swapping vendor mid-series breaks the comparison the bar
depends on rather than resolving it. Publish both attributed, adopt neither, hold the score.
**Name the vendor in the branch text from now on.**

### 5.2 Farside rows settle incrementally and get revised
On Sept 16 this deck read ETH Sept 15 as **-$49.5M** from three posted lines and published it as the
session total. Farside now carries Sept 15 at **-$142.0M** across seven lines. A ~3x revision.
An early read of a same-day or previous-day row can be materially incomplete. Re-read prior rows on
each run; do not assume a published row is final. (The revised -$142.0M still sits above the -$150M
bar, so no leg fired retroactively — but it could have.)

### 5.3 centralbank.watch updates its table without advancing its stamp
Read **57.9 / 42.1 / 0.0** on Sept 21 01:00 and **55.9 / 44.1 / 0.0** on Sept 21 06:00 — both
displaying the **same "Sept 18" stamp**. The stamp does not date the figure. Quote the read and the
time *you* took it. The page states the policy rate (3.88%) correctly throughout; that anchor being
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

## 6. Tape method

- **Prices: Coinbase Exchange public API only** (`api.exchange.coinbase.com`), **completed candles
  only**. Hourly granularity 3600. The candle opening at `H` closes at `H+1`; at 05:56 UTC the last
  *complete* candle is the one opening 04:00. Exclude the in-progress hour.
- **The build stamp is the close time of the last completed candle.**
- State the **7-day and 21-day window** next to every drawdown. They often differ and the difference
  is load-bearing: on Sept 21 BTC set a fresh *seven-day* high (82,087.11) while its *twenty-one-day*
  high stayed 82,283.00 from Sept 3. Saying "fresh high" unqualified would have been wrong.
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
  ("Just a moment..."). It loads fine in headless Chromium, which clears the challenge in ~6s.
- **Playwright's Chromium does not trust the agent proxy CA** and fails every HTTPS request with
  `ERR_CERT_AUTHORITY_INVALID` — including, silently, the page's own live-price fetches. Importing
  the CA into the NSS store is *not* enough for Chromium 141 (it uses the Chrome Root Store). The
  fix that works is the supported enterprise policy: write
  `{"CACertificates": ["<base64 DER>", ...]}` from `/root/.ccr/agent-proxy-ca.crt` to
  `/etc/chromium/policies/managed/ccr-ca.json` (also `/etc/opt/chrome/policies/managed/`).
  Never disable TLS verification. This must be done **before** the validation render, or the render
  is not faithful to what a real visitor sees.

## 9. Open items (re-verify every run; correct them when they go stale)

- [x] **GitHub push blocker — RESOLVED.** Earlier notes referenced a push blocker for this routine.
      This run pushed to `main` successfully with the ambient credentials; there is no blocker.
      Remove this item if it stays clean for another run or two.
- [ ] **Sept 21 (Mon) ETF session** settles after the US close — first real test of both flow legs
      since Sept 18. BTC re-cut bar: one session < -$300M or two consecutive < -$150M.
      ETH: two consecutive < -$150M.
- [ ] **SOL weekly print** for the week ending Sept 25, due ~Sept 26. Bar: >$50M restores, <$5M
      re-cuts. **Read the SoSoValue figure specifically** (see 5.1).
- [ ] **Oct 6, 13:53:36 UTC** — Glamsterdam on Sepolia, epoch 353024, slot 11296768. Activation
      *and finality* adds 0.1 to ETH; a slip or failure to finalise cuts 0.1. Buffer is seven days
      against the usual fourteen.
- [ ] **Oct 27** — Hoodi Glamsterdam, provisional, contingent on Sepolia. (This retires the
      long-carried "Hoodi has no activation date" item.)
- [ ] **XRP** — no second cloture vote scheduled; Tillis motion to reconsider still preserved. The
      blocker is the **ethics text on crypto holdings by public officials**, not the whip count.
      Lame duck after the midterms is the named realistic slot.
- [ ] **HYPE** — still no disclosed fee split or protocol revenue term on the Payward/Bitnomial
      deployment; Payward explicitly declined to give one. Subject to regulatory approval.
- [ ] **Stray snapshot** — `signal-deck-2026-09-21-0100utc.html` remains in the repo root. Harmless
      (Pages serves `index.html`), left in place deliberately. Decide whether to keep dated
      snapshots as a series or drop them.
- [ ] **Pre-break levels** live only in prose (see 6). Consider a commented constant.
