# Spec Delta

## Purpose

Provide an evidence-backed, stage-gated delivery contract for a clean-break
RimWorld 1.7/Odyssey-native SOS2 variant. The roadmap guides separately scoped
feature changes without declaring unimplemented gameplay capabilities complete.

## ADDED Requirements

### Requirement: Clean-break target boundary

The roadmap SHALL target fresh campaigns on a documented RimWorld 1.7 baseline
with Odyssey. Legacy saves, older game versions, inherited extension APIs,
historical balance, and existing third-party integrations SHALL NOT impose
compatibility requirements on the new variant.

#### Scenario: Legacy compatibility would preserve a competing system
- **WHEN** a candidate stage would retain an old ship or space implementation
  solely to support an existing save, version, or integration
- **THEN** the roadmap excludes that compatibility work rather than weakening
  the harmonization contract

#### Scenario: The game baseline changes
- **WHEN** a later child change selects a different supported 1.7 build
- **THEN** it records that baseline and rechecks affected evidence without
  promising simultaneous support for prior builds

### Requirement: Toolchain selection follows official compatibility evidence

The roadmap SHALL require S00 to select the newest stable compatible SDK using
official RimWorld and Microsoft documentation and release evidence, and record
a reproducible SDK pin and update policy. SDK, target framework, supported
language version, and game-supplied runtime SHALL be recorded separately.
Installed tooling and inherited upstream settings SHALL NOT impose automatic
version ceilings.

#### Scenario: Local or inherited tooling is older
- **WHEN** official evidence supports newer stable tooling than the installed
  SDK or inherited upstream settings
- **THEN** the roadmap selects from documented compatibility rather than retaining
  the older toolchain solely because it is installed or inherited

#### Scenario: A newer SDK is evaluated
- **WHEN** S00 or a later child considers a newer stable SDK
- **THEN** it rechecks official compatibility and release evidence and records
  the SDK pin separately from the runtime target and supported language version,
  without assuming that newer build tooling authorizes a newer game runtime

#### Scenario: A child uses the established toolchain baseline
- **WHEN** a runtime child records its build baseline
- **THEN** it carries forward S00's SDK pin, target framework, supported language
  version, game runtime and native reference identity, or explicitly justifies
  and validates an update against official compatibility and release evidence

### Requirement: One authoritative vessel lifecycle

The roadmap SHALL designate the native gravship model as the authority for
vessel structure, membership, shared resources, and travel. Extension state and derived
caches SHALL NOT independently decide ownership or create a competing travel
lifecycle. Player and hostile craft SHALL follow the same authority principle.

#### Scenario: A vessel changes map or travel state
- **WHEN** a proposed extension follows a vessel through native travel
- **THEN** its state remains associated with the native vessel lifecycle without
  introducing a separately authoritative copy of the craft or its contents

#### Scenario: Structure is damaged or the engine is lost
- **WHEN** a proposed feature handles disconnected sections or engine destruction
- **THEN** it specifies native-compatible invalidation and wreck behavior rather
  than restoring the legacy ship ownership model

### Requirement: One space and environmental framework

The roadmap SHALL use native locations, orbital layers, space terrain, and
environmental rules for shared concepts. New sites and encounters SHALL inhabit
that framework without private orbital coordinates, competing space identity,
or an independent determination of room breathability and pawn exposure.

#### Scenario: An encounter uses another map
- **WHEN** a combat design uses multiple maps for an encounter
- **THEN** those maps share native location, travel, and environmental semantics
  rather than creating a second version of space

#### Scenario: A ship room is breached
- **WHEN** acceptance scenarios assess oxygen, airtightness, or vacuum harm
- **THEN** they assess the native environmental outcome and reject conflicting
  legacy survival calculations

### Requirement: Native reuse before additional systems

Each proposed mechanic SHALL first be compared with native capabilities.
Departures SHALL identify a genuine missing capability or an explicit extension
of existing behavior. A new mechanic representing a distinct concept SHALL NOT
silently replace or duplicate a native authority for a shared concept.

#### Scenario: Existing native equipment overlaps a mechanic
- **WHEN** shielding, discovery, transport, or another mechanic already has a
  native foundation
- **THEN** its disposition explains native reuse or the specific reason and
  bounded behavior for an extension or replacement

#### Scenario: Specialized heat management is considered
- **WHEN** the programme considers a weapon waste-heat mechanic
- **THEN** it identifies the distinct gameplay purpose and its interaction with
  native temperature instead of introducing a conflicting room-temperature model

### Requirement: Explicit mechanic disposition

The roadmap SHALL inventory surveyed mechanic families and assign each a
disposition: native as-is, extend native, adapt SOS2, new extension, retire, or
deferred decision. Each entry SHALL identify evidence, rationale, candidate child
scope, and relevant gate. Provisional entries SHALL NOT imply feature commitment
or an exhaustive per-definition audit.

#### Scenario: A surveyed mechanic has no approved port decision
- **WHEN** a mechanic's inclusion or approach remains unsettled
- **THEN** its entry is marked as a deferred or provisional decision with a
  specific decision point rather than silently omitted or promised

### Requirement: Traceable and honestly classified evidence

Findings SHALL distinguish confirmed user decisions, observed repository code,
observed native definitions or API surfaces, official documentation and release
information, proposed defaults, and unverified runtime behavior. Evidence SHALL
record its source and inspection baseline or access date. Static inspection and
published documentation SHALL NOT count as a passed build, gameplay, or
persistence test.

#### Scenario: A native transfer interface exists
- **WHEN** local metadata exposes relevant transfer and serialization operations
- **THEN** the roadmap records API availability while keeping actual extension
  state retention unverified until an appropriate runtime investigation passes

#### Scenario: Official documentation establishes toolchain compatibility
- **WHEN** official documentation identifies a supported runtime target or
  language version, or release information identifies an available SDK
- **THEN** the roadmap records the source, access date and documented claim
  separately from local observations, without declaring the selected
  toolchain/reference combination or any runtime gate validated

### Requirement: Bounded child changes and explicit dependencies

Each roadmap stage SHALL name its intended outcome, prerequisites, boundaries,
affected capabilities, unresolved gate inputs, and verifiable exit criteria.
Independent work SHALL be distinguished from prerequisite edges. Approval of
this parent roadmap SHALL NOT authorize or scaffold all future child changes.

#### Scenario: A maintainer selects the next stage
- **WHEN** a child change is proposed from the roadmap
- **THEN** its prerequisites and evidence are reviewable and its scope is bounded
  without treating every later stage as approved implementation work

### Requirement: Feasibility gates block dependent commitments

The roadmap SHALL identify blocking investigations for native lifecycle,
structural damage and wrecks, combat arrangement, and vessel scale or concurrency.
Each gate SHALL specify evidence and a pass or stop/revise outcome. Failure SHALL
block dependent implementation rather than justify a competing ship or space
authority.

#### Scenario: A lifecycle investigation fails
- **WHEN** additional state cannot survive native travel or membership changes
  under the investigated approach
- **THEN** dependent feature work stops for redesign, reduced scope, or an
  explicit programme decision without silently falling back to legacy movement

#### Scenario: Combat arrangement has not been proven
- **WHEN** implementation of topology-dependent weapons, boarding, or salvage is
  considered before the encounter gate passes
- **THEN** the dependent implementation remains blocked and its detailed design
  is not represented as settled

### Requirement: First playable slice has an end-to-end exit

The roadmap SHALL define a minimal playable slice in which a native vessel
travels through native space, encounters one hostile craft, exchanges weapon
fire, resolves the encounter, and continues operating. Acceptance SHALL include
resource accounting, native damage and defenses, environment consequences, and
fresh-save persistence without requiring the full content catalogue.

#### Scenario: Individual systems work but the journey does not
- **WHEN** weapons function in isolation but encounter resolution or continued
  native travel fails
- **THEN** the playable-slice stage does not pass

### Requirement: Reliability applies to new campaigns

Every runtime child scope SHALL specify relevant fresh-save/load, transition,
destruction, and failure-recovery acceptance scenarios. Contents and extension
resources SHALL NOT be duplicated or silently lost through native transitions.
Legacy-save migration SHALL remain outside these obligations.

#### Scenario: A supported transition is interrupted or reloaded
- **WHEN** a newly created campaign is saved and loaded at a supported lifecycle
  point or a transition is cancelled or fails
- **THEN** acceptance checks verify consistent ownership, contents, resources,
  and recoverable state for the affected feature

### Requirement: Dependencies and scale require evidence

The roadmap SHALL justify required external dependencies by capability rather
than inherited use. Large-vessel, fleet, and concurrent-transition commitments
SHALL include native-limit investigations and measurable performance acceptance
before they become prerequisites for broader content delivery.

#### Scenario: A transport dependency is proposed
- **WHEN** a child change proposes retaining an external vehicle framework
- **THEN** it identifies the required capability, evaluates native transport,
  and records the resulting decision without assuming upstream coupling is a
  requirement

#### Scenario: Capital-ship content is scheduled
- **WHEN** a content stage depends on vessel sizes beyond demonstrated capacity
- **THEN** the relevant size and performance gate must pass before that content
  is committed for delivery

### Requirement: Retirement and obligations are acceptance conditions

Each child scope SHALL identify superseded runtime authorities and acceptance
checks showing they are absent from its supported path. It SHALL preserve
applicable licensing, attribution, provenance, and archived credits, keep game
code and assets out of redistributed planning evidence, and leave upstream
repository operations subject to explicit demand.

#### Scenario: An old subsystem is replaced
- **WHEN** a child stage claims a harmonized replacement is complete
- **THEN** its review checks both positive native behavior and the absence of
  the superseded competing behavior while retaining required notices and credits

### Requirement: The parent change remains planning-only

This parent change SHALL produce the roadmap, evidence, contracts, and review
tasks only. Applying or completing it SHALL NOT alter gameplay, build or loading
configuration, initialize child changes, publish anything, or declare future
runtime gates passed. Runtime work SHALL require a separately scoped child
proposal and an explicit implementation request.

#### Scenario: The parent planning tasks are completed
- **WHEN** a maintainer completes or archives this roadmap change
- **THEN** the game runtime remains unchanged and candidate child changes remain
  proposed future work rather than automatically starting implementation
