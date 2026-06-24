# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [1.0.0] - 2026-06-24

### Added

- 15-industry × seniority decision matrix with auto-derivation for uncovered industries
- Three operational modes: generate from scratch (A), review (B), incremental edit (C)
- Full mode-switching state machine across all three modes
- ATS compatibility rules: linear layout, font separation, keyword strategy, DOCX vs PDF delivery
- Chinese and English resume support with STAR framework for English
- Privacy protection: 6 categories of automatically filtered PII
- Three-layer DOCX generation fallback: docx-js → python-docx → Markdown
- Minimal user input coping strategy: single-project deep expansion, skill compensation, layout compensation
- Low-seniority / career-switcher candidate strategy section
- Batch mode for fast-track information collection
- Compressed keyword-block auto-parsing for terse user input
- User skip/negation rule engine during information collection
- Cross-dimensional single-reply information extraction
- Progress visualization with per-dimension status table
- Design portfolio link handling: 10+ supported platforms, drive link preservation, QR code avoidance
- Single-project resume strategy (1 project → 5-6 bullets from orthogonal angles)
- Freelance/part-time project vs. employment classification logic
- Post-edit consistency checks: job target sync, tech stack alignment, tense uniformity, bullet density balance
- Edit session change log tracking (≥3 edits)
- Platform compatibility reference table (Claude Code / Cursor / Copilot / Windsurf / ChatGPT)
- FAQ section with 7 common questions
- Companion documentation: `docs/ats-guide.md`, `docs/english-resume.md`, `docs/docx-spec.md`
- Windows Python GBK encoding workaround for verification scripts

### Changed

- Refactored monolithic SKILL.md (originally 566 lines) — extracted ATS, English, and DOCX deep dives into `docs/`
- Decoupled Skill synergy layer into platform-agnostic rules + Claude Code enhancements + fallback strategies
- Normalized scoring weights across all 14 built-in industries (was: one-line adjustment rule)

### Fixed

- docx-js v8/v9 `format: "bullet"` vs `LevelFormat.BULLET` version conflict with runtime detection code
- Missing `.gitignore` — open-source repos were shipping `node_modules/` and IDE cruft
- Missing `CONTRIBUTING.md` and CHANGELOG — no contribution path for first-time contributors
- Missing `.github/` Issue and PR templates — no structured bug report or feature request flow
- Terminology inconsistency: "行业-6 类" in old README vs. actual 14 matrix rows
- Missing `version` frontmatter in SKILL.md — no way to track breaking changes across releases

## [Unreleased]

### Added

- Industry-specific structural templates for 4 high-variance industries (design, finance, law, education)
- CODE_OF_CONDUCT.md (Contributor Covenant 2.1)
- docx-js runtime version detection: `try/catch LevelFormat` pattern + package.json parsing

### Changed

- Constraint rules renumbered from 0-based flat list to 3-group system: F1-F3 (Flow), C1-C3 (Content), T1 (Tech)
- Phase 0 scanning steps merged with Skill synergy section — eliminated ~20 lines of duplicate content

[1.0.0]: https://github.com/Tissue-for-charlie/resume-expert/releases/tag/v1.0.0
