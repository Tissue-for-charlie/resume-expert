# DOCX 生成规范参考

> 本文是 SKILL.md 中 docx 生成规范的扩展，包含完整的排版参数和常见坑点修复。

## 页面设置

```
页面尺寸：A4（210mm × 297mm）= 11906 × 16838 twips
         Letter（215.9mm × 279.4mm）= 12240 × 15840 twips
页边距：0.6 inch = 864 twips（所有边统一）
```

## 字体规范

| 元素 | 中文字体 | 英文字体 | 字号 | 颜色 |
|------|---------|---------|------|------|
| 姓名 | 微软雅黑 | Arial | 16pt (32 half-pts) | #1A1A1A |
| 章节标题 | 微软雅黑 | Arial | 11pt (22 half-pts) | #1A1A1A |
| 正文 | 微软雅黑 | Arial | 9pt (18 half-pts) | #333333 |
| 副文本 | 微软雅黑 | Arial | 8.5pt (17 half-pts) | #666666 |
| 超链接 | 微软雅黑 | Arial | 继承上下文 | #2B579A |

### 中英文字体分离（关键）

所有 `TextRun` 必须显式设置 `font`：

```javascript
font: { ascii: "Arial", eastAsia: "微软雅黑" }
```

**为什么必须分离？**
- 如果不设置 `font.ascii`，英文数字会使用中文字体的回退——在 Word 中显示为微软雅黑英文字，与 Arial 的数字宽度不同，导致对齐问题
- 如果不设置 `font.eastAsia`，中文字会使用英文字体回退——导致中文渲染异常

## 高发坑点

### 1. `format: "bullet"` 在不同 docx-js 版本的差异

```javascript
// docx-js v8 及以下
format: "bullet"

// docx-js v9+（如果安装了最新版本）
format: LevelFormat.BULLET  // 需要 import { LevelFormat } from "docx"
```

> 如果报 `format "bullet" is not valid`，说明 docx-js 已升级到 v9+。改为 `LevelFormat.BULLET`。

**运行时自动检测（推荐在脚本开头执行）**：

```javascript
// 方法 1：try/catch 探测（最可靠，零副作用）
let BULLET_FORMAT;
try {
  const { LevelFormat } = require("docx");
  BULLET_FORMAT = LevelFormat.BULLET; // v9+
} catch (e) {
  BULLET_FORMAT = "bullet";           // v8 及以下
}
// 之后所有 numbering config 使用 BULLET_FORMAT 变量

// 方法 2：读 package.json 判断主版本号
const docxVersion = require("docx/package.json").version;
const BULLET_FORMAT = parseInt(docxVersion.split(".")[0]) >= 9 
  ? require("docx").LevelFormat.BULLET 
  : "bullet";
```

> 推荐方法 1——方法 2 依赖 `docx/package.json` 路径，未来版本可能变化。

### 2. Bullet 缩进

```javascript
{
  level: 0,
  format: "bullet",
  text: "•",
  alignment: AlignmentType.LEFT,
  style: {
    paragraph: {
      indent: { left: 360, hanging: 180 }  // left=缩进, hanging=悬挂缩进
    }
  }
}
```

- `left: 360`：bullet 段落的左缩进
- `hanging: 180`：悬挂缩进（bullet 符号反缩进）

### 3. ExternalHyperlink 颜色

```javascript
new ExternalHyperlink({
  children: [
    new TextRun({
      text: "🔗 作品集",
      size: 18,
      font: { ascii: "Arial", eastAsia: "微软雅黑" },
      color: "2B579A",
      underline: { type: UnderlineType.SINGLE }
    })
  ],
  link: "https://example.com"
})
```

- `ExternalHyperlink` 内部的 `TextRun` 不会自动继承文档默认样式——每个 TextRun 都需要显式设置 color 和 underline
- 忘记设置 `underline` → 链接没有下划线，用户看不出可点击

### 4. 章节底部分隔线

```javascript
border: {
  bottom: {
    style: BorderStyle.SINGLE,
    size: 1,
    color: "#CCCCCC",
    space: 4  // 线与文字之间的间距
  }
}
```

### 5. Windows Python GBK 编码

验证脚本在 Windows 上运行时，如果简历包含 emoji 或混合中英文，`print()` 会抛异常。解决方案：

```python
import sys, io
sys.stdout = io.TextIOWrapper(sys.stdout.buffer, encoding='utf-8')
```

## 文件命名

```
{姓名}_简历.docx     # 例：张三_简历.docx
{Name}_Resume.docx   # 英文
{Name}_CV.docx       # 英式
```

---

## HTML 排版的通用规范

当用户选择 HTML 格式时（或 DOCX 生成失败回退到 HTML 时），遵循以下规范：

### 页面与布局

```
纸张模拟：@media print 中设 A4 尺寸
最大宽度：700-800px（居中）
页边距：body padding 40px 20px（桌面），20px 10px（手机）
版面：线性流式单栏（ATS 兼容），禁止表格/双栏布局
```

### 字体规范

| 元素 | 推荐字体 | 字号 | 颜色 |
|------|---------|------|------|
| 姓名 | `'Noto Sans SC', '微软雅黑', sans-serif` | 36-40px | 主色 |
| 章节标题 | 同字体，加粗 | 20-22px | 主色 |
| 正文 | `'Noto Sans SC', '微软雅黑', sans-serif` | 14-15px | #333~#555 |
| 副文本 | 同字体 | 12-13px | #888~#999 |

### 样式规范

- **配色**：深底色系用金色/琥珀色点缀，浅底色系用青碧/蓝色点缀。全简历统一一套主色 + 辅色
- **分隔线**：章节标题下方 1px，颜色为主色 15-20% 透明度
- **技能标签**：圆角矩形（`border-radius: 6-8px`），背景为主色 5-10% 透明度
- **卡片**：简介框/作品卡片用浅背景 + 左边框（`border-left: 3px solid`）
- **打印样式**：必须有完整的 `@media print`，切为白底深字，隐藏渐变/阴影
- **响应式**：设置 `@media (max-width: 768px)` 断点，mobile 端纵向堆叠
- **无外链依赖**（推荐）：字体使用系统安全字体栈，无需 Google Fonts 也可正常显示

### 验证清单

1. ✅ 单文件自包含（所有 CSS 内联）
2. ✅ `@media print` 打印样式存在
3. ✅ 手机端与桌面端均正常显示
4. ✅ 无表格/双栏布局（ATS 兼容）
5. ✅ 颜色对比度满足可读性

---

## LaTeX 排版的通用规范

当用户选择 LaTeX 格式时，遵循以下规范：

### 编译环境

```
编译器：xelatex（必须）
中文支持：fontspec + xeCJK 宏包
编码：UTF-8
```

### 字体规范

| 元素 | 推荐字体 | 备注 |
|------|---------|------|
| 中文正文 | `SimSun`（宋体）或 `Source Han Serif SC`（思源宋体） | 非 Windows 系统推荐思源系列 |
| 中文标题 | `SimHei`（黑体）或 `Source Han Sans CN`（思源黑体） | 确保 Bold 权重可用 |
| 英文/数字 | `Times New Roman` 或系统默认 | — |

**关键注意**：
- 使用 `\setCJKmainfont` + `\setCJKsansfont` 分别设置中文衬线/无衬线字体
- 对于 `Source Han Serif SC` 等字体，其 Bold 权重可能是 Heavy——若缺失全角标点（括号、冒号），改用 `AutoFakeBold` 或换 `SimSun`/`SimHei`
- 编译前用 `fc-list :lang=zh` 确认系统中文字体存在

### 页面设置

```
纸张：A4（article 类 a4paper 选项）
页边距：top/bottom 1.8-2.2cm, left/right 2.2-2.8cm
行距：1.25-1.35（setspace 宏包）
```

### 内容布局

- **头部**：姓名用 `\fontsize{30-36pt}` 居中，头衔用 `\large\color{accent}`，联系方式一行
- **可量化数据用 `\textcolor{numcolor}{\bfseries}` 突出**（如播放量、粉丝数）
- **关键成就用 `\textcolor{highlight}{\bfseries}` 高亮**（如代表作品、获奖名称）
- 不用 `\sffamily` 渲染中文（Latin 字体无 CJK 字形）

### 自定义命令

推荐封装为辅助命令，保持主文档简洁：

```latex
\newcommand{\sectiontitle}[1]{
  \vspace{0.7em}%
  \noindent{\large\bfseries\color{primary} #1}\par%
  \nopagebreak\vspace{0.1em}%
  \noindent\textcolor{rulecolor}{\rule{\textwidth}{0.6pt}}\par\vspace{0.5em}%
}
\newcommand{\numhl}[1]{\textcolor{numcolor}{\bfseries #1}}
\newcommand{\hl}[1]{\textcolor{highlight}{\bfseries #1}}
```

### 验证清单

1. ✅ `xelatex` 编译无报错（`xelatex -interaction=nonstopmode`）
2. ✅ 中文字体正确渲染，无 Missing character 警告（关键标点符号）
3. ✅ 页数控制在目标范围内
4. ✅ 所有自定义命令不影响原生 LaTeX 行为
5. ✅ 单文件可编译（不依赖外部 `.sty`/`.cls` 文件）

---

## 生成后验证清单

1. ✅ 所有 TextRun 的 `font` 非 null —— 检查 XML 中 `<w:rFonts>` 属性
2. ✅ `<w:hyperlink>` 标签存在于 `word/document.xml` —— 确保链接可点击
3. ✅ Bullet 使用 numbering config 而非 unicode 符号 —— 检查 `<w:numPr>` 存在
4. ✅ 整体篇幅在目标页数内
5. ✅ 无个人信息泄露（身份证号、完整地址等）
