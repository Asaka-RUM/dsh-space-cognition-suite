# dsh-space-cognition-suite

English | [中文](README.zh.md)

J-Space Cognition Suite as a DeepSeek Harness (DSH) plugin.

An inference-time cognitive control layer: it gives an agent a deliberate inner workspace and a discipline for using it — a premise, a task gate (fast/full/loop), module-based on-demand loading, seam-based auditing, and a durable ledger that carries state across seams and turns.

## What it does

- **Activation** — injects a compact J-Space activation header into every agent session (once per session): the premise, the gate, the module index, and the invariants. No manual skill loading required.
- **Ledger tool** — registers a `jspace` tool wrapping the bundled `jspace.py` controller. The model uses it in loop passes to keep labelled state (`.jspace/WORKSPACE.md`) in the task workspace: `seam`, `resume`, `note` (`--goal/--next/--core/--core-slot/--check/--by/--open/--settled-by/--close`), `ship`.
- **Discovery** — syncs the bundled `j-space/` skill tree into the agent skills directory (default `~/.agents/skills/j-space`) so skill-aware hosts discover it as `j-space` with zero manual steps. The sync is content-aware and idempotent.

## Install

Requires a DSH desktop/web profile with Node 18+ and Python 3.

Add to the profile's `cordis.patch.yml`:

```yaml
- insert:
    - id: dsh-space-cognition-suite
      name: 'dsh-space-cognition-suite'
      config:
        python: 'C:\Python314\python.exe'  # path to your python3
```

Then install the package into the profile's `node_modules` and restart the harness.

## Layout

```
lib/index.js          plugin entry (activation + tool + sync)
j-space/SKILL.md      the J-Space skill entry
j-space/modules/      modules loaded on demand by the gate
j-space/references/   evidence base, techniques, worked exemplars
j-space/scripts/      jspace.py ledger controller + verify_suite.py
cordis.patch.yml      loader patch manifest
```

## License

Apache-2.0