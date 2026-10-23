# Proposal

## Why

SOS2 currently layers its own vessel ownership, movement, space classification,
and environmental rules alongside Odyssey's native systems. Establish an
evidence-backed, staged programme for a clean-break RimWorld 1.7/Odyssey-native
variant: one authoritative vessel model and one space framework, with SOS2
extending genuine gameplay gaps rather than maintaining parallel simulations.

## What Changes

- Create a planning-only parent change: a "spec of specs" that identifies native
  authorities, mechanic dispositions, candidate child changes, dependencies,
  feasibility gates, and acceptance evidence.
- Adopt native gravship structure and travel, native orbital locations, and
  native vacuum/exposure as the intended authorities for shared concepts.
  Derived equipment caches and genuinely new mechanics remain permissible;
  independently authoritative copies of those native systems do not.
- Record source inspection and the locally available native baseline separately
  from unverified runtime assumptions. Require lifecycle, structural damage,
  combat arrangement, and scale investigations before dependent implementation.
- Prefer a minimal native-first runtime with selectively adapted SOS2 mechanics
  over making the entire inherited runtime a prerequisite. Basic transport,
  shielding, and discovery must first be compared with existing native options.
- **BREAKING (target product boundary):** fresh campaigns and the selected 1.7
  API baseline only. No legacy-save migration, older-version fallback, upstream
  API/definition identity preservation, historical balance parity, or existing
  third-party compatibility commitments. Dependencies require new justification.
- Preserve attribution, licensing, the archived README, and fork-only repository
  defaults. A technical clean break does not waive rights obligations.

This proposal captures the programme; it does not implement any gameplay stage,
scaffold child changes, or authorize their implementation. Feature inclusion
beyond the confirmed harmonization principles remains subject to child scopes.

## Capabilities

### New Capabilities

- `harmonization-roadmap`: A durable programme-level delivery contract for the
  Odyssey-native variant: authority rules, evidence classification, mechanic
  disposition, dependency-ordered child scopes, and readiness/acceptance gates.
  It governs future feature specifications without claiming those features exist.

### Modified Capabilities

None. The project currently has no main capability specifications.

## Impact

- Immediate scope: this change's `proposal.md`, `design.md`,
  `specs/harmonization-roadmap/spec.md`, `tasks.md`, and CLI-created change
  metadata only. No runtime, build configuration, main specs, or repository
  governance files are changed by this proposal.
- Future child changes will principally concern `Source/1.7/`, `1.7/Defs/`,
  expansion patches, loading/package metadata, and retained shared assets.
  Existing ship caches, movement, environment patches, encounter coordination,
  and Vehicle Framework coupling are reference/touchpoint evidence, not mandatory
  foundations for the new runtime.
- Local inspection baseline: RimWorld `1.7.4985 rev1269` and .NET SDK `10.0.113`.
  Native metadata/definitions are accessible; builds and gameplay behavior have
  not been validated. No game assemblies, decompiled implementations, or official
  assets will be copied into these planning artifacts.
