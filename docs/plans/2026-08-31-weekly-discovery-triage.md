# Weekly Discovery Triage Implementation Plan

> **For Claude:** REQUIRED SUB-SKILL: Use superpowers:executing-plans to implement this plan task-by-task.

**Goal:** Triage weekly discovery issue #46, catalog each qualifying BOF repository, and close the issue with an auditable summary.

**Architecture:** Evaluate every issue candidate against `AGENTS.MD` and the current catalog. Add qualified repositories to `BOF-CATALOG.md`, regenerate both search indexes without disturbing the user's existing `msi-search` edits, verify the artifacts, commit the weekly review, and push only with explicit approval.

**Tech Stack:** GitHub CLI/API, Python 3, Markdown, JSON, Git.

---

### Task 1: Record candidate decisions

**Files:**
- Reference: `AGENTS.MD`
- Reference: GitHub issue #46
- Reference: `BOF-CATALOG.md`

**Step 1:** Check every candidate against the current catalog.

**Step 2:** Inspect repository metadata, file trees, READMEs, source, build instructions, and warnings.

**Step 3:** Include `antroguy/enumdepend-bof`, `An0nUD4Y/ScriptSentry-BOF`, `An0nUD4Y/PoolParty-BOF`, and `An0nUD4Y/Zipper-BOF`.

**Step 4:** Skip `niddalA-sec/ctf-bof` because it contains buffer-overflow CTF challenges, `lktp/Bofs` because its lone BOF lacks a reproducible build and required source headers, and `BishopFox/sliver` because it is a C2 framework rather than a BOF repository.

### Task 2: Update the catalog and indexes

**Files:**
- Modify: `BOF-CATALOG.md`
- Modify: `bof-index.json`
- Modify: `site/data/bof-index.json`

**Step 1:** Add the four qualified repositories to `## 🧩 Other BOFs` with concise descriptions and standard badges.

**Step 2:** Run `python3 scripts/bof_indexer.py --skip-clone` and `bash scripts/update-site-data.sh`.

**Step 3:** Confirm both JSON files parse, match exactly, include all four additions, and retain `mandiant/msi-search`.

### Task 3: Verify and commit

**Files:**
- Verify: `BOF-CATALOG.md`
- Verify: `bof-index.json`
- Verify: `site/data/bof-index.json`

**Step 1:** Run `python3 -m unittest discover -s tests -v`.

**Step 2:** Run `git diff --check` and targeted catalog/index checks.

**Step 3:** Commit only the weekly-review rows and their generated index entries, leaving the user's `msi-search` changes uncommitted.

### Task 4: Publish and close the report

**Files:**
- Reference: GitHub issue #46

**Step 1:** Ask for approval before pushing the weekly-review commit.

**Step 2:** After a successful push, close issue #46 with Added and Skipped tables that list every candidate and decision.
