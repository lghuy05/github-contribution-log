
# Contribution 1: [feat: create docs/glossary.md]

**Contribution Number:** 1 
**Student:** Huy Luong 
**Issue:** [[GitHub issue link](https://github.com/pgrwl/pgrwl/issues/278)]  
**Pull Request:** [pgrwl/pgrwl#344](https://github.com/pgrwl/pgrwl/pull/344)  
**Status:** PR submitted — awaiting maintainer review
---

## Why I Chose This Issue

This issue is a good fit for me because it combines technical writing with core PostgreSQL backup and recovery concepts that are important for new users to understand. The glossary needs short, precise explanations for terms like WAL, LSN, PITR, replication slot, and base backup, which makes it a practical way to contribute while improving documentation clarity for people evaluating backup tools and trying to understand how PITR works.

I also chose it because it requires careful reading of the official PostgreSQL documentation and turning complex internal concepts into accessible terminology. That matches my interest in making technical systems easier to understand, and it gives me a chance to learn the relationships between these backup and recovery components while producing something directly useful for users.

Shorter version:

I chose this issue because it focuses on clarifying essential PostgreSQL backup and recovery terms for new users. It matches my interest in technical writing and will help me deepen my understanding of concepts like WAL, LSN, PITR, replication slots, and base backups while creating documentation that is practical and easy to follow.

---

## Understanding the Issue

### Problem Description

This is a documentation gap rather than a bug. `pgrwl` is a continuous-backup tool for PostgreSQL, and its docs assume the reader already knows core PostgreSQL terms (WAL, LSN, timeline, replication slot, `.partial` file, base backup, PITR, RPO). New users evaluating the tool have no single place that explains these concepts concisely or shows how they fit together to make point-in-time recovery possible.

### Expected Behavior

A `docs/pgrwl/glossary.md` page exists with short, precise definitions of each term, a link to the official PostgreSQL documentation for each, and an overview that connects them into one story.

### Current Behavior

No glossary existed. The terms were scattered across the README and other docs with no beginner-friendly definitions or a single reference page.

### Affected Components

Documentation only — `docs/pgrwl/`. No application/Go code is involved, so a local build was not required.

---

## Reproduction Process

### Environment Setup

Forked and cloned `pgrwl`. Because this is a docs-only change, I did not need to build the Go binary or run the integration tests. Setup was limited to reading the existing docs and confirming the project's conventions:
- `CONTRIBUTING.md` — conventional commits, fork-and-PR workflow.
- `docs/pgrwl/` — existing doc style (short sections, markdown links to official PostgreSQL docs), e.g. `links.md` and `developer-notes.md`.

### Steps to Reproduce (confirming the gap)

1. Open the `pgrwl` README and `docs/pgrwl/` directory.
2. Look for a glossary or beginner-friendly definitions of WAL, LSN, PITR, etc.
3. Observed result: no glossary page exists; terms are used but never defined in one place.

### Reproduction Evidence

- **Where the gap lives:** `docs/pgrwl/` had `installation.md`, `configuration.md`, `rest-api.md`, `restore-command.md`, `links.md`, `developer-notes.md` — but no `glossary.md`.
- **My findings:** The maintainer's issue comment is effectively the spec: short, precise terminology for users new to PostgreSQL, each linked to official docs, explaining why PITR needs many components working together.

---

## Solution Approach

### Analysis

The "root cause" is missing onboarding documentation. The concepts are inherently interrelated — you can't understand PITR without WAL, base backup, and LSN — so a flat list of definitions isn't enough. The page needs both per-term definitions and a narrative that shows how the pieces connect.

### Proposed Solution

Create `docs/pgrwl/glossary.md` with:
1. A short intro framing the page for PostgreSQL newcomers.
2. A "big picture" overview that tells the end-to-end backup/recovery story, with each key term linked down to its full definition.
3. One section per term (WAL, LSN, Timeline, Replication slot, `.partial` file, Base backup, PITR, RPO), each with a plain-language definition, a note on how `pgrwl` uses it, and a link to the official PostgreSQL docs.

### Implementation Plan

Using UMPIRE framework (adapted):

**Understand:** Users new to PostgreSQL lack a concise reference for the core backup/recovery terms `pgrwl` relies on.

**Match:** Followed the existing `docs/pgrwl/` style — `#` title, short sections, bullet lists, and markdown links to the official PostgreSQL documentation (as seen in `links.md` and `developer-notes.md`). The README itself already references concepts in this order, so I mirrored that ordering.

**Plan:**
1. Add `docs/pgrwl/glossary.md`.
2. Write the 8 term definitions in dependency order (WAL → LSN → Timeline → Replication slot → `.partial` file → Base backup → PITR → RPO).
3. Add a "big picture" section with in-page anchor links to each term.
4. Link each term to its official PostgreSQL doc.

**Implement:** Branch `docs/glossary.md-278`, squashed into one clean commit (`b458406`).

**Review:** Follows `CONTRIBUTING.md` — conventional commit (`docs:` prefix), issue number referenced (#278), matches existing doc style.

**Evaluate:** Verify the markdown renders correctly on GitHub and that the in-page anchor links in the "big picture" section jump to the right headings.

---

## Testing Strategy

### Unit Tests

N/A — documentation-only change, no code paths to unit test.

### Integration Tests

N/A — no application behavior changes.

### Manual Testing

- [x] Markdown renders correctly (headings, lists, code spans, links).
- [x] Each term links to a valid official PostgreSQL documentation URL.
- [x] "Big picture" in-page anchor links jump to the correct term headings (the `.partial file` heading anchor is the one to double-check, since GitHub strips the backticks and leading dot).
- [x] Definitions reviewed for plain, beginner-friendly language.

---

## Implementation Notes

### Week 1 Progress

- Claimed issue #278 and confirmed scope with the maintainer.
- Built a focused reading path through the repo (CONTRIBUTING → high-level README → `docs/pgrwl/` style) instead of reading the whole Go codebase, since this is a docs task.
- Drafted `glossary.md` with all 8 terms, then added a "big picture" overview linking each term to its definition.
- Rewrote the prose to be plain and beginner-friendly, and added a short "how `pgrwl` uses this" note to each term.
- Squashed the branch into one clean commit and opened the PR.

### Code Changes

- **Files modified:** `docs/pgrwl/glossary.md` (new file).
- **Key commits:** `b458406` — docs: add glossary of core PostgreSQL concepts (#278).
- **Approach decisions:**
  - Ordered terms by dependency so each builds on the previous one.
  - Added a narrative "big picture" section because the concepts only make sense in relation to each other.
  - Matched the existing `docs/pgrwl/` style (links to official PostgreSQL docs) rather than inventing a new format.

---

## Pull Request

**PR Link:** https://github.com/pgrwl/pgrwl/pull/344

**PR Description:** Adds `docs/pgrwl/glossary.md` with short, precise explanations of the core PostgreSQL concepts behind `pgrwl` (WAL, LSN, Timeline, Replication slot, `.partial` file, Base backup, PITR, RPO), aimed at users new to PostgreSQL. Each term has a concrete definition, a note on how `pgrwl` uses it, and a link to the official PostgreSQL docs, plus a "big picture" overview tying them together. Closes #278.

**Maintainer Feedback:**
- _(none yet — awaiting first review)_

**Status:** Awaiting review

---

## Learnings & Reflections

### Technical Skills Gained

- A clearer understanding of how PostgreSQL backup and recovery actually fits together: WAL as the ordered change log, LSNs as positions in it, base backups as the starting image, and PITR as "restore a base backup, then replay WAL forward."
- Why streaming WAL can reach RPO=0 while the older `archive_command` approach can lose up to a full 16 MiB segment.
- The open-source contribution workflow end to end: claiming an issue, branching, conventional commits, squashing messy history into one clean commit, and opening a cross-fork PR with `gh`.

### Challenges Overcome

- Avoiding the trap of trying to understand the whole Go codebase. I scoped my reading to what the docs task actually required (conventions + high-level architecture), which saved a lot of time.
- Turning dense PostgreSQL internals into plain language without losing accuracy.
- Cleaning up a noisy branch history (a stray "reading flow" commit and a scratch file) into a single clear commit before opening the PR.

### What I'd Do Differently Next Time

- Branch off `master` immediately before starting, rather than committing exploratory/scratch work onto the feature branch and squashing later.
- Confirm doc formatting details (like heading-anchor behavior for `` `.partial` ``) earlier in the process.

---

## Resources Used

- [pgrwl README](https://github.com/pgrwl/pgrwl) and `docs/pgrwl/` — project conventions and existing doc style.
- [PostgreSQL: Reliability and the Write-Ahead Log](https://www.postgresql.org/docs/current/wal-intro.html)
- [PostgreSQL: Continuous Archiving and Point-in-Time Recovery](https://www.postgresql.org/docs/current/continuous-archiving.html)
- [PostgreSQL: pg_lsn data type](https://www.postgresql.org/docs/current/datatype-pg-lsn.html)
- [PostgreSQL: Replication slots](https://www.postgresql.org/docs/current/warm-standby.html#STREAMING-REPLICATION-SLOTS)
- [Conventional Commits](https://www.conventionalcommits.org/en/v1.0.0/)
