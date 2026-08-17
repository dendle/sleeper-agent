# Sleeper Fantasy Agent — Guidance for Future Sessions

## League & Identity
- **League:** UK 12T PPR Superflex (Dynasty, SF PPR, 12 teams)
- **League ID:** `1317862186214780928`
- **Draft ID:** `1317862186223149056`
- **User:** rainmannfl | **User ID:** `1160282581892685824` | **Roster ID:** 10 | **Draft Slot:** 9
- **Season:** 2026

## Strategy
`strategy.md` in this folder is the CURRENT team strategy (last-updated date + TLDR + detail). Read it before making any decision — draft pick, trade, waiver claim, or lineup call — it is the decision framework. It only ever contains current strategy: update it in place on significant events (draft picks affecting our board, trade outcomes/offers, material injuries, phase changes like Aug 26 cuts or season start, new instructions from Matt, KTC shifts that change a recommendation), rewrite affected sections so no stale/old plans remain, and bump its date. Do NOT update it on quiet monitoring runs, and never append history to it — history lives in the run logs.

## Cached Data (refresh as needed)
All cached files live in `cache/` in this folder:
- `cache/league.json` — league settings, scoring, roster positions
- `cache/rainmannfl_roster.json` — full roster with position analysis and needs
- `cache/2026_rookie_rankings.json` — 2026 rookie draft rankings and picks made

## Key API Endpoints (Sleeper public API — no auth required)
```
# League state
GET https://api.sleeper.app/v1/league/1317862186214780928

# Draft state + picks made
GET https://api.sleeper.app/v1/draft/1317862186223149056
GET https://api.sleeper.app/v1/draft/1317862186223149056/picks
GET https://api.sleeper.app/v1/draft/1317862186223149056/traded_picks

# Rosters (all 12 teams)
GET https://api.sleeper.app/v1/league/1317862186214780928/rosters

# Users
GET https://api.sleeper.app/v1/league/1317862186214780928/users

# Trending adds (last 24h)
GET https://api.sleeper.app/v1/players/nfl/trending/add?lookback_hours=24&limit=50

# IMPORTANT: Full players JSON is ~10MB — WebFetch will fail with maxContentLength error.
# Use the Chrome browser JS tool instead:
# await fetch('https://api.sleeper.app/v1/players/nfl').then(r => r.json())
# Then filter in JS. This works because the browser has no size limit.
# The position filter ?position=RB does work but misses many 2026 rookies.
# years_exp=0 filter is unreliable — many rookies don't appear.
# Best approach: fetch all players in JS and filter by years_exp===0 + position + team.
```

## Player Lookup Pattern (use JS tool in Chrome)
```javascript
// Look up specific player IDs
const data = await fetch('https://api.sleeper.app/v1/players/nfl').then(r => r.json());
const ids = [4984, 8155, ...];
const result = {};
for (const id of ids) {
  const p = data[String(id)];
  if (p) result[id] = { name: p.full_name, pos: p.position, team: p.team, age: p.age, years_exp: p.years_exp, rank: p.search_rank };
}

// Get all 2026 rookies ranked
const rookies = Object.entries(data)
  .filter(([id, p]) => p.years_exp === 0 && ['QB','RB','WR','TE'].includes(p.position) && p.team)
  .map(([id, p]) => ({ id, name: p.full_name, pos: p.position, team: p.team, rank: p.search_rank || 9999999, depth: p.depth_chart_order }))
  .sort((a, b) => a.rank - b.rank);
```

## Trade Evaluation — MANDATORY: use the KTC Trade Calculator, never raw value sums
Before proposing, accepting, or judging ANY trade, follow `.claude/skills/ktc-trades/SKILL.md`. In short: simulate the exact trade at `https://keeptradecut.com/trade-calculator` (Superflex mode), and trust the calculator's adjusted verdict — it applies a **Value Adjustment** that penalizes quantity-for-quality packages. Summing raw KTC values overrates multi-player packages: 10 players rated 1,000 do NOT equal one 9,999 player. The Wilson + Williams → Chase offer (3rd run) made this mistake — raw sums looked ~even, but the adjusted verdict was a clear loss for the Chase side, and it was rejected. Expect to overpay on raw value in any 2-for-1 for a stud.

## Draft Actions (Chrome browser required — no public API for picks)
To make a draft pick:
1. Navigate to: `https://sleeper.com/draft/nfl/1317862186223149056`
2. Wait for the draft room to load
3. Use `computer(screenshot)` to verify current state
4. Search for the player using the search box (Ctrl+U shortcut)
5. Click the "+" button or the player row to queue them
6. Click the pick/draft button to confirm
7. Screenshot to verify pick was made

**IMPORTANT:** Sleeper draft picks CANNOT be made via REST API. Must use browser automation.

## rainmannfl Roster Summary (updated 2026-08-15, confirmed live 8th run)

### Starters (current)
| Pos | Player | Team | Age | Notes |
|-----|--------|------|-----|-------|
| QB | Josh Allen (4984) | BUF | 30 | Elite, franchise QB |
| RB | Breece Hall (8155) | NYJ | 25 | RB1, elite |
| RB | David Montgomery (5892) | HOU | 29 | Aging, needs replacement |
| WR | Jakobi Meyers (5947) | JAX | 29 | Aging, depth 3 at JAX |
| WR | Michael Pittman (6819) | PIT | 28 | QUES preseason — monitor for Week 1 |
| TE | Trey McBride (8130) | ARI | 26 | Elite TE |
| FLEX | Javonte Williams (7588) | DAL | 26 | Depth 1 at DAL — starting RB! |
| FLEX | Brock Bowers (11604) | LV | 23 | Elite TE, moved to WRT starter (7th run) |
| SF | Jared Goff (3163) | DET | 31 | Good SF option |

### Bench (12 players — as of 7th/8th run, roster is clean)
- **Garrett Wilson** (WR, NYJ, id 8146) — elite WR depth 1, 91% start%, bench behind Pittman/Meyers; swap in if Pittman remains QUES for Week 1
- **Xavier Worthy** (WR, KC, id 11624) — QUES preseason, depth 2
- **Audric Estime** (RB, NO, id 11579) — depth 6 at NO — minimal value, potential drop candidate
- **Kaleb Johnson** (RB, PIT, id 12504) — 2026 rookie RB, depth 4 at PIT
- **Tre' Harris** (WR, LAC, id 12509) — 2026 rookie WR
- **Kirk Cousins** (QB, LV, id 1166) — excess QB, trade candidate (pitched to Revs1); depth 2 at LV behind Mendoza
- **Christian Kirk** (WR, SF, id 4950) — aging WR, QUES preseason, depth 4
- **Jauan Jennings** (WR, MIN, id 7049) — aging WR, depth 3
- **Jake Ferguson** (TE, DAL, id 8110) — depth TE, depth 1 at DAL
- **Quentin Johnston** (WR, LAC, id 9754) — depth 2 at LAC
- **Tucker Kraft** (TE, GB, id 9484) — QUES (knee recovery), depth 1 at GB; moved from IR to bench in 7th run

### Reserve/IR
- **EMPTY** — all 3 IR slots are clear after 7th run cleanup

### Taxi (2)
- Spencer Rattler (QB, NO, id 11562) — excess QB depth
- Javon Baker (WR, FA/no team, id 11645) — no NFL team, minimal value

### Roster Needs (Dynasty Priority)
1. **WR youth** — Meyers/Kirk/Jennings all 29+, need replacements (draft pick 1.9 targets this)
2. **RB youth** — Conner 31, Montgomery 29, declining
3. **NOT QB** — have Allen, Goff, Cousins, Rattler (4 QBs now, after O'Connell dropped)
4. **NOT TE** — have Bowers (rank 20!), McBride, Kraft, Ferguson — overstacked at TE

## 2026 Draft Strategy

### Draft Slot: Pick 9 of 12 (Rounds 1, 2, 3)

### Round 1 (Pick 9) — LIVE STATE as of 2026-08-14: draft restarted, now at pick 1.3, RexRocknut on the clock
**⚠️ The draft was restarted since the 2026-07-16/07-22 notes below were written.** Live `GET /draft/1317862186223149056/picks` on 2026-08-14 shows only **2 picks made total** (not 5), and pick 2 is now a different player than before — confirming the "restart vs. continue" discussion in league chat resolved to a full restart with a reshuffled order, not a resume from pick 6.

**Confirmed live picks (as of 2026-08-14):**
- 1.1: Jeremiyah Love (RB, ARI) — picked by DarrenA1 (roster 1)
- 1.2: Carnell Tate (WR, TEN) — picked by Kimish (roster 7)

**On the clock: Pick 1.3 — RexRocknut (roster 3, draft slot 3)** — confirmed both by the user directly and by cross-referencing `slot_to_roster_id` (slot 3 → roster 3) against `users.json` (roster 3 owner → RexRocknut). Note: the league object's own `metadata.current_pick_no` ("6") and `on_the_clock_user_id` (resolves to FORDJTFC, slot 6) are **stale/unreliable** — don't trust those two fields; trust the picks endpoint + slot map instead.

Pick 9 (rainmannfl, us) is still **6 picks away** in round 1. The prior "available at pick 6+" analysis below was built against the old (pre-restart) pick 1-5 board and needs to be re-evaluated once picks 3-8 land in the new draft, since the player pool remaining at our actual pick 9 slot may now differ.

**Prior (pre-restart, now stale) available-at-pick-6+ analysis — re-verify before acting:**
1. Makai Lemon (WR, PHI, rank 77) — will likely go pick 6
2. Kenyon Sadiq (TE, NYJ, rank 109) — TE need low for rainmannfl
3. KC Concepcion (WR, CLE, rank 116) — WR1 at CLE, good value
4. Omar Cooper (WR, NYJ, rank ~95 draft room) — Sleeper projects at pick 9
5. Jonah Coleman (RB, DEN, rank 118)

**Recommendation for Pick 9 (pending re-verification against the restarted board):** Omar Cooper (WR, NYJ) or KC Concepcion (WR, CLE) — whichever best WR is available. Skip Kenyon Sadiq (don't need TE). Skip Ty Simpson (don't need QB).

### Round 2 (Pick 9) — Target: Best available RB or WR
### Round 3 (Pick 9) — Target: Upside WR or RB with good landing spot

## Slot-to-Roster Mapping (draft order)
| Slot | Roster ID | Manager |
|------|-----------|---------|
| 1 | 11 | Revs1 |
| 2 | 7 | Kimish |
| 3 | 3 | RexRocknut |
| 4 | 12 | cdavis2506 |
| 5 | 9 | jiedunbar |
| 6 | 2 | FORDJTFC |
| 7 | 4 | Lurchh |
| 8 | 1 | DarrenA1 |
| **9** | **10** | **rainmannfl ← US** |
| 10 | 6 | CMCPanthers |
| 11 | 8 | FukLender |
| 12 | 5 | antsinpants |

## In-Season Tasks (post-draft)
- Set lineups each week via Sleeper browser UI
- Monitor waiver wire via trending adds API
- Check injury reports and adjust starters
- Key watch: Brock Bowers return from reserve (rank 20!)
- Key watch: Garrett Wilson should be starting over Meyers

## Context Notes
- Draft was paused by commish on 2026-07-16 after 5 picks
- League chat discussed restarting vs. continuing — decided to restart/pick up
- Some autopicks were made (picks 2, 4 were CPU autopicks per chat)
- Traded picks: FORDJTFC/Revs1 made a 2-way trade (saw in chat)

## Standing Instructions from Matt (durable — do not violate)
- **No nudges on silent trade offers (2026-08-15):** Do NOT follow up / nudge Revs1 (or anyone) about an unanswered trade offer. If an offer gets no reply, leave it; forget it entirely if still silent after ~1 month (~2026-09-15). No follow-up DMs on silent offers, ever.
- **Chase pursuit CLOSED (2026-08-15):** Matt confirmed via WhatsApp that RexRocknut rejected the Wilson+Williams-for-Chase deal and doesn't want anything we have. Do not re-approach RexRocknut on Chase.
- **Picks API lags the real board (2026-08-16 lesson):** `/draft/<id>/picks` can lag the live board by several picks. ALWAYS verify draft state via the browser draft board when close to our pick. The league object's `metadata.current_pick_no` / `on_the_clock_user_id` are also stale/unreliable post-restart.
- **Pick 1.9 board CONFIRMED by Matt (2026-08-16):** 1) Makai Lemon (WR-PHI), 2) Omar Cooper (WR-NYJ), 3) De'Zhaun Stribling (WR). Skip QB (Simpson/Mendoza-tier) and TE (Sadiq). Execute without further confirmation when 1.9 arrives.

## Current Status (snapshot — OVERWRITE this section each run, don't append)
_As of: 2026-08-17 14:00, 35th automated run._
- **Draft:** Still one pick away (1.9). Board confirmed live: 1.7 = Makai Lemon (WR-PHI, FORDJTFC); FORDJTFC on the clock for 1.8 (2nd pick via DarrenA1 trade), ~7h20m remaining on the 24h clock when checked. Both board targets — Omar Cooper (WR-NYJ) and De'Zhaun Stribling (WR-SF) — confirmed still available. Execute without asking per standing instruction the moment 1.9 arrives. Picks API still lags the live board by ~1 pick (known gotcha) — browser board is ground truth.
- **Trades:** Active Trades tab confirms exactly 1 open trade — our outgoing Revs1 offer (Cousins + Rattler + C. Kirk → Travis Hunter). No reply yet — no nudge per standing instruction. RexRocknut/Chase thread remains closed, nothing new. FORDJTFC thread confirmed stale/dead (2mo old, unanswered). Trade block scanned — no new listings match our pre-identified buy targets, no unsolicited pitches sent.
- **Roster:** Confirmed via `/rosters` — 22-player list unchanged since 2026-08-14, no IR slots in use, taxi unchanged (Rattler, Baker). Injury re-check via players/nfl: same 5 Questionable tags as before (Estime, Worthy, C. Kirk, Pittman, Kraft), none escalated — no IR moves or drops triggered.
- **NFL state:** Preseason, league status "drafting", `/matchups/1` empty (no active matchup), no waivers before Aug 26 cuts.
- **Next-run watch:** We're one pick from 1.9 — verify board and execute Cooper/Stribling the moment FORDJTFC's 1.8 clock resolves. Keep watching for a Revs1 reply on the Hunter offer (no nudge).

## Audit Trail (run logs)
Per-run session notes live under `runs/<YYYY>/<MM>/<DD>/`, one file per run:
- **New runs:** write a new file `runs/<YYYY>/<MM>/<DD>/<HHMM>-<slug>.md` (24h local time, short slug like `monitoring`, `trade-submission`, `draft-pick`). Do NOT append run logs to this file.
- **Historical runs** (before this structure existed) are named `run-NN-<slug>.md`; NN is the run ordinal.
- **Reading back:** to catch up, read this file plus only the most recent 1–2 run files (`ls` the latest date folder). Only dig into older runs if investigating something specific.
- After logging the run, update the **Current Status** snapshot above (overwrite in place) and fold any new durable rules/lessons into the sections above — that's what keeps this file small.
