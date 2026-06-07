# Client Mining Pass - 2026-05-16

Hidden contributor staging page for the broad client-mining pass requested after the wiki rough pass. Public pages should only use the stable rules below. Anything marked "server-side" or "needs data" should stay out of gameplay reference pages until confirmed.

## 1. Daily Events

Sources: `ENIALFMHHLL.cs`, `DFHOJHHBAMJ.cs`, `DDEIFGPEOMI.cs`, `KMOBGNPOEEM.cs`.

Daily tech/event scopes:

- `NULL`
- `Small`, `Medium`, `Large`, `Huge`
- `Human`, `Wyrd`, `Het`, `Precursor`
- `Random1`, `Random2`, `Random3`

The client has three daily-tech slots backed by server config fields:

| Slot | Scope field | Variant field |
|---|---|---|
| DailyTech1 | `DNDEPCEPJMP` | `OCEDINKOMLJ` |
| DailyTech2 | `CKCFAMJNHDD` | `LOEEOBIHGDO` |
| DailyTech3 | `KECGIAICDNG` | `KANFPPNFMNE` |

Important client behavior:

- Small scope applies to ship size Small or smaller.
- Medium, Large, and Huge scopes require exact size.
- Human scope applies to Human and Pirate faction units.
- Wyrd, Het, and Precursor scopes require exact faction.
- Random2 variant 4 requires `IsCaptainNaked()`.
- Random2 variant 0 checks `IsCaptainYoung()`, `IsCaptainOld()`, or `IsCaptainAdmiral()`.
- Love Day skips Random2 variant 5, Random1 variant 5, and Random1 variant 6.
- Oblivion server skips Random1 variant 1.
- Variants above 10, except 99, are treated as "boring" for non-random scopes Small through Precursor.

Client-visible event catalog:

| Variant | Scope | Client description |
|---:|---|---|
| 0 | Size/faction | Scoped ships move 20% faster |
| 0 | Random1 | Mission Rewards Doubled |
| 0 | Random2 | Young is Brash - Old is Wise - Admirals are Critical - Crafters are Masterful |
| 0 | Random3 | 50% Chance Crafted Items Gain +1 Rarity Upgrade |
| 1 | Size/faction | Scoped ships gain 20% more XP |
| 1 | Random1 | Item Durability Repairs Cost 33% Less |
| 1 | Random2 | Ancient Alien Secrets Hidden In Asteroids |
| 1 | Random3 | Crafted Items Gain +10 Quality Bonus |
| 2 | Size/faction | Scoped ships repairs can Critical and Splash |
| 2 | Random1 | Convert Credits to Tech Points Gets 10% Bonus |
| 2 | Random2 | Arena Awards Bonus Loot and Skulls |
| 2 | Random3 | Blueprint Discovery Unlocks Extra Item |
| 3 | Size/faction | Scoped ships can Cloak and Scan (Power 1) |
| 3 | Random1 | No Huge or Massive Ships Allowed in The Arena |
| 3 | Random2 | Double XP Bonus for Defense Unit Level Up |
| 3 | Random3 | Double Resources Gained From Tech Point Trades |
| 4 | Size/faction | Scoped ships have Advanced Grappling III |
| 4 | Random1 | Pirate and Alien Defense Units Drop Bonus Loot |
| 4 | Random2 | Naked Aggression |
| 4 | Random3 | Crafted Ships Gain Higher Random Stat Bonus |
| 5 | Size/faction | Scoped ships have Reverse Hack and Reverse Grapple |
| 5 | Random1 | Double Skulls for World PvP Kills |
| 5 | Random2 | Double Rewards for Alliance Defense Kills |
| 5 | Random3 | Double Skill Gain From Item and Ship Crafting |
| 6 | Random1 | Double Loot for Hardcore Ships in PvP and Homeworld Maps |
| 6 | Random2 | Created in the Image of the Space Lord or Space Lady |
| 6 | Random3 | They Stole Our Holy Relics! |
| 7 | Random1 | Invasion Bosses Drop Blueprints |
| 7 | Random2 | Hull Repairs Reduced by 80% in The Arena |
| 7 | Random3 | Assassin Leaders Can Drop Powerful Item Blueprints |
| 8 | Random1 | Invasion Bosses Drop Powerful Holiday Gem Loot |
| 8 | Random2 | Grapple and Drain Attacks Splash to Multiple Enemies |
| 8 | Random3 | Taunt and Hacking Attacks Splash to Multiple Enemies |
| 9 | Random1 | Pirate Leaders Hide in Rock Asteroids |
| 9 | Random2 | Alien Leaders Hide in Non-Rock Asteroids |
| 9 | Random3 | Rescue Drifting Crew for Rewards |
| 10 | Random1 | Item Damage Only 1% in All World PvP and SR8+ PvE Deaths |
| 10 | Random2 | Alien Leaders and Invasion Bosses Always Drop Void Loot |
| 10 | Random3 | Double Item Rewards for Invasion and Arena Victory |
| 99 | Random1 | Bonus Loot and PvP Skulls with Low Item Durability Damage |
| 99 | Random2 | Special Holiday Event |

## 2. Missions

Sources: `MissionDb.cs`, `MLGDJJKFBBH.cs`, `AHJEJEBENMA.cs`, `ChainMissionData.cs`, `UiManager.GetMissionList()`, `PlayerDbObj.cs`, `CorpDbObj.cs`, `DbPlayerStats.cs`, `DbCorpStats.cs`, `DbStats.cs`.

Mission record facts:

- `MissionDb.D` stores packed mission data.
- `MissionDb.GetMissionFromDataInt` decodes bytes as: mission type, metadata1, metadata2, metadata3.
- `M` is progress max.
- `P` is current progress.
- `E` is an optional expiry timestamp.
- Mission records can carry a tutorial flag and optional `ExtraData`.
- Serialization chooses byte, ushort, or int progress storage depending on max progress.

Mission UI buckets:

- Tutorial Missions
- System-chain missions
- Captain Missions
- Corp Mission
- Alliance Missions
- Universe Mission

Client mission objective enum:

- `KillPlayers`
- `KillNpcDefenses`
- `HuntNpcLeaders`
- `HarvestResources`
- `HuntNPCs`
- `HuntEliteNPCs`
- `Explore`
- `Deposit`
- `CraftItem`
- `UpgradeItem`
- `EquipItem`
- `ScrapItem`
- `Mine`
- `Rescue`
- `Distress`
- `OutpostDeposit`
- `HuntNamedNPC`

Shared-mission display:

- Corp, alliance, and universe mission rows show lifetime completed counts.
- Corp mission rows can show `Contribution #`.
- Alliance mission rows can show `Contribution #` and the contributing corporation name.
- Universe mission rows can show `Contribution #`.

Stats and leaderboards:

- `DbPlayerStats` stores `SolMis`, `CrpMis`, `AliMis`, `UnvMis`.
- `DbCorpStats` stores `SoloMissions`, `CorpMissions`, `AllianceMissions`.
- `DbStats.TpMis` maps to `MissionTechPoints`.

Needs data:

- Final server reward formula.
- Mission generation and refresh rules beyond training data.
- Whether any mission objective variants are server-only and absent from client text helpers.

## 3. Security Rating, Map Rules, and Quick Jump

Sources: `CEEFLMECOIP.cs`, `AHFAPFNMNPJ.cs`, `NCJPKNGDBKM.cs`, `IGDDJEMDJEJ.cs`, `IKOLEGFOADL.cs`.

Security Rating enum:

- `NULL`
- `R1` through `R9`
- `Boss`
- `FactionBoss`
- `Instance`

Client labels:

- SR1 displays as Safe Zone / Security Safe Zone in fallback naming.
- SR2-SR8 display as Security 2 through Security 8, or Security Rating 2 through Security Rating 8.
- SR9 displays as Security MAX / Security Rating MAX.
- Contested maps append `PvP` to the map summary label.

Client NPC level bands:

| Rating | Level band |
|---|---:|
| R1 | 2-8 |
| R2 | 7-13 |
| R3 | 13-23 |
| R4 | 23-35 |
| R5 | 35-50 |
| R6 | 50-80 |
| R7 | 80-110 |
| R8 | 110-130 |
| R9 | 130-150 |
| Boss | 140-160 |
| FactionBoss | 150-180 |
| Instance | 100-130 |

Quick Jump eligibility:

- Target must exist and be deployed.
- Target cannot be inside the Arena.
- Selected ship cannot already be in or adjacent to the destination sector.
- Player must have at least 1 Tech Point.
- Corporation-owned targets are valid for members of that corporation.
- Alliance-owned targets are valid for alliance members.
- Human defense targets are eligible only for Planets and Garrisons.
- Human Garrison targets used as Jump Gates must have a Jump Gate reference and must be discovered by the player.
- Non-human hostile defense units reject Quick Jump as "Hostile Enemy Defense Unit."

Needs data:

- Any server-side override that blocks jumps during combat or structure attack states beyond the client-side validation.
- Exact public wording for "human/home territory" edge cases in SR9 maps.

## 4. Free Gifts and Daily Gifts

Sources already staged in public pages and fallback wiki text.

Confirmed stable public facts:

- The `FREE` button at discovered defense units claims daily crafting resources.
- The hamburger-menu `GIFT BOX` randomly upgrades ships, elite ranks, equipped item rarity/quality, repairs, and similar upgrade bonuses.
- Daily resets are described as 00:00 UTC in the fallback wiki text.

Needs data:

- Exact gift table and weighting.
- Whether `freegift` command rewards are current in the 2.1.0 live server.

## 5. Achievements and Leaderboards

Sources: `AHJEJEBENMA.cs`, `DbStats.cs`, `DbPlayerStats.cs`, `DbCorpStats.cs`, existing `Client-Extracted-Loot-Rewards.md`.

Already staged:

- Loot rarity achievement thresholds in `Client-Extracted-Loot-Rewards.md`.
- Total-loot ladder in `Client-Extracted-Loot-Rewards.md`.
- Leaderboard mappings for loot, missions, PvP kills, structure kills, and mission Tech Points.

Additional mission-related leaderboard labels:

- Solo Missions
- Corp Missions
- Alliance Missions
- Universe Missions
- Mission Tech Points

Needs data:

- Full achievement threshold ladder for every stat category.
- Whether public pages should list achievement ladders or keep them as contributor reference.

## 6. Skills

Sources: `AHFAPFNMNPJ.cs`, `PlayerDbObj.cs`, `CombatEntityDbObj.cs`, `CorpDbObj.cs`, existing `Client-Extraction-Notes.md`.

Current client confirms these skill-upgradable stats:

- ResourceCapacity
- HullRepair
- OutgoingDamage
- ShieldDamage
- IncomingDamage
- XpBonus
- CriticalDamage
- CriticalChance
- EvasionChance
- BatteryDrainPower
- GrapplePower
- HackPower
- SplashChance
- HitChance
- HackResist
- GrappleResist
- CriticalResist
- SplashResist
- BatteryDrainResist

Storage facts:

- Players, combat entities, and corporations all store skill arrays of `DCGMGIEBAKC`.
- Player DB separately stores Scientist, Engineer, NextScientist, and NextEngineer fields.

Needs data:

- Exact skill point sources by unit type.
- Exact max-point rules in live server.
- Public wording for diminishing returns and per-point values.

## 7. Crafting and Upgrades

Sources: `FOACJEKBFLG.cs`, `AJCLEHJNBNJ.cs`, `ItemCraftDb.cs`, existing `Client-Extracted-Crafting.md`, `Client-Extracted-Items.md`, `Client-Extracted-Ships.md`.

Already staged:

- Item crafting level thresholds and cooldown table in `Client-Extracted-Crafting.md`.
- Crafting quality helper flow: total crafts -> crafting level -> quality type.
- Ship crafting resource formulas and faction multipliers in `Client-Extracted-Ships.md`.
- Item consumable classes, CPU upgrade decoding, and upgrade kit metadata in `Client-Extracted-Items.md` and `Client-Extracted-Item-Stat-Formulas-Narrow.md`.

Needs data:

- Server-side craft queue and command behavior.
- Which crafting pages should expose huge threshold tables versus link to contributor references.

## 8. Ship and Defense Construction

Sources already staged in `Client-Extracted-Ships.md`, `Client-Extracted-Structures.md`, and `Client-Extracted-Factions.md`.

Already staged:

- Fleet size requirements corrected from current runtime logic.
- Shipyard required levels and faction differences.
- Defense unit caps, default techs, EP/slot behavior, and build-cap Tech Point costs.
- Corp ship crafting skill and faction resource cost formulas.

Needs data:

- Any server-side checks omitted from client preview helpers.
- Full public ship/defense stat tables if we want exact build planning pages.

## 9. Combat Targeting and AI

Sources: `DDEIFGPEOMI.cs`, `CHCIGDNAAPI.cs`, `IGDDJEMDJEJ.cs`, `IKOLEGFOADL.cs`.

Stable client facts:

- Entities expose `GetEntityRelation`, `IsPlayerEnemy`, and `IsCorpEnemy` helpers.
- Attack target setting calls `SetWeaponLockTimes` against the target.
- Weapon lock time uses base targeting config plus target-size contribution, then applies `TargetingSpeedPercent`.
- Existing target is cleared in several state-change paths.
- Corp/player relation helpers drive friend/enemy classification in PvP and structure contexts.

Needs data:

- Server-authoritative target selection order.
- Full AI behavior for Corporate Defenders, NPCs, and structure targeting.
- Whether sort-order UI affects server target choice or only player coordination.

## 10. Special Items and Technologies

Sources already staged in `Client-Extracted-Technology.md`, `Client-Extracted-Items.md`, `Client-Extracted-Ships.md`, and `Items/Specials.md`.

Already staged:

- Technology enum/effect notes for major movement, targeting, ability, repair, and combat modifiers.
- Deception Module details.
- Interdictor sector state and active-source packet details.
- Consumable metadata and special-item/CPU upgrade decoding.
- Special item public overview with needs-data rows.

Needs data:

- Exact EP/stat per rank for every Special.
- Server-side special blueprint drops and event-only acquisition rules.
- Full public technology table policy: huge reference table versus focused gameplay pages.

