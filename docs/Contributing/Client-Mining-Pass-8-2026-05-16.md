# Client Mining Pass 8 - Quick Jump, Artifacts, Cargo, Research, Defense Growth

Date: 2026-05-16

Scope: Current Steam client decompile under `E:\TIB2 DEV FOLDER\2.1.0 Steam Client\Decompiled\Assembly-CSharp`.

This note covers five more extraction areas after `Client-Mining-Pass-7-2026-05-16.md`:

24. Quick Jump and Jump Gate destination rules
25. Artifact study and capture rules
26. Cargo loot gates
27. Corporation technology research and skill investment
28. Defense unit growth, cap investment, and daily XP limit

Public wiki rule: keep these as mechanics/reference material. Strategy pages may link to these rules, but the public rule pages should not drift into advice.

## 24. Quick Jump and Jump Gate Destination Rules

Useful source files:

- `IKOLEGFOADL.cs`
- `IGDDJEMDJEJ.cs`

### Quick Jump to defense units

`IKOLEGFOADL.CanQuickJump(ship, defense, out message)` validates the player action. It then delegates destination eligibility to `IGDDJEMDJEJ.CanQuickJump(player, out reason)`.

Stable behavior:

- The acting ship must pass the shared ship validator.
- The acting ship must be deployed, not in combat, not a Corp Defender, and not in Arena.
- The target defense unit must exist.
- The target defense unit must be deployed.
- The defense unit must pass its own quick-jump eligibility test.
- The acting ship cannot already be in the same sector or a neighboring sector.
- Quick Jump costs 1 player Tech Point.
- If the player has zero Tech Points, Quick Jump is blocked.

### Defense unit quick-jump eligibility

`IGDDJEMDJEJ.CanQuickJump(player, out reason)` decides whether a defense unit can be a Quick Jump target.

Stable behavior:

- The defense unit must be deployed and have valid map/sector context.
- Defense units in Arena context cannot be Quick Jump targets.
- Human-faction deployed defense units are valid Quick Jump targets.
- A defense unit owned by the player's corporation is valid.
- A defense unit in the player's alliance is valid.
- In some special map states, only Planets and Garrisons are valid targets.
- Outside those special states, non-human hostile defense units are blocked.
- For human territory, Planets are valid targets.
- Garrisons in human territory require a jump-gate destination.
- Human-territory Garrison Quick Jump can be blocked if the destination is outside valid human/jump-gate rules.
- The destination jump gate must have been explored by the player.

Public use:

- Movement/Starmap pages can now distinguish Quick Jump to defense units from direct Jump Gate use.
- The old wiki claim that Quick Jump can go to alliance defense units and discovered human jump gates is broadly supported, but the exact Planet/Garrison special cases should be documented carefully.

Needs confirmation:

- Public names for the special map flags that restrict Quick Jump targets to Planets/Garrisons.
- Whether "same or neighboring sector" is the right player-facing phrase for `IsNeighbor(...)`.
- Whether all human Planets are intended Quick Jump targets, or whether additional server validation exists.

### Direct Jump Gate use

`CanUseJumpGate(...)` was noted in Pass 7 and is repeated here for contrast.

Stable behavior:

- The ship must pass the shared ship validator.
- Battery must be at least 75% charged.
- The ship must not have remaining wait time from the summed movement/jump timer fields.
- The current sector must have a Jump Gate destination.

Public use:

- Direct Jump Gate use and Quick Jump should be separate subsections in a movement reference.

## 25. Artifact Study and Capture Rules

Useful source files:

- `IKOLEGFOADL.cs`
- `KHEBEGGPJKL.cs`

### Artifact object behavior

Observed artifact model behavior:

- Artifact display names are `Artifact: [artifact name]`.
- Artifacts can have a controlling corporation.
- When control changes, the artifact bonus is removed from the old corporation and added to the new corporation.
- `GetCorp()` returns the controlling corporation.
- Artifact size is Medium for non-major artifacts and Large for major artifacts.
- Artifact bonus technology is stored on the artifact object.

Public use:

- The Artifacts page can state that captured artifact bonuses are attached to the controlling corporation.
- Artifact size should be checked against public UI before publishing, because size may matter mostly for targeting/display internals.

### Studying artifacts

`CanStudyArtifact(...)` validates artifact study.

Stable behavior:

- The artifact must exist.
- The ship must be in the same sector as the artifact.
- The player cannot study the same artifact twice.
- If a corporation controls the artifact, outsiders cannot study it unless they are in the same alliance as the controlling corporation.
- The acting ship must pass the shared ship validator.
- Corp Defender ships are blocked by the shared validator.

Public use:

- The old embedded wiki text saying captured artifacts can only be studied by alliance members is supported by client validation.
- The permanent +1 skill point reward still needs confirmation from reward/application code, but the access gate is clear.

### Capturing artifacts

`CanCaptureArtifact(...)` validates the base capture action.

Stable behavior:

- The artifact must exist.
- The player must be in a corporation.
- A corporation cannot capture an artifact it already controls.
- An artifact controlled by another corporation cannot be captured directly; local defenses must be destroyed first.
- The acting ship must be in the same sector as the artifact.
- The acting ship must pass the shared ship validator.
- The acting ship cannot be in Arena.

### Capturing artifacts to a defense unit

`CanCaptureArtifactToDefense(...)` adds destination defense rules.

Stable behavior:

- The base artifact capture validator must pass first.
- The target defense unit must exist.
- Only defense-unit types that support artifact capture can be used.
- The target defense unit must be deployed.
- The target defense unit cannot already protect another artifact.
- Capturing an artifact costs a configured amount of corporation Tech Points.
- The corporation must have enough corporation Tech Points.
- Artifacts may only be captured to PvP systems.

Public use:

- The Artifacts and Structures pages should link to one canonical artifact capture rule section.
- The exact capture cost should come from configuration extraction before publishing a numeric value.

Needs confirmation:

- Which exact defense unit types support artifact capture. The client exposes this through a defense property rather than a direct enum list.
- Whether "protects another artifact" maps to a single protected artifact per defense unit in public wording.

## 26. Cargo Loot Gates

Useful source file:

- `IKOLEGFOADL.cs`

`CanLoot(...)` first validates targeted action, then dispatches by cargo type.

Observed cargo types:

- Cargo Money
- Cargo Item
- Cargo Resource

### Cargo Money

Stable behavior:

- Money cargo cannot be looted if the cargo amount is zero or below.

### Cargo Item

Stable behavior:

- Item cargo cannot be looted if it contains no item.
- Item cargo cannot be looted if the player's item bank is full.

### Cargo Resource

Stable behavior:

- Resource cargo cannot be looted if the cargo amount is zero or below.
- The acting ship's current amount of that resource is compared against the ship's resource capacity.
- If storage for that resource is already full, looting is blocked.

Public use:

- Cargo pages can document the three cargo target types and the common "empty cargo" / storage capacity gates.
- Resource cargo capacity is per resource type on the ship, not just a single generic cargo check.

Needs confirmation:

- Whether partial pickup occurs server-side when cargo amount exceeds remaining capacity. The client gate only blocks when already at capacity.

## 27. Corporation Technology Research and Skill Investment

Useful source file:

- `IKOLEGFOADL.cs`

### Corporation technology research

`CanResearchTechnology(...)` validates corporation research unlocks.

Stable behavior:

- The selected technology must be researchable by corporations.
- The acting player must be a corporation commander.
- Major technologies consume Major Research Points.
- Minor technologies consume Minor Research Points.
- Major Research Points are described by the client as `+1 Major Research Point every 30 Corporation Levels`.
- Minor Research Points are described by the client as `+1 Minor Research Point every 10 Corporation Levels`.
- Already-unlocked technology cannot be researched again.

Public use:

- Technology pages should distinguish researched corporation technology from artifact-granted technology and item technology.
- The major/minor research point cadence can be published once verified against current server behavior.

### Corporation and entity skill investment

`CanAddCorpSkill(...)` and `CanAddEntitySkill(...)` both use `ValidateAddSkill(...)`.

Stable behavior:

- Adding corporation skills requires corporation commander rank.
- Adding defense/entity skills requires permission to modify the entity, with commander rank required for defense entities.
- The target skill must be upgradeable.
- The skill tree must have available skill points.
- A skill cannot exceed its skill point cap.
- Hardcore units gain an additional +5 skill point cap according to the client message.
- Skills ignored by defense units cannot be increased on defense units.

Public use:

- Skills pages should avoid repeating investment cap logic everywhere. Link to a canonical skill investment section.

Needs confirmation:

- Exact skill point caps should come from the skill/tree data extraction.
- The hardcore +5 cap wording should be verified in UI/server behavior before being treated as complete.

## 28. Defense Unit Growth, Cap Investment, and Daily XP Limit

Useful source file:

- `IKOLEGFOADL.cs`

### Leveling defense units with resources

`CanLevelUpDefense(...)` validates resource transfers into defense unit XP.

Stable behavior:

- The selected resources are converted into defense XP with `resource.GetDefenseXp(amount)`.
- Computed XP is rounded with `(int)(0.5 + totalXp)`.
- The target defense unit must exist.
- The target defense unit must belong to the player's corporation.
- At least one resource must be selected.
- The player must have enough of each selected resource in their crafting/resource bank.
- Defense units have a configured maximum XP they can receive per day.
- If the transfer would exceed the daily cap, the client blocks it and shows time until reset.

Public use:

- Structures pages should describe defense leveling as resource-to-XP contribution, with daily cap.
- Exact resource-to-defense-XP formulas should be extracted from `GetDefenseXp(...)` before making a public table.

### Increasing corporation defense caps

`CanIncreaseCorpDefenseCap(...)` validates Tech Point investment into extra defense unit capacity.

Stable behavior:

- The player must be in a corporation.
- Investment must be at least 1 Tech Point.
- If using corporation bank Tech Points, the player must be Commander or Leader.
- If using corporation bank Tech Points, the corp bank must have enough Tech Points.
- If using personal Tech Points, the player must have enough Tech Points.
- Supported cap types are Garrison, Outpost, and Shipyard.
- Each supported cap type blocks investment once already at max.
- Planet is not a supported cap-increase target in this method.

Public use:

- Corporation Defense Structures can document Garrison/Outpost/Shipyard cap investment separately from initial/free defense units.

Needs confirmation:

- Exact max caps and Tech Point-to-cap conversion rules need a deeper pass.
- The reset time for daily defense XP should be aligned with existing daily reset documentation.

## Public Page Candidates

Potential public updates from this pass:

- `Movement.md` or `The-Starmap.md`: Quick Jump versus Jump Gate rules.
- `Artifacts.md`: study, capture, control, and corporation bonus rules.
- `Cargo.md` or loot/economy page: cargo money/item/resource loot gates.
- `Technology.md`: corporation research, major/minor research points, artifact-granted technology distinction.
- `Skills.md`: skill investment cap and defense-unit ignored skills.
- `Structures.md`: defense leveling, daily XP cap, and defense cap investment.

## Needs Confirmation List

- Public names for special map flags affecting Quick Jump.
- Whether Quick Jump neighbor checks should be described as same/adjacent sectors.
- Artifact capture cost from configuration extraction.
- Exact defense unit types eligible to hold/protect artifacts.
- Whether artifact study always grants +1 skill point in current server behavior.
- Partial pickup behavior for resource cargo.
- Exact skill point caps from skill tree data.
- Resource-to-defense-XP formulas.
- Defense cap maximums and Tech Point conversion rules.
- Daily defense XP reset timing.
