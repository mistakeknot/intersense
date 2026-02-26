# intersense

Domain detection for Claude Code plugins.

## What this does

intersense classifies your project into domains — game engine, CLI tool, ML pipeline, web API, and 8 more — by scanning for structural signals: specific directories, manifest files, dependency names, and source code keywords. Each signal gets scored against a confidence threshold, and a project can match multiple domains simultaneously (a game server is both `game-simulation` and `web-api`).

The detection result gets cached at `.claude/intersense.yaml` so downstream plugins (like [interflux](https://github.com/mistakeknot/interflux)) can inject domain-specific review criteria without re-scanning every time.

This is a scripts-only plugin — no skills, no commands, no hooks. Other plugins call its scripts directly or through delegation stubs.

## Installation

First, add the [interagency marketplace](https://github.com/mistakeknot/interagency-marketplace) (one-time setup):

```bash
/plugin marketplace add mistakeknot/interagency-marketplace
```

Then install the plugin:

```bash
/plugin install intersense
```

## How it works

```bash
# Detect domains for the current project
python3 scripts/detect-domains.py /path/to/project

# Check if the cached result is stale
python3 scripts/detect-domains.py /path/to/project --check-stale

# Content hash for staleness detection
python3 scripts/content-hash.py /path/to/file
```

Detection scans against `config/domains/index.yaml`, which maps each domain to its signals and minimum confidence threshold. When a domain matches, its corresponding profile (e.g., `config/domains/game-simulation.md`) provides domain-specific review injection criteria for each flux-drive agent, plus Research Directives for external research agents.

## Domains

11 domain profiles ship out of the box:

| Domain | Detects |
|--------|---------|
| `claude-code-plugin` | Plugin manifests, hooks dirs, SKILL.md files |
| `cli-tool` | Cobra/click/argparse, main entry points |
| `data-pipeline` | Airflow, dbt, Spark, ETL patterns |
| `desktop-tauri` | Tauri configs, Electron, native bindings |
| `embedded-systems` | HAL, RTOS, bare-metal toolchains |
| `game-simulation` | Game loops, ECS, physics engines |
| `library-sdk` | Package manifests without entry points |
| `ml-pipeline` | PyTorch, transformers, training scripts |
| `mobile-app` | React Native, Flutter, platform configs |
| `tui-app` | Bubble Tea, curses, terminal UI frameworks |
| `web-api` | Express, FastAPI, route handlers |

## Architecture

```
scripts/
  detect-domains.py      Signal-based domain classifier
  content-hash.py        Content-addressable hashing for cache staleness
config/domains/
  index.yaml             Signal definitions + confidence thresholds
  *.md                   Domain profiles with review injection criteria
```

## Ecosystem

intersense was extracted from [interflux](https://github.com/mistakeknot/interflux) to make domain detection available to any Interverse plugin. interflux's `detect-domains.py` is now a thin stub that delegates here via `os.execv`.
