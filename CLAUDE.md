# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

FRI is a corrections and enhancements repository for the Cologne digitization of Frish's *Sanskrtská čítanka* (Sanskrit Reader), published in Moscow (2015, Vol. 2). The canonical source data lives in `csl-orig`. This repo holds tooling and issue-specific correction workflows.

## Architecture

| Directory | Purpose |
|---|---|
| `fri_01/` | Display and correction work for the first processed version |
| `issues/` | Per-issue correction workflows (`issueNNN/` pattern) |
| `fri_00.txt` | Initial SLP1 source text |

### Correction workflow

Each issue folder follows the standard pattern:
1. Copy current `fri.txt` to `temp_fri_0.txt` (not tracked)
2. Apply corrections as `temp_fri_1.txt`, `temp_fri_2.txt`, etc.
3. Rebuild XML with `generate_dict.sh`, validate with `xmlchk_xampp.sh`
4. Commit corrected file to `csl-orig`; commit docs back here

## GitHub Issue Conventions

### Milestones and projects

Every issue belongs to exactly one milestone, which mirrors an org-level kanban project:

| Milestone | Project | Scope |
|---|---|---|
| Dictionary to Book (1) | Project 1 | Link targets |
| Digitization Quality (2) | Project 2 | Scan quality, encoding, bug fixes |
| Structured Data (3) | Project 3 | Markup, abbreviation tooltips |
| Major Enhancements (4) | Project 4 | Display upgrades, new versions |

### Type labels

Every issue has exactly one type label:

| Label | When to use |
|---|---|
| `link-target` | Building a click-through from a `<ls>` abbreviation to scanned PDF pages |
| `link-splitting` | Splitting combined `SOURCE N,N` refs into individual per-page links |
| `markup` | Normalising XML tag content or abbreviation tooltips |
| `text-correction` | Corrections to dictionary text |
| `content-enhancement` | New material, display upgrades, or new versions |
| `encoding` | Character rendering, Latin/Cyrillic conversion |
| `scan-quality` | Replacing wrong or poor-quality scan images |
| `bug` | Broken display or XML structure errors |
| `question` | Scholarly or editorial questions requiring research |

### Severity labels

Every issue also has exactly one severity label:

| Label | When to use |
|---|---|
| `minor` | Targeted, self-contained fix |
| `medium` | Standard unit of work — initial display version, batch corrections |
| `hard` | Large effort spanning many files or sources |
