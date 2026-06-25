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

## 生成后验证清单

1. ✅ 所有 TextRun 的 `font` 非 null —— 检查 XML 中 `<w:rFonts>` 属性
2. ✅ `<w:hyperlink>` 标签存在于 `word/document.xml` —— 确保链接可点击
3. ✅ Bullet 使用 numbering config 而非 unicode 符号 —— 检查 `<w:numPr>` 存在
4. ✅ 整体篇幅在目标页数内
5. ✅ 无个人信息泄露（身份证号、完整地址等）
