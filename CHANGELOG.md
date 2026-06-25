# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [1.1.0] - 2026-06-25

### Added

- **Chinese ATS-specific adaptation**: new `references/chinese-ats.md` covering 北森/Beisen, Moka, 大易/Dayee parsing behaviors, GBK quirks, Chinese JD keyword patterns, and platform-specific document handling
- **Horizontal benchmark comparison**: Mode B scoring now appends a per-industry/seniority benchmark row (median + top-25% threshold) for relative positioning in the candidate pool
- **Government/non-profit matrix deepening**: expanded row with 选调类别 (定向/非定向), 申论/行测 scores, 基层服务项目 (西部计划/三支一扶/特岗); added Step 4 rewrite tilt for public sector
- **PIPL/GDPR compliance note**: C2 privacy constraint now references PIPL Article 6 and GDPR Article 5(1)(c) data minimization principles
- **Zero-dependency path** in README: explicit Markdown output guidance for non-technical users (designers, liberal arts)
- **Mode A dimension auto-skip**: 核心课程 (2a) and 到岗时间 (8) now auto-skip for experienced candidates and low-information scenarios
- **references/ directory**: new architecture — SKILL.md slimmed to ~400 lines as scheduling layer; 9 reference files for detailed rules

### Changed

- **Architecture refactor**: SKILL.md 735 → 396 lines; detailed content extracted to `references/`
  - `docs/ats-guide.md` → `references/ats-guide.md`
  - `docs/english-resume.md` → `references/english-resume.md`
  - `docs/docx-spec.md` → `references/docx-spec.md`
  - 6 new reference files: `industry-matrix.md`, `chinese-ats.md`, `scoring-system.md`, `rewrite-rules.md`, `privacy-ethics.md`, `low-info-strategies.md`
  - `docs/` directory removed
- ATS section condensed; Chinese ATS cross-reference added
- Mode B scoring section slimmed; extended scoring details moved to `references/scoring-system.md`
- Mode B Step 3 now includes benchmark comparison row after score table
- All internal cross-references updated from `docs/` to `references/`

## [1.0.1] - 2026-06-25

### Added

- **Pre-generation page count estimation**: Step 5 now estimates content fit before generating DOCX, with experience-level defaults (0–5y → 1 page, 5–15y → 1–2 pages, 15y+ → 2 pages; intern/campus/part-time always 1 page)
- **Post-scoring page evaluation**: Mode B Step 3 now outputs page evaluation with three tiers (✓ okay / ⚠️ tight / 🔴 overflow) below the scoring table
- **Protection mode**: when user signals satisfaction ("这个版本可以了"), subsequent edits default to incremental (Mode C) to avoid overwriting manual adjustments
- **Hard constraint against script re-run**: Mode C Step C3 now explicitly forbids re-running generation scripts that would overwrite manual Word edits, with a single confirmed exception path

### Changed

- Mode B Step 2 scoring dimensions: "排版可读性" now includes page count check
- Mode B Step 3 feedback tiers: 🔴 must-fix now includes page overflow, 🟡 suggest-fix now includes borderline page overflow

## [1.0.0] - 2026-06-24

### Added

- 14-industry × seniority decision matrix with auto-derivation for uncovered industries
- Industry-specific structural templates for 4 high-variance industries (design, finance, law, education)
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
- CODE_OF_CONDUCT.md (Contributor Covenant 2.1)
- docx-js runtime version detection: `try/catch LevelFormat` pattern + package.json parsing

### Changed

- Refactored monolithic SKILL.md (originally 566 lines) — extracted ATS, English, and DOCX deep dives into `docs/`
- Decoupled Skill synergy layer into platform-agnostic rules + Claude Code enhancements + fallback strategies
- Normalized scoring weights across all 14 built-in industries (was: one-line adjustment rule)
- Constraint rules renumbered from 0-based flat list to 3-group system: F1-F3 (Flow), C1-C3 (Content), T1 (Tech)
- Phase 0 scanning steps merged with Skill synergy section — eliminated ~20 lines of duplicate content

### Fixed

- docx-js v8/v9 `format: "bullet"` vs `LevelFormat.BULLET` version conflict with runtime detection code
- Missing `.gitignore` — open-source repos were shipping `node_modules/` and IDE cruft
- Missing `CONTRIBUTING.md` and CHANGELOG — no contribution path for first-time contributors
- Missing `.github/` Issue and PR templates — no structured bug report or feature request flow
- Terminology inconsistency: "行业-6 类" in old README vs. actual 14 matrix rows
- Missing `version` frontmatter in SKILL.md — no way to track breaking changes across releases

## [Unreleased]

### Added

- **评分金标准测试集 (Golden Test Set)**：`references/scoring-golden-tests.md` — 6 份经人工专家评分的校准简历，覆盖 5 个分数段 × 3 个行业（互联网/金融/设计），用于验证 AI 评分一致性
- **评分前校准流程**：`scoring-system.md` 末尾新增 AI 自检流程（找锚点→对齐权重→评分后自检→允许 ±5 波动）
- Mode B Step 2 新增评分前校准指引，引用 golden tests 建立分数段基准感
- SKILL.md references/ 索引表新增 `scoring-golden-tests.md` 条目
- CONTRIBUTING.md 提交前检查清单新增 Golden Test 同步要求

### Changed

- README references badge 9 → 10 文件
- README 文件树和核心能力列表中新增 golden tests 相关说明

[1.1.0]: https://github.com/Tissue-for-charlie/resume-expert/releases/tag/v1.1.0
[1.0.1]: https://github.com/Tissue-for-charlie/resume-expert/releases/tag/v1.0.1
[1.0.0]: https://github.com/Tissue-for-charlie/resume-expert/releases/tag/v1.0.0
