# Design

## Context

See [proposal.md](proposal.md) for motivation and the
[roadmap contract](specs/harmonization-roadmap/spec.md) for requirements.
This is a programme design, not the detailed implementation design for every
future mechanic. Its outputs are a bounded set of candidate child changes and
the evidence required to advance them.

### Inspection baseline and evidence vocabulary

- Repository revision: `b6ea614c130ff112d96d66094e61d17739eef7bb`. Mod source is
  inherited from the preserved baseline documented in `repo/Provenance.md`.
- Inspection date: 2026-10-23.
- Local game: `1.7.4985 rev1269`, identified by the installed `Version.txt`.
- Local .NET SDK: `10.0.113`, an inspection observation rather than a tooling
  constraint. The current source project targets `net10.0` but explicitly caps
  the language at C# 10; neither inherited setting determines the new toolchain.
- Native `Assembly-CSharp.dll` SHA-256:
  `0be7a7ea4b3111d4430f45b36c234a5e43287880b0514b23915f2ef9a0629e16`.
- The game was found at the conventional Linux Steam installation path. Its
  references exist locally even though the project's configured relative paths
  do not resolve. This observation is not a portable build configuration.

Use these evidence classifications throughout the programme:

- **Confirmed:** a user decision, including the clean break and harmonization.
- **Observed-source:** inspected repository code or definitions, not necessarily
  code verified active in a running build.
- **Observed-native:** installed game definitions or assembly metadata. A method
  or field exists; its suitability for a proposed extension is not yet proven.
- **Documented-official:** published Ludeon or Microsoft documentation/release
  information, with source and access date; not a local build or runtime result.
- **Proposed:** a recommended disposition, boundary, or child scope.
- **Unverified-runtime:** behavior requiring a future authorized experiment or
  acceptance run. No runtime gate below is currently passed.

No restore, build, game launch, prototype, or gameplay/persistence test was run.
Source counts include obsolete and excluded files; textual Harmony-annotation
counts also include commented historical patches and are not active patch counts.

### Official toolchain evidence

The following sources were checked on 2026-10-23. Published compatibility and
release information is separate from the local inspection baseline above.

| ID | Official source | Documented finding |
| --- | --- | --- |
| D1 | [Ludeon: Modder Primer for 1.7](https://docs.google.com/document/d/e/2PACX-1vSykw5_DYaaw42nEznI9zmBZVT_Vgg2bxYq_v2XWvAsHC3QSKFuDK2OyiQ5WC9jvVRUcrjpFt7xLLF5/pub), especially “Compiling against Waylith” | Waylith uses .NET 10; mods should target `net10.0`. The primary references are `Assembly-CSharp.dll`, `Waylith.dll` and `UnityStubs.dll`, with `RimWorld.dll` where needed. |
| D2 | [Ludeon: Announcing the Waylith Engine and Update 1.7](https://ludeon.com/blog/2026/10/announcing-the-waylith-engine-and-update-1-7/), published 2026-10-12 | The 1.7 update moves the game to Waylith and explicitly permits modern C# language features. Its legacy-mod compatibility goals do not impose a compatibility commitment on this variant. |
| D3 | [Microsoft: .NET release index](https://dotnetcli.blob.core.windows.net/dotnet/release-metadata/releases-index.json) | The newest stable SDK listed is `10.0.402`, released 2026-10-13. .NET 11 is still prerelease; these SDK/runtime release entries do not identify the runtime patch bundled with the installed game. |
| D4 | [Microsoft: C# language versioning](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/language-versioning) and [SDK/runtime version selection](https://learn.microsoft.com/en-us/dotnet/core/versions/selection) | `net10.0` defaults to C# 14. Newer SDK tooling can target an earlier runtime; a newer SDK does not itself authorize a newer runtime target or an unsupported language/TFM combination. |

### Repository evidence anchors

Paths below are relative to the repository root; line anchors refer to the
inspection revision and will drift during implementation.

| ID | Evidence | Significance |
| --- | --- | --- |
| E1 | `Source/1.7/SpaceShipCache.cs:29`, `Source/1.7/Comp/CompShipCachePart.cs:122` | SOS2 maintains its own membership, structural registration, mass and equipment collections. |
| E2 | `Source/1.7/CompShipEngineBreakdownable.cs:118` and `:178` | Existing guards detach SOS2 parts on native substructure and prevent engines serving two ownership systems. |
| E3 | `Source/1.7/HarmonyCustomPatches.cs:25` | Native gravship targeting is patched to reject combat maps; the patch also depends on compiler-generated delegate names. |
| E4 | `Source/1.7/Comp/ShipGameComp.cs:25`, `Source/1.7/AccessExtensions.cs:15`, `Source/1.7/HarmonyPatches.cs:852` | Private space classification and a biome override underpin many unrelated behaviors. |
| E5 | `1.7/Defs/BiomeDefs/Biomes_Space.xml`, `1.7/Defs/TerrainDefs/Terrain_Space.xml`, `1.7/Defs/MapGeneration/SpaceMapGenerator.xml` | SOS2 defines its own space biome, terrain and map generation. |
| E6 | `Source/1.7/ShipInteriorMod2.cs:709`, `Source/1.7/WorldObject/WorldObjectOrbitingShip.cs:62`, `Source/1.7/WorldObject/WorldObject_FastTileGetter.cs:18` | Native orbit tiles are already reused, but custom coordinates/display positions remain and are translated back into tiles. |
| E7 | `Source/1.7/HarmonyPatches.cs:876`, `Source/1.7/Comp/ShipMapComp.cs:875`, `Source/1.7/Building/Building_ShipVent.cs` | Legacy temperature/exposure and life-support rules coexist with Odyssey integration. |
| E8 | `Source/1.7/Comp/ShipMapComp.cs:312` and `:1012`, `Source/1.7/Projectile/ShipCombatProjectile.cs`, `Source/1.7/Building/Building_ShipTurret.cs` | Combat is coordinated through map state, origin/target maps, abstract travel and incoming projectiles; persistence spans multiple systems. |
| E9 | `Source/1.7/ShipHeatNet.cs`, `Source/1.7/Comp/CompShipHeat*.cs`, `Source/1.7/Building/Building_ShipBridge.cs`, `Source/1.7/AccuracyCalculator.cs` | Combat engineering, controls and crew effects are coupled to existing networks/caches; they are candidates for adaptation, not drop-in modules. |
| E10 | `Source/1.7/ShipInteriorMod2.cs:44`, `Source/1.7/Vehicles/`, `Source/1.7/Comp/ShipMapComp.cs`, `Source/1.7/Comp/CompShipBaySalvage.cs` | Vehicle Framework is required by the inherited runtime and participates beyond transport alone. Removal is not just deleting a dependency declaration. |
| E11 | `Source/1.7/RimworldMod.csproj:31` | `CompGravshipConversion.cs` is excluded; its name is not evidence of an existing working converter. |
| E12 | `Source/1.7/Comp/CompShipScanner.cs`, `1.7/Defs/QuestScriptDefs/`, `1.7/Defs/ResearchProjectDefs/`, `1.7/Defs/Scenarios/` | Discovery, quests, research, starts and endgames require a content-level disposition as well as a code port. |
| E13 | `LoadFolders.xml`, `About/About.xml`, root `Textures/` and `Sounds/` | Version removal must distinguish old code from shared assets and metadata. No automated test projects or CI build configuration were found in the survey. |

### Native evidence anchors

These are summaries and qualified symbol references, not copies of game code.
Native definition paths are relative to the installed game's `Data/Odyssey/Defs/`.

| ID | Observed native evidence | What remains unverified |
| --- | --- | --- |
| N1 | `RimWorld.Building_GravEngine` exposes connected/valid substructure, facilities, fuel and launch checks; `RimWorld.GravshipUtility` exposes generation, travel, arrival and fuel-cost operations. | Additional-state retention, invalidation, cancellation and engine-loss behavior under extension load. |
| N2 | `RimWorld.Planet.Gravship` contains the engine, things, pawns, foundations, roofs, areas and room temperature/vacuum data and exposes serialization. | Exact lifecycle/identity association and what extension state survives each supported transition. |
| N3 | `Verse.VacuumComponent` and `Verse.VacuumUtility`; `BiomeDefs/Space.xml` supplies native `Space`/`Orbit` biomes; `MapGeneration/SpaceMapGenerator.xml` supplies native space-map foundations. | Behavior of new equipment and encounters, especially breaches and transitions. Native `Space` and `Orbit` are variants of the same framework, not duplicate mod-owned space systems. |
| N4 | `RimWorld.CompGravshipShieldGenerator` uses `RimWorld.CompProjectileInterceptor`; `ThingDefs_Buildings/Buildings_Gravship.xml` defines charging, activation, power and facility behavior. | Interception of candidate ship weapons and any required sustained-shield or heat extension. |
| N5 | `RimWorld.CompOrbitalScanner` and `RimWorld.Planet.OrbitalScannerWorldComponent`; `QuestScriptDefs/Script_SpaceSites.xml` uses orbital-scanner quest tags and selection weights. | Suitability for selected SOS2 encounters, progression pacing and threat selection. |
| N6 | `ThingDefs_Buildings/Buildings_Misc.xml` and `WorldObjectDefs/WorldObjects.xml` define passenger-shuttle transporter, launchable, fuel and orbital-travel components. | Boarding/interception and armed strikecraft; transport existence does not prove carrier missions. |
| N7 | `TerrainDefs/Terrain_Foundation.xml` defines substructure as foundation terrain; `Verse.TerrainGrid` exposes foundation removal/destruction operations and `Verse.TerrainDef` exposes bomb-damage destruction fields. | Holes, detached sections, repair and salvage behavior equivalent to the desired gameplay; destructible SOS2 plating is not automatically equivalent. |
| N8 | `ThingDefs_Buildings/Buildings_Gravship.xml` supplies support stat offsets and facility limits; `Verse.WorldComponent_GravshipController` holds transition/cutscene state. | Demonstrated vessel scale, multiple engines/craft, concurrent travel and performance. Metadata does not establish either full fleet support or impossibility. |

## Goals / Non-Goals

**Goals:**

- Make the next child proposal possible without rediscovering the programme's
  intent, major coupling, evidence quality or predecessor gates.
- Keep a single native authority for shared concepts while permitting narrowly
  defined additional mechanics and derived caches.
- Reduce uncertainty before content expansion through a minimal, complete
  journey/combat slice and explicit destructive/failure scenarios.
- Let independent later capabilities proceed without waiting for an entire
  catalogue or an unnecessary all-features combat rewrite.

**Non-Goals:**

- Implementing the new runtime, changing build/loading configuration, deleting
  old versions, creating child changes, or executing runtime experiments here.
- Reproducing every upstream feature, formula, def name, API or UI. The ledger
  records candidate retention, not a blanket feature-parity commitment.
- Supporting old saves, old game versions, upstream coexistence, or inherited
  mod compatibility. Existing dependencies are not grandfathered in.
- Promising support for future game builds without revalidation, requiring the
  inherited SOS2 runtime to build before native-first work can start, or asserting
  native behavior based solely on metadata.
- Selecting combat topology, production package identifiers, arbitrary scale
  limits, or every late-game feature before their child decision points.

## Decisions

### 1. Separate the parent planning contract from runtime delivery

`harmonization-roadmap` is a programme-level planning/review capability. It owns
the stable authority principles, evidence standards, stage readiness and mechanic
disposition contract. Runtime features receive their own bounded capabilities
and child proposals when ready; this spec does not claim they are implemented.

Applying this parent means reviewing and finalizing its four artifacts only.
There is no automatic continuation into prototypes or gameplay changes.

**Alternative rejected:** one umbrella change with tasks to rewrite every
subsystem. That would turn unresolved feasibility into premature implementation
commitments and make partial completion difficult to assess.

### 2. Build a minimal native-first runtime and selectively reuse mechanics

Use the native game plus Odyssey as the behavioral baseline. A future lifecycle
investigation can introduce its own explicitly scoped minimal probe/test host;
it does not require the final production package or a functioning legacy runtime.
The package stage then promotes only demonstrated foundations into the supported
runtime. Inherited code stays reference material until deliberately adapted.

| Concept | Intended authority | Permitted extension boundary |
| --- | --- | --- |
| Ship structure and membership | Native grav engine/substructure lifecycle | Derived views of equipment and additional capabilities; no independent owning graph. |
| Travel and shared resources | Native launch/transit/landing, fuel, power and inventory mechanisms | Explicit costs/capabilities on those resources; no duplicate fuel or movement loop. |
| Location and space environment | Native layers, tiles, space maps and room/vacuum behavior | New native-world sites, content, equipment and environmental effects with bounded interactions. |
| Defenses and discovery | Native interception and orbital-scanner foundations where suitable | Changed parameters or additional mechanics justified against the native options. |
| Tactical encounters | New extension where native behavior is insufficient | Native vessels as participants; encounter range is not an alternative world position or travel authority. |
| Specialized engineering | Native foundations plus explicitly distinct new mechanics | Weapon waste heat, for example, is distinct from room temperature if selected and specified. |
| Wrecks and capture | Native-compatible damaged structure, contents and ownership | Recovery/salvage capabilities without falling back to old ship identity. |

A conceptual vessel need not be represented by one permanently instantiated
object during every native state. The lifecycle gate must establish how to
associate extension state with native ownership across landed and in-flight
representations. Do not assume a native stable-ID or attachment hook exists.

**Alternatives rejected:** maintaining two runtime modes, simply treating SOS2
plating as native substructure, broadening `IsSpace()` before reconciling its
callers, or preserving existing code boundaries at the expense of native ownership.
These retain the conflicting assumptions demonstrated by E1-E8.

#### Select modern tooling independently of inherited constraints

Select tooling from documented RimWorld compatibility, not the versions already
installed locally, upstream build conventions, legacy framework support, or
inherited dependencies. The proposed build baseline is .NET SDK `10.0.402`,
targeting `net10.0` with C# 14 (D1-D4). This uses the newest stable SDK identified
at review time without retaining the inherited C# 10 cap. Local SDK `10.0.113`
remains historical inspection evidence only.

Keep three decisions distinct: SDK/compiler version, target framework/language
version, and the runtime supplied by the selected game build. Using this SDK
does not require replacing or upgrading the game's bundled runtime. Do not infer
its runtime patch version from Microsoft's latest release. Current official
RimWorld documentation establishes `net10.0`, not `net11.0`; .NET 11 prerelease
tooling is not selected for this baseline.

S00 rechecks official game documentation, update notes and SDK releases, records
the newest stable compatible SDK it selects, and defines a reproducible SDK pin
and update policy for its authorized implementation. Later stable SDKs may be
evaluated while retaining `net10.0` and its supported language version. Prefer
the TFM-supported default or an explicit C# 14 setting over an unbounded
`LangVersion=latest`. Verify game references and any justified dependencies
against the selected native build; an inherited dependency's tooling restriction
is a reason to reassess that dependency, not an automatic programme ceiling.

This parent changes no SDK installation or build configuration. Documentation
alone passes neither a build nor a runtime gate; the selected toolchain and
native reference combination still require evidence under G0 and later gates.

**Alternatives rejected:** freezing the toolchain at the locally installed SDK,
preserving upstream's C# 10 cap for its own sake, or treating the newest SDK as
permission to target a runtime/language combination unsupported by RimWorld 1.7.

### 3. Track mechanic dispositions explicitly

The following is a roadmap-level survey, not an exhaustive per-definition audit.
Dispositions marked **proposed** need confirmation in the owning child scope.
Any unlisted definition encountered during detailed work must be added to that
child's inventory rather than treated as implicitly ported or deleted.

| Mechanic family | Disposition and rationale | Evidence | Child / gate |
| --- | --- | --- | --- |
| Vessel ownership and contents | **Extend native:** attach additional state; retire the legacy owning cache. Confirmed direction. | E1-E2, N1-N2 | S01-S02 / G1 |
| Launch, transit, landing, fuel | **Extend native:** one journey/resource lifecycle. Confirmed direction. | E6-E8, N1-N2 | S01-S03 / G1 |
| Orbital locations, map generation, space rendering | **Extend native:** native world/map semantics; retire private space identity and coordinates. Confirmed direction. | E4-E6, N3 | S03 / G1 |
| Airtightness, oxygen, exposure and suits | **Extend native:** retire competing survival authority; adapt selected equipment. Confirmed direction. | E7, N3 | S03 / G2 |
| Hull variants, holes, detached sections and hullfoam | **Deferred decision:** native foundation damage differs from building plating; specify desired damage/repair outcome before porting. | E1-E2, E5, N7 | S01, S08 / G2 |
| Power generation, storage and specialized reactors | **Adapt SOS2 (proposed):** retained equipment participates in native power; exact catalogue and hazards are not approved. | E9, `1.7/Defs/ThingDefs_Buildings/Buildings_Ship*.xml` | S06 |
| Waste heat, cooling, purging and overdrive | **Deferred decision:** potentially distinct engineering gameplay, not a second room-temperature simulation. | E9 | S06 / G3 |
| Ship shields | **Extend native (proposed):** compare activation, sustained operation and weapon interactions before retaining old heat/shield code. | E9, N4 | S04-S06 / G3 |
| Guns, torpedoes, spinal weapons and point defense | **Adapt SOS2 (proposed):** rework around the selected encounter contract and native damage/interception; no historic balance commitment. | E8-E9 | S04-S06 / G3 |
| Pursuit, escape, combat agility, RCS and piloting | **New extension (proposed):** derive needed tactical properties from real vessel equipment/resources; travel range and tactical agility are distinct concepts. | E1, E9, N1 | S04-S06 / G3-G4 |
| Encounter coordination and enemy AI | **New extension (proposed):** native participants, coherent native-world entry/exit, bounded combat state. | E3, E8 | S04-S05 / G3 |
| Basic cargo/passenger transport and bays | **Extend native (proposed):** evaluate native shuttles before any external vehicle dependency. | E10, N6 | S03, S07 / G5 |
| Boarding, capture and prisoners | **Adapt SOS2 (proposed):** reuse intent/AI where suitable, not the inherited vehicle mission container by default. | E8, E10, N6 | S07 / G3-G5 |
| Armed shuttles, fighters and carrier missions | **Deferred decision:** transport is not proof of strikecraft or interception support. | E10, N6 | S07 / G5 |
| Docking, moving wreck sections and salvage beams | **Deferred decision:** resolve native-compatible boundaries for disconnected structure and contents before porting movement tools. | E1, E10, N7 | S08 / G2-G3 |
| Sensors, discovery, orbital sites and derelicts | **Extend native (proposed):** feed selected content into native scanner/quest patterns rather than a parallel discovery authority. | E12, N5 | S09 |
| Traders, navies, fleets, threat selection and notoriety | **Adapt SOS2 (proposed):** integrate selected content and pacing into native-world encounters; fleets require demonstrated limits. | E8, E12, N8 | S06, S09 / G3-G4 |
| Research, recipes, rewards, starts and ship catalogues | **Adapt SOS2 (proposed):** redesign progression around Odyssey access and demonstrated vessel sizes; no wholesale blueprint/catalogue import. | E12-E13 | S09 / G4 where scale-dependent |
| Cloaking, AI cores, formgels, archotech and endgames | **Deferred decision:** justify each capability and any non-Odyssey DLC requirement separately; preserve experiences only when selected. | E9, E12 | S10 |
| Old version loaders, save shims, legacy APIs and compatibility patches | **Retire:** no compatibility constraints justify their presence in the new supported path. Confirmed direction. | E10-E13 | S02 and each replacement stage |
| Controls, settings, translations and diagnostics | **New extension (proposed):** expose the unified model and only supported features; reuse suitable assets/text with attribution. | E9, E12-E13 | Each owning child |

Harmony/publicizer use must be justified by required hooks; neither is forbidden
nor automatically required. Vehicle Framework is not a default dependency. Other
official DLCs are not silently made mandatory because an inherited late-game
feature references them. No requirement to preserve third-party compatibility
means no compatibility budget, not a promise that other mods will work or fail.

### 4. Use explicit feasibility gates

Only G0's static availability observations are established. All runtime evidence
below is outstanding. A future child must record the build/profile, exact
scenario, outcome, relevant diagnostics, and pass or stop/revise decision.
Metadata existence, a successful compile, or a happy-path video alone is not a
substitute for the gate's failure/persistence checks.

| Gate | Required investigation and evidence | Pass / stop boundary |
| --- | --- | --- |
| G0: baseline and isolation | Record the native build/assembly identity and bundled runtime identity; recheck official compatibility/release sources, select and reproducibly pin the newest stable compatible SDK, record TFM/language choices separately, and verify usable native references and a minimal test profile. Establish a reproducible native baseline without modifying the installed game or default mod profile. | Enter runtime investigations only with an identified baseline, evidenced toolchain/reference combination and isolated execution path. Installed tools and inherited settings are not ceilings; documentation alone is not a passed build/runtime check. Do not require legacy SOS2 to compile first. |
| G1: lifecycle and ownership | Probe native membership, equipment attachment/invalidation, launch, supported save/load points, arrival/rotation, cancellation/failure, and repeat travel with tracked pawns/items/resources and extension state. | Pass only with one authority and no duplication/loss. Otherwise revise the association/hook or reduce scope; do not restore legacy movement. |
| G2: structural loss and environment | Probe foundation destruction, breaches and repair, disconnected components, engine destruction, map retention/removal, stranded pawns and recoverable remains. | Pass with native-consistent ownership, environment and recovery semantics. Defer unsupported salvage operations rather than invent a second owning graph. |
| G3: combat arrangement | Compare linked native-space maps with a shared encounter map. Evaluate targeting, incoming damage, native shields, room breaches, retreat/travel locks, capture/map cleanup and save/load. Demonstrate the selected minimal approach. | Pass only when participants and effects remain native-world coherent. Stop dependent weapon/boarding/salvage commitments if neither approach meets the invariants. |
| G4: scale and concurrency | Investigate support/footprint/facility limits, multiple engines/craft and the world controller's transitions. Measure chosen small and proposed large/fleet cases, recording cell/thing counts, map count and tick/transition costs. | Establish measured targets and an explicit supported envelope before committing large-vessel or fleet content. Do not assume default limits are hard limits or that metadata proves concurrency. |
| G5: transport and strikecraft | Demonstrate native orbital passenger/cargo transfer and define boarding/interception needs separately. Evaluate whether bounded native extensions suffice for selected armed missions before proposing another dependency. | Basic transport does not pass armed-carrier acceptance. Explicitly scope out unsupported missions or propose a justified child solution. |

G3's topology and G2/G4/G5 outcomes are deliberately scoped investigation outputs
of future children, not unresolved implementation choices inside this parent.
Their outcome can change future child designs; it cannot silently change this
parent's authority rules. A failed invariant requires an explicit programme
revision, not an undocumented fallback.

### 5. Deliver bounded child changes in dependency order

Stage IDs are roadmap references, not existing OpenSpec changes. Suggested slugs
are candidates only. Before scaffolding any child, obtain its requested scope;
use the CLI and preserve the fork's `sanicek-feat/<description>` convention for
any later implementation branch. Preparing a candidate is not starting it.

| Stage / candidate change | Prerequisites | Bounded scope and capabilities | Exit evidence and exclusions |
| --- | --- | --- | --- |
| S00 `establish-native-baseline` | Parent reviewed | Reproducibility/isolation contract; refresh D1-D4 and select the newest stable compatible SDK with a reproducible pin/update policy, separate runtime/TFM/language records and verified game references. Include exact native hook assessment, active-vs-reference code and shared-asset inventory, dependency/DLC decisions and validation approach; close G0. | Identified baseline, evidenced toolchain/reference combination and isolated native test path, specific probe scenarios and unresolved evidence recorded. No inherited SDK/language ceiling, generic rediscovery task, full legacy build requirement, or broad code port. |
| S01 `prove-native-vessel-lifecycle` | S00 / G0 | An explicitly scoped minimal probe host for G1 and the foundational G2 cases: ownership, transfer/state association, structural invalidation, engine loss and environment consequences. | Repeatable success/failure/save-load evidence; native association and destruction contracts chosen. No production combat, catalogue port, or parallel runtime mode. Probe code requires its own implementation request. |
| S02 `establish-odyssey-native-runtime` | S01 / foundational G1-G2 pass | Promote proven foundations into a distinct 1.7/Odyssey package, minimal build/dependency graph, loading and metadata. Keep shared licensed assets actually needed by the new path. | Clean build and fresh-campaign smoke test with old-version loaders and legacy owning/travel paths absent from the supported runtime. Do not import obsolete folders by default. Exact package identifiers/layout are chosen here. |
| S03 `unify-native-space-environment` | S02 | Native orbital/site generation and travel, oxygen/exposure and selected equipment; remove old space predicates/biome/temperature authority from the supported path. Verify ordinary native transport access. | Fresh ground/orbit/ground loop, breach/repressurization, equipment and map-persistence scenarios. No SOS2-only alternate orbit/environment. Basic transport is not armed-carrier support. |
| S04 `prove-native-ship-combat` | S03 / foundational G2 | Resolve G3 with one player and one hostile native craft. Specify encounter entry/exit, topology, projectile/damage/interception boundary, tactical resource rules and persistence. | Reproducible minimal exchange, retreat/resolution and supported save/load under the selected contract. No fleet AI, complete weapons catalogue or implicit old topology decision. |
| S05 `deliver-first-native-combat-loop` | S04 / G3 pass | Turn the selected proof into a repeatable playable loop with one basic weapon, native-based defense and minimal controls/feedback. | Native travel -> encounter -> actual damage/resource use -> resolution -> continued operation, with fresh-save and failure cases. No requirement for waste heat, all weapon classes or late-game content. |
| S06 `extend-native-ship-engineering` | S05; G4 for scale-dependent features | Split selected weapons, PD, thermal engineering, shield changes, crew roles and agility into focused children. Decide additional concepts before adapting old networks. | Each selected system has native-compatible resource/damage ownership, invalidation, diagnostics and measurable acceptance. Preserve neither old formulas nor incompatible network boundaries merely for parity. |
| S07 `extend-native-boarding-transport` | S05 / G3; G5 for selected missions | Native-based cargo/passenger/boarding/capture behavior. Propose armed missions and any dependency only after their separate feasibility decision. | Contents, faction changes, interception and return/recovery verified through supported transitions and save/load. No automatic Vehicle Framework retention or promise of every carrier role. |
| S08 `extend-native-wrecks-salvage` | S05 / G2-G3 | Selected recovery, repair, salvage and docking operations on native-consistent wrecks/structure; extend G2 for each advanced operation. | Engine-loss/stranding and partial-structure cases preserve contents and environmental consequences without legacy movement. Unsupported operations remain explicitly deferred. |
| S09 `integrate-native-space-progression` | S03 for discovery; S05 for combat encounters; G4 for scale-dependent catalogues | Native-scanner quests, selected sites/derelicts, faction encounters, research/economy, rewards and starts. Content adaptation uses the demonstrated vessel envelope. | A reachable progression path and encounters that enter/exit the same world model. Discovery planning can proceed early; hostile or oversized content cannot bypass its runtime gates. |
| S10 `extend-native-advanced-progression` | S09 plus specifically selected earlier capabilities/gates | Separate proposals for chosen cloaking, archotech, AI/formgel and endgame experiences. Interstellar extensions must justify behavior beyond native planetary travel. | Each selected experience has declared DLC/dependency scope, progression and fresh-save acceptance. No blanket endgame parity or new private space framework. |

The principal execution graph is:

```text
S00 --> S01 --> S02 --> S03 --> S04 --> S05
                                      |
                 +--------------------+-------------------+
                 |              |              |          |
                 v              v              v          v
                S06            S07            S08        S09
                 |              |              |          |
                 +--------------+--------------+----------+
                                      |
                                      v
                                     S10
```

The table is authoritative for prerequisites: S06-S09 are not a mandatory serial
chain, and S10 depends only on the earlier capabilities its selected features
actually need. Per-definition inventory, attribution review, content research and
acceptance design can proceed in parallel without claiming their runtime gates
passed. UI, translations, testing, licensing and superseded-code removal are
part of each owning stage, not a final cleanup-only milestone.

### 6. Define child readiness and acceptance, including negative checks

Every child proposal must provide:

1. Player/developer outcome, explicit exclusions and selected mechanic rows.
2. Evidence references and build baseline; facts separated from assumptions and
   published documentation separated from tested outcomes. Record the selected
   SDK/pin, TFM, supported language version, game-supplied runtime and native
   reference identity, carrying forward S00's baseline or explicitly justifying
   and validating an update from official compatibility/release evidence.
3. Native authority and additional-state boundary; planned retirement of any
   overlapping old behavior on its supported path.
4. Prerequisite stages/gates, their evidence status, and a concrete stop/revise
   outcome for each still-blocking experiment.
5. Native integration seams, assets/definitions affected, dependency/DLC decisions
   and any benchmark envelope. Implementation details belong to that child's
   design, not speculative runtime specs in this parent.
6. Acceptance scenarios for success, denial/failure, destruction, supported
   transition/save-load points, resource/content conservation and relevant scale.
7. Both positive behavior and negative checks for duplicate structural ownership,
   fuel consumption, alternative location/exposure authority and active legacy
   patches. Source files left as reference are not themselves duplicate runtime
   behavior; the supported execution path is what must be demonstrated.
8. Attribution/provenance and applicable notice review; no copied game assemblies,
   publicized outputs, decompiled implementation dumps or official assets in the
   repository. Local API summaries and version/hash references suffice.

Use layered validation: pure-logic tests for extracted algorithms where useful,
definition/reference validation, an isolated minimal game profile, repeatable
developer-mode scenarios and measured stress cases. No existing automated suite
or headless-game testing capability is assumed. Completing this parent validates
the plan, not any of those future runtime scenarios.

## Risks / Trade-offs

- **Native API surfaces are not demonstrated extension behavior** -> Keep gates
  unpassed until their named scenarios run against the recorded build.
- **A native-first reconstruction loses convenient legacy shortcuts** -> Reuse
  selected algorithms/content behind the chosen native boundaries; accept a
  smaller coherent slice before restoring breadth.
- **Substructure is not destructible plating** -> Resolve G2 before committing
  to hullfoam, detachable sections or salvage tools; use native destruction and
  invalidation rather than retaining a hidden owning cache.
- **Combat topology can reshape several downstream features** -> Resolve it in
  S04; do not pre-author topology-dependent implementation tasks here.
- **Native controller/facility constraints may limit large or multiple craft** ->
  Measure G4 and declare an envelope; extend native mechanisms or reduce scope
  explicitly, never infer impossibility or unlimited scale from metadata alone.
- **The old catalogue may dominate porting effort or alter progression** -> Use
  the disposition ledger and native progression baseline; require selected
  content, not the historical catalogue, for each milestone.
- **Removing a vehicle dependency can affect combat and map cleanup as well as
  shuttles** -> Audit E10 and isolate G5; do not treat a native shuttle definition
  as a complete replacement for strikecraft and carrier missions.
- **Shared assets and credits can be lost during version pruning** -> Inventory
  references and preserve the obligations in `repo/` before removing duplicates;
  the archived README and its marked root section remain unchanged.
- **A planning parent could be mistaken for permission to rewrite everything** ->
  Its tasks are planning/review only; each child needs a bounded proposal and an
  explicit implementation request. No commits, pushes or upstream contacts are
  implied by planning completion.

## Migration Plan

This parent deploys no game change and migrates no saves. Its artifacts remain
within its CLI-created OpenSpec change until separately reviewed and archived;
main specs are not edited by this proposal.

Future adoption is a new package/test profile and fresh campaign, not an upgrade
path for an existing SOS2 campaign. Production identity, layout and exact required
dependencies are selected in S02 from the demonstrated foundation. Isolated S01
probe work avoids a circular prerequisite on that final package. Existing native
game files and the user's default mod profile must not be modified by probes.

Before later runtime experiments, record code revisions and back up disposable
test saves. Recover a failed experiment using its known code/profile/save state,
not compatibility shims or destructive Git operations on unrelated work. No
long-term save migration guarantee is inferred for new variant versions; within
each supported baseline, its declared fresh-save persistence must still work.

Parent review completion means its evidence, ledger, gates and stage boundaries
are coherent and validated. The next recommended scope is S00, followed by the
separately authorized S01 lifecycle investigation. Neither is scaffolded or
implemented by this change.
