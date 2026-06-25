<h1 align="center">📄 resume-expert</h1>

<p align="center">
  <strong>简历生成 · 深度评审 · 增量修改</strong> —— AI 一站式搞定
</p>

<p align="center">
  <a href="https://github.com/Tissue-for-charlie/resume-expert/blob/master/LICENSE"><img src="https://img.shields.io/badge/license-MIT-blue.svg" alt="License: MIT"></a>
  <a href="https://github.com/Tissue-for-charlie/resume-expert/releases"><img src="https://img.shields.io/badge/version-1.1.0-blue" alt="Version"></a>
  <a href="#安装"><img src="https://img.shields.io/badge/platform-Claude%20Code%20%7C%20Cursor%20%7C%20Copilot%20%7C%20ChatGPT%20%7C%20Windsurf-8A2BE2" alt="Platforms"></a>
  <a href="https://github.com/Tissue-for-charlie/resume-expert/stargazers"><img src="https://img.shields.io/github/stars/Tissue-for-charlie/resume-expert?style=social" alt="Stars"></a>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/中文-English-brightgreen" alt="Language">
  <img src="https://img.shields.io/badge/行业-14%20类-ff69b4" alt="Industries">
  <img src="https://img.shields.io/badge/职级-实习%20%7C%20校招%20%7C%20社招-orange" alt="Career Levels">
  <img src="https://img.shields.io/badge/references-10%20文件-blue" alt="References">
  <img src="https://img.shields.io/badge/SKILL.md-~400%20行-lightgrey" alt="Size">
</p>

---

## 这是什么？

一个 **AI Skill** —— 把 `SKILL.md` 丢进项目中，你的 AI 编程助手立刻获得简历专家的能力。自动识别意图，自动适配行业和职级，输出专业级 .docx 文件。

> 不是模板生成器。内置招聘市场知识：ATS 规则、行业×职级策略、中英文规范。

---

## 快速安装

**推荐：克隆完整仓库**（含 `references/` 细则文档和示例）

```bash
git clone https://github.com/Tissue-for-charlie/resume-expert.git
```

**或者只下载核心文件**（SKILL.md 自包含所有核心逻辑，`references/` 为可选深度阅读）

| 工具 | 命令 |
|------|------|
| **Claude Code** | `git clone https://github.com/Tissue-for-charlie/resume-expert.git` |
| **Cursor** | `curl -o .cursorrules https://raw.githubusercontent.com/Tissue-for-charlie/resume-expert/master/SKILL.md` |
| **GitHub Copilot** | `curl -o .github/copilot-instructions.md https://raw.githubusercontent.com/Tissue-for-charlie/resume-expert/master/SKILL.md` |
| **Windsurf** | `curl -o .windsurfrules https://raw.githubusercontent.com/Tissue-for-charlie/resume-expert/master/SKILL.md` |
| **Cline / Roo Code** | `curl -o .clinerules https://raw.githubusercontent.com/Tissue-for-charlie/resume-expert/master/SKILL.md` |
| **ChatGPT Custom GPT** | 创建 GPT 时将 `SKILL.md` 粘贴到 Instructions |

> ⚠️ Cursor / Copilot / Windsurf / ChatGPT 用户：只用 `curl` 下载 SKILL.md 单文件即可正常使用全部功能——核心规则（行业矩阵、ATS 避坑、评分体系、重写策略）都在里面。`references/` 目录是可选的深度参考资料，AI 需要时会提示你查看，但不影响正常使用。当然，直接 `git clone` 体验最完整。

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
| "帮我看一下这份简历" | **评审模式** — 四维评分 + 基准对比 + 逐条修改建议 |
| "帮我把这段改一下" | **修改模式** — 精准替换 + 一致性检查 |

```
👤 帮我看一下这份简历

🤖 📊 总分：65 / 100
    📊 同岗位对比：您的得分 65 | 同岗位中位数 58 | 前 25% 门槛 68
    → 您处于中上水平，距前 25% 还差 3 分。建议聚焦关键词覆盖。
    
    🔴 必须改：2 项 — 项目描述无量化数据、技能关键词缺失
    🟡 建议改：3 项 — 弱动词过多、bullet 密度失衡...
    📄 页数评估：1 页 ✓
```

---

## 核心能力

- ✅ **行业 × 职级适配** — 14 个行业（互联网 / 金融 / 外企 / 国企 / 产品 / 设计 / 教育 / 医疗 / 法律 / 建筑 / 媒体 / 零售 / 游戏 / 政府）+ 通用策略自动推导 × 实习 / 校招 / 社招，42+ 种组合各有策略
- ✅ **ATS 兼容** — 线性布局、禁止表格双栏、关键词双写、格式避坑指南。🆕 **中国 ATS 专项**：北森 / Moka / 大易适配
- ✅ **同岗位基准对比** — 评分后自动对比同行业同职级中位数，帮用户定位竞争水位。🆕 **金标准评分测试集**：70 份校准简历（14 行业 × 5 分数段全覆盖）+ Web 搜索增强
- ✅ **项目描述重写** — 将"负责 XX 模块"转为个人实践叙事 + 量化产出
- ✅ **英文简历** — STAR 框架、按职能分类动作动词、严格一页、LinkedIn 必填
- ✅ **隐私保护** — 自动过滤身份证号、完整住址、出生日期、薪资等（参考 PIPL / GDPR）
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
├── SKILL.md                    # 核心调度，自包含全部逻辑
├── references/                 # 可选深度阅读（不影响 SKILL.md 独立使用）
│   ├── industry-matrix.md      #   行业×职级全量策略 + 改写倾斜
│   ├── scoring-system.md       #   评分权重表 + 分数锚点 + 基准对比
│   ├── scoring-golden-tests.md  #   🆕 评分金标准测试集（6 份校准简历）
│   ├── rewrite-rules.md        #   描述重写规则 + STAR 框架 + 动词库
│   ├── ats-guide.md            #   ATS 工作原理 + JD 逆向工程
│   ├── chinese-ats.md          #   北森 / Moka / 大易专项适配
│   ├── english-resume.md       #   英文简历实战示例 + 常见错误
│   ├── docx-spec.md            #   排版参数 + bullet 版本检测 + 坑点
│   ├── privacy-ethics.md       #   不虚构原则 + 隐私清单 + PIPL/GDPR
│   └── low-info-strategies.md  #   极简输入策略 + 低年级/转行指南
├── examples/                   # 示例输出
│   ├── sample-review-output.md
│   ├── sample-skeleton-resume.md
│   └── sample-english-star.md
├── .github/                    # Issue/PR 模板
├── README.md
├── LICENSE
├── CHANGELOG.md
├── CONTRIBUTING.md
└── CODE_OF_CONDUCT.md
```

[📂 查看示例输出 →](examples/)

---

## 许可证

MIT © [Tissue-for-charlie](https://github.com/Tissue-for-charlie)
