# Team Strategy — rainmannfl (Dog Tits)

**Last updated: 2026-08-18 15:35** (Revs1 accepted the Travis Hunter trade — processing 2026-08-20)

> This file always reflects the CURRENT strategy only. No history, no stale plans — old strategy lives in the run logs under `runs/`. Overwrite sections in place when the strategy changes and bump the date above.

## TLDR
- **Window: contend now** — the core (Allen, Hall, McBride, Bowers, G. Wilson) is elite and in-prime. Don't rebuild; get younger at WR/RB around the core.
- **Draft: Pick 1.9 DONE — took Omar Cooper (WR-NYJ)**, per the confirmed board. Rounds 2 & 3 (both pick 9) still to come — best available young WR/RB by landing spot when they arrive (linear order, several picks away).
- **Trades: Hunter deal ACCEPTED, processing 2026-08-20.** Revs1 accepted Cousins + Rattler + C. Kirk → Travis Hunter — no action needed, auto-processes Thursday. Once it clears: roster gains Hunter (WR-JAX, buy-low ex-top pick), loses Cousins/Rattler/C.Kirk; taxi loses Rattler (backfill from rookie picks); QB depth drops to 3 (Allen/Goff — fine, was surplus); remaining sell candidates: Jake Ferguson (TE4), Jauan Jennings (aging bench WR). Refresh roster cache and re-evaluate lineup/bench once Hunter is rostered.
- **Every trade goes through the KTC calculator** (Superflex, adjusted verdict) — never raw value sums. Accept within ~10% fair in our favor; flag core-starter deals for Matt instead of deciding.
- **FAAB: hold all $100 until after Aug 26 roster cuts**, then spend on clear upgrades over worst bench players.
- **Lineup for Week 1:** Garrett Wilson (91% start) must start — swap him in over Pittman if Pittman is still QUES, otherwise over Meyers.

## Team identity & window
Superflex PPR dynasty, 12-team. Strengths: elite QB room (Allen + Goff covers both QB-capable slots), elite TE room (McBride + Bowers both startable), RB1 (Hall), WR1-quality depth (Wilson). Weaknesses: aging WR corps behind Wilson (Meyers 29, Kirk, Jennings), aging RB2 (Montgomery 29), thin young depth. Verdict: this is a contender whose supporting cast ages out in 1–2 seasons — every move should either help now at no future cost, or swap aging/surplus pieces for players aged ≤25.

## Draft (2026 rookie draft, in progress)
- **Pick 1.9: DONE (2026-08-17).** Took Omar Cooper (WR-NYJ) — Lemon was gone (1.7, FORDJTFC), Cooper was still available at 1.9. Note: preseason camp news same day flagged him "losing ground for early-season work" behind Garrett Wilson/Isaiah Williams/Adonai Mitchell at NYJ — treat as a dynasty stash, not a Week 1 lock; monitor depth chart, no action needed now.
- **Skip at any pick:** QB (5 rostered incl. taxi) and TE (4 rostered).
- **Rounds 2 & 3 (both pick 9):** best available WR or RB, weight youth + NFL landing spot/depth-chart path over raw ADP. Re-check the live board and KTC before each pick — do not trust the picks API (lags; browser board is ground truth).
- **Pick trades:** we hold 1.9, 2.9, 3.9. Only trade up if it's cheap insurance for Lemon (e.g. 1.8 swap + small sweetener); don't buy extra late 1sts — no need.

## Trades
- **Method (mandatory):** simulate every deal in the KTC trade calculator, Superflex mode, and trust the adjusted verdict (value adjustment penalizes quantity-for-quality). See `.claude/skills/ktc-trades/SKILL.md`.
- **Decision rule:** accept if within ~10% of fair in our favor or better; counter once if lowball but engaged; reject politely if clearly bad. If a deal moves a core current starter and it's a close call — log it for Matt, don't execute.
- **Sell list (surplus, post-Hunter-trade):** Jake Ferguson (TE4), Jauan Jennings (aging bench WR). Kraft is sellable once healthy but only at fair TE2 value.
- **Buy profile:** WR/RB aged ≤25 whose KTC value has dipped below talent level (the Travis Hunter play was exactly this — WR50-ish pricing on a former top-2 pick — now closing 2026-08-20). Scan KTC risers/fallers when a trade is in motion.
- **Open threads:** None outstanding. Hunter deal with Revs1 ACCEPTED, processing 2026-08-20 — no further action. Chase/RexRocknut is CLOSED — do not re-approach.

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
