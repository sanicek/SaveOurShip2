# Fork provenance and attribution

Repository governance and metadata belong in `repo/`. `Docs/` remains dedicated
to product/gameplay documentation. This record was prepared on 2026-10-23 from
the local checkout; recording upstream links does not configure an upstream remote
or authorize contacting it.

## Source baseline

- Personal fork: <https://github.com/sanicek/SaveOurShip2>.
- Immediate upstream: <https://github.com/Bqr1s/SaveOurShip2>.
- Upstream branch at the time of the fork: `super_unstable`.
- Initial upstream commit: `af176bf643dc3ca33c9248efa52d261edb54e32e`
  (`Updatre version and assembly`).
- Preserved local/fork baseline branch: `sanicek-super_unstable`.
- Personal working/default branch: `sanicek-main`.

The inherited mod metadata also identifies
<https://github.com/KentHaeger/SaveOurShip2> as its original official GitHub
repository. The original README identifies
<https://github.com/SonicTHI/SaveOurShip2Experimental> as an earlier
community-maintained repository. These are provenance references, not claims that
this personal fork has official status or endorsement.

## Original README snapshot

[UpstreamREADME.md](UpstreamREADME.md) is an exact copy of `README.md` at the
initial upstream commit above, obtained from the existing local Git objects.
It contains the original contributor lists, acknowledgments, and source links.
Keep it unchanged, including wording, formatting, and historical inaccuracies.
Record any later context or corrections here or in the fork-specific README
introduction rather than editing the snapshot.

- Git blob ID: `92c791fb635a9cc2d39cd555b7c32e1e2a159362`.
- SHA-256: `2d3db326158266313c08d00cc6d6e88ea78ba70872f6bbbe6c1fb64ee50a3cc6`.

The root `README.md` also retains the same original bytes between the
`BEGIN PRESERVED UPSTREAM README` and `END PRESERVED UPSTREAM README` HTML comment
markers. New fork-specific text belongs above that section.

For an offline integrity check, compare the snapshot and the marked section
against `git show af176bf643dc3ca33c9248efa52d261edb54e32e:README.md`.
The preservation rule is a maintenance convention, not a technical file lock.

## Credits and licensing

The inherited [project license](../License.md) is Creative Commons
Attribution-NonCommercial-ShareAlike 4.0 International (CC BY-NC-SA 4.0):
<https://creativecommons.org/licenses/by-nc-sa/4.0/>.
Retain its complete text, including the warranty/liability disclaimer.
Fork-specific adaptations and repository documentation authored by sanicek are
offered under the same license. Separately licensed third-party material retains
its own terms; see [ThirdPartyNotices.md](ThirdPartyNotices.md).

Existing attribution includes Kentington, Thain, SonicTHI, Boris (Bqr1s), and the
many contributors, testers, shipwrights, and submod supporters listed in:

- The preserved section of the [root README](../README.md) and
  [UpstreamREADME.md](UpstreamREADME.md).
- [About/About.xml](../About/About.xml), including its author field, credits, and
  source links.
- [CreditsUpdate.txt](../CreditsUpdate.txt).
- In-game credits, including
  [1.7/Languages/English/Keyed/Letters.xml](../1.7/Languages/English/Keyed/Letters.xml).

These existing credit records must not be replaced with the fork maintainer's
name. sanicek maintains this unofficial personal fork and is credited separately
for fork-specific modifications. The Git history retains earlier authorship and
modification records.

## Fork modifications

Changes to date concern branch names, repository workflow, attribution, README
preservation, and licensing/provenance documentation. Mod source, game assets,
and shipped assemblies remain unchanged from the baseline. The guide originally
added at `Docs/ForkWorkflow.md` has moved to `repo/ForkWorkflow.md` to separate
repository metadata from product documentation.

Record subsequent changes with meaningful commits and update this section and
the fork-specific README summary when their scope changes. Do not rewrite earlier
modification records or the archived README.

## Review scope and unresolved questions

- This is a practical documentation and notice review, not legal advice or a
  complete rights-clearance certification.
- This fork is public. Publishing changes here is sharing even without a release
  archive, Steam upload, or separate download. Apply attribution, modification,
  and ShareAlike requirements accordingly.
- Personal noncommercial experimentation and keeping separate releases out of
  scope are the current intentions, not additional restrictions on recipients.
- The bundled historical Harmony DLL and identified merged components are covered
  by the notices and evidence in [ThirdPartyNotices.md](ThirdPartyNotices.md).
- The authorship and licensing provenance of every inherited texture, sound,
  historical contribution, and precompiled mod assembly have not been independently
  verified. Retaining upstream credits is not a substitute for resolving a specific
  rights concern if one is discovered.
- Game/engine assemblies and external build/runtime dependencies have separate
  rights and terms. References to them do not authorize redistribution or relabel
  them under the root license. Review exact versions and packaging before adding
  binaries or making a separate distribution.
- Review any new imported material before inclusion, and resolve uncertain
  permissions rather than assuming the root license grants them. Follow
  [ForkWorkflow.md](ForkWorkflow.md) for the ongoing maintenance rules.
