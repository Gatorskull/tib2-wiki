# Client-Extracted Technology

Hidden contributor staging page. This is raw client-extracted technology display data from the current 2.1.0 Steam client decompile. Use it to build public pages, but do not copy blindly without checking whether the wording belongs in player-facing reference, guide, or strategy content.

Source files:

- `Assembly-CSharp\BCHEAEJKAJI.cs` technology enum
- `Assembly-CSharp\DFHOJHHBAMJ.cs` `GetName(this BCHEAEJKAJI)`, `GetDescription(this BCHEAEJKAJI, ...)`, and daily-tech helpers
- `Assembly-CSharp\JEKJDKMBIGN.cs` `GetRegenerationTechHull(...)`
- `Assembly-CSharp\PGJIDFCBFCC.cs` regeneration default backing values

Notes:

- `NULL` and unused/future enum values are included when the client exposes a label or description.
- Daily tech descriptions are dynamic and depend on the assigned daily tech type; see the matrix below the main table.
- The daily-tech matrix is client wording and should be cleaned before becoming public-facing copy.

## Runtime-Confirmed Numerical Effects

Source: `Assembly-CSharp\GKFECKLMHGM.cs`.

The main table below is built from client display names/descriptions. This section records values also seen in runtime stat aggregation helpers, which makes them stronger candidates for public rules pages.

Movement and targeting:

| Tech/effect | Runtime effect |
|---|---:|
| HyperDrive1 | `-10%` move time modifier |
| HyperDrive2 | `-15%` move time modifier |
| HyperDrive3 | `-20%` move time modifier |
| SpaceLaneEffect1 | `-10%` move time modifier |
| SpaceLaneEffect2 | `-15%` move time modifier |
| SpaceLaneEffect3 | `-20%` move time modifier |
| FriendlyTerritoryEffect | `-10%` move time modifier |
| NanobotCharge | `-10%` move time modifier |
| Targeting1 | `-5%` targeting-time modifier |
| Targeting2 | `-10%` targeting-time modifier |
| Targeting3 | `-15%` targeting-time modifier |
| InterdictorEffect1 | `+15%` move and targeting-time penalty |
| InterdictorEffect2 | `+20%` move and targeting-time penalty |
| InterdictorEffect3 | `+25%` move and targeting-time penalty |
| InterdictorEffect4 | `+30%` move and targeting-time penalty |

XP, evasion, and hit chance:

| Tech | Runtime effect |
|---|---:|
| Analysis1 | `+10%` XP |
| Analysis2 | `+15%` XP |
| Analysis3 | `+20%` XP |
| Intuition1 | `+5%` XP and `+5` evasion |
| Intuition2 | `+10%` XP and `+10` evasion |
| Intuition3 | `+15%` XP and `+15` evasion |
| EvasiveManeuvers1 | `+6` evasion |
| EvasiveManeuvers2 | `+10` evasion |
| EvasiveManeuvers3 | `+14` evasion |
| Intimidation1 | `+6` hit chance |
| Intimidation2 | `+10` hit chance |
| Intimidation3 | `+14` hit chance |

Hull and shield max:

| Tech family | Runtime effect |
|---|---|
| HullMax1-8 | highest rank only: `+5%`, `+8%`, `+11%`, `+14%`, `+17%`, `+20%`, `+23%`, `+30%` hull |
| AdvancedAlloys1-2 | additional `+2%`, `+4%` hull |
| ShieldMax1-7 | highest rank only: `+5%`, `+8%`, `+11%`, `+14%`, `+17%`, `+20%`, `+23%` shield |
| ShieldAmplifier1-3 | additional `+3%`, `+6%`, `+9%` shield |

Outgoing and incoming damage modifiers:

| Tech/effect | Runtime effect |
|---|---:|
| Overpower | `+10%` outgoing damage and `+15%` incoming damage |
| Vanquisher | `+15%` outgoing damage |
| SmallStrikeTeamEffect | `+5%` outgoing damage |
| NanobotCharge | `+10%` outgoing damage |
| LeadershipEffect1 | `+3%` outgoing damage |
| LeadershipEffect2 | `+5%` outgoing damage |
| LeadershipEffect3 | `+7%` outgoing damage |
| Freighter1 | `-50%` outgoing damage |
| Freighter2 | `-45%` outgoing damage |
| Freighter3 | `-40%` outgoing damage |
| Freighter4 | `-35%` outgoing damage |
| Freighter5 | `-30%` outgoing damage |
| EnemyTerritoryEffect | `+10%` incoming damage |

Repair facility hull-repair bonuses:

| Tech | Runtime hull-repair bonus |
|---|---:|
| RepairFacility1 | `+10%` |
| RepairFacility2 | `+15%` |
| RepairFacility3 | `+20%` |
| RepairFacility4 | `+25%` |

## Main technology table

| Enum | Client display name | Client description |
|---|---|---|
| NULL |  |  |
| UNUSED1 | Future Technology | An Unused Future Technology Type |
| RepairFacility1 | Repair Facility Rank 1 | -10% Repair Cooldown & +10% Hull Repair Bonus |
| RepairFacility2 | Repair Facility Rank 2 | -20% Repair Cooldown & +15% Hull Repair Bonus |
| RepairFacility3 | Repair Facility Rank 3 | -30% Repair Cooldown & +20% Hull Repair Bonus |
| RepairFacility4 | Repair Facility Rank 4 | -40% Repair Cooldown & +25% Hull Repair Bonus |
| EvasiveManeuvers1 | Evasive Maneuvers | +6 Evasion Bonus |
| EvasiveManeuvers2 | Evasive Maneuvers II | +10 Evasion Bonus |
| EvasiveManeuvers3 | Evasive Maneuvers III | +14 Evasion Bonus |
| Intimidation1 | Intimidation | +6 Hit Chance Bonus |
| Intimidation2 | Intimidation II | +10 Hit Chance Bonus |
| Intimidation3 | Intimidation III | +14 Hit Chance Bonus |
| Intuition1 | Intuition | +5% XP Bonus and +5 Evasion |
| Intuition2 | Intuition II | +10% XP Bonus and +10 Evasion |
| Intuition3 | Intuition III | +15% XP Bonus and +15 Evasion |
| SkipJump | Skip Jump | Very Fast Movement Speed |
| CrewFurnace | Crew Furnace | Fast Movement Speed |
| Analysis1 | Analysis | +10% XP Bonus |
| Analysis2 | Analysis II | +15% XP Bonus |
| Analysis3 | Analysis III | +20% XP Bonus |
| HyperDrive1 | HyperDrive | 10% Ship Movement Speed Bonus |
| HyperDrive2 | HyperDrive II | 15% Ship Movement Speed Bonus |
| HyperDrive3 | HyperDrive III | 20% Ship Movement Speed Bonus |
| SpaceLaneEffect1 | Space Lane Effect | 10% Ship Movement Speed Bonus (Blue Sector Lines) |
| SpaceLaneEffect2 | Space Lane Effect II | 15% Ship Movement Speed Bonus (Blue Sector Lines) |
| SpaceLaneEffect3 | Space Lane Effect III | 20% Ship Movement Speed Bonus (Blue Sector Lines) |
| Vorpal1 | Vorpal Rank 1 | Attacks Versus Enemies Below 5% Health Always Critical |
| Vorpal2 | Vorpal Rank 2 | Attacks Versus Enemies Below 10% Health Always Critical |
| Vorpal3 | Vorpal Rank 3 | Attacks Versus Enemies Below 15% Health Always Critical |
| Vorpal4 | Vorpal Rank 4 | Attacks Versus Enemies Below 20% Health Always Critical |
| Targeting1 | Targeting | 5% Weapon & Drone Targeting Speed Bonus |
| Targeting2 | Targeting II | 10% Weapon & Drone Targeting Speed Bonus |
| Targeting3 | Targeting III | 15% Weapon & Drone Targeting Speed Bonus |
| Junker1 | Junker | +5% Chance to Repair When Damaging Enemy Hull |
| Junker2 | Junker II | +10% Chance to Repair When Damaging Enemy Hull |
| Junker3 | Junker III | +15% Chance to Repair When Damaging Enemy Hull |
| Mechanic1 | Mechanic | Repair 5% Hull When Enemy NPC Killed |
| Mechanic2 | Mechanic II | Repair 10% Hull When Enemy NPC Killed |
| Mechanic3 | Mechanic III | Repair 15% Hull When Enemy NPC Killed |
| ShieldCapacitors1 | Shield Capacitors | +5% Chance to Resist Shield Damage and Convert to Battery |
| ShieldCapacitors2 | Shield Capacitors II | +10% Chance to Resist Shield Damage and Convert to Battery |
| ShieldCapacitors3 | Shield Capacitors III | +15% Chance to Resist Shield Damage and Convert to Battery |
| ShieldAmplifier1 | Shield Amplifier | +3% Shield Max |
| ShieldAmplifier2 | Shield Amplifier II | +6% Shield Max |
| ShieldAmplifier3 | Shield Amplifier III | +9% Shield Max |
| ShieldPierce1 | Shield Bypass | +5% Chance for Attacks to Ignore Shields |
| ShieldPierce2 | Shield Bypass II | +10% Chance for Attacks to Ignore Shields |
| ShieldPierce3 | Shield Bypass III | +15% Chance for Attacks to Ignore Shields |
| Freighter1 | Freighter Rank 1 | -50% Damage but +100% Resource & Harvesting Capacity |
| Freighter2 | Freighter Rank 2 | -45% Damage but +125% Resource & Harvesting Capacity |
| Freighter3 | Freighter Rank 3 | -40% Damage but +150% Resource & Harvesting Capacity |
| Freighter4 | Freighter Rank 4 | -35% Damage but +175% Resource & Harvesting Capacity |
| Freighter5 | Freighter Rank 5 | -30% Damage but +200% Resource & Harvesting Capacity |
| Scavenger1 | Scavenger Rank 1 | 2% Fleet Resource & Loot Bonus Chance |
| Scavenger2 | Scavenger Rank 2 | 4% Fleet Resource & Loot Bonus Chance |
| Scavenger3 | Scavenger Rank 3 | 6% Fleet Resource & Loot Bonus Chance |
| Scavenger4 | Scavenger Rank 4 | 8% Fleet Resource & Loot Bonus Chance |
| Scavenger5 | Scavenger Rank 5 | 10% Fleet Resource & Loot Bonus Chance |
| Scavenger6 | Scavenger Rank 6 | 12% Fleet Resource & Loot Bonus Chance |
| Scavenger7 | Scavenger Rank 7 | 14% Fleet Resource & Loot Bonus Chance |
| Harvesting1 | Harvesting Rank 1 | Gain XP From Asteroids & 5% Resource Harvest Bonus Chance |
| Harvesting2 | Harvesting Rank 2 | Gain XP From Asteroids & 10% Resource Harvest Bonus Chance |
| Harvesting3 | Harvesting Rank 3 | Gain XP From Asteroids & 15% Resource Harvest Bonus Chance |
| Harvesting4 | Harvesting Rank 4 | Gain XP From Asteroids & 20% Resource Harvest Bonus Chance |
| Harvesting5 | Harvesting Rank 5 | Gain XP From Asteroids & 25% Resource Harvest Bonus Chance |
| Harvesting6 | Harvesting Rank 6 | Gain XP From Asteroids & 30% Resource Harvest Bonus Chance |
| Harvesting7 | Harvesting Rank 7 | Gain XP From Asteroids & 35% Resource Harvest Bonus Chance |
| AdvancedAlloys1 | Advanced Alloys | +2% Hull Max |
| AdvancedAlloys2 | Advanced Alloys II | +4% Hull Max |
| AdvancedHacking1 | Advanced Hacking | +1 Second Hack Duration |
| AdvancedHacking2 | Advanced Hacking II | +2 Second Hack Duration |
| AdvancedHacking3 | Advanced Hacking III | +3 Second Hack Duration & Targets Lose Special Abilities |
| AdvancedGrappling1 | Advanced Grappling | +1 Second Grapple Duration |
| AdvancedGrappling2 | Advanced Grappling II | +2 Second Grapple Duration |
| AdvancedGrappling3 | Advanced Grappling III | +3 Second Grapple Duration & Targets Dragged on Move |
| AdvancedDraining1 | Advanced Draining | +20 Shield & +2 Battery Stolen by Drain Attack |
| AdvancedDraining2 | Advanced Draining II | +40 Shield & +4 Battery Stolen by Drain Attack |
| AdvancedDraining3 | Advanced Draining III | +60 Shield & +6 Battery Stolen by Drain Attack & Can Critical |
| SpeedHack1 | Hack Speed | -4 Second Hack Cooldown |
| SpeedHack2 | Hack Speed II | -6 Second Hack Cooldown |
| SpeedHack3 | Hack Speed III | -8 Second Hack Cooldown |
| SpeedGrapple1 | Grapple Speed | -4 Second Grapple Cooldown |
| SpeedGrapple2 | Grapple Speed II | -6 Second Grapple Cooldown |
| SpeedGrapple3 | Grapple Speed III | -8 Second Grapple Cooldown |
| SpeedDrain1 | Drain Speed | -4 Second Drain Cooldown |
| SpeedDrain2 | Drain Speed II | -6 Second Drain Cooldown |
| SpeedDrain3 | Drain Speed III | -8 Second Drain Cooldown |
| HullMax1 | Improved Hulls Rank 1 | 5% Hull Bonus |
| HullMax2 | Improved Hulls Rank 2 | 8% Hull Bonus |
| HullMax3 | Improved Hulls Rank 3 | 11% Hull Bonus |
| HullMax4 | Improved Hulls Rank 4 | 14% Hull Bonus |
| HullMax5 | Improved Hulls Rank 5 | 17% Hull Bonus |
| HullMax6 | Improved Hulls Rank 6 | 20% Hull Bonus |
| HullMax7 | Improved Hulls Rank 7 | 23% Hull Bonus |
| HullMax8 | Improved Hulls Rank 8 | 30% Hull Bonus |
| ShieldMax1 | Improved Shields Rank 1 | 5% Shield Bonus |
| ShieldMax2 | Improved Shields Rank 2 | 8% Shield Bonus |
| ShieldMax3 | Improved Shields Rank 3 | 11% Shield Bonus |
| ShieldMax4 | Improved Shields Rank 4 | 14% Shield Bonus |
| ShieldMax5 | Improved Shields Rank 5 | 17% Shield Bonus |
| ShieldMax6 | Improved Shields Rank 6 | 20% Shield Bonus |
| ShieldMax7 | Improved Shields Rank 7 | 23% Shield Bonus |
| Leadership1 | Leadership | Speed Bonus and +3% Damage for Nearby Corporate Ships |
| Leadership2 | Leadership II | Speed Bonus and +5% Damage for Nearby Corporate Ships |
| Leadership3 | Leadership III | Speed Bonus and +7% Damage for Nearby Corporate Ships |
| LeadershipEffect1 | Leadership Effect | Speed Bonus and +3% Damage from Nearby Carrier |
| LeadershipEffect2 | Leadership Effect II | Speed Bonus and +5% Damage from Nearby Carrier |
| LeadershipEffect3 | Leadership Effect III | Speed Bonus and +7% Damage from Nearby Carrier |
| Interdictor1 | Interdictor | 15% Targeting & Movement Speed Penalty to Nearby Enemies |
| Interdictor2 | Interdictor II | 20% Targeting & Movement Speed Penalty to Nearby Enemies |
| Interdictor3 | Interdictor III | 25% Targeting & Movement Speed Penalty to Nearby Enemies |
| InterdictorEffect1 | Interdictor Effect | 15% Targeting & Movement Speed Penalty |
| InterdictorEffect2 | Interdictor Effect II | 20% Targeting & Movement Speed Penalty |
| InterdictorEffect3 | Interdictor Effect III | 25% Targeting & Movement Speed Penalty |
| GarrisonStrikes2 | Garrison Strikes II | Doubles Garrison Strike Damage Radius |
| GarrisonStrikes3 | Garrison Strikes III | Reduces Garrison Strike Warning Time |
| Overpower | Overpower | +10% Damage Bonus and 15% Damage Vulnerability |
| ReverseHacking | Reverse Hacking | Very High Chance of Hack Deflected Back at Attackers |
| ReverseGrappling | Reverse Grappling | Very High Chance of Grapple Deflected Back at Attackers |
| ReverseBatteryDrain | Reverse Drain | Very High Chance of Drain Deflected Back at Attackers |
| Deflector1 | Deflector Rank 1 | 3% Chance Damage Deflected Back At Attackers |
| Deflector2 | Deflector Rank 2 | 5% Chance Damage Deflected Back At Attackers |
| Deflector3 | Deflector Rank 3 | 7% Chance Damage Deflected Back At Attackers |
| Deflector4 | Deflector Rank 4 | 9% Chance Damage Deflected Back At Attackers |
| Deflector5 | Deflector Rank 5 | 11% Chance Damage Deflected Back At Attackers |
| Deflector6 | Deflector Rank 6 | 13% Chance Damage Deflected Back At Attackers |
| Deflector7 | Deflector Rank 7 | 15% Chance Damage Deflected Back At Attackers |
| Technician1 | Technician | Repair Removes Negative Status Effects |
| Technician2 | Technician II | Repair Can Critical & Removes Negative Status Effects |
| Technician3 | Technician III | Repair Can Splash, Critical & Removes Negative Status Effects |
| Technician4 | Technician IV | Repair Heals Over Time, Splashes, Criticals & Removes Effects |
| RepairOverTimeEffect | Repair Over Time | Immune to Effects & Repairs 3 Times Over 21 Seconds |
| AlienDamage1 | Damage vs Aliens Rank 1 | 3% Damage Bonus vs Alien Races |
| AlienDamage2 | Damage vs Aliens Rank 2 | 4% Damage Bonus vs Alien Races |
| AlienDamage3 | Damage vs Aliens Rank 3 | 5% Damage Bonus vs Alien Races |
| AlienDamage4 | Damage vs Aliens Rank 4 | 6% Damage Bonus vs Alien Races |
| AlienDamage5 | Damage vs Aliens Rank 5 | 7% Damage Bonus vs Alien Races |
| AlienDamage6 | Damage vs Aliens Rank 6 | 8% Damage Bonus vs Alien Races |
| AlienDamage7 | Damage vs Aliens Rank 7 | 9% Damage Bonus vs Alien Races |
| PvPDamage1 | Damage vs Players Rank 1 | 1% Damage Bonus vs Players |
| PvPDamage2 | Damage vs Players Rank 2 | 2% Damage Bonus vs Players |
| PvPDamage3 | Damage vs Players Rank 3 | 3% Damage Bonus vs Players |
| PvPDamage4 | Damage vs Players Rank 4 | 4% Damage Bonus vs Players |
| PvPDamage5 | Damage vs Players Rank 5 | 5% Damage Bonus vs Players |
| PvPDamage6 | Damage vs Players Rank 6 | 6% Damage Bonus vs Players |
| PvPDamage7 | Damage vs Players Rank 7 | 7% Damage Bonus vs Players |
| PvPBonusXP1 | Player Kill Bonus XP | +10% Bonus XP For Killing Players |
| PvPBonusXP2 | Player Kill Bonus XP II | +15% Bonus XP For Killing Players |
| PvPBonusXP3 | Player Kill Bonus XP III | +20% Bonus XP For Killing Players |
| NovaInversion | Nova Inversion | Very High Chance Nova Repairs Hull Instead of Damage |
| NovaDeath1 | Nova Death | Damage enemies when you die! (100% Strength) |
| NovaDeath2 | Nova Death II | Damage enemies when you die! (125% Strength) |
| NovaDeath3 | Nova Death III | Damage enemies when you die! (150% Strength) |
| NovaDeath4 | Nova Death IV | Damage enemies when you die! (175% Strength) |
| NovaDeath5 | Nova Death V | Damage enemies when you die! (200% Strength) |
| NovaDeath6 | Nova Death VI | Damage enemies when you die! (250% Strength) |
| NovaDeath7 | Nova Death VII | Damage enemies when you die! (300% Strength) |
| Regeneration1 | Regeneration Rank 1 | Units Repair 25 Hull Every 30 Seconds |
| Regeneration2 | Regeneration Rank 2 | Units Repair 50 Hull Every 30 Seconds |
| Regeneration3 | Regeneration Rank 3 | Units Repair 75 Hull Every 30 Seconds |
| Regeneration4 | Regeneration Rank 4 | Units Repair 100 Hull Every 30 Seconds |
| Regeneration5 | Regeneration Rank 5 | Units Repair 150 Hull Every 30 Seconds |
| Regeneration6 | Regeneration Rank 6 | Units Repair 200 Hull Every 30 Seconds |
| Regeneration7 | Regeneration Rank 7 | Units Repair 250 Hull Every 30 Seconds |
| Marauder1 | Marauder | +4% Damage vs Defense Units |
| Marauder2 | Marauder II | +8% Damage vs Defense Units |
| Marauder3 | Marauder III | +12% Damage vs Defense Units |
| Guardian1 | Guardian | +4% Damage vs Defense Unit Attackers |
| Guardian2 | Guardian II | +6% Damage vs Defense Unit Attackers |
| AttackDrones1 | Attack Drones | +3% Attack Drone Damage |
| AttackDrones2 | Attack Drones II | +5% Attack Drone Damage |
| AttackDrones3 | Attack Drones III | +7% Attack Drone Damage |
| AttackDrones4 | Attack Drones ADV | +9% Attack Drone Damage |
| RepairDrones1 | Repair Drones | +5% Drone Hull Repairs |
| RepairDrones2 | Repair Drones II | +7% Drone Hull Repairs |
| RepairDrones3 | Repair Drones III | +9% Drone Hull Repairs |
| RepairDrones4 | Repair Drones ADV | +11% Drone Hull Repairs |
| SpeedRepair1 | Repair Speed | -4 Second Repair Cooldown |
| SpeedRepair2 | Repair Speed II | -6 Second Repair Cooldown |
| SpeedRepair3 | Repair Speed III | -8 Second Repair Cooldown |
| BattleRam1 | Battle Ram Rank 1 | 5% Chance to Ram Hostiles on Move |
| BattleRam2 | Battle Ram Rank 2 | 10% Chance to Ram Hostiles on Move |
| BattleRam3 | Battle Ram Rank 3 | 15% Chance to Ram Hostiles on Move |
| BattleRam4 | Battle Ram Rank 4 | 20% Chance to Ram Hostiles on Move |
| BattleRam5 | Battle Ram Rank 5 | 25% Chance to Ram Hostiles on Move |
| BattleRam6 | Battle Ram Rank 6 | 30% Chance to Ram Hostiles on Move |
| BattleRam7 | Battle Ram Rank 7 | 35% Chance to Ram Hostiles on Move |
| LongRangeVision | Long Range Vision | Increased Sector Vision Range |
| PassiveScan1 | Passive Scanning | Counter Sneak Attacks and +15% Detect Cloaked Enemy Chance |
| PassiveScan2 | Passive Scanning II | Counter Sneak Attacks and +20% Detect Cloaked Enemy Chance |
| PassiveScan3 | Passive Scanning III | Counter Sneak Attacks and +30% Detect Cloaked Enemy Chance |
| Stealth1 | Basic Stealth | Movement Direction & Time Hidden |
| Stealth2 | Advanced Stealth | Movement Direction Hidden & Immune to Passive Scan |
| Scan1 | Scanning Rank 1 | Active Ability to Reveal Rank 1 Cloaking |
| Scan2 | Scanning Rank 2 | Active Ability to Reveal Rank 2 Cloaking |
| Scan3 | Scanning Rank 3 | Active Ability to Reveal Rank 3 Cloaking |
| Scan4 | Scanning Rank 4 | Active Ability to Reveal Rank 4 Cloaking |
| Scan5 | Scanning Rank 5 | Active Ability to Reveal Rank 5 Cloaking |
| Scan6 | Scanning Rank 6 | Active Ability to Reveal Rank 6 Cloaking |
| Scan7 | Scanning Rank 7 | Active Ability to Reveal Rank 7 Cloaking |
| AdvancedScanning | Advanced Scanning | +1 Scanning Power (Requires Scanning) |
| SpeedScan1 | Scan Speed | -4 Second Scan Cooldown |
| SpeedScan2 | Scan Speed II | -6 Second Scan Cooldown |
| SpeedScan3 | Scan Speed III | -8 Second Scan Cooldown |
| Cloak1 | Cloaking Rank 1 | Hide From Enemy Vision (Power 1) |
| Cloak2 | Cloaking Rank 2 | Hide From Enemy Vision (Power 2) |
| Cloak3 | Cloaking Rank 3 | Hide From Enemy Vision (Power 3) |
| Cloak4 | Cloaking Rank 4 | Hide From Enemy Vision (Power 4) |
| Cloak5 | Cloaking Rank 5 | Hide From Enemy Vision (Power 5) |
| Cloak6 | Cloaking Rank 6 | Hide From Enemy Vision (Power 6) |
| Cloak7 | Cloaking Rank 7 | Hide From Enemy Vision (Power 7) |
| AdvancedCloaking | Advanced Cloaking | +1 Cloaking Power (Requires Cloaking) |
| CloakDuration1 | Cloak Duration | +3 Second Cloak Duration |
| CloakDuration2 | Cloak Duration II | +5 Second Cloak Duration |
| CloakDuration3 | Cloak Duration III | +7 Second Cloak Duration |
| SpeedCloak1 | Cloak Speed | -4 Second Cloak Cooldown |
| SpeedCloak2 | Cloak Speed II | -6 Second Cloak Cooldown |
| SpeedCloak3 | Cloak Speed III | -8 Second Cloak Cooldown |
| Vanquisher | Vanquisher | +15% Damage Bonus and Immune to Hack and Grapple |
| Savior1 | Savior Rank 1 | Repairs of Targets Below 10% Health Always Critical & Splash |
| Savior2 | Savior Rank 2 | Repairs of Targets Below 15% Health Always Critical & Splash |
| Savior3 | Savior Rank 3 | Repairs of Targets Below 20% Health Always Critical & Splash |
| Savior4 | Savior Rank 4 | Repairs of Targets Below 25% Health Always Critical & Splash |
| Rebirth1 | Rebirth Rank 1 | Fatal Damage Restores 10% Health & Cloaks (6 Hour Cooldown) |
| Rebirth2 | Rebirth Rank 2 | Fatal Damage Restores 15% Health & Cloaks (5 Hour Cooldown) |
| Rebirth3 | Rebirth Rank 3 | Fatal Damage Restores 20% Health & Cloaks (4 Hour Cooldown) |
| Rebirth4 | Rebirth Rank 4 | Fatal Damage Restores 25% Health & Cloaks (3 Hour Cooldown) |
| Interdictor4 | Interdictor IV | 30% Targeting & Movement Speed Penalty to Nearby Enemies |
| InterdictorEffect4 | Interdictor Effect IV | 30% Targeting & Movement Speed Penalty |
| UNUSED11 | Future Technology | An Unused Future Technology Type |
| SmallStrikeTeamEffect | Small Strike Team | +5% Damage & +5 Resists if Fleet is 33% Small or Medium |
| OnFireEffect | On Fire! | Ship Takes Fire Damage Every 6 Seconds |
| CollisionEffect | Collision Warning! | Ship Takes Collision Damage Every 5 Seconds |
| UNUSED20 | Future Technology | An Unused Future Technology Type |
| EnemyTerritoryEffect | Enemy Territory | 10% Damage Vulnerability and All Resists Reduced by 10 |
| FriendlyTerritoryEffect | Friendly Territory | 10% Movement Speed Bonus and All Resists Increased by 5 |
| UNUSED30 | Future Technology | An Unused Future Technology Type |
| ResourceLootBonusPvP | PvP Loot & Xp Bonus | Xp and Loot Bonus in Player-vs-Player Zones |
| PvPProtection | PvP Protection | Temporary Protection from Player vs Player Attacks |
| NanobotCharge | Nanobot Charge | +10% XP Gain, +10% Outgoing Damage, +10% Move Speed Bonus |
| SneakAttack | Sneak Attack! | +30 Critical Chance and +25% Critical Damage Bonus |
| DailyTech1 | Daily Tech Bonus 1 | [Daily tech description depends on assigned daily tech type] |
| DailyTech2 | Daily Tech Bonus 2 | [Daily tech description depends on assigned daily tech type] |
| DailyTech3 | Daily Tech Bonus 3 | [Daily tech description depends on assigned daily tech type] |
| ShieldRepair1 | Shield Repair | Repair 10% More Shields with Hull Repair and Cloak |
| ShieldRepair2 | Shield Repair II | Repair 15% More Shields with Hull Repair and Cloak |
| ShieldRepair3 | Shield Repair III | Repair 20% More Shields with Hull Repair and Cloak |
| ShieldRepair4 | Shield Repair IV | Repair 25% More Shields with Hull Repair and Cloak |
| ShieldRepair5 | Shield Repair V | Repair 30% More Shields with Hull Repair and Cloak |
| HackRam1 | Hack Ram Rank 1 | 5% Chance to Hack Hostiles on Move |
| HackRam2 | Hack Ram Rank 2 | 10% Chance to Hack Hostiles on Move |
| HackRam3 | Hack Ram Rank 3 | 15% Chance to Hack Hostiles on Move |
| HackRam4 | Hack Ram Rank 4 | 20% Chance to Hack Hostiles on Move |
| HackRam5 | Hack Ram Rank 5 | 25% Chance to Hack Hostiles on Move |
| HackRam6 | Hack Ram Rank 6 | 30% Chance to Hack Hostiles on Move |
| HackRam7 | Hack Ram Rank 7 | 35% Chance to Hack Hostiles on Move |

## Technology Helper Classifications

Source: `Assembly-CSharp\DFHOJHHBAMJ.cs`.

These helpers are client-side classifications. Use them as source-backed staging data, but do not automatically turn every helper name into public wording.

### Effect remaps

| Source tech | Effect tech |
|---|---|
| Leadership1 | LeadershipEffect1 |
| Leadership2 | LeadershipEffect2 |
| Leadership3 | LeadershipEffect3 |
| Interdictor1 | InterdictorEffect1 |
| Interdictor2 | InterdictorEffect2 |
| Interdictor3 | InterdictorEffect3 |
| Interdictor4 | InterdictorEffect4 |

### Family helpers

| Helper | Client rule |
|---|---|
| `IsStealthRelated()` | Cloak1 through AdvancedCloaking |
| `IsScanningRelated()` | PassiveScan1 through AdvancedScanning; this range includes Stealth1 and Stealth2 because of enum order |
| `IsDeflector()` | Deflector1 through Deflector7 |
| `GetEffectsVision()` | true for stealth-related or scanning-related techs |
| `GetIsPvPDamage()` | PvPDamage1 through PvPDamage7 |
| `GetIsPassiveScanning()` | PassiveScan1 through PassiveScan3 |
| `IsGarrisonsOnly()` | GarrisonStrikes2 and GarrisonStrikes3 |
| `IsDailyTech()` | DailyTech1 through DailyTech3 |

### Status effects

`IsStatusEffect(tech, entityType)` returns true for these status-style techs:

| Tech/group | Condition |
|---|---|
| RepairFacility1 | status effect unless entity type is Outpost |
| RepairFacility2 | status effect unless entity type is Garrison |
| RepairFacility3 | status effect unless entity type is Planet |
| RepairFacility4 | status effect unless entity type is Shipyard |
| SpaceLaneEffect1-3 | always status effects |
| LeadershipEffect1-3 | always status effects |
| InterdictorEffect1-4 | always status effects |
| RepairOverTimeEffect | always status effect |
| SmallStrikeTeamEffect | always status effect |
| OnFireEffect | always status effect |
| CollisionEffect | always status effect |
| EnemyTerritoryEffect | always status effect |
| FriendlyTerritoryEffect | always status effect |
| ResourceLootBonusPvP | always status effect |
| PvPProtection | always status effect |
| NanobotCharge | always status effect |
| SneakAttack | always status effect |
| DailyTech1-3 | status effects through `IsDailyTech()` |

### Researchable technologies

`CanBeResearched()` returns true for:

| Researchable group | Ranks / techs |
|---|---|
| EvasiveManeuvers | 1 |
| Intimidation | 1 |
| Targeting | 1-2 |
| ShieldAmplifier | 1-2 |
| Scavenger | 1-2 |
| Harvesting | 1-2 |
| AdvancedAlloys | 1-2 |
| AdvancedHacking | 1-2 |
| AdvancedGrappling | 1-2 |
| AdvancedDraining | 1-2 |
| SpeedHack | 1-2 |
| SpeedGrapple | 1-2 |
| SpeedDrain | 1-2 |
| GarrisonStrikes | 2-3 |
| AlienDamage | 1-2 |
| PvPDamage | 1-2 |
| PvPBonusXP | 1-2 |
| Marauder | 1-2 |
| Guardian | 1-2 |
| AttackDrones | 1-2 |
| RepairDrones | 1-2 |
| SpeedRepair | 1-2 |
| PassiveScan | 2-3 |
| AdvancedScanning | single tech |
| SpeedScan | 1-2 |
| AdvancedCloaking | single tech |
| CloakDuration | 1-2 |
| SpeedCloak | 1-2 |
| HackRam | 1-2 |

### Stacks with other ranks

`GetStacksWithOtherRanks()` returns true for:

| Stackable group | Ranks / techs |
|---|---|
| EvasiveManeuvers | 1-3 |
| Intimidation | 1-3 |
| Intuition | 1-3 |
| Analysis | 1-3 |
| HyperDrive | 1-3 |
| Targeting | 1-3 |
| Junker | 1-3 |
| ShieldCapacitors | 1-3 |
| ShieldAmplifier | 1-3 |
| ShieldPierce | 1-3 |
| AdvancedAlloys | 1-2 |
| AdvancedHacking | 1-3 |
| AdvancedGrappling | 1-3 |
| AdvancedDraining | 1-3 |
| SpeedHack | 1-3 |
| SpeedGrapple | 1-3 |
| SpeedDrain | 1-3 |
| GarrisonStrikes | 2-3 |
| PvPBonusXP | 1-3 |
| Marauder | 1-3 |
| Guardian | 1-2 |
| AttackDrones | 1-4 |
| RepairDrones | 1-4 |
| SpeedRepair | 1-3 |
| PassiveScan | 1-3 |
| SpeedScan | 1-3 |
| CloakDuration | 1-3 |
| SpeedCloak | 1-3 |
| ShieldRepair | 1-5 |

Notably, several ranked families are not returned by this helper, including Scavenger, Harvesting, Freighter, HullMax, ShieldMax, Deflector, AlienDamage, PvPDamage, NovaDeath, Regeneration, BattleRam, Scan, Cloak, and HackRam. Those may still have max-rank override behavior through `GetMaxOverrideTech()`.

### Major technologies

`IsMajor()` returns true for:

| Major group | Ranks / techs |
|---|---|
| SkipJump | single tech |
| CrewFurnace | single tech |
| Analysis | 1-3 |
| HyperDrive | 1-3 |
| Targeting | 2-3 |
| ShieldCapacitors | 2-3 |
| ShieldAmplifier | 2-3 |
| ShieldPierce | 2-3 |
| Scavenger | 2-7 |
| Harvesting | 2-7 |
| AdvancedAlloys | 2 |
| AdvancedHacking | 2-3 |
| AdvancedGrappling | 2-3 |
| AdvancedDraining | 2-3 |
| SpeedHack | 2-3 |
| SpeedGrapple | 2-3 |
| SpeedDrain | 2-3 |
| HullMax | 1-8 |
| ShieldMax | 1-7 |
| Leadership | 1-3 |
| GarrisonStrikes | 2-3 |
| Overpower | single tech |
| ReverseHacking | single tech |
| ReverseGrappling | single tech |
| ReverseBatteryDrain | single tech |
| Deflector | 1-7 |
| Technician | 2-4 |
| AlienDamage | 2-7 |
| PvPDamage | 2-7 |
| PvPBonusXP | 2-3 |
| NovaInversion | single tech |
| NovaDeath | 1-7 |
| Regeneration | 2-7 |
| Marauder | 2-3 |
| Guardian | 2 |
| AttackDrones | 2-4 |
| RepairDrones | 2-4 |
| SpeedRepair | 2-3 |
| BattleRam | 3-7 |
| PassiveScan | 3 |
| Scan | 3-7 |
| AdvancedScanning | single tech |
| SpeedScan | 2-3 |
| Cloak | 3-7 |
| AdvancedCloaking | single tech |
| CloakDuration | 2-3 |
| Vanquisher | single tech |
| ShieldRepair | 3-5 |
| HackRam | 2 |

### Defense eligibility

`CanDefenseHave()` returns false for the groups below and true for other technology values. This is a client helper classification, not a complete public rule for how defense units acquire techs.

| Not defense-eligible group | Ranks / techs |
|---|---|
| NULL / UNUSED1 | excluded |
| EvasiveManeuvers | 1-3 |
| Intuition | 1-3 |
| SkipJump | single tech |
| CrewFurnace | single tech |
| Analysis | 1-3 |
| HyperDrive | 1-3 |
| SpaceLaneEffect | 1-3 |
| Targeting | 1-3 |
| Junker | 1-3 |
| Mechanic | 1-3 |
| Freighter | 1-5 |
| Scavenger | 1-7 |
| Harvesting | 1-7 |
| Leadership | 1-3 |
| LeadershipEffect | 1-3 |
| InterdictorEffect | 1-4 |
| PvPBonusXP | 1-3 |
| Stealth | 1-2 |
| Cloak | 1-7 |
| AdvancedCloaking | single tech |
| CloakDuration | 1-3 |
| SpeedCloak | 1-3 |
| UNUSED11 | excluded |
| SmallStrikeTeamEffect | single tech |
| OnFireEffect | single tech |
| CollisionEffect | single tech |
| UNUSED20 | excluded |
| EnemyTerritoryEffect | single tech |
| FriendlyTerritoryEffect | single tech |
| UNUSED30 | excluded |
| ShieldRepair | 1-5 |

Notable defense-eligible groups by omission include RepairFacility1-4, Intimidation1-3, Vorpal1-4, ShieldCapacitors1-3, ShieldAmplifier1-3, ShieldPierce1-3, Interdictor1-4 source techs, PvPDamage1-7, and most advanced/combat utility tech families not listed above.

### Paid tech-point boost candidates

`CanPaidTechPointBoost()` returns true for rank-1/base entries only:

Analysis1, HyperDrive1, Targeting1, ShieldPierce1, Scavenger1, Harvesting1, SpeedHack1, SpeedGrapple1, SpeedDrain1, HullMax1, ShieldMax1, AlienDamage1, PvPDamage1, PvPBonusXP1, Marauder1, Guardian1, AttackDrones1, RepairDrones1, SpeedRepair1, SpeedScan1, CloakDuration1, and SpeedCloak1.

### Artifact candidates

`CanBeArtifact()` returns true for:

| Artifact-capable group | Ranks / techs |
|---|---|
| EvasiveManeuvers | 1 |
| Intimidation | 1 |
| Analysis | 1-3 |
| HyperDrive | 1-2 |
| Targeting | 1 |
| Junker | 1 |
| Mechanic | 1 |
| ShieldCapacitors | 1 |
| ShieldAmplifier | 1-2 |
| ShieldPierce | 1 |
| Scavenger | 1 |
| Harvesting | 1 |
| AdvancedAlloys | 1-2 |
| AdvancedHacking | 1-2 |
| AdvancedGrappling | 1-2 |
| AdvancedDraining | 1-2 |
| SpeedHack | 2 |
| SpeedGrapple | 2 |
| SpeedDrain | 2 |
| ShieldMax | 1 |
| GarrisonStrikes | 2-3 |
| Overpower | single tech |
| AlienDamage | 1 |
| PvPDamage | 1 |
| PvPBonusXP | 1 |
| NovaInversion | single tech |
| NovaDeath | 1 |
| Regeneration | 1 |
| Marauder | 1 |
| Guardian | 1 |
| AttackDrones | 1-3 |
| RepairDrones | 1-3 |
| SpeedRepair | 2 |
| PassiveScan | 2-3 |
| Stealth | 1-2 |
| AdvancedScanning | single tech |
| SpeedScan | 2 |
| AdvancedCloaking | single tech |
| CloakDuration | 2 |
| HackRam | 1 |

### Max override families

`GetMaxOverrideTech()` returns the max-rank representative for these ranked families. A `NULL` result means the helper does not override that tech family.

| Family | Max override |
|---|---|
| Freighter1-5 | Freighter5 |
| Scavenger1-7 | Scavenger7 |
| Harvesting1-7 | Harvesting7 |
| HullMax1-8 | HullMax8 |
| ShieldMax1-7 | ShieldMax7 |
| Deflector1-7 | Deflector7 |
| AlienDamage1-7 | AlienDamage7 |
| PvPDamage1-7 | PvPDamage7 |
| NovaDeath1-7 | NovaDeath7 |
| Regeneration1-7 | Regeneration7 |
| BattleRam1-7 | BattleRam7 |
| Scan1-7 | Scan7 |
| Cloak1-7 | Cloak7 |
| HackRam1-7 | HackRam7 |

## Daily tech generic categories

Source: `DFHOJHHBAMJ.cs`, method `GetDailyTechGenericDescription(this ENIALFMHHLL)`.

| Daily type | Generic description |
|---|---|
| Small | Small Ships Random Daily Bonus |
| Medium | Medium Ships Random Daily Bonus |
| Large | Large Ships Random Daily Bonus |
| Huge | Huge Ships Random Daily Bonus |
| Human | Human Faction Units Random Daily Bonus |
| Wyrd | Wyrd Faction Units Random Daily Bonus |
| Het | Het Faction Units Random Daily Bonus |
| Precursor | Precursor Faction Units Random Daily Bonus |
| Random1 | Random Daily Bonus |
| Random2 | Random Daily Bonus |
| Random3 | Random Daily Bonus |

## Daily tech exact variants

Source: `DFHOJHHBAMJ.cs`, method `GetDailyTechDescription(this ENIALFMHHLL, byte)`. The numeric code appears to choose the daily-bonus variant; `0/default` means any non-99 code not explicitly handled by cases 1-10.

| Variant code | Daily type | Client description |
|---|---|---|
| 0/default | Small/Medium/Large/Huge/Human/Wyrd/Het/Precursor | Matching ship size or faction moves 20% faster |
| 0/default | Random1 | Mission Rewards Doubled |
| 0/default | Random2 | Young is Brash - Old is Wise - Admirals are Critical - Crafters are Masterful |
| 0/default | Random3 | 50% Chance Crafted Items Gain +1 Rarity Upgrade |
| 1 | Small/Medium/Large/Huge/Human/Wyrd/Het/Precursor | Matching ship size or faction gains 20% more XP |
| 1 | Random1 | Item Durability Repairs Cost 33% Less |
| 1 | Random2 | Ancient Alien Secrets Hidden In Asteroids |
| 1 | Random3 | Crafted Items Gain +10 Quality Bonus |
| 2 | Small/Medium/Large/Huge/Human/Wyrd/Het/Precursor | Matching ship size or faction repairs can critical and splash |
| 2 | Random1 | Convert Credits to Tech Points Gets 10% Bonus |
| 2 | Random2 | Arena Awards Bonus Loot and Skulls |
| 2 | Random3 | Blueprint Discovery Unlocks Extra Item |
| 3 | Small/Medium/Large/Huge/Human/Wyrd/Het/Precursor | Matching ship size or faction can cloak and scan at power 1 |
| 3 | Random1 | No HUGE or MASSIVE Ships Allowed in The Arena |
| 3 | Random2 | Double XP Bonus for Defense Unit Level Up |
| 3 | Random3 | Double Resources Gained From Tech Point Trades |
| 4 | Small/Medium/Large/Huge/Human/Wyrd/Het/Precursor | Matching ship size or faction has Advanced Grappling III |
| 4 | Random1 | Pirate & Alien Defense Units Drop Bonus Loot |
| 4 | Random2 | Naked Aggression |
| 4 | Random3 | Crafted Ships Gain Higher Random Stat Bonus |
| 5 | Small/Medium/Large/Huge/Human/Wyrd/Het/Precursor | Matching ship size or faction has Reverse Hack and Reverse Grapple |
| 5 | Random1 | Double Skulls for World PvP Kills |
| 5 | Random2 | Double Rewards for Alliance Defense Kills |
| 5 | Random3 | Double Skill Gain From Item & Ship Crafting |
| 6 | Random1 | Double Loot for Hardcore Ships in PvP & Homeworld Maps |
| 6 | Random2 | Created in the Image of the Space Lord or Space Lady |
| 6 | Random3 | They Stole Our Holy Relics! |
| 7 | Random1 | Invasion Bosses Drop Blueprints |
| 7 | Random2 | Hull Repairs Reduced by 80% in The Arena |
| 7 | Random3 | Assassin Leaders Can Drop Powerful Item Blueprints |
| 8 | Random1 | Invasion Bosses Drop Powerful Holiday Gem Loot |
| 8 | Random2 | Grapple & Drain Attacks Splash to Multiple Enemies |
| 8 | Random3 | Taunt & Hacking Attacks Splash to Multiple Enemies |
| 9 | Random1 | Pirate Leaders Hide in Rock Asteroids |
| 9 | Random2 | Alien Leaders Hide in Non-Rock Asteroids |
| 9 | Random3 | Rescue Drifting Crew for Rewards |
| 10 | Random1 | Item Damage Only 1% in All World PvP and SR8+ PvE Deaths |
| 10 | Random2 | Alien Leaders & Invasion Bosses Always Drop Void Loot |
| 10 | Random3 | Double Item Rewards for Invasion & Arena Victory |
| 99 | Random1 | Bonus Loot and PvP Skulls with Low Item Durability Damage |
| 99 | Random2 | Special Holiday Event |
