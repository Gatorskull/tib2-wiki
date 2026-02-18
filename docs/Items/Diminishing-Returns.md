# Stat Bonus Diminishing Returns

**Diminishing returns** in *The Infinite Black 2* means that the more you stack a single [**stat**](Stats.md), the **less** each extra point helps. This keeps balance (e.g. no infinite evasion) and lets newer players compete with less maxed gear. The concept applies to many stats: once you have more than a certain amount, additional gear that adds the same stat is slightly less effective. Your ship’s **displayed stats** already reflect the diminished value.

Example: **Outgoing Damage**. Once you have more than +5% Outgoing Damage, any extra Outgoing Damage from gear is slightly less effective. So if all your items give +6% Outgoing Damage, your ship might show about +5.8% instead of 6%.

---

## Resist Stat Table

For **resist-type** stats (e.g. resist damage), the **total** from gear is converted to an **actual** value used in combat as follows:

| TOTAL Resist Stat | ACTUAL Resist Stat |
|-------------------|---------------------|
| 05 | 05.00 |
| 10 | 10.00 |
| 15 | 15.00 |
| 20 | 20.00 |
| 25 | 25.00 |
| 30 | 28.85 |
| 35 | 32.41 |
| 40 | 35.71 |
| 45 | 38.79 |
| 50 | 41.67 |
| 55 | 44.35 |
| 60 | 46.88 |
| 65 | 49.24 |
| 70 | 51.47 |
| 75 | 53.57 |
| 80 | 55.56 |
| 85 | 57.43 |
| 90 | 59.21 |

So stacking 90 total resist gives an actual 59.21; the higher you go, the more each point is scaled down.

---

## Chance Stat Table

For **chance-type** stats (e.g. critical chance, splash chance), the **total** from gear is converted to an **actual** value as follows:

| TOTAL Chance Stat | ACTUAL Chance Stat |
|-------------------|---------------------|
| 05 | 05.00 |
| 10 | 10.00 |
| 15 | 15.00 |
| 20 | 18.85 |
| 25 | 22.41 |
| 30 | 25.71 |
| 35 | 28.79 |
| 40 | 31.67 |
| 45 | 34.35 |
| 50 | 36.88 |
| 55 | 39.24 |
| 60 | 41.47 |
| 65 | 43.57 |
| 70 | 45.56 |
| 75 | 47.43 |
| 80 | 49.21 |
| 85 | 50.90 |
| 90 | 52.50 |

So stacking 90 total chance gives an actual 52.50. As with resists, going past 20–25 shows clear diminishing returns.

---

## Why It Matters

- **Build diversity** — Maximizing one stat has a ceiling; mixing stats and item types is encouraged.
- **Catch-up** — Newer players can close the gap with less perfect gear because heavy stacking is less efficient.
- **Display** — The ship inspect panel shows the **actual** (diminished) values, not the raw sum from items.

---

## See Also

* [Stats](Stats.md) — Full list of stats and what they do
* [Items](index.md) — Item types and Gear Score
* [Mutate Item Kit](Mutate-Item-Kit.md) — Stat bonuses that also stack and are subject to DR
* [Void Items](Void-Items.md) — Extra stats that stack and are subject to DR
* [FAQ](../Getting-Started/FAQ.md) — “Why do my ship stats seem lower than they should be?”
