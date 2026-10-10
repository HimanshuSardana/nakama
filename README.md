# nakama 仲間

Talk to one captain. Ship with a crew.

nakama is a tiny, personal crew runner for coding agents. You talk to a
single agent — the captain — and it sails tasks out to a fleet of crewmates
(nakama), each working in isolation in its own git worktree and its own
[herdr](https://herdr.dev) tab, running [pi](https://github.com/badlogic/pi-mono).
When a crewmate finishes, the captain reviews and merges — or files the
scouting report.

One Piece logic: one captain, many nakama, one Grand Fleet. Nobody touches
the main ship (your checkout) except the captain, and only after review.

## Requirements

- `herdr` running (the session backend — tabs are the ships)
- `pi` as the agent harness (`herdr agent start --kind pi`)
- `git`, `jq`, `bash`

## Quick start

```bash
# launch your captain inside this repo, then:
nakama spawn --repo ~/personal/projects/kite-dev --kind ship \
  --brief "Fix the flaky login test. Keep the diff small."

nakama list                 # see every crewmate + live agent status
nakama read nk-261010-a1b2c3
nakama wait nk-261010-a1b2c3 --timeout 1800000
nakama collect nk-261010-a1b2c3   # diff review + merge instructions
nakama retire nk-261010-a1b2c3    # close tab, remove worktree
```

Two task shapes:

- **ship** — delivers authorized changes on a `nakama/<id>` branch in a
  worktree. Captain reviews the diff, then merges.
- **scout** — investigates and reports back. Detached worktree, no branch,
  no code changes; ends in a `report.md`.

Full operator contract for the captain lives in [AGENTS.md](AGENTS.md).
Task contracts live in [skills/ship](skills/ship/SKILL.md) and
[skills/scout](skills/scout/SKILL.md).

## Layout

```
nakama            # the CLI (bash, herdr backend)
AGENTS.md         # captain's orders — how your agent runs a crew
skills/ship/      # contract for change-delivering tasks
skills/scout/     # contract for investigation tasks
```

State lives outside the repo in `${NAKAMA_HOME:-~/.config/nakama}`:
one directory per crewmate (`task.json`, `brief.md`, `report.md`) plus
`trees/<id>` worktrees. Restart-proof: the next session reconciles from
disk, and every crewmate is visible in the `nakama-fleet` herdr workspace.

## Roadmap

- [ ] `nakama watch` — event-driven wakeups instead of polling `wait`
- [ ] second fleets on SSH-reachable hosts
- [ ] `gh pr create` collect path for shared repos
- [ ] zellij/tmux backend adapters
