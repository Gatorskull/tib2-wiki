# Gootchat Source Review

Review of `Gathered Training Data/gootchat.txt`, a raw export of Goot/Gooter/Gaytor outgoing in-game messages across channels.

This is a high-value **community teaching source**, but it is still chat. Treat it as practical guidance and lead-player observations unless confirmed by the in-game wiki, current testing, or direct developer data.

---

## What this source improves

| Topic | What gootchat helps define | Suggested wiki destination |
|-------|----------------------------|----------------------------|
| Carrier / Leadership | Level 35 carrier milestone, carrier bonus requiring corporation membership, fleet move speed inheriting carrier movement, carrier gearing priority: speed first, survivability second. | `Ships/Carrier-Leadership.md`. |
| Item slot priority | First gun/drone/battery slot gives full item stats; later slots are "aux" and only give 10%. Technologies and main item actions still apply in full. | `Items/Equipment-Slots.md`. |
| Interdictors | Enemy interdictors nerf target speed and move speed; target speed is especially important in PvP; world-sector visual cues appear to distinguish enemy vs friendly interdictor influence. | `Ships/Interdictor-Carrier.md`, `World/Maps/Sectors.md`. |
| Outpost missions | Mission tab + question mark can identify the source map/outpost. Outpost tasks can include kills and resource deposit steps. Resource deposits must go to the issuing outpost. | `Gameplay/Missions.md`, possible `Gameplay/Activities/Outpost-Missions.md`. |
| Structure gear score | Structures need minimum gear score to deploy; PvP structure skull payout is based on Gear Score. Low-GS-but-effective structures are used to reduce enemy payout. | `Entities/Structures/index.md`. |
| Freighter | Freighter technology improves harvesting; gootchat describes doubled harvest yield, while the in-game wiki describes doubled harvesting chances. | `Ships/Ship-Mods.md`, `Gameplay/Activities/Player vs Environment (PVE)/Open World Farming.md`. |
| PvP sorting and drivers | Drivers can be targeted by sort order; "blend in" gearing matters; common concerns include small hull, worst gear, largest size, fastest, first to arrive, most in danger. | PvP guide pages, not core reference pages. |
| Settings | Local sector ship count and top-down camera view are repeatedly explained to players. | New `Getting-Started/Settings.md`. |
| Follow behavior | Follows drop as soon as the followed ship is 3 sectors away and cannot resume until close enough. | `World/Maps/Sectors.md`. |
| Wyrd shield builds | Wyrd ships have stable shield-regeneration and shield-capacitor behavior, with practical farming implications. | `World/Factions/Wyrd.md`; deeper guide later. |

---

## Likely new pages from this source

| Page | Why it may be useful |
|------|----------------------|
| `Getting-Started/Settings.md` | Repeated practical advice: local sector counts, top-down view, sort options, camera behavior. |
| `Ships/Carrier-Leadership.md` | Carrier behavior is important enough for new players that it may deserve a focused page instead of being buried in Ships index. |
| `Items/Equipment-Slots.md` | First-slot vs aux-slot rules are core, easy to miss, and affect every build. |
| `Gameplay/Activities/Outpost-Missions.md` | Outpost missions are distinct enough from general missions to deserve a guide. |
| `Gameplay/Activities/Player vs Player (PVP)/Fleet-vs-Fleet-Guide.md` | Good place for driver, sort-order, collision, and interdictor strategy without polluting reference pages. |

---

## Confirmed by Goot

| Claim | Confirmation |
|-------|--------------|
| Carrier bonus only works when the player is in a corporation. | Confirmed. |
| Carrier-led fleets inherit carrier movement pacing. | Confirmed. |
| Hard minimum move times are 3.0 s small, 3.2 s medium, 3.3 s large, and 3.5 s huge/massive. | Confirmed. |
| Ships can overstack move speed past the hard minimum to counter enemy Interdictor penalties. | Confirmed. |
| Aux slots give 10% of all stats on that item. | Confirmed. |
| Technologies from aux-slot items apply in full. | Confirmed. |
| Weapon/drone main actions are not reduced by aux-slot status. | Confirmed. |
| Follow drops as soon as the followed ship is 3 sectors away. | Confirmed. |
| Interdictor UI cues: enemy is bright red/pulsing, friendly is light gray pulsing ring. | Confirmed. |
| Outpost missions should have a dedicated page. | Confirmed. |
| Wyrd shield mechanics are stable enough to document. | Confirmed. |

---

## Claims still needing exact source or formula

| Claim | Why it needs confirmation |
|-------|---------------------------|
| Freighter technology makes each harvest from that ship yield 2x normal. | Likely useful, but confirm whether it is exactly 2x and whether it applies to all harvested resources. |
| Largest-size sort is EP-based rather than ship class alone. | Important PvP sorting behavior; needs exact definition. |

---

## Content guidance

Use gootchat mostly for:

- practical player-facing guides
- workflow steps players repeatedly ask for
- examples of confusing UI
- strategy notes labeled as community guidance

Avoid using gootchat alone for:

- exact formulas
- market prices
- current meta builds
- balance claims
- "best" recommendations without context

---

## Immediate wiki opportunities

1. Add a **Settings** page for new players.
2. Expand **Carrier Leadership** with examples if needed.
3. Expand **Equipment Slots** with screenshots or examples if needed.
4. Expand **Outpost Missions** with rewards and chain rules once exact values are verified.
5. Expand **Interdictor Carrier** with rank math when confirmed.
