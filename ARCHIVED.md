# intersense — ARCHIVED

**Archived 2026-03-26.** Domain detection unified into interflux's LLM-based classification (flux-drive Step 1.0.1). See Demarch-1qjs, Demarch-goqc.

## What moved where

| Component | New location |
|-----------|-------------|
| Domain profiles (`config/domains/*.md`) | `interverse/interflux/config/flux-drive/domains/` (already had copies) |
| `detect-domains.py` | Deleted — LLM classification replaces signal-based detection |
| `content-hash.py` | Deleted — no cache to detect staleness for |
| `index.yaml` | No longer used — LLM classifies without an index |

## Why archived

The deterministic signal-based detection was redundant with the LLM classification that flux-drive already performed in Step 1.0.1. The LLM reads the project (README, build files, source) and classifies domains with better nuance than the keyword/directory scanner, without maintaining a separate script, cache, or plugin.
