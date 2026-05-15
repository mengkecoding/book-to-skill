# book-to-skill

[English](./README.md)

从书籍文件中提炼知识，生成可复用的 AI 助手指令集。支持 Claude Code、Trae、Cursor、Windsurf、Hermes Agent。

[![Hermes Skill](https://img.shields.io/badge/Hermes-Skill-blue)](https://hermes-agent.nousresearch.com)
[![Version](https://img.shields.io/badge/version-1.1.0-green)]()

## 这是什么

`book-to-skill` 把一本书（PDF / EPUB / Markdown / TXT）读进去，提炼出可复用的思维框架，生成各平台立即可用的 AI 助手指令集——Claude Code 的 `CLAUDE.md`、Cursor 的 `.cursorrules`、Trae 规则、或 Hermes Agent Skill。

## 支持的书类型

| 类型 | 代表 | 生成的 Skill 类型 |
|------|------|-------------------|
| 技术书 / 方法论 | *Pro Git*、*重构*、*DDIA* | 工具手册 / 操作规范 / 实战+顾问 |
| 小说 / 传记 / 思想书 | *1984*、*反脆弱* | 决策框架 / 响应协议 |

## 示例

**输入**：乔治·奥威尔《1984》
**输出**：**doublethink-detection** —— 识别信息控制、叙事操纵与正统思想压制的批判性思维框架。包含 5 个思维模型（双重思想、鸭话、思想罪、忘怀洞、二加二等于四）和完整的决策框架。

## 工作流

```
0. 前置判断（这本书适合吗？）
1. 读取 & 分析（转换 → 目录 → 类型判断）
2. 提炼核心（统一入口 + 类型专属章节）
3. 生成输出文件
4. 质量验证（7 项 checklist）
5. Self-test（书中真实场景验证）
6. 交付 → 用户确认
```

## 模式

- **审查模式**（默认）：每阶段暂停，用户审核确认
- **快速模式**：一口气生成，只在最终交付时暂停

## 平台适配

| 文件 | 平台 |
|------|------|
| `SKILL.md` | Hermes Agent（完整版） |
| `CLAUDE.md` | Claude Code |
| `.cursorrules` | Cursor |
| `trae-rule.md` | Trae |
| `.windsurfrules` | Windsurf |

## 安装

```bash
# Hermes Agent
cp -r book-to-skill ~/.hermes/skills/software-development/

# Claude Code / Cursor / Windsurf
# 将适配文件复制到项目根目录

# Trae
# 设置 → Rules 中导入 trae-rule.md
```

## 依赖

- Python 3（用于 EPUB 转换）
- pdftotext / poppler-utils（用于 PDF 转换）

```bash
# Debian/Ubuntu
sudo apt install poppler-utils

# macOS
brew install poppler
```

## 使用

在 AI 助手中说：

> 把这本书生成一个指令集：/path/to/book.pdf

支持格式：`.pdf` `.epub` `.md` `.txt`

## License

MIT
