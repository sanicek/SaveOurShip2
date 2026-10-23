# Tasks

This is the review/finalization checklist for the **planning parent**, not an
implementation checklist for S00-S10. Its editable deliverables are this change's
`proposal.md`, `design.md`, `specs/harmonization-roadmap/spec.md`, and `tasks.md`.
Repository/native evidence inspection is read-only. No task below authorizes a
build, game launch, probe implementation, runtime/configuration edit, child
scaffold, main-spec sync, commit, push, or upstream operation.

Draft creation and automated validation do not mark maintainer-review tasks done.
Future runtime investigations remain unperformed and must use their own child
changes and explicit implementation requests.

## 1. Confirm the programme boundary and evidence

- [ ] 1.1 Review the proposal and roadmap requirements against the confirmed clean-break direction; verify that one native vessel/space/environment authority, fresh campaigns, 1.7/Odyssey targeting, and no inherited compatibility commitments are stated consistently, without claiming all old features are approved.
- [ ] 1.2 Cross-check design evidence E1-E13 against the recorded repository revision and N1-N8 against the recorded local game baseline using read-only inspection; verify that paths/symbols are traceable, obsolete/excluded code is not counted as active behavior, and API availability is never labeled a runtime pass.
- [ ] 1.3 Review the mechanic disposition ledger for coverage of the surveyed systems; verify that each row has a rationale, evidence, candidate child scope and relevant gate or stage, and that uncertain feature inclusion is explicitly provisional or deferred rather than silently promised or omitted.

## 2. Review stage boundaries and feasibility gates

- [ ] 2.1 Review G0-G5 in the design; verify that every gate names specific evidence and pass/stop outcomes, runtime outcomes remain unverified, failed invariants block dependent work, and structural damage, engine loss, cancellation and supported save/load cases are covered.
- [ ] 2.2 Review S00-S10 and their prerequisites as a dependency graph; verify that the graph is acyclic, the S01 probe does not depend on the S02 production package, later tracks are not unnecessarily serialized, and no unresolved gate is bypassed by a feature commitment.
- [ ] 2.3 Trace S05's exit to the first-playable-slice requirement; verify that native travel, one hostile encounter, damage/defenses, resource accounting, resolution, continued operation and fresh-save failure cases form one testable loop without requiring the whole catalogue or waste-heat system.
- [ ] 2.4 Review the child-readiness contract and selected stage scopes; verify that dependency/DLC decisions, measurable scale acceptance where relevant, positive and duplicate-authority-negative tests, and superseded-runtime retirement belong to each child rather than an unspecified final cleanup stage.

## 3. Verify preservation and planning-only scope

- [ ] 3.1 Check the recorded licensing/provenance constraints and preserved README integrity; verify that `License.md` is unchanged, `repo/UpstreamREADME.md` and the marked root README block still match the baseline recorded in `repo/Provenance.md`, and no game binaries, decompiled implementations or official assets have been added to planning evidence.
- [ ] 3.2 Inspect the working-tree changes relative to the pre-proposal state; verify that this change adds only its CLI metadata and four planning artifacts, leaves the pre-existing `.opencode/` and OpenSpec setup untouched, and changes no source, build/loading configuration, repository rules, game installation, mod profile or remotes.

## 4. Integrate and hand off the roadmap

- [ ] 4.1 Validate cross-artifact consistency, evidence/stage/gate references and local Markdown links; verify `openspec validate plan-odyssey-native-harmonization --strict` passes and `openspec status --change plan-odyssey-native-harmonization --json` reports all four planning artifacts done, without treating file-existence status as gameplay completion.
- [ ] 4.2 Present the reviewed roadmap and record any maintainer-approved revisions within these artifacts; verify that the handoff names S00 as the next candidate, records outstanding runtime gates, and neither creates a child nor begins implementation without a new explicit request.

## Workflow follow-up

- Archive or sync this parent only after its review is complete and the maintainer
  explicitly requests that workflow; neither operation is part of proposing it.
- Use a separately requested `/opsx-propose` for the bounded S00 baseline scope,
  then an explicit `/opsx-apply` request for that child's work. Do not interpret
  applying this planning parent as permission to apply the programme's stages.
- The subsequent S01 lifecycle probe and all later runtime stages likewise need
  their own scoped proposals and explicit implementation requests.
