# Contributing to nakama

## The one rule

**Never commit directly to `main`.** Every change — feature, fix, docs —
goes through a branch and a pull request:

```bash
git checkout -b feat/watch-command
# ... work in small, reviewable commits ...
git push -u origin feat/watch-command
gh pr create --fill
```

`main` only ever moves via merges (or squash-merges) of reviewed PRs.
If you are an agent captain working this repo, this applies to you too —
open the PR and let the human merge.

## Branch names

- `feat/<thing>` — new capability
- `fix/<thing>` — bug fix
- `docs/<thing>` — docs only
- `chore/<thing>` — tooling, repo hygiene

## Commits

- Conventional Commits: `feat(cli): ...`, `fix(spawn): ...`, `docs: ...`.
- Small and logical: one commit = one idea. Split rather than cram —
  `spawn` + `list` + `collect` in one commit would have been three PRs
  here, and the history shows it.
- `bash -n nakama` must pass before every CLI commit.

## PRs

- Keep them reviewable: one concern per PR, description says what + why.
- CLI changes: paste a `nakama --help` / smoke-test transcript.
- Docs changes: no test needed, but keep the captain's contract
  (AGENTS.md) and the README in sync when behavior changes.
