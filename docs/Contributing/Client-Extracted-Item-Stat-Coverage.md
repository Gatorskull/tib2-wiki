# Client-Extracted Item Stat Coverage

Hidden contributor staging page. This maps which runtime item family classes override each stat property in the current 2.1.0 Steam client decompile. It is a coverage map, not final public stat math.

Source pattern: runtime item classes override obfuscated stat properties consumed by `JCGFOGKIBPM.CalculateStat(...)`.

Important handling notes:

- A listed stat means the item family has custom client logic for that stat.
- This does not yet mean every item class within that family grants that stat; many overrides contain switch statements and return 0 for most classes.
- The next pass should normalize formulas per family and class, especially weapons, drones, computers, and specials.
- Some constants in decompiled formulas may be noisy/obfuscated; verify unusual values before publishing player-facing tables.

## Summary matrix

| Stat | Weapon | Armor | Storage | Drone | Engine | Computer | Special | Shield | Battery | Consumable |
|---|---|---|---|---|---|---|---|---|---|---|
| EquipPointCost | yes | yes | yes | yes | yes | yes | yes | yes | yes | yes |
| EquipPointMax | yes |  | yes |  | yes | yes | yes |  | yes |  |
| ResourceCapacity | yes |  | yes | yes |  | yes | yes |  |  |  |
| MoveSpeedPercent | yes | yes | yes | yes | yes | yes | yes |  | yes |  |
| HullRepair | yes | yes | yes | yes |  | yes | yes |  | yes |  |
| OutgoingDamage | yes |  | yes | yes |  | yes | yes |  |  |  |
| ShieldDamage | yes |  |  | yes |  |  | yes |  | yes |  |
| IncomingDamage |  |  | yes | yes |  | yes |  | yes |  |  |
| XpBonus | yes | yes | yes | yes |  | yes | yes |  | yes |  |
| MaxHull | yes | yes |  | yes |  |  | yes |  |  |  |
| CriticalDamage | yes |  |  | yes | yes |  | yes |  |  |  |
| CriticalChance | yes | yes | yes | yes |  | yes | yes |  | yes |  |
| EvasionChance | yes | yes | yes | yes | yes | yes | yes |  | yes |  |
| BatteryDrainPower | yes |  |  | yes |  |  | yes |  | yes |  |
| GrapplePower | yes |  |  | yes |  |  | yes |  | yes |  |
| HackPower | yes |  |  | yes |  |  | yes |  |  |  |
| SplashChance | yes | yes |  | yes |  | yes | yes |  |  |  |
| HitChance | yes | yes | yes | yes |  | yes | yes |  | yes |  |
| HackResist | yes | yes |  | yes |  | yes | yes | yes | yes |  |
| GrappleResist | yes | yes |  | yes | yes | yes | yes | yes | yes |  |
| CriticalResist | yes | yes | yes | yes | yes | yes | yes | yes | yes |  |
| SplashResist | yes | yes |  | yes |  | yes | yes | yes | yes |  |
| BatteryDrainResist |  | yes |  | yes |  |  | yes | yes | yes |  |
| PowerRecharge |  |  |  |  |  |  | yes |  | yes |  |
| PowerCapacity |  |  |  |  | yes |  | yes |  | yes |  |
| ShieldCapacity | yes |  |  | yes |  |  | yes | yes | yes |  |
| ShieldPenetration | yes | yes |  | yes |  | yes |  |  | yes |  |
| TargetingSpeedPercent | yes | yes | yes | yes |  |  | yes |  | yes |  |
| HullDamage | yes | yes |  |  |  | yes | yes |  |  |  |

## Weapon

Source: `Assembly-CSharp\EBNNOMPAHAF.cs`

| Stat | Obfuscated property | Source line |
|---|---|---:|
| BatteryDrainPower | `AKHIEAMMMAD` | 934 |
| CriticalChance | `MOLDAGLDGFJ` | 2068 |
| CriticalDamage | `EPIANIDJPJF` | 598 |
| CriticalResist | `CDLEBDHOLGB` | 2213 |
| EquipPointCost | `OMIBOKEONLA` | 367 |
| EquipPointMax | `AKAAAIOKMOP` | 2880 |
| EvasionChance | `CICMMLJMJKP` | 382 |
| GrapplePower | `AAALLHAEEIB` | 2006 |
| GrappleResist | `AFNCJMNENCA` | 1576 |
| HackPower | `MMDGCIJKKPF` | 1673 |
| HackResist | `IJICKEGDCCE` | 995 |
| HitChance | `AMFJDLDNMHO` | 1863 |
| HullDamage | `LELKJKHKIMC` | 1843 |
| HullRepair | `LDCKLGHOKDN` | 232 |
| MaxHull | `PAGFCABKGBN` | 2803 |
| MoveSpeedPercent | `JCKNDPELNLG` | 2337 |
| OutgoingDamage | `AIMFBLFHGNO` | 2532 |
| ResourceCapacity | `ACABLPPGOFC` | 2244 |
| ShieldCapacity | `KHAGACJJONM` | 1760 |
| ShieldDamage | `AEDGBNCKKPF` | 2175 |
| ShieldPenetration | `BIDNACKAGFL` | 2469 |
| SplashChance | `DPMALIMOOBI` | 1448 |
| SplashResist | `BFILEEDOAPJ` | 27 |
| TargetingSpeedPercent | `KHLBGHAAHOE` | 1524 |
| XpBonus | `LMJGMPDOOHH` | 743 |

## Armor

Source: `Assembly-CSharp\KKKEBKMMOBA.cs`

| Stat | Obfuscated property | Source line |
|---|---|---:|
| BatteryDrainResist | `LDOFEGMICPK` | 197 |
| CriticalChance | `MOLDAGLDGFJ` | 652 |
| CriticalResist | `CDLEBDHOLGB` | 157 |
| EquipPointCost | `OMIBOKEONLA` | 559 |
| EvasionChance | `CICMMLJMJKP` | 524 |
| GrappleResist | `AFNCJMNENCA` | 171 |
| HackResist | `IJICKEGDCCE` | 674 |
| HitChance | `AMFJDLDNMHO` | 120 |
| HullDamage | `LELKJKHKIMC` | 29 |
| HullRepair | `LDCKLGHOKDN` | 237 |
| MaxHull | `PAGFCABKGBN` | 317 |
| MoveSpeedPercent | `JCKNDPELNLG` | 211 |
| ShieldPenetration | `BIDNACKAGFL` | 861 |
| SplashChance | `DPMALIMOOBI` | 337 |
| SplashResist | `BFILEEDOAPJ` | 733 |
| TargetingSpeedPercent | `KHLBGHAAHOE` | 287 |
| XpBonus | `LMJGMPDOOHH` | 64 |

## Storage

Source: `Assembly-CSharp\KJEIOMFAJOC.cs`

| Stat | Obfuscated property | Source line |
|---|---|---:|
| CriticalChance | `MOLDAGLDGFJ` | 160 |
| CriticalResist | `CDLEBDHOLGB` | 68 |
| EquipPointCost | `OMIBOKEONLA` | 1609 |
| EquipPointMax | `AKAAAIOKMOP` | 1983 |
| EvasionChance | `CICMMLJMJKP` | 991 |
| HitChance | `AMFJDLDNMHO` | 1729 |
| HullRepair | `LDCKLGHOKDN` | 942 |
| IncomingDamage | `PLHGOLKMLJJ` | 1127 |
| MoveSpeedPercent | `JCKNDPELNLG` | 1223 |
| OutgoingDamage | `AIMFBLFHGNO` | 209 |
| ResourceCapacity | `ACABLPPGOFC` | 698 |
| TargetingSpeedPercent | `KHLBGHAAHOE` | 2341 |
| XpBonus | `LMJGMPDOOHH` | 1426 |

## Drone

Source: `Assembly-CSharp\BBNPEFEJEEC.cs`

| Stat | Obfuscated property | Source line |
|---|---|---:|
| BatteryDrainPower | `AKHIEAMMMAD` | 714 |
| BatteryDrainResist | `LDOFEGMICPK` | 912 |
| CriticalChance | `MOLDAGLDGFJ` | 477 |
| CriticalDamage | `EPIANIDJPJF` | 866 |
| CriticalResist | `CDLEBDHOLGB` | 1381 |
| EquipPointCost | `OMIBOKEONLA` | 36 |
| EvasionChance | `CICMMLJMJKP` | 1527 |
| GrapplePower | `AAALLHAEEIB` | 818 |
| GrappleResist | `AFNCJMNENCA` | 1178 |
| HackPower | `MMDGCIJKKPF` | 444 |
| HackResist | `IJICKEGDCCE` | 1900 |
| HitChance | `AMFJDLDNMHO` | 1494 |
| HullRepair | `LDCKLGHOKDN` | 1595 |
| IncomingDamage | `PLHGOLKMLJJ` | 959 |
| MaxHull | `PAGFCABKGBN` | 1100 |
| MoveSpeedPercent | `JCKNDPELNLG` | 1992 |
| OutgoingDamage | `AIMFBLFHGNO` | 1336 |
| ResourceCapacity | `ACABLPPGOFC` | 1959 |
| ShieldCapacity | `KHAGACJJONM` | 1234 |
| ShieldDamage | `AEDGBNCKKPF` | 1424 |
| ShieldPenetration | `BIDNACKAGFL` | 1315 |
| SplashChance | `DPMALIMOOBI` | 1449 |
| SplashResist | `BFILEEDOAPJ` | 757 |
| TargetingSpeedPercent | `KHLBGHAAHOE` | 1664 |
| XpBonus | `LMJGMPDOOHH` | 211 |

## Engine

Source: `Assembly-CSharp\OIBAMMKGNBK.cs`

| Stat | Obfuscated property | Source line |
|---|---|---:|
| CriticalDamage | `EPIANIDJPJF` | 1003 |
| CriticalResist | `CDLEBDHOLGB` | 778 |
| EquipPointCost | `OMIBOKEONLA` | 647 |
| EquipPointMax | `AKAAAIOKMOP` | 355 |
| EvasionChance | `CICMMLJMJKP` | 295 |
| GrappleResist | `AFNCJMNENCA` | 792 |
| MoveSpeedPercent | `JCKNDPELNLG` | 108 |
| PowerCapacity | `JEFDOBNBCJO` | 864 |

## Computer

Source: `Assembly-CSharp\KOBILLCNLAJ.cs`

| Stat | Obfuscated property | Source line |
|---|---|---:|
| CriticalChance | `MOLDAGLDGFJ` | 9 |
| CriticalResist | `CDLEBDHOLGB` | 458 |
| EquipPointCost | `OMIBOKEONLA` | 182 |
| EquipPointMax | `AKAAAIOKMOP` | 3422 |
| EvasionChance | `CICMMLJMJKP` | 1027 |
| GrappleResist | `AFNCJMNENCA` | 649 |
| HackResist | `IJICKEGDCCE` | 2305 |
| HitChance | `AMFJDLDNMHO` | 779 |
| HullDamage | `LELKJKHKIMC` | 307 |
| HullRepair | `LDCKLGHOKDN` | 688 |
| IncomingDamage | `PLHGOLKMLJJ` | 850 |
| MoveSpeedPercent | `JCKNDPELNLG` | 3143 |
| OutgoingDamage | `AIMFBLFHGNO` | 1868 |
| ResourceCapacity | `ACABLPPGOFC` | 1471 |
| ShieldPenetration | `BIDNACKAGFL` | 3334 |
| SplashChance | `DPMALIMOOBI` | 1825 |
| SplashResist | `BFILEEDOAPJ` | 3018 |
| XpBonus | `LMJGMPDOOHH` | 1380 |

## Special

Source: `Assembly-CSharp\KKHJOEBCGAP.cs`

| Stat | Obfuscated property | Source line |
|---|---|---:|
| BatteryDrainPower | `AKHIEAMMMAD` | 736 |
| BatteryDrainResist | `LDOFEGMICPK` | 795 |
| CriticalChance | `MOLDAGLDGFJ` | 672 |
| CriticalDamage | `EPIANIDJPJF` | 220 |
| CriticalResist | `CDLEBDHOLGB` | 1626 |
| EquipPointCost | `OMIBOKEONLA` | 1261 |
| EquipPointMax | `AKAAAIOKMOP` | 517 |
| EvasionChance | `CICMMLJMJKP` | 1737 |
| GrapplePower | `AAALLHAEEIB` | 943 |
| GrappleResist | `AFNCJMNENCA` | 1277 |
| HackPower | `MMDGCIJKKPF` | 1412 |
| HackResist | `IJICKEGDCCE` | 267 |
| HitChance | `AMFJDLDNMHO` | 1128 |
| HullDamage | `LELKJKHKIMC` | 239 |
| HullRepair | `LDCKLGHOKDN` | 1780 |
| MaxHull | `PAGFCABKGBN` | 1471 |
| MoveSpeedPercent | `JCKNDPELNLG` | 1607 |
| OutgoingDamage | `AIMFBLFHGNO` | 898 |
| PowerCapacity | `JEFDOBNBCJO` | 343 |
| PowerRecharge | `ENGLBKJJOGE` | 1526 |
| ResourceCapacity | `ACABLPPGOFC` | 1679 |
| ShieldCapacity | `KHAGACJJONM` | 498 |
| ShieldDamage | `AEDGBNCKKPF` | 1426 |
| SplashChance | `DPMALIMOOBI` | 1108 |
| SplashResist | `BFILEEDOAPJ` | 378 |
| TargetingSpeedPercent | `KHLBGHAAHOE` | 1094 |
| XpBonus | `LMJGMPDOOHH` | 1247 |

## Shield

Source: `Assembly-CSharp\BNCBECFCPHP.cs`

| Stat | Obfuscated property | Source line |
|---|---|---:|
| BatteryDrainResist | `LDOFEGMICPK` | 171 |
| CriticalResist | `CDLEBDHOLGB` | 303 |
| EquipPointCost | `OMIBOKEONLA` | 618 |
| GrappleResist | `AFNCJMNENCA` | 9 |
| HackResist | `IJICKEGDCCE` | 244 |
| IncomingDamage | `PLHGOLKMLJJ` | 754 |
| ShieldCapacity | `KHAGACJJONM` | 718 |
| SplashResist | `BFILEEDOAPJ` | 804 |

## Battery

Source: `Assembly-CSharp\ECCOKHAPHDD.cs`

| Stat | Obfuscated property | Source line |
|---|---|---:|
| BatteryDrainPower | `AKHIEAMMMAD` | 51 |
| BatteryDrainResist | `LDOFEGMICPK` | 513 |
| CriticalChance | `MOLDAGLDGFJ` | 686 |
| CriticalResist | `CDLEBDHOLGB` | 717 |
| EquipPointCost | `OMIBOKEONLA` | 460 |
| EquipPointMax | `AKAAAIOKMOP` | 436 |
| EvasionChance | `CICMMLJMJKP` | 763 |
| GrapplePower | `AAALLHAEEIB` | 422 |
| GrappleResist | `AFNCJMNENCA` | 865 |
| HackResist | `IJICKEGDCCE` | 295 |
| HitChance | `AMFJDLDNMHO` | 580 |
| HullRepair | `LDCKLGHOKDN` | 196 |
| MoveSpeedPercent | `JCKNDPELNLG` | 814 |
| PowerCapacity | `JEFDOBNBCJO` | 400 |
| PowerRecharge | `ENGLBKJJOGE` | 118 |
| ShieldCapacity | `KHAGACJJONM` | 550 |
| ShieldDamage | `AEDGBNCKKPF` | 364 |
| ShieldPenetration | `BIDNACKAGFL` | 91 |
| SplashResist | `BFILEEDOAPJ` | 470 |
| TargetingSpeedPercent | `KHLBGHAAHOE` | 604 |
| XpBonus | `LMJGMPDOOHH` | 154 |

## Consumable

Source: `Assembly-CSharp\NLLPDCFPKJM.cs`

| Stat | Obfuscated property | Source line |
|---|---|---:|
| EquipPointCost | `OMIBOKEONLA` | 744 |
