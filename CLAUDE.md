_Created: 07-05-2026 · Last updated: 05-09-2026_

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

_Dr. Mārcis Gasūns_
