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

## rainmannfl Roster Summary (updated 2026-08-19 13:05, confirmed live — Hunter trade processed, pick 2.9 made)

### Starters (current)
| Pos | Player | Team | Age | Notes |
|-----|--------|------|-----|-------|
| QB | Josh Allen (4984) | BUF | 30 | Elite, franchise QB |
| RB | Breece Hall (8155) | NYJ | 25 | RB1, elite. QUES — groin strain (news 2026-08-19), expected back for Sept 13 opener |
| RB | David Montgomery (5892) | HOU | 29 | Aging, needs replacement |
| WR | Jakobi Meyers (5947) | JAX | 29 | Aging, depth 3 at JAX |
| WR | Michael Pittman (6819) | PIT | 28 | Hamstring, QUES tag still on but news (2026-08-19 19:05) says expected ready for Week 1, no lingering concern |
| TE | Trey McBride (8130) | ARI | 26 | Elite TE |
| FLEX | Javonte Williams (7588) | DAL | 26 | Depth 1 at DAL — starting RB! |
| FLEX | Brock Bowers (11604) | LV | 23 | Elite TE, moved to WRT starter (7th run) |
| SF | Jared Goff (3163) | DET | 31 | Good SF option |

### Bench (11 players synced + 2 pending draft-pick sync — Cousins/Rattler/C.Kirk traded away, Hunter added, 2026-08-19; Omar Cooper + Braelon Allen not yet synced to /rosters API — known lag)
- **Braelon Allen** (RB, NYJ, id 11576) — drafted 2.9 (2026-08-19). RB2 behind our own Breece Hall (direct handcuff/insurance given Hall's groin strain), age 22, proven producer (802 rookie-yr yards 2024). Not yet synced to /rosters API — expected, syncs once the 3-round draft fully completes.
- **Omar Cooper** (WR, NYJ, id 13276) — drafted 1.9 (2026-08-17 rookie draft), rank 107. Camp news: losing ground for early-season slot work behind G. Wilson/Isaiah Williams/Adonai Mitchell — dynasty stash, monitor depth chart, no action needed. Still absent from /rosters API as of 2026-08-19 — expected, syncs once the 3-round draft fully completes.
- **Travis Hunter** (WR, JAX, id 12530) — ACQUIRED 2026-08-19 via trade w/ Revs1 (sent Cousins+Rattler+C.Kirk). Buy-low ex-top-2 pick, recovering from Nov 2025 knee surgery; camp reports (2026-08-19) say recovery "going as expected," two-way WR/CB role planned, WR snaps possibly limited early season — monitor camp/Week 1 role.
- **Garrett Wilson** (WR, NYJ, id 8146) — elite WR depth 1, 91% start%, bench behind Pittman/Meyers; swap in if Pittman remains QUES for Week 1
- **Xavier Worthy** (WR, KC, id 11624) — QUES preseason, depth 2
- **Audric Estime** (RB, NO, id 11579) — depth 6 at NO — minimal value, potential drop candidate
- **Kaleb Johnson** (RB, PIT, id 12504) — 2026 rookie RB, depth 4 at PIT
- **Tre' Harris** (WR, LAC, id 12509) — 2026 rookie WR
- **Jauan Jennings** (WR, MIN, id 7049) — aging WR, depth 3
- **Jake Ferguson** (TE, DAL, id 8110) — depth TE, depth 1 at DAL
- **Quentin Johnston** (WR, LAC, id 9754) — depth 2 at LAC
- **Tucker Kraft** (TE, GB, id 9484) — QUES (knee recovery), depth 1 at GB; moved from IR to bench in 7th run

### Reserve/IR
- **EMPTY** — all 3 IR slots are clear

### Taxi (1 of 3 slots used)
- Javon Baker (WR, FA/no team, id 11645) — no NFL team, minimal value
- 2 slots open — backfill from rookie draft picks (e.g. Omar Cooper) once draft completes and picks sync to roster. Spencer Rattler left the taxi squad via the Hunter trade (2026-08-19).

### Roster Needs (Dynasty Priority)
1. **WR youth** — Meyers/Kirk/Jennings all 29+, need replacements (draft pick 1.9 targets this)
2. **RB youth** — Conner 31, Montgomery 29, declining
3. **NOT QB** — have Allen, Goff, Cousins, Rattler (4 QBs now, after O'Connell dropped)
4. **NOT TE** — have Bowers (rank 20!), McBride, Kraft, Ferguson — overstacked at TE

## 2026 Draft Strategy

### Draft Slot: Pick 9 of 12 (Rounds 1, 2, 3)

### Round 1 (Pick 9) — DONE (2026-08-17): took Omar Cooper (WR-NYJ). Board through 1.9: 1.1 Love, 1.2 Tate, 1.3 Tyson, 1.4 Mendoza, 1.5 Concepcion, 1.6 Price, 1.7 Lemon (FORDJTFC), 1.8 Branch (FORDJTFC, traded 2nd pick), **1.9 Cooper (us)**.

### Round 2 (Pick 9) — DONE (2026-08-19): took Braelon Allen (RB-NYJ) — RB2 behind our own Breece Hall, proven producer, better landing spot than any rookie WR/RB left on the board. **This is a LINEAR draft, not snake** — confirmed via live board: round 2 order is identical to round 1 (2.1 Revs1 → 2.2 Kimish → ... → 2.9 rainmannfl → 2.12 antsinpants), round 3 follows the same pattern. Do not assume snake reversal.
### Round 3 (Pick 9) — Target: best available WR or RB at the time, no fixed list — re-check live board + KTC before acting. Same linear order as round 2 (3.1 starts at Revs1, works down to us at 3.9). ~11 picks away as of 2026-08-19 13:05.

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

## Git on this mount — workaround required (2026-08-17 lesson)
This folder is a write-once-ish FUSE mount: files can be created and **overwritten**, but **never unlinked or renamed** (`rm`/`mv` return `Operation not permitted` even on files you just created, even as the owning user). Plain `git commit`/`git add` will eventually leave a stale `.git/index.lock` or `.git/HEAD.lock` that can never be cleaned up, permanently breaking normal git commands in this repo. **Do not run plain `git add`/`git commit` here.** Use this workaround every time you need to commit:
```bash
export GIT_INDEX_FILE=/tmp/sleeper_index_$$   # index lives in /tmp, not the mount — avoids index.lock entirely
git read-tree HEAD
git add -A                                     # stage against the temp index
TREE=$(git write-tree)
COMMIT=$(echo "commit message" | git commit-tree $TREE -p HEAD)
echo "$COMMIT" > .git/refs/heads/main          # overwrite (not rename) the loose ref directly — bypasses HEAD.lock
cp $GIT_INDEX_FILE .git/index                  # sync the real index (overwrite, not rename) so `git status` reads correctly after
```
Harmless `warning: unable to unlink '.git/objects/xx/tmp_obj_...'` lines during `write-tree`/`commit-tree` are expected (temp object files can't be cleaned up either) — the permanent object still gets created correctly; ignore these warnings. If a stray `.git/index.lock`/`HEAD.lock` already exists from a prior broken run, it cannot be removed — just use the workaround above, which never touches those files.

**Verify every commit before moving on (2026-08-18 lesson):** occasionally `git read-tree HEAD` / `git add -A` against the temp index silently fails (`fatal: unable to write new index file`) while still returning exit 0 further down the pipeline, producing a commit whose tree is stale/wrong (e.g. missing just-added files, or reverting other files to an older version) even though the commit object gets created and the ref gets updated without visible fatal errors at the top level. **Always run `git show --stat HEAD` (or `git diff <expected-parent> HEAD --stat`) right after committing** and confirm the file list matches exactly what you intended to change — nothing unexpected added/removed/reverted. If it doesn't match, don't try to patch on top: re-run the whole workaround from `git read-tree HEAD^` (the last known-good commit) with a fresh temp index file (new filename), re-stage, and recommit, then re-verify. Always `rm -f` the temp index path first / use a unique name — a leftover temp index from an earlier failed attempt can cause exactly this symptom.

## Standing Instructions from Matt (durable — do not violate)
- **No nudges on silent trade offers (2026-08-15):** Do NOT follow up / nudge Revs1 (or anyone) about an unanswered trade offer. If an offer gets no reply, leave it; forget it entirely if still silent after ~1 month (~2026-09-15). No follow-up DMs on silent offers, ever.
- **Chase pursuit CLOSED (2026-08-15):** Matt confirmed via WhatsApp that RexRocknut rejected the Wilson+Williams-for-Chase deal and doesn't want anything we have. Do not re-approach RexRocknut on Chase.
- **Picks API lags the real board (2026-08-16 lesson):** `/draft/<id>/picks` can lag the live board by several picks. ALWAYS verify draft state via the browser draft board when close to our pick. The league object's `metadata.current_pick_no` / `on_the_clock_user_id` are also stale/unreliable post-restart.
- **Pick 1.9 board CONFIRMED by Matt (2026-08-16):** 1) Makai Lemon (WR-PHI), 2) Omar Cooper (WR-NYJ), 3) De'Zhaun Stribling (WR). Skip QB (Simpson/Mendoza-tier) and TE (Sadiq). Execute without further confirmation when 1.9 arrives.

## Current Status (snapshot — OVERWRITE this section each run, don't append)
_As of: 2026-08-21 21:04 BST (20:04 UTC), 103rd automated run — quiet monitoring sweep, no action needed._
- **Draft:** Not our turn. **Still Round 3** — 3.2 (T. Hurst, WR-TB) remains the last landed pick, no new picks since last run. **FORDJTFC still on the clock for 3.3** (traded pick from RexRocknut's slot, timer at 23:39/24h remaining — same pick, clock ticking down). 2.9 Braelon Allen still our last completed pick. **Still 6 picks away from 3.9**, unchanged from last run. No urgency, no action.
- **Trades:** Active Trades: 0, nothing pending on us. DM threads with Revs1 (6d)/RexRocknut (6d) still unanswered, no change — per standing instruction, no nudge, left alone. Trade block unchanged: RexRocknut's Chase/Vele/Stevenson/Kamara + 1.03 (CLOSED, not re-approaching), FukeLender's 1.11, Lurchh's 1.07, DarrenA1's Isaiah Likely (TE) + Malik Golden (WR), CMCPanthers' Rashee Rice (WR) + T.J. Hockenson (TE), FORDJTFC's Allgeier/Dowdle/Neal (RB) + D. Jones (QB) — none fit our buy profile or are pre-identified targets, no unsolicited pitch sent.
- **Messages/chat:** No new DMs, no new @mentions. League chat unchanged in substance from last run (jiedunbar's OTC comment, Revs1's FA drops, FukeLender's Quinn Ewers pickup — all previously seen).
- **Roster:** Braelon Allen (11576) and Omar Cooper (13276) still not confirmed synced to the roster API (known lag, syncs once the 3-round draft completes). `reserve: null`, taxi still just Baker (1/3 slots), FAAB $0 used.
- **Injuries:** Chrome JS fetch (all rostered player IDs incl. pending picks). Questionable list unchanged: Hall (Thigh), Pittman (Leg), Estime (Leg), Worthy (Shoulder), Kraft (Knee/ACL), Q. Johnston (Lower Body), Tre' Harris (Undisclosed). No Out/Doubtful/IR. No IR moves needed.
- **NFL state:** `/matchups/2` empty — nothing to set (still preseason). No waivers before Aug 26 cuts (5 days out).
- **Next-run priority:** (1) FORDJTFC still on the clock for 3.3 — check progression toward our 3.9 (6 picks away). (2) Check if Cooper/Allen have synced to `/rosters` yet — backfill taxi (2 of 3 slots open) if so. (3) Re-check matchups once week 1 begins. (4) Continue routine DM/trade/injury sweep. (5) Watch draft board for 3.9 approaching — no fixed target list, evaluate live. (6) Only 5 days to Aug 26 cuts — waivers become live soon.

## Audit Trail (run logs)
Per-run session notes live under `runs/<YYYY>/<MM>/<DD>/`, one file per run:
- **New runs:** write a new file `runs/<YYYY>/<MM>/<DD>/<HHMM>-<slug>.md` (24h local time, short slug like `monitoring`, `trade-submission`, `draft-pick`). Do NOT append run logs to this file.
- **Historical runs** (before this structure existed) are named `run-NN-<slug>.md`; NN is the run ordinal.
- **Reading back:** to catch up, read this file plus only the most recent 1–2 run files (`ls` the latest date folder). Only dig into older runs if investigating something specific.
- After logging the run, update the **Current Status** snapshot above (overwrite in place) and fold any new durable rules/lessons into the sections above — that's what keeps this file small.
