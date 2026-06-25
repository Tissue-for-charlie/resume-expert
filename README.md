<h1 align="center">📄 resume-expert</h1>

<p align="center">
  <strong>简历生成 · 深度评审 · 增量修改</strong> —— AI 一站式搞定
</p>

<p align="center">
  <a href="https://github.com/Tissue-for-charlie/resume-expert/blob/master/LICENSE"><img src="https://img.shields.io/badge/license-MIT-blue.svg" alt="License: MIT"></a>
  <a href="#安装"><img src="https://img.shields.io/badge/platform-Claude%20Code%20%7C%20Cursor%20%7C%20Copilot%20%7C%20ChatGPT%20%7C%20Windsurf-8A2BE2" alt="Platforms"></a>
  <a href="https://github.com/Tissue-for-charlie/resume-expert/stargazers"><img src="https://img.shields.io/github/stars/Tissue-for-charlie/resume-expert?style=social" alt="Stars"></a>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/中文-English-brightgreen" alt="Language">
  <img src="https://img.shields.io/badge/行业-14%20类-ff69b4" alt="Industries">
  <img src="https://img.shields.io/badge/职级-实习%20%7C%20校招%20%7C%20社招-orange" alt="Career Levels">
  <img src="https://img.shields.io/badge/SKILL.md-~400%20行-lightgrey" alt="Size">
</p>

---

## 这是什么？

一个 **AI Skill** —— 把 `SKILL.md` 丢进项目中，你的 AI 编程助手立刻获得简历专家的能力。自动识别意图，自动适配行业和职级，输出专业级 .docx 文件。

> 不是模板生成器。内置招聘市场知识：ATS 规则、行业×职级策略、中英文规范。

---

## 快速安装

**选择你的 AI 工具，复制对应命令，终端回车即可。**

| 工具 | 命令 |
|------|------|
| **Claude Code** | `git clone https://github.com/Tissue-for-charlie/resume-expert.git` |
| **Cursor** | `curl -o .cursorrules https://raw.githubusercontent.com/Tissue-for-charlie/resume-expert/master/SKILL.md` |
| **GitHub Copilot** | `curl -o .github/copilot-instructions.md https://raw.githubusercontent.com/Tissue-for-charlie/resume-expert/master/SKILL.md` |
| **Windsurf** | `curl -o .windsurfrules https://raw.githubusercontent.com/Tissue-for-charlie/resume-expert/master/SKILL.md` |
| **Cline / Roo Code** | `curl -o .clinerules https://raw.githubusercontent.com/Tissue-for-charlie/resume-expert/master/SKILL.md` |
| **ChatGPT Custom GPT** | 创建 GPT 时将 `SKILL.md` 粘贴到 Instructions |

装好后，对话中说"帮我做一份简历"即触发。

---

## 怎么用？

```
👤 帮我做一份简历，投字节跳动后端开发实习

🤖 📋 预扫描结果：已从你的项目和 GitHub 获取到以下信息...
   确认无误的话，我们先确定基本信息？

👤 张三，13800138000，zhangsan@example.com，北京

🤖 [逐维收集信息 → 设计结构 → 重写项目描述 → 生成 .docx]
   ✅ 简历已生成：输出文件/张三_简历.docx
```

| 你说 | AI 做什么 |
|------|-----------|
| "写简历" / "投秋招" | **生成模式** — 收集信息 → 输出 .docx |
| "帮我看一下这份简历" | **评审模式** — 四维评分 + 逐条修改建议 |
| "帮我把这段改一下" | **修改模式** — 精准替换 + 一致性检查 |

---

## 核心能力

- ✅ **行业 × 职级适配** — 14 个行业（互联网 / 金融 / 外企 / 国企 / 产品 / 设计 / 教育 / 医疗 / 法律 / 建筑 / 媒体 / 零售 / 游戏 / 政府）+ 通用策略自动推导 × 实习 / 校招 / 社招，42+ 种组合各有策略
- ✅ **ATS 兼容** — 线性布局、禁止表格双栏、关键词双写、格式避坑指南
- ✅ **项目描述重写** — 将"负责 XX 模块"转为个人实践叙事 + 量化产出
- ✅ **英文简历** — STAR 框架、按职能分类动作动词、严格一页、LinkedIn 必填
- ✅ **隐私保护** — 自动过滤身份证号、完整住址、出生日期、薪资等
- ✅ **骨架简历** — 信息不足时先生成占位版，后续逐段填充，不反复追问
- ✅ **三层回退** — docx-js → python-docx → Markdown，任一层失败自动降级
- ✅ **批量模式** — 用户想快速推进时，一次性抛出全部待确认项

---

## 可选依赖

```bash
npm install docx          # .docx 生成（核心）
pip install python-docx   # 回退生成 / 读取验证
pip install pymupdf       # PDF 文本提取
```

无需全部安装——缺失时 AI 会自动降级到 Markdown 输出或纯文本评审。

**零依赖方案**（设计师/文科用户友好）：不需要安装任何工具。在对话中直接说"输出 Markdown 版本"，AI 会产出一份格式精美的纯文本简历，复制到 Word 即可。

---

## 文件

```
resume-expert/
├── SKILL.md              # 核心调度，约 400 行
├── references/           # 细则文档
│   ├── industry-matrix.md
│   ├── ats-guide.md
│   ├── chinese-ats.md
│   ├── scoring-system.md
│   ├── rewrite-rules.md
│   ├── english-resume.md
│   ├── docx-spec.md
│   ├── privacy-ethics.md
│   └── low-info-strategies.md
├── README.md
├── LICENSE
├── CHANGELOG.md
├── CONTRIBUTING.md
├── CODE_OF_CONDUCT.md
├── .gitignore
├── .github/
│   ├── ISSUE_TEMPLATE/
│   │   ├── bug_report.md
│   │   ├── feature_request.md
│   │   └── config.yml
│   └── PULL_REQUEST_TEMPLATE.md
├── examples/
│   ├── sample-review-output.md    # 评审报告示例
│   ├── sample-skeleton-resume.md  # 骨架简历示例
│   └── sample-english-star.md     # 英文 STAR 重写示例
├── CHANGELOG.md
├── CONTRIBUTING.md

[📂 查看示例输出 →](examples/)

---

## 许可证

MIT © [Tissue-for-charlie](https://github.com/Tissue-for-charlie)
