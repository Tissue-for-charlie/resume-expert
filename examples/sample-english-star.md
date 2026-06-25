# 示例：英文简历生成（STAR 框架输出）

以下是一份英文简历中某段项目经历的 STAR 框架重写对照——展示 Skill 自动切换英文模式后的输出质量。

> **场景**：用户选择英文简历，目标为海外科技公司 SDE 实习

---

## 👤 用户提供的原始描述

> I worked on a campus e-commerce platform project. Used React, Node.js, MongoDB. Did the frontend pages and some backend APIs. The project was for a course.

---

## 🤖 AI 重写后的 STAR 版本

**Campus E-Commerce Platform** · React, Node.js, MongoDB
*Jul 2025 – Oct 2025*

- Engineered a full-stack marketplace connecting 300+ students across 12 dormitory buildings, reducing offline transaction friction by consolidating listings into a single searchable interface
- Built the React frontend with 14 responsive views (listing, checkout, chat, order tracking) and the Node.js REST API backend serving 8 endpoints, handling 200+ concurrent sessions during peak course registration period
- Implemented real-time in-app messaging with Socket.io, replacing a previously WeChat-based communication flow that caused 40% of deals to fall through due to delayed responses
- Designed MongoDB schema with compound indexes on `category + price` and `seller + status`, reducing average listing query time from 600ms to under 80ms

---

## 对照点评

| 原文问题 | STAR 修复 | 效果 |
|----------|-----------|------|
| "I worked on" | 省略主语，直用 Engineered/Built/Implemented/Designed | 主动动词开头，符合英文简历规范 |
| "Used React, Node.js" | 技术名词融入叙事 | ATS 在上下文中识别关键词，匹配权重更高 |
| "for a course" | 补充 300+ students / 14 views / 200+ concurrent 等数据 | 课程项目也能量化，不因"只是作业"而显得空洞 |
| 无结果 | 每条 bullet 结尾都有量化结果（40% deal failure reduction, 600ms → 80ms） | 满足 STAR 框架的 R（Result）要素 |
| 4 条 bullet 用不同动词开头 | Engineered → Built → Implemented → Designed | 避免动词重复，面试官不会审美疲劳 |

---

> 📖 完整英文简历规则见 [`references/english-resume.md`](../references/english-resume.md)
