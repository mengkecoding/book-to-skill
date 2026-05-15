# book-to-skill · 从书中提炼 AI 指令集

Extract reusable AI instructions from books. Supports Claude Code, Trae, Cursor, Windsurf, and Hermes Agent.

[![Hermes Skill](https://img.shields.io/badge/Hermes-Skill-blue)](https://hermes-agent.nousresearch.com)
[![Version](https://img.shields.io/badge/version-1.1.0-green)]()

---

## What is this · 这是什么

`book-to-skill` reads a book (PDF / EPUB / Markdown / TXT), extracts its knowledge, and generates deployable instructions for AI coding assistants — a Claude Code CLAUDE.md, a Cursor `.cursorrules`, a Trae rule, or a Hermes Agent Skill.

`book-to-skill` 把一本书读进去，提炼出可复用的思维框架，生成各平台立即可用的 AI 助手指令集。

## Supported Book Types · 支持的书类型

| Type | Examples | Output Skill Type |
|------|----------|-------------------|
| Tech / Methodology | *Pro Git*, *Refactoring*, *DDIA* | Tool Manual / Procedural / Hands-on Advisor |
| Fiction / Biography / Philosophy | *1984*, *Antifragile*, *The Art of War* | Decision Framework / Response Protocol |

## Example · 示例

Input: George Orwell's *1984*
↓
Output: **doublethink-detection** — a critical thinking framework that identifies information control, narrative manipulation, and orthodoxy suppression. Contains 5 mental models (Doublethink, Duckspeak, Thoughtcrime, Memory Hole, 2+2=4) and a complete decision framework.

输入《1984》→ 输出 **doublethink-detection**：识别信息控制、叙事操纵与正统思想压制，包含 5 个思维模型和决策框架。

## Workflow · 工作流

```
0. Pre-check (is this book suitable?)
   ↓
1. Read & Analyze (convert → TOC → classify)
   ↓
2. Extract core (unified entry + type-specific sections)
   ↓
3. Generate output → write to file
   ↓
4. Quality verification (7-item checklist)
   ↓
5. Self-test (real scenario from the book)
   ↓
6. Deliver → user confirmation
```

## Modes · 模式

- **Review mode** (default): pause at each stage for user approval
- **Quick mode**: full auto, pause only on final delivery

- **审查模式**（默认）：每阶段暂停确认
- **快速模式**：一气呵成，最终确认

## Platform Adapters · 平台适配

| File | Platform |
|------|----------|
| `SKILL.md` | Hermes Agent (full version) |
| `CLAUDE.md` | Claude Code |
| `.cursorrules` | Cursor |
| `trae-rule.md` | Trae |
| `.windsurfrules` | Windsurf |

## Install · 安装

```bash
# Hermes Agent
cp -r book-to-skill ~/.hermes/skills/software-development/

# Claude Code / Cursor / Windsurf
# Copy the adapter file to your project root

# Trae
# Import trae-rule.md via Settings → Rules
```

## Requirements · 依赖

- Python 3 (for EPUB conversion)
- pdftotext / poppler-utils (for PDF conversion)

```bash
# Debian/Ubuntu
sudo apt install poppler-utils

# macOS
brew install poppler
```

## Usage · 使用

In your AI assistant:

> Turn this book into an instruction set: /path/to/book.pdf
> 把这本书生成一个 skill：/path/to/book.pdf

Supported: `.pdf` `.epub` `.md` `.txt`

## License

MIT
