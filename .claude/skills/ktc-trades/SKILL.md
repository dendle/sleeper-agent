# ktc-trades — Evaluating trades with KeepTradeCut

Use this skill EVERY time a trade is being evaluated, constructed, or pitched. Never judge a trade by summing raw KTC player values.

## Why raw sums are wrong

KTC's trade calculator applies a **Value Adjustment** on top of raw player values. It compensates the side giving up the single best asset: consolidating multiple pieces into one stud costs a premium, because roster spots have value and studs are scarce (ten 1,000-value players do NOT equal one 9,999 player).

Practical consequences:
- In any 2-for-1 or 3-for-1, the side sending the package must OVERPAY on raw value for the calculator to call it fair.
- A package that sums "even" or "+2%" against a stud is actually a LOSING offer and will read as such to the other manager (this is exactly what happened with the Wilson + Javonte Williams → Ja'Marr Chase offer: raw sum ~10,210 vs ~9,972 looked even, but the calculator's value adjustment made it a clear loss for the Chase side).
- The bigger the gap between the best player in the deal and the supporting pieces, the larger the adjustment.

## Required procedure

1. Open the calculator in the browser: `https://keeptradecut.com/trade-calculator`
2. **Set league format to Superflex** (this league is SF PPR — the SF/1QB toggle drastically changes QB values). TE Premium off.
3. Enter the exact players (and picks) on each side using the search boxes. Picks are supported (e.g. "2026 Early 1st").
4. Screenshot the result. Read:
   - The verdict bar (which side wins and by how much)
   - The **Value Adjustment** line item and which side it's applied to
5. A trade is only "fair" if the calculator's adjusted verdict says so — not the raw sums.
6. When constructing an offer to acquire a stud, iterate in the calculator: add value to our side until the bar shows even or a slight win for the OTHER side, then sanity-check whether we're comfortable with the real overpay.
7. Record in agents.md: the adjusted verdict (e.g. "KTC calc: even after +1,200 value adjustment to their side"), not just raw values.

## Notes

- Cite KTC values as "raw" only for quick scans of who's roughly in whose tier. Any go/no-go decision goes through the calculator.
- If the calculator page can't be automated, do NOT fall back to raw sums silently — flag it and approximate the adjustment manually (a 2-for-1 for a top-3 asset typically needs roughly 10–25% raw-value overpay; steeper as the stud's value grows).
- KTC values shift daily; re-run the calculator at decision time rather than reusing numbers from a previous session.
