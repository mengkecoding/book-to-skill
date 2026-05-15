# book-to-skill

[中文版](./README_CN.md)

Extract reusable AI instructions from books. Supports Claude Code, Trae, Cursor, Windsurf, and Hermes Agent.

[![Hermes Skill](https://img.shields.io/badge/Hermes-Skill-blue)](https://hermes-agent.nousresearch.com)
[![Version](https://img.shields.io/badge/version-1.1.0-green)]()

## What is this

`book-to-skill` reads a book (PDF / EPUB / Markdown / TXT), extracts its knowledge, and generates deployable instructions for AI coding assistants — a Claude Code `CLAUDE.md`, a Cursor `.cursorrules`, a Trae rule, or a Hermes Agent Skill.

## Supported Book Types

| Type | Examples | Output Skill Type |
|------|----------|-------------------|
| Tech / Methodology | *Pro Git*, *Refactoring*, *DDIA* | Tool Manual / Procedural / Hands-on Advisor |
| Fiction / Biography / Philosophy | *1984*, *Antifragile* | Decision Framework / Response Protocol |

## Example

**Input**: George Orwell's *1984*
**Output**: **doublethink-detection** — a critical thinking framework that identifies information control, narrative manipulation, and orthodoxy suppression. Contains 5 mental models (Doublethink, Duckspeak, Thoughtcrime, Memory Hole, 2+2=4) and a complete decision framework.

## Workflow

```
0. Pre-check (is this book suitable?)
1. Read & Analyze (convert → TOC → classify)
2. Extract core (unified entry + type-specific sections)
3. Generate output
4. Quality verification (7-item checklist)
5. Self-test (real scenario from the book)
6. Deliver → user confirmation
```

## Modes

- **Review mode** (default): pause at each stage for user approval
- **Quick mode**: full auto, pause only at final delivery

## Platform Adapters

| File | Platform |
|------|----------|
| `SKILL.md` | Hermes Agent (full version) |
| `CLAUDE.md` | Claude Code |
| `.cursorrules` | Cursor |
| `trae-rule.md` | Trae |
| `.windsurfrules` | Windsurf |

## Install

```bash
# Hermes Agent
cp -r book-to-skill ~/.hermes/skills/software-development/

# Claude Code / Cursor / Windsurf
# Copy the adapter file to your project root

# Trae
# Import trae-rule.md via Settings → Rules
```

## Requirements

- Python 3 (for EPUB conversion)
- pdftotext / poppler-utils (for PDF conversion)

```bash
# Debian/Ubuntu
sudo apt install poppler-utils

# macOS
brew install poppler
```

## Usage

In your AI assistant:

> Turn this book into an instruction set: /path/to/book.pdf

Supported formats: `.pdf` `.epub` `.md` `.txt`

## License

MIT
