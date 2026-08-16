# Team Strategy — rainmannfl (Dog Tits)

**Last updated: 2026-08-16 21:01** (Lemon taken at 1.7 — board updated)

> This file always reflects the CURRENT strategy only. No history, no stale plans — old strategy lives in the run logs under `runs/`. Overwrite sections in place when the strategy changes and bump the date above.

## TLDR
- **Window: contend now** — the core (Allen, Hall, McBride, Bowers, G. Wilson) is elite and in-prime. Don't rebuild; get younger at WR/RB around the core.
- **Draft 1.9: Makai Lemon is GONE (taken 1.7 by FORDJTFC). Take Omar Cooper (WR-NYJ)** if he survives pick 1.8. Fallback: De'Zhaun Stribling (WR). Never QB or TE — massively overstocked at both. Rounds 2–3: best available young WR/RB by landing spot.
- **Trades: sell surplus, buy youth.** Surplus = QB depth (Cousins, Rattler) and TE depth (Ferguson, or Kraft once healthy). Target = WR/RB aged ≤25 at value dips. Live offer out: Cousins + Rattler + C. Kirk → Travis Hunter (buy-low, no nudging).
- **Every trade goes through the KTC calculator** (Superflex, adjusted verdict) — never raw value sums. Accept within ~10% fair in our favor; flag core-starter deals for Matt instead of deciding.
- **FAAB: hold all $100 until after Aug 26 roster cuts**, then spend on clear upgrades over worst bench players.
- **Lineup for Week 1:** Garrett Wilson (91% start) must start — swap him in over Pittman if Pittman is still QUES, otherwise over Meyers.

## Team identity & window
Superflex PPR dynasty, 12-team. Strengths: elite QB room (Allen + Goff covers both QB-capable slots), elite TE room (McBride + Bowers both startable), RB1 (Hall), WR1-quality depth (Wilson). Weaknesses: aging WR corps behind Wilson (Meyers 29, Kirk, Jennings), aging RB2 (Montgomery 29), thin young depth. Verdict: this is a contender whose supporting cast ages out in 1–2 seasons — every move should either help now at no future cost, or swap aging/surplus pieces for players aged ≤25.

## Draft (2026 rookie draft, in progress)
- **Pick 1.9 board (Matt-confirmed, execute without asking):** 1) ~~Makai Lemon~~ — TAKEN 1.7 by FORDJTFC (2026-08-16), no longer available; 2) **Omar Cooper (WR-NYJ) — current top target**, healthy, edges Stribling on age; 3) De'Zhaun Stribling (WR) — fallback if Cooper goes at 1.8.
- **Skip at any pick:** QB (5 rostered incl. taxi) and TE (4 rostered).
- **Rounds 2 & 3 (both pick 9):** best available WR or RB, weight youth + NFL landing spot/depth-chart path over raw ADP. Re-check the live board and KTC before each pick — do not trust the picks API (lags; browser board is ground truth).
- **Pick trades:** we hold 1.9, 2.9, 3.9. Only trade up if it's cheap insurance for Lemon (e.g. 1.8 swap + small sweetener); don't buy extra late 1sts — no need.

## Trades
- **Method (mandatory):** simulate every deal in the KTC trade calculator, Superflex mode, and trust the adjusted verdict (value adjustment penalizes quantity-for-quality). See `.claude/skills/ktc-trades/SKILL.md`.
- **Decision rule:** accept if within ~10% of fair in our favor or better; counter once if lowball but engaged; reject politely if clearly bad. If a deal moves a core current starter and it's a close call — log it for Matt, don't execute.
- **Sell list (surplus):** Kirk Cousins (QB3), Spencer Rattler (taxi QB), Jake Ferguson (TE4), Christian Kirk / Jauan Jennings (aging bench WRs). Kraft is sellable once healthy but only at fair TE2 value.
- **Buy profile:** WR/RB aged ≤25 whose KTC value has dipped below talent level (the Travis Hunter play — WR50 pricing on a former top pick). Scan KTC risers/fallers when a trade is in motion.
- **Open threads:** Hunter offer to Revs1 (Cousins + Rattler + C. Kirk) — outstanding, NO nudges ever (standing instruction); abandon if silent by ~2026-09-15. Chase/RexRocknut is CLOSED — do not re-approach.

## Roster management
- **Drop-candidate order** when a spot is needed: Javon Baker (taxi, no NFL team) > Audric Estime (depth 6 at NO, now QUES) > Jennings > C. Kirk.
- **IR discipline:** only IR-eligible players in reserve slots; move players out promptly when healthy (Sleeper locks the roster otherwise).
- **Taxi:** Rattler + Baker. If Rattler moves in a trade, backfill taxi from rookie draft picks.

## Waivers / FAAB
- $100 budget, fully unused — that's an asset. **No claims before the Aug 26 NFL roster cuts** (camp-body churn). After cuts: claim only when a free agent clearly beats our worst bench player at a position of need (WR/RB youth). Expect to spend meaningfully early — an unused budget in December is a wasted asset for a contender.

## Lineup principles (from Week 1)
- Start by projected value, not name: Wilson (91%) over Meyers (41%) / Pittman (38%, QUES watch). Bowers stays in the WRT flex (99%).
- Check injury designations before every lock; QUES starters need a healthy pivot benched-and-ready.
- Preseason: nothing to set; matchups endpoint empty until Week 1.
