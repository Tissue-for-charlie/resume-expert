<h1 align="center">📄 resume-expert</h1>

<p align="center">
  <strong>简历生成 · 深度评审 · 增量修改</strong> —— AI 一站式搞定
</p>

<p align="center">
  <a href="https://github.com/Tissue-for-charlie/resume-expert/blob/master/LICENSE"><img src="https://img.shields.io/badge/license-MIT-blue.svg" alt="License: MIT"></a>
  <a href="https://github.com/Tissue-for-charlie/resume-expert/releases"><img src="https://img.shields.io/badge/version-1.5.0-blue" alt="Version"></a>
  <a href="#安装"><img src="https://img.shields.io/badge/platform-Claude%20Code%20%7C%20Cursor%20%7C%20Copilot%20%7C%20ChatGPT%20%7C%20Windsurf-8A2BE2" alt="Platforms"></a>
  <a href="https://github.com/Tissue-for-charlie/resume-expert/stargazers"><img src="https://img.shields.io/github/stars/Tissue-for-charlie/resume-expert?style=social" alt="Stars"></a>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/中文-English-brightgreen" alt="Language">
  <img src="https://img.shields.io/badge/行业-15%20类-ff69b4" alt="Industries">
  <img src="https://img.shields.io/badge/职级-实习%20%7C%20校招%20%7C%20社招-orange" alt="Career Levels">
  <img src="https://img.shields.io/badge/格式-DOCX%20%7C%20HTML%20%7C%20LaTeX%20%7C%20Markdown-blue" alt="Formats">
  <img src="https://img.shields.io/badge/references-12%20文件-blue" alt="References">
  <img src="https://img.shields.io/badge/SKILL.md-~700%20行-lightgrey" alt="Size">
</p>

---

## 这是什么？

一个 **AI Skill** —— 把 `SKILL.md` 丢进项目中，你的 AI 编程助手立刻获得简历专家的能力。自动识别意图，自动适配行业和职级，支持 DOCX / HTML / LaTeX / Markdown 多格式输出，内置内容质量自检机制，并支持针对目标岗位 JD 做匹配度扫描。

> 不是模板生成器。内置招聘市场知识：ATS 规则、行业×职级策略、JD 命中率分析、多格式排版规范、内容自检。

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
| "这个 JD 我能投吗" + JD 文本 | **JD 匹配模式** — 五维匹配度 + 红旗检测 + 优化建议 |
| "面试会问什么" / "准备面试" | **面试预测模式** — 简历信号提取 + Web 搜索面经 + 生成可交互 HTML Q&A |

```
👤 帮我看一下这份简历

🤖 📊 总分：65 / 100
    📊 同岗位对比：您的得分 65 | 同岗位中位数 58 | 前 25% 门槛 68
    → 您处于中上水平，距前 25% 还差 3 分。建议聚焦关键词覆盖。
    
    🔴 必须改：2 项 — 项目描述无量化数据、技能关键词缺失
    🟡 建议改：3 项 — 弱动词过多、bullet 密度失衡...
    📄 页数评估：1 页 ✓
```

```
👤 看看这份简历和这个 JD 匹配度（附 JD 文本）

🤖 📊 JD 匹配度报告
    🎯 目标岗位：字节跳动 - 后端开发工程师
    📈 总匹配度：72 / 100（中上匹配，建议小修后投）
    
    📊 五维得分：
       硬性门槛     24/25 ✓
       关键词覆盖   18/25 ⚠️
       经验匹配    15/20 ✓
       资质匹配    12/15 ✓
       加分项覆盖   3/15 ❌
    
    🚩 红旗（1 项）：必备技术栈缺失 — Kafka（JD 要求"熟悉"）
    
    📋 关键词清单：
       ✓ 命中：Spring Boot, MySQL, Redis, 微服务, Docker
       ✗ 缺失：Kafka, ELK
    
    💡 优化建议：
       1. 🔴 评估项目 Y 中能否补充 Kafka 使用场景
       2. 🟡 技能区补齐 ELK 监控栈关键词
       3. 🟢 加分项"开源贡献"移至技能区单独标注
```

---

## 核心能力

- ✅ **行业 × 职级适配** — 15 个行业（互联网 / 金融 / 外企 / 国企 / 产品 / 设计 / 教育 / 医疗 / 法律 / 建筑 / 媒体 / **娱乐/演艺** / 零售 / 游戏 / 政府）+ 通用策略自动推导 × 实习 / 校招 / 社招，45+ 种组合各有策略
- ✅ **ATS 兼容** — 线性布局、禁止表格双栏、关键词双写、格式避坑指南。**中国 ATS 专项**：北森 / Moka / 大易适配
- ✅ **同岗位基准对比** — 评分后自动对比同行业同职级中位数，帮用户定位竞争水位。**金标准评分测试集**：75 份校准简历（15 行业 × 5 分数段全覆盖）+ Web 搜索增强
- ✅ **JD 匹配度扫描** 🆕 — 对标具体岗位 JD 的命中率分析：五维评分（硬性门槛 / 关键词覆盖 / 经验匹配 / 资质匹配 / 加分项覆盖）+ 红旗检测（必备项缺失 / 经验不足 / 学历不达标）+ 优化建议（按优先级补齐缺失关键词，受 C1 不虚构原则约束）
- ✅ **面试预测与 Q&A 生成** 🆕 — 基于简历内容预测面试官高频追问（6 类问题：技术深度 / 量化数据 / 行为面试 / 行业认知 / 弱势因素 / 反向提问）+ Web 搜索面经增强 + 生成可交互 HTML Q&A（离线自包含、移动端适配、掌握度标记）
- ✅ **弱势群体专项策略** 🆕 — 自动检测空窗期 / 双非背景 / 大龄求职者三类候选人，应用差异化简历策略 + 面试话术模板 + 投递路径建议
- ✅ **项目描述重写** — 将"负责 XX 模块"转为个人实践叙事 + 量化产出
- ✅ **英文简历** — STAR 框架、按职能分类动作动词、严格一页、LinkedIn 必填
- ✅ **多格式输出** — 支持 DOCX（ATS 优先）、HTML（网页/打印）、LaTeX（学术/精确排版）、Markdown（零依赖保底），任选格式
- ✅ **内容质量自检** — 生成后自动检查联系方式完整性、量化数据覆盖、荣誉奖项/代表作缺失等，确保内容完备
- ✅ **隐私保护** — 自动过滤身份证号、完整住址、出生日期、薪资等（参考 PIPL / GDPR）
- ✅ **骨架简历** — 信息不足时先生成占位版，后续逐段填充，不反复追问
- ✅ **四层回退** — docx-js → python-docx → HTML/LaTeX → Markdown，任一层失败自动降级
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
│   ├── industry-matrix.md      #   行业×职级全量策略（15 行业）+ 改写倾斜
│   ├── scoring-system.md       #   评分权重表 + 分数锚点 + 基准对比 + 五维评分（娱乐/媒体）
│   ├── scoring-golden-tests.md #   评分金标准测试集（75 份校准简历）
│   ├── jd-matching.md          #   JD 匹配度扫描（五维评分 + 红旗检测 + 优化建议）
│   ├── interview-prediction.md #   面试预测（6 类问题 + Web 搜索 + 可交互 HTML Q&A 模板）
│   ├── rewrite-rules.md        #   描述重写规则 + STAR 框架 + 动词库（含表演/音乐分类）
│   ├── ats-guide.md            #   ATS 工作原理 + JD 逆向工程
│   ├── chinese-ats.md          #   北森 / Moka / 大易专项适配
│   ├── english-resume.md       #   英文简历实战示例 + 常见错误
│   ├── docx-spec.md            #   排版参数大全（DOCX / HTML / LaTeX）+ 坑点
│   ├── privacy-ethics.md       #   不虚构原则 + 隐私清单 + PIPL/GDPR
│   └── low-info-strategies.md #   极简输入策略 + 低年级/转行 + 空窗期/双非/大龄专项
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
