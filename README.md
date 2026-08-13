# Daily Market Report — Prototype v1.5

Static HTML/CSS/JS prototype. No build step — open any file directly, or serve the folder as-is.

**Send testers to `index.html`.**

## Why v1.5 exists

v2 replaced the report's news table with **twelve curated items**. That only holds together if the full list is one click away with a summary on every entry — and at launch the news area won't have full summary coverage. So cutting the report from ~29 announcements to 12 would be a straight subtraction with nothing offered in return, felt hardest by the small-cap community who comment most.

v1.5 keeps everything and changes the hierarchy instead. It is **close to the version already tested, with the analyst notes pulled above the table rather than sitting below it.**

| | v1 / today's live report | v1.5 | v2 |
| --- | --- | --- | --- |
| Announcements shown | ~29 in a table | **28 in a table** | 12 |
| Analyst notes | long-form sections *below* the table | **a stream *above* the table** | inline in each of the 12 items |
| Coverage loss | — | **none** | 17 announcements |
| Depends on AI summaries | no | **no** | yes |

## The page

1. **The overnight** — macro and market moves, unchanged
2. **Analyst notes** — a live stream of the notes filed so far, newest first
3. **Companies reporting (28)** — one uniform table, every row with a summary
4. **Today's news** — links to the full market and portfolio lists
5. **Meet the analysts**, **Discussion**

### Analyst notes — the stream

Modelled on a newspaper live blog. Entries run **newest first**, each introduced by its filing time sitting on the rule above it. Anything filed since the reader's last visit (hardcoded `lastVisit = '11:00'`) is marked **New** in red; everything older is grey.

Each entry is deliberately spare — a headline naming the company, then the analyst's note in italic with face, name, rating and a link to the full article. No earnings chip and no price: both are on that company's row in the table below, and repeating them was what made an earlier two-tier attempt read as a jumble.

### Why the split works here

The two tiers differ in **depth, not just layout**: the stream carries the analyst's judgement, the table carries the RNS summary. And the criterion for appearing in the stream is objective — an analyst wrote about it — rather than an editorial ranking that has to be defended.

## The three states

The selector top-right is prototype scaffolding, labelled `v1.5` so it can't be confused with v2 in a session. Hide or ignore it when framing.

| State | Stream | Table |
| --- | --- | --- |
| **08:30** | Empty — "No analyst notes yet. The first are filed mid-morning" | All 28, every one summarised |
| **12:30** | 6 notes, 2 marked New | All 28 |
| **17:05** | 8 notes, 4 marked New | All 28 |

At 08:30 the page is essentially today's live report — a complete table — with analysis accumulating above it through the morning. That is a truthful model of how the report actually works, and it avoids v2's problem of presenting editorial structure at 08:30 with no editorial content in it.

## Interaction

- **Company name** (in stream or table) → the StockReport
- **Announcement title** in the table → the full RNS in a bottom sheet
- **View analysis** → the atomic article (`gaw.html`, `pzc.html`, etc.)
- The stream's headline is **not** a link — View analysis is the route

## Data

Placeholder content only — **nothing here reflects real Stockopedia data.**

28 announcements, 8 with an analyst note, 4 held in the reader's portfolios. Coverage is limited to the eight items that have an article behind them, which matches the live report (8 of 29 carried a view on 17 June 2026).

## Relationship to the other folders

- `../prototype/` — v1, the tested reference
- `../prototype-v2/` — the twelve-item curated version
- `./` — this

All three hold **their own copy of the announcement data.** They agree today; editing one will not update the others. Reconcile by hand, or extract a shared data file before the next round.

## Known gaps

- `test-links.html` doesn't list `news.html`.
- If Material Symbols fails to load, ligature names render as text — the folder marker would read "£6.7bnfolder". Relevant on locked-down networks.
- Ratings still use Ed's five bands; the live report uses GREEN / AMBER / AMBER-GREEN. Worth not changing both structure and rating vocabulary in one release.
