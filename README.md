# Atris Tasks

[![GitHub stars](https://img.shields.io/github/stars/atrislabs/atris-tasks?style=social)](https://github.com/atrislabs/atris-tasks/stargazers)

The work primitive for Atris.

Atris Tasks turns work into a durable contract that humans, agents, desktop apps, cloud teams, Swarlo, and RL evaluators can all understand.

```text
Plan -> Do -> Review -> Done
```

This repo is the public spec and product surface.

The working implementation currently lives in [`atris-cli`](https://github.com/atrislabs/atris).

## What A Task Is

A task is not just a checkbox.

It is a small work room with:

- a goal
- an owner or agent
- a thread
- an event trace
- proof
- review
- a lesson
- the next task

## System Shape

```text
atris-cli
  -> SQLite task DB
  -> CLI commands
  -> projection JSON
  -> cloud sync plan

Atris Desktop
  -> Command Center
  -> task board
  -> voice and chat entry points

Swarlo
  -> live leases
  -> heartbeat
  -> worker presence

Atris Cloud
  -> shared company task truth
  -> collaboration
  -> sync across machines

RL / eval layer
  -> task episodes
  -> proof
  -> reward
  -> trajectory data
```

## Current Contract

Local source of truth:

```text
~/.atris/tasks.db
```

UI projection:

```text
.atris/state/tasks.projection.json
```

Review episodes:

```text
.atris/state/task_episodes.jsonl
```

Goal file:

```text
atris/goals.md
```

Headless CLI:

```bash
atris task new "Ship the task board" --tag ui --json
atris task next --as codex --json
atris task finish <task_id> --proof "tests passed" --as codex --json
atris task sync --dry-run --business-id <business_id> --json
```

## Self-Improvement Loop

```text
goal
  -> task
  -> claim
  -> proof
  -> review reward
  -> lesson
  -> next task
```

That is the core loop.

Every useful task should leave enough signal for the next agent to do a sharper task.

## Read Next

- [`tasks.md`](tasks.md) - full task system spec
- [`examples/goals.md`](examples/goals.md) - goals file that tasks can map against
- [`examples/task.projection.json`](examples/task.projection.json) - UI projection example
- [`examples/task_episode.jsonl`](examples/task_episode.jsonl) - RL/eval episode example

## Atris ecosystem

| Repo | What |
|------|------|
| [atris](https://github.com/atrislabs/atris) | CLI + task DB implementation |
| [member](https://github.com/atrislabs/member) | Agent team member spec |
| [app.md](https://github.com/atrislabs/app.md) | Agent-runnable app manifest |
| [swarlo](https://github.com/atrislabs/swarlo) | Coordination protocol |

Agents: [`FOR_AGENTS.md`](FOR_AGENTS.md)
