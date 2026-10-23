# Personal fork workflow

Repository rules and metadata live in `repo/`; `Docs/` is for product/gameplay
documentation. See [provenance and attribution](Provenance.md) and
[third-party notices](ThirdPartyNotices.md).

This checkout is for `sanicek/SaveOurShip2`. Its working and GitHub default branch
is `sanicek-main`, initially created from `super_unstable`. The starting branch
is preserved as `sanicek-super_unstable`. The old local and fork branch names
`main` and `super_unstable` have been replaced with these prefixed names; the
original repository is unchanged.

Use `sanicek-feat/<description>` for new feature branches, for example:

```sh
git switch sanicek-main
git switch --create sanicek-feat/something-new
git push --set-upstream origin sanicek-feat/something-new
```

## Safe defaults

- The only configured remote is `origin`: `git@github.com:sanicek/SaveOurShip2.git`.
- Git pushes default to `origin`, with `push.default=simple` (only the current
  branch, with branch-name checks).
- `sanicek-main` tracks `origin/sanicek-main`.
- `sanicek-super_unstable` tracks `origin/sanicek-super_unstable`.
- GitHub CLI defaults to `sanicek/SaveOurShip2`. Use an explicit repository for
  commands, for example `gh pr create --repo sanicek/SaveOurShip2`.
- No upstream remote is configured, so ordinary fetches, including
  `git fetch --all`, do not contact the original repository.

Do not fetch, sync, push, open pull requests, or perform other operations against
the original repository unless explicitly requested. These are workflow defaults,
not an access-control boundary: explicit URLs, repository overrides, and GitHub's
website can still target other repositories. The GitHub fork relationship remains.

Git configuration and the GitHub CLI default are local to this checkout, not
versioned. When setting up another clone, inspect `git remote -v` first, ensure
`origin` points to this fork, and remove any upstream remote if present. Then set:

```sh
git config --local remote.pushDefault origin
git config --local push.default simple
gh repo set-default sanicek/SaveOurShip2
```

## Upstream sync: explicit request only

The original repository is `Bqr1s/SaveOurShip2`, with branch `super_unstable`.
It does not need to be configured as a remote for an intentional one-time fetch.

Only when upstream contact is explicitly requested, fetch and inspect its changes:

```sh
git switch sanicek-main
git fetch --no-tags git@github.com:Bqr1s/SaveOurShip2.git super_unstable
git log --oneline sanicek-main..FETCH_HEAD
git diff --stat sanicek-main...FETCH_HEAD
```

Fetching does not merge anything. `FETCH_HEAD` is temporary and can be replaced
by another fetch, so review it before running further fetches. If integration is
also explicitly requested, start with a clean working tree and merge the reviewed
commit, resolve any conflicts, test, and push only to the fork:

```sh
git merge FETCH_HEAD
git push origin sanicek-main
```

Do not use GitHub's fork-sync action on `sanicek-main` unless intentionally syncing it.

## Attribution and licensing rules for changes

- Keep the root `License.md` intact. Fork-specific adaptations and repository
  documentation authored by sanicek use CC BY-NC-SA 4.0; separately licensed
  third-party material retains its own license.
- Treat `repo/UpstreamREADME.md` as an immutable historical snapshot. Do not
  reformat, correct, or update it, including contributor names, links, and typos.
  Its source commit and checksum are recorded in [Provenance.md](Provenance.md).
- Leave the original section between the preservation markers in the root
  `README.md` unchanged. Put fork-specific information above it. Later upstream
  syncs must preserve the archived snapshot and review any attribution changes
  deliberately rather than silently overwriting the original section.
- Preserve existing author/contributor credits, copyright and license notices,
  warranty disclaimers, source links, and indications of previous modifications,
  including those in `About/About.xml`, `CreditsUpdate.txt`, and in-game credits.
  Add fork-maintainer credit separately; do not replace the original authors.
- Identify modifications with meaningful commits and update the fork-specific
  README summary when the scope changes. Clearly distinguish this unofficial
  personal fork from upstream; do not imply endorsement.
- Keep use noncommercial. Reassess licensing before any monetization or
  commercial use. Having no download price is not by itself sufficient.
- Before importing code, assets, or binaries, verify their source, version,
  license, compatibility, and required notices. Record the evidence and add any
  required text to [ThirdPartyNotices.md](ThirdPartyNotices.md). Do not treat
  missing or uncertain permission as consent.
- Do not commit game/engine DLLs, publicized game assemblies, external dependency
  binaries, or copied assets without first verifying redistribution permission.
  Build references do not themselves grant that permission.
- Do not add terms such as "no redistribution" or technological measures that
  restrict recipients' licensed rights. The current intention not to publish
  separate releases is not an additional license condition.
- Before any separately packaged distribution, review its contents and carry
  the applicable license, attribution, disclaimer, modification information, and
  third-party notices with it. Review outstanding provenance questions first.

These are maintenance rules for this fork, not amendments to any license.
