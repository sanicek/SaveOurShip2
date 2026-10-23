# Personal fork workflow

This checkout is for `sanicek/SaveOurShip2`. Its working and GitHub default branch
is `main`, initially created from `super_unstable`. The original local and fork
branches named `super_unstable` were left unchanged.

## Safe defaults

- The only configured remote is `origin`: `git@github.com:sanicek/SaveOurShip2.git`.
- Git pushes default to `origin`, with `push.default=simple` (only the current
  branch, with branch-name checks).
- `main` tracks `origin/main`.
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
git switch main
git fetch --no-tags git@github.com:Bqr1s/SaveOurShip2.git super_unstable
git log --oneline main..FETCH_HEAD
git diff --stat main...FETCH_HEAD
```

Fetching does not merge anything. `FETCH_HEAD` is temporary and can be replaced
by another fetch, so review it before running further fetches. If integration is
also explicitly requested, start with a clean working tree and merge the reviewed
commit, resolve any conflicts, test, and push only to the fork:

```sh
git merge FETCH_HEAD
git push origin main
```

Do not use GitHub's fork-sync action on `main` unless intentionally syncing it.
