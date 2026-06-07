# Level and XP Reference

Level is calculated from total XP. Level is capped at `500`; XP at or above `235,261,135` returns level `500.0`.

XP below `540` returns integer level `1`.

## Fractional Level Formula

Between level thresholds, level progress uses:

```text
level = current integer level + (current XP - XP required for current level) / (XP required for next level - XP required for current level)
```

## XP Required By Level

This table lists early and major milestones.

| Level | Total XP required |
|---:|---:|
| 1 | 100 |
| 2 | 540 |
| 3 | 1,215 |
| 4 | 2,135 |
| 5 | 3,310 |
| 6 | 4,750 |
| 7 | 6,465 |
| 8 | 8,465 |
| 9 | 10,760 |
| 10 | 13,360 |
| 15 | 31,285 |
| 20 | 58,335 |
| 25 | 95,760 |
| 30 | 144,810 |
| 35 | 206,735 |
| 40 | 282,785 |
| 45 | 374,210 |
| 50 | 482,260 |
| 55 | 608,185 |
| 60 | 753,235 |
| 65 | 918,660 |
| 70 | 1,105,710 |
| 75 | 1,315,635 |
| 80 | 1,549,685 |
| 85 | 1,809,110 |
| 90 | 2,095,160 |
| 95 | 2,409,085 |
| 100 | 2,752,135 |
| 500 | 235,261,135 |

## See Also

* [Skills](Skills.md)
* [Technology Reference](Technology-Reference.md)
* [Ships](../Ships/index.md)
