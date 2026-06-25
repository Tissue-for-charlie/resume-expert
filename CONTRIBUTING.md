# Contributing to resume-expert

感谢你考虑为这个项目做贡献！以下指南帮你快速上手。

## 如何贡献

### 报告 Bug

1. 在 [Issues](https://github.com/Tissue-for-charlie/resume-expert/issues) 中搜索，确认 bug 未被报告过
2. 使用描述性标题（如"设计岗作品集链接在头部换行异常"而不是"有 bug"）
3. 包含：**复现步骤** + **预期行为** + **实际行为** + **AI 工具名称和版本**

### 提议新功能 / 新行业

1. 先在 Issues 中描述提案，等待讨论
2. **行业矩阵扩展**是最高频的贡献方向——如果你要添加新行业，请按现有矩阵格式提供：
   - 全级别通用关注重点
   - 实习 / 校招 / 社招 三级策略
   - Step 4 改写倾斜规则
   - 评分权重调整（如适用）
3. 避免添加只有你个人需要的硬编码规则——优先扩展 `references/` 下的对应矩阵而非修改 SKILL.md 核心逻辑

### 提交 PR

1. Fork 仓库，创建 feature 分支
2. 若修改 SKILL.md，同步更新：
   - README 中的数据（行数、行业数、组合数学）
   - CHANGELOG.md 的 `[Unreleased]` 节
3. PR 标题用中文或英文皆可，描述清楚"做了什么"和"为什么"
4. 一个 PR 做一件事——不要混入无关改动

### 文档规范

- SKILL.md 是核心调度文件，保持其可读性——超过 400 行时考虑抽出独立文档到 `references/`
- 代码块指定语言（```python、```yaml、```bash）
- 表格对齐，方便纯文本阅读

## 开发环境

无需特殊环境。SKILL.md 是纯 Markdown，用任何编辑器打开即可。测试方式：加载到你的 AI 工具中，对话验证。

## 行为准则

本项目采用 [Contributor Covenant 行为准则](CODE_OF_CONDUCT.md)，参与即视为同意遵守。

## 版本策略

- 本项目遵循 [Semantic Versioning](https://semver.org/lang/zh-CN/)（主版本.次版本.修订号）
- **主版本号**：不兼容的 API/规则变更（如约束规则重新编号、核心工作流重组）
- **次版本号**：向后兼容的新功能（如新增行业、新增模式、新增 FAQ）
- **修订号**：文档勘误、排版修复、不涉及逻辑变更的增补
- `SKILL.md` 的 `version` frontmatter 字段与 git tag 保持同步
- 每个发布的版本在 CHANGELOG.md 中按 [Keep a Changelog](https://keepachangelog.com/zh-CN/1.1.0/) 格式记录

## 开发流程

### 如何验证你的修改

由于本项目是 AI Skill（纯文本 Markdown），"测试"不是跑自动化脚本，而是**在 AI 工具中验证行为**：

1. **加载修改后的 SKILL.md** 到你的 AI 工具中（Claude Code 直接放在项目根目录，其他工具见 README 安装说明）
2. **对话验证**：构造一个覆盖你改动路径的对话场景，确认 AI 行为符合预期。例如：
   - 修改了行业矩阵 → 用该行业的模拟用户对话测试
   - 修改了约束规则 → 构造会触发该规则的场景验证
   - 修改了 docx 生成规则 → 实际生成一份 .docx 检查
3. **回归检查**：确保你的改动没有破坏已有功能。至少验证：
   - 默认流程（从零生成 → 收集信息 → 结构设计 → 生成 .docx）仍能走通
   - 评审模式（给一份简历 → 四维评分 + 修改建议）仍正常
   - 增量修改（改一段经历 → 一致性检查）仍正常

### 提交前检查清单

- [ ] SKILL.md 行数是否控制在合理范围（当前 ~400 行，目标 ≤450）？如果新增内容超过 50 行，是否应考虑抽出到 `references/` 下？
- [ ] 如果新增了行业，是否同时更新了评分权重映射表（`references/scoring-system.md`）和改写倾斜列表（`references/industry-matrix.md`）？
- [ ] 如果修改了约束规则编号（F1-F3 / C1-C3 / T1），是否全文搜索并更新了所有引用处？
- [ ] 是否运行了隐私信息泄露检查（`grep` 真实姓名/电话/邮箱）？
- [ ] 是否更新了 CHANGELOG.md 的 `[Unreleased]` 节？
- [ ] 如果修改了 SKILL.md 的 frontmatter `version`，是否与计划发布的版本号一致？
- [ ] 是否在至少一种 AI 工具中进行了对话验证（Claude Code / Cursor / Copilot / ChatGPT 其中之一）？
