# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [1.5.0] - 2026-06-25

### Added

- **新增模式 E：面试预测与 Q&A 生成** — 基于简历内容预测面试官高频追问，让候选人在投递前准备面试，填补"简历通过筛选但面试翻车"的空白
  - **简历信号提取**：6 类信号（项目深挖 / 技能等级 / 时间线 / 量化数据 / 职业轨迹 / 差异化），按强度 🔴🟡🟢 分级
  - **6 类问题生成**：技术深度追问（3-4 层深度）/ 量化数据追问 / 行为面试（STAR）/ 行业认知 / 弱势因素追问 / 反向提问准备
  - **Web 搜索增强**：5 类搜索（目标公司面经 / 岗位通用题 / 技术热点 / 行业趋势 / JD 对标），不可用时回退到内置题库
  - **可交互 HTML Q&A**：单文件自包含（CSS/JS 内联，可离线）、移动端适配、折叠展开 / 掌握度标记 / 搜索过滤 / localStorage 存储 / 导出 Markdown
  - **答案区设计**：建议回答方向（结论→论据→数据框架，不生成完整标准答案避免背诵）+ 简历相关内容引用 + 避免陷阱提示
  - **高风险预警**：简历超出理解深度 / 量化数据无法解释 / 弱势因素未处理 / 技术栈与行业热点脱节
  - **模式联动**：B→E（复用简历文本）/ D→E（叠加 JD 信号）/ A→E（评估翻车风险）/ E→C（高风险项建议修改简历）
  - **伦理约束**：受 C1 不虚构原则约束——预测问题的目的是帮候选人准备真实经历的表达，不是教他编造答案
- **新文件** `references/interview-prediction.md`：面试预测完整规范——信号提取规则、6 类问题生成逻辑、Web 搜索策略、HTML Q&A 模板、高风险预警、模式联动规则
- **触发条件扩展**：新增 "面试预测" / "面试题" / "面试会问什么" / "准备面试" / "面试官会怎么问" / "面试会翻车吗" / "模拟面试" 等触发词
- **模式切换规则扩展**：新增模式 E 相关 4 条切换路径（A→E / B→E / D→E / E→C）
- **FAQ 扩展**：Q10 说明模式 E 不教背标准答案；Q11 说明 HTML 文件离线可用；Q12 弱势群体专项策略说明

### Changed

- **补齐 1.4.0 遗漏的 SKILL.md 同步**（1.4.0 已在 references/README/CHANGELOG 声明但 SKILL.md 未实际更新）：
  - SKILL.md frontmatter 版本 1.3.0 → 1.5.0，description 补"15 个行业"+"模式 E 面试预测"+"多格式输出"+"内容质量自检"
  - SKILL.md 行业矩阵表补娱乐/演艺行（14 → 15 行业）
  - SKILL.md 模式 B Step 2 补五维评分变体说明（娱乐/演艺/媒体专用）
  - SKILL.md 模式 A Step 5 从"生成 DOCX"扩展为"多格式输出"分支表（DOCX/HTML/LaTeX/Markdown）
  - SKILL.md 模式 A Step 6 新增内容质量自检 6 项（联系方式完整性 / 荣誉奖项为空 / 代表作品为空 / 量化数据覆盖 / 量化数据一致性 / 硬性成就遗漏）
  - SKILL.md Phase 0 新增"空目录快速判定"
  - SKILL.md 模式 A Step 2 新增"行业感知信息收集"和"联系方式字段行业自适应"
  - SKILL.md Step 3 行业差异化结构 4 → 5 行（补娱乐/演艺）
  - SKILL.md T1 约束从"docx 输出规范"扩展到"多格式输出规范"
  - SKILL.md Step 7 回退链扩展：docx-js → python-docx → HTML → LaTeX → Markdown
  - SKILL.md references/ 索引表 4 处更新（scoring-system 补五维评分 / scoring-golden-tests 70→75 份 14→15 行业 / rewrite-rules 补表演动词库 / docx-spec 补 HTML/LaTeX）
  - SKILL.md 各处行业计数 14 → 15
- **`references/jd-matching.md` 行业权重映射表补娱乐/演艺行**：硬性门槛 25 / 关键词覆盖 20 / 经验匹配 15 / 资质匹配 20 / 加分项覆盖 20，与 scoring-system.md 五维评分体系对齐
- README 版本徽章 v1.4.0 → v1.5.0

## [1.4.0] - 2026-06-25

### Added

- **新增行业：娱乐/演艺** — 15 个内置行业（原 14 + 娱乐/演艺）。覆盖歌手/演员/音乐人/艺人等角色，包含独立模块布局（影响力数据→代表作品→荣誉奖项→演出经历）和改写倾斜规则
- **多格式输出支持** — Step 5 扩展为格式选择分支：
  - **DOCX**（默认）：docx-js 生成，原有规范不变
  - **HTML**：新增完整排版规范（CSS 内联、`@media print`、响应式、线性布局）
  - **LaTeX**：新增完整排版规范（xelatex + xeCJK、字体配置、标点避坑、自定义命令）
  - **Markdown**：最终保底
  - 回退链扩展：`docx-js → python-docx → HTML → LaTeX → Markdown`
- **内容质量自检机制** — Step 6 新增 6 项自动检查：联系方式完整性、荣誉奖项为空、代表作品为空、量化数据覆盖、量化数据一致性、硬性成就遗漏。全格式适用
- **Phase 0 空目录快速判定** — 检测到当前目录为空且用户未提供简历文本时，跳过所有本地/GitHub/依赖扫描，直接进入 Step 1
- **行业感知信息收集** — 模式 A Step 2 各维度内容按行业自适应：娱乐/演艺行业追问社交/流媒体平台账号；项目经历替换为演出/项目经历；竞赛/证书替换为荣誉奖项/证书；作品/博客替换为代表作品/作品集
- **联系方式字段行业自适应** — Step 2-1 基本信息联系方式字段按行业类型追问不同平台：技术行业追问 GitHub/LinkedIn；娱乐行业追问微博/流媒体/短视频；设计行业追问作品集平台
- **五维评分框架（娱乐/媒体行业）** — `references/scoring-system.md` 新增五维评分变体：内容质量(30) + 排版可读性(20) + 影响力数据(20) + 关键词覆盖(10) + 差异化定位(20)
- **表演/音乐动词库** — `references/rewrite-rules.md` 新增英文表演类动作动词（Performed/Headlined/Composed/Toured 等）和中文表演类动词表（献唱/巡演/录制/编曲/统筹等）
- **HTML/LaTeX 排版规范** — `references/docx-spec.md` 新增完整 HTML 和 LaTeX 输出规范，含字体表、布局参数、验证清单

### Changed

- SKILL.md 行业矩阵表新增娱乐/演艺行，矩阵行数 14 → 15
- SKILL.md 行业差异化结构新增娱乐/演艺（5 个差异最大行业）
- SKILL.md T1 约束从"docx 输出规范"扩展到"多格式输出规范"
- SKILL.md references/ 索引表更新：industry-matrix.md（15 行业）、scoring-golden-tests.md（14→15 行业，70→75 份）、scoring-system.md（15 行业+五维评分）、rewrite-rules.md（表演动词库）、docx-spec.md（HTML/LaTeX 规范）
- 各文件行业计数引用 14 → 15
- README 版本徽章 v1.3.0 → v1.4.0，行业计数 14 → 15，新增格式徽章（DOCX/HTML/LaTeX/Markdown）
- CONTRIBUTING.md 行业计数 14 → 15

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

[1.5.0]: https://github.com/Tissue-for-charlie/resume-expert/releases/tag/v1.5.0
[1.4.0]: https://github.com/Tissue-for-charlie/resume-expert/releases/tag/v1.4.0
[1.3.0]: https://github.com/Tissue-for-charlie/resume-expert/releases/tag/v1.3.0
[1.2.0]: https://github.com/Tissue-for-charlie/resume-expert/releases/tag/v1.2.0
[1.1.0]: https://github.com/Tissue-for-charlie/resume-expert/releases/tag/v1.1.0
[1.0.1]: https://github.com/Tissue-for-charlie/resume-expert/releases/tag/v1.0.1
[1.0.0]: https://github.com/Tissue-for-charlie/resume-expert/releases/tag/v1.0.0
