# book-to-skill

从书籍文件中提炼知识，生成可复用的 Hermes Agent Skill。

[![Hermes Skill](https://img.shields.io/badge/Hermes-Skill-blue)](https://hermes-agent.nousresearch.com)
[![Version](https://img.shields.io/badge/version-1.1.0-green)]()

## 这是什么

`book-to-skill` 是一个 Hermes Agent 的工作流引擎型 Skill。它把一本书（PDF / EPUB / Markdown / TXT）读进去，提炼出可复用的思维框架，生成一个立即可用的 Hermes Skill。

## 支持的书类型

| 类型 | 代表 | 生成的 Skill 类型 |
|------|------|-------------------|
| 技术书 / 方法论 | 《Pro Git》《重构》《DDIA》 | 工具手册 / 操作规范 / 实战+顾问 |
| 小说 / 传记 / 思想书 | 《1984》《反脆弱》《孙子兵法》 | 决策框架 / 响应协议 |

## 从 1984 到 doublethink-detection

用 `book-to-skill` 处理乔治·奥威尔《1984》后生成的示例 Skill：

**[doublethink-detection](https://github.com/mengkecoding/hermes-skills/tree/main/doublethink-detection)** — 识别信息控制、叙事操纵与正统思想压制的批判性思维框架。

包含 5 个思维模型（双重思想、鸭话、思想罪、忘怀洞、二加二等于四）和完整的决策框架，帮助 Agent 在受限信息环境中保持独立判断。

## 工作流

```
0. 前置判断（这本书适合生成 Skill 吗？）
1. 读取 & 分析（PDF 转文本 → 读目录 → 判断类型）
2. 提炼核心（统一入口 + 类型专属章节）
3. 生成 SKILL.md → 写入 _drafts/
4. 质量验证（7 项 checklist）
5. Self-test（书中真实场景验证）
6. 交付 → 用户确认
```

## 两种模式

- **审查模式**（默认）：每阶段暂停，用户审核确认后进入下一步
- **快速模式**：一口气生成，只在最终交付时暂停

## 文件结构

```
book-to-skill/
├── SKILL.md                    # Skill 主文件（工作流定义）
├── references/
│   └── epub-convert.md         # EPUB → TXT 转换脚本
└── README.md
```

## 安装

将整个目录放到 Hermes 的 skills 目录下：

```bash
cp -r book-to-skill ~/.hermes/skills/software-development/
```

或在 Hermes Agent 中直接搜索安装：

```bash
hermes skills search "book-to-skill"
hermes skills install <id>
```

## 要求

- Hermes Agent
- Python 3（用于 EPUB 转换）
- pdftotext / poppler-utils（用于 PDF 转换，仅 Linux/macOS）

```bash
# Debian/Ubuntu
sudo apt install poppler-utils

# macOS
brew install poppler
```

## 使用

在 Hermes Agent 对话中提供书的路径：

> 把这本书生成一个 skill：/path/to/book.pdf

支持格式：`.pdf` `.epub` `.md` `.txt`

## License

MIT
