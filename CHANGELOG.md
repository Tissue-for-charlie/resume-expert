# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [1.3.0] - 2026-06-25

### Added

- **新增模式 D：JD 匹配度扫描** — 对标具体目标岗位 JD 的命中率分析，填补 HR 视角下"对标 JD"评估的空白
  - **JD 深度解析**：三层信息提取（硬性要求 Must-have / 加分项 Nice-to-have / 隐性要求 Implicit），含经验区间解析、能力等级映射（了解 < 熟悉 < 精通）、关键词归一化表
  - **五维匹配度评分**：硬性门槛(30) + 关键词覆盖(25) + 经验匹配(20) + 资质匹配(15) + 加分项覆盖(10)，14 个行业各有独立权重映射
  - **红旗检测**：5 类必查红旗（学历不达标 / 经验不足 / 必备证书缺失 / 必备技术栈缺失 / 时间线冲突）+ 3 类软红旗，每触发 1 项硬性红旗扣 10 分
  - **优化建议生成**：缺失关键词按优先级建议补齐方式（受 C1 不虚构原则约束——严禁建议编造）
  - **报告输出**：标准六部分报告 / 极简三行版 / 无 JD 引导提示三种模式
  - **模式联动**：模式 A → D（生成后追加简版报告）/ 模式 B → D（不重复评分）/ 模式 D → C（按红旗→缺失关键词→加分项优先级修改）
  - **竞争水位估计**：基于 JD 公开薪资范围 + 公司类型估计市场竞争激烈度
- **新文件** `references/jd-matching.md`：JD 匹配度扫描完整规范——JD 解析规则、能力等级映射全表、行业权重映射、关键词归一化表、优化建议模板、报告格式示例
- **触发条件扩展**：新增 "JD 匹配" / "匹配度" / "岗位匹配" / "这个 JD 我能投吗" / "match this JD" 等触发词；附带 JD 文本（招聘链接 / 描述原文）并提到"看看" / "匹配" / "评估"也触发
- **模式路由规则**：触发后自动路由到模式 A/B/C/D
- **FAQ 扩展**：Q8 解释模式 B 与模式 D 的边界；Q9 说明模式 D 受 C1 不虚构原则约束

### Changed

- **模式切换规则扩展**：新增模式 D 相关 5 条切换路径（A→D / B→D / C→D / D→C / D→A）
- **references/ 索引表**：新增 `jd-matching.md` 条目
- **`scoring-system.md` 新增边界章节**：明确模式 B（行业基准评分）与模式 D（JD 匹配度扫描）的评估标尺、输入要求、评分维度、输出形式、HR 视角差异，及 B→D 衔接规则（不重复评分）
- **README 更新**：版本徽章 1.2.0 → 1.3.0；references 计数 10 → 11；SKILL.md 行数徽章 ~400 → ~500；新增 JD 匹配模式用法示例和核心能力条目
- **SKILL.md frontmatter**：版本 1.2.0 → 1.3.0，description 新增"JD 匹配度扫描"描述

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

## [1.2.0] - 2026-06-25

### Added

- **评分金标准测试集 (Golden Test Set) 重大扩展**：`references/scoring-golden-tests.md` — 从 6 份扩展到 **70 份**经人工专家评分的校准简历，**14 行业 × 5 分数段全覆盖**（90-100/75-89/60-74/40-59/<40），用于验证 AI 评分一致性
- **🌐 互联网实时搜索增强**：评分前校准流程新增 Web 搜索增强步骤——可选搜索目标行业当前市场数据（JD 关键词趋势、薪资报告、竞争格局）来动态校准评分和基准中位数
- 14 个行业新增 cases 的简历内容均参考 2025-2026 年互联网公开数据（RGF 薪酬观察、智联春招周报、脉脉高聘报告）编写，标注"🌐 Web 搜索校准"
- `scoring-system.md` 评分前校准流程新增步骤 5（Web 搜索增强）+ 搜索 query 模板
- 70 份 cases 按分数段分为 5 个区（90-100/75-89/60-74/40-59/<40），每区 14 个行业各一份

### Changed

- `scoring-golden-tests.md` 结构重构：从平铺 → 按分数段分区，新增 14×5 全量汇总矩阵
- SKILL.md 评分前校准指引更新（1-2 个 → 2-3 个用例，新增 Web 搜索增强说明）
- README 核心能力列表 golden tests 描述更新（6 份 → 70 份）
- SKILL.md references/ 索引表 golden tests 条目更新
- CONTRIBUTING.md 提交前检查清单 golden test 条目更新（14 行业全覆盖）

[1.3.0]: https://github.com/Tissue-for-charlie/resume-expert/releases/tag/v1.3.0
[1.2.0]: https://github.com/Tissue-for-charlie/resume-expert/releases/tag/v1.2.0
[1.1.0]: https://github.com/Tissue-for-charlie/resume-expert/releases/tag/v1.1.0
[1.0.1]: https://github.com/Tissue-for-charlie/resume-expert/releases/tag/v1.0.1
[1.0.0]: https://github.com/Tissue-for-charlie/resume-expert/releases/tag/v1.0.0
