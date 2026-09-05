# Weekly Discovery Triage Implementation Plan

> **For Claude:** REQUIRED SUB-SKILL: Use superpowers:executing-plans to implement this plan task-by-task.

**Goal:** Triage the open weekly discovery reports, add qualifying BOF repositories to the catalog, and close the reports with an auditable summary.

**Architecture:** Deduplicate candidates across issues #44 and #45, screen each repository against `AGENTS.MD`, then add only source-backed, in-scope BOFs. Regenerate the catalog-derived search index and synchronize the GitHub Pages copy before recording the exact added and skipped sets in both Git history and the source issues.

**Tech Stack:** GitHub CLI/API, Python 3, Markdown, JSON, Git.

---

### Task 1: Finalize candidate decisions

**Files:**
- Reference: `AGENTS.MD`
- Reference: GitHub issues #44 and #45
- Reference: `BOF-CATALOG.md`

**Step 1:** Deduplicate candidates across both reports and check every repository against the current catalog.

**Step 2:** Verify each candidate's source, build documentation, activity, and any copycat warnings through its GitHub metadata, README, and relevant source files.

**Step 3:** Record a concrete include or skip decision for every candidate.

### Task 2: Update the catalog and generated indexes

**Files:**
- Modify: `BOF-CATALOG.md`
- Modify: `bof-index.json`
- Modify: `site/data/bof-index.json`

**Step 1:** Add every qualified repository to the appropriate catalog section using the standard badge row format.

**Step 2:** Run `python3 scripts/bof_indexer.py --skip-clone` and `bash scripts/update-site-data.sh` in the `v` environment.

**Step 3:** Verify that both index files parse as JSON, match exactly, and include every added repository.

### Task 3: Verify, commit, and close reports

**Files:**
- Verify: `BOF-CATALOG.md`
- Verify: `bof-index.json`
- Verify: `site/data/bof-index.json`

**Step 1:** Run `python -m unittest discover -s tests -v`, `git diff --check`, and the JSON/index checks.

**Step 2:** Commit the three catalog artifacts with a message that references issues #44 and #45.

**Step 3:** Close each issue with the required structured added/skipped summary. Do not push without explicit approval.
