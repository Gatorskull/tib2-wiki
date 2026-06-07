# Client Mining Pass 3 - Runtime, Maps, Assets, Packets

Source scope: 2.1.0 Steam client decompile at `E:\TIB2 DEV FOLDER\2.1.0 Steam Client\Decompiled\Assembly-CSharp`, plus adjacent installed Unity data folders where noted.

Status: contributor-only source notes. Do not publish these as public rules without either matching a public gameplay page to the code path or getting player/server confirmation. Some values are client defaults and can be replaced by server packets.

## 1. Runtime/config values

Primary classes:

- `JEKJDKMBIGN.cs`: static config wrapper used throughout gameplay logic.
- `PGJIDFCBFCC.cs`: backing config object with client default values and network serialization.
- `GKFECKLMHGM.cs`: stat and derived-stat formula logic.
- `OPDJFCNPEMJ.cs`: network command that can deserialize/apply config data.

Important conclusion: `PGJIDFCBFCC` has real default values in the client, but the config object is also deserialized from server/network data. Treat these as client fallback/default config, not guaranteed live-server constants.

Confirmed defaults found:

| Topic | Client field/formula | Default |
| --- | --- | --- |
| Arena minimum Gear Score | `OGDOBALMMDJ` | `1000` |
| Base move speed | `GetBaseMoveSpeedMS(size)` | `JLGIMFCBOJJ + size * 500` |
| Base move speed seed | `JLGIMFCBOJJ` | `8000` ms |
| Move speed percent floor | `KAIHHELAKEE` via `GetMoveSpeedPercentMod()` | `-0.65` |
| Final move speed hard floor | `ODGHLDCPIOE` via `GetModifiedMoveSpeedMS()` | `3000` ms |
| Final move speed formula | `base + base * MoveSpeedPercent`, then max with hard floor | rounded ms |
| Targeting speed percent floor | `HOLJMFMHLPN` | `-0.65` |
| Weapon base lock | `GGMMFKMJCHO` | `3500` ms |
| Fighter/drone base lock | `OJIGAFHCNDB` | `5000` ms |
| Minimum lock time | `LEAOGINMOPH` | `800` ms |
| Size-difference lock step | `JHCCMDDDJFO` | `400` ms |
| Purge cooldown | hardcoded in `GetAbilityCooldownMS` | `8000` ms |
| Scan cooldown | `ALMPMOBFMIE` | `40000` ms |
| Cloak cooldown | `LJGJFGELEFD` | `76000` ms |
| Repair cooldown | `KDHEPKJOKKK` | `50000` ms |
| Default status/offensive ability cooldown | `GIDPJINOOGK` | `50000` ms |

Move prep defaults:

| Ship size/path | Field | Default |
| --- | --- | --- |
| Default/small/skirmisher path | `FHFBKBJMJHC` | `700` ms |
| Medium | `PKJFJCLLDFI` | `1000` ms |
| Large | `MOOCLGPLLML` | `1300` ms |
| Huge | `DEGAIDCMJHP` | `1700` ms |
| Massive | `PCNDFMLGGKN` | `1700` ms |
| Special boolean override path | `GIFJNPIPOIA || DPGJNLDGPBF` | `500` ms |

Open rule question: the user-defined size-specific practical minimums are small `3.0s`, medium `3.2s`, large `3.3s`, huge/massive `3.5s`, with a `-65%` move-speed floor per size. The code also has a final hard floor of `3000` ms. Public movement documentation should reconcile these as "effective minimum from -65% modifier by size" versus "absolute client hard floor" before rewriting.

Ship craft cost multipliers from config:

| Ship class | Field | Default |
| --- | --- | --- |
| Assassin | `OLIMPLNDFCP` | `4.0` |
| Flagship | `JHECOOJNDEB` | `3.0` |
| Carrier | `EJPHAHLCPJP` | `3.5` |
| Hades | `HLFGHDDKNLD` | `3.5` |
| Emperor | `FEHOHBMKKHD` | `5.0` |

Ship build relic costs:

| Ship class | Normal | Hardcore |
| --- | ---: | ---: |
| Assassin | `1` | needs verification |
| Carrier | `15` | `8` |
| Hades | `3` | `2` |
| Emperor | `50` | `25` |

Regeneration tech hull defaults found in `GetRegenerationTechHull`: `25`, `50`, `75`, `100`, `150`, `200`, `250`. Need map these to exact technology tiers before public use.

## 2. Serialized map/system data

Primary classes:

- `HBCLPLAMOJI.cs`: map template.
- `NCJPKNGDBKM.cs`: active/instanced map object.
- `IOJAKKPHIGB.cs`: sector object.
- `AMPIBGMCEKF.cs`: map template create/update command.
- `GEPGIDFFFJO.cs`: active map create/update command.

Confirmed map template model:

| Field | Meaning from usage |
| --- | --- |
| `HJIBAHOLMCG` | map template id |
| `BNAECDENEBA` | map/template name |
| `JLHEDDMDBGJ`, `EENBPPFCCLO` | template coordinate or ordering fields, exact public meaning needs confirmation |
| `GOFMHCBFNEP` | faction |
| `DFEGOILLMGA` | map type enum |
| `DBLNKNDPDCL` | sector link/path data |
| `MBPECGGHNBH` | extra sector coordinate markers |
| `PHNGJOPAMOE` | linked map templates |

Confirmed structure:

- `HBCLPLAMOJI` has constant `15`, and `AMPIBGMCEKF` serializes/deserializes `225` `DBLNKNDPDCL` entries. This strongly confirms map templates are a 15x15 sector grid.
- `AMPIBGMCEKF` serializes map id, name, two int fields, faction byte, map type byte, 225 sector-link entries, linked map IDs, and extra coordinate markers.
- `AMPIBGMCEKF.Execute()` applies that payload into `HBCLPLAMOJI.GetOrCreate(id)`.
- `NCJPKNGDBKM` separates normal and arena maps, provides center-sector access through `GetSector(7,7)`, exposes active sectors, and formats map labels like `SR#` or `SR# PvP` in prior pass findings.

Legacy map JSON:

- Old Goot Mod files under `E:\TIB2 DEV FOLDER\1.5.6 Client - Goot Mod\TheInfiniteBlack2\Mods\Maps` show a JSON schema with `Coords` and `Connections`.
- These are legacy/non-current. They are useful for understanding a likely map graph shape, but not for current 2.1.0 canonical system layouts.

Embedded old wiki fallback:

- `AJDGBIOKNKA.cs` contains a large `WIKI ERROR FALLBACK` string with old in-game wiki text.
- It mentions "over 50 Solar Systems", "over 30,000 sectors", five factions, Sol tutorial language, and `Quick Jump costs 1 Tech Point`.
- Treat as old bundled help text, not current canon unless cross-checked.

## 3. Unity asset/resource mining

The named 2.1.0 decompile folder only contains C# decompiled source and the solution file. It does not include current Unity asset files.

Adjacent installed client folders do contain Unity assets:

- `E:\TIB2 DEV FOLDER\TheInfiniteBlack2\TheInfiniteBlack2_Data`
- `E:\TIB2 DEV FOLDER\1.9.1 Steam Client\TheInfiniteBlack2\TheInfiniteBlack2_Data`

Observed asset files:

- `globalgamemanagers.assets`
- `resources.assets`
- `sharedassets*.assets`
- `StreamingAssets\UnityServicesProjectConfiguration.json`

Raw string extraction from `globalgamemanagers.assets` exposed type/object names but not readable XML payload content. Direct searches for `<?xml`, `<ShipDbObj`, `<ItemDbObj`, `<CombatEntityDbObj`, and similar content markers returned no payload hits in the checked assets.

Useful DB/XML asset names found:

- `PlayerDbObj.Xml`
- `GearSet.Xml`
- `ItemDbObj.Xml`
- `DbPlayerStats.Xml`
- `DbStats.Xml`
- `CombatEntityDbObj.Xml`
- `PortraitDbObj.Xml`
- `SbAccountDb.Xml`
- `ShipDbObj.Xml`
- `EntityDbObj.Xml`

Useful object names found:

- `AsteroidDbObj`
- `EntityDbObj`
- `GarrisonDbObj`
- `CargoResourceDbObj`
- `ArtifactDbObj`
- `CombatEntityDbObj`
- `CargoMoneyDbObj`
- `OutpostDbObj`
- `PlanetDbObj`
- `CorpDbObj`
- `ShipDbObj`
- `DefenseEntityDbObj`
- `AuctionDbObj`
- `PortraitDbObj`
- `ShipyardDbObj`
- `ItemDbObj`

Useful network/map names found in assets:

- `RequestInspectMap`
- `CreateMapCommand`
- `CreateMapTemplateCommand`
- `SetMapExploredCommand`
- `SetSectorVisibilityCommand`
- `SetSectorStatesCommand`
- `ClearMapStatusCommand`
- `MapExploration`
- `MapEvent`
- `MapEventHiddenClue`
- `MapEventNova`
- `MapEventGarrisonStrike`
- `MapEventGarrisonStrikeEnd`

Extraction blockers:

- `UnityPy` and `unitypack` were not installed in the available Python runtime.
- AssetsTools-related DLLs exist in adjacent client/MelonLoader folders, but no standalone extractor was found during this pass.
- Next deeper option: build a small extraction tool against `AssetsTools.NET.dll` or use AssetRipper/UnityPy outside the current available toolset to read TextAsset/MonoBehaviour object payloads by type.

## 4. Network packet models

Packet factory:

- `DHEDFIGEIFL.Create(byte)` maps server command byte IDs to command classes.
- Confirmed map command IDs from factory:
  - command id `5` -> `GEPGIDFFFJO`
  - command id `6` -> `AMPIBGMCEKF`

Likely original names from asset strings:

| Obfuscated class | Likely original name | Why |
| --- | --- | --- |
| `LOAINHBADJP` | `RequestInspectMap` | Sent by `PPKFDLLBBOP.DoInspectMap(int)`; asset name exists |
| `GEPGIDFFFJO` | `CreateMapCommand` | Applies active map state to `NCJPKNGDBKM`; asset name exists |
| `AMPIBGMCEKF` | `CreateMapTemplateCommand` | Applies full template payload to `HBCLPLAMOJI`; asset name exists |
| `BEJCCIGCHBD` | `SetSectorVisibilityCommand` | Payload is map id, x, y, visibility enum; executes `sector.SetVisibility(...)`; asset name exists |

`RequestInspectMap` behavior:

- `PPKFDLLBBOP.DoInspectMap(int mapId)` throttles repeat requests for the same map id for 14 seconds.
- It sends `LOAINHBADJP.Get(mapId)`.
- `LOAINHBADJP` serializes only `PDDMBBHEBMI`, the target map id.

`CreateMapTemplateCommand` behavior:

- Command byte id: `6`.
- Applies to `HBCLPLAMOJI.GetOrCreate(mapTemplateId)`.
- Payload includes:
  - template id
  - name
  - two int fields
  - faction byte
  - map type byte
  - `225` sector-link entries
  - linked map template id array
  - coordinate marker array
- This is a strong source for map topology, but the actual payload values come from server packets/assets, not from hardcoded C# constants.

`CreateMapCommand` behavior:

- Command byte id: `5`.
- Applies to `NCJPKNGDBKM.GetOrCreate(mapId)`.
- Payload includes:
  - map id
  - two faction-like enum bytes (`NNMICCDNLEJ`, `GCLEIOMGAOO`)
  - one map status/type enum (`LOBBBAAJPGJ`)
- It sets `IDPOINBEIKB` to true/false depending on update path. This appears to mark whether the active map object is loaded/valid/known in the client cache, but the exact public wording should be verified.

`SetSectorVisibilityCommand` behavior:

- Obfuscated class: `BEJCCIGCHBD`.
- Command byte id: `161`.
- Payload is four bytes:
  - map id
  - x coordinate
  - y coordinate
  - `JHEHCFOAKHK` visibility enum
- Execute path:
  - `NCJPKNGDBKM.GetOrCreate(mapId).GetSector(x, y)`
  - `sector.SetVisibility(visibility)`

Important packet-model caveat:

- Assets expose original command names, while decompiled C# classes are obfuscated. The class/name mapping above is inferred by matching asset names to payload behavior and call sites. It is strong for map/template/visibility commands, but still worth tagging as "client inferred" in contributor notes.

## What This Unlocks

Good public-candidate updates after confirmation:

- Movement page can quote the actual formula shape and clearly distinguish percent modifier floor from final hard floor.
- Map pages can state that systems use a 15x15 sector grid, with linked sectors forming the reachable graph.
- Contributor docs can say old embedded wiki fallback text is historical evidence only.
- Future map-mining work should target server packet capture or Unity TextAsset/MonoBehaviour extraction rather than more broad source grepping.

Needs confirmation or deeper extraction:

- Current live values when server config overrides the client defaults.
- Exact mapping for regeneration tech hull tiers.
- Exact public meaning of map template coordinate/order fields.
- Full item/ship DB payloads from Unity assets, if they are stored as TextAssets or serialized MonoBehaviours.
- Full set of `SetMapExplored`, `SetSectorStates`, and `ClearMapStatus` command class mappings.
