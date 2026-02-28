# intersense Philosophy

## Purpose
Domain detection — classifies projects by signals (directories, manifests, dependencies, keywords) into domains for review and research targeting.

## North Star
Correctly classify any project's domain on first scan.

## Working Priorities
- Classification accuracy (right domain, right confidence)
- Signal coverage (enough heuristics to handle diverse projects)
- Integration with downstream consumers (interflux triage, research targeting)

## Brainstorming Doctrine
1. Start from outcomes and failure modes, not implementation details.
2. Generate at least three options: conservative, balanced, and aggressive.
3. Explicitly call out assumptions, unknowns, and dependency risk across modules.
4. Prefer ideas that improve clarity, reversibility, and operational visibility.

## Planning Doctrine
1. Convert selected direction into small, testable, reversible slices.
2. Define acceptance criteria, verification steps, and rollback path for each slice.
3. Sequence dependencies explicitly and keep integration contracts narrow.
4. Reserve optimization work until correctness and reliability are proven.

## Decision Filters
- Does this improve domain classification accuracy?
- Does this reduce false positives in triage?
- Is the signal set extensible without breaking existing classifications?
- Can a misclassification be corrected and learned from?
