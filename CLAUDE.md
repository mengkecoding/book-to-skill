# book-to-skill

从书籍文件中提炼知识，生成可复用的 AI 编程助手指令集。

## 什么时候用

用户提供书籍文件（PDF/EPUB/Markdown/TXT），想把书中的知识沉淀成项目可用的规则/技能。

## 工作流

```
0. 前置判断（书适合吗？）
1. 读取 & 分析（转换 → 目录 → 类型判断）
2. 提炼核心（统一入口 + 类型专属章节）
3. 生成指令文件
4. 质量验证（7 项 checklist）
5. Self-test（书中真实场景验证）
6. 交付
```

## 书类型判断

**A 类（操作知识类）**：技术书/方法论 → 工具手册/操作规范/实战+顾问

**B 类（思维模型类）**：小说/传记/思想书 → 决策框架/响应协议

小说如《1984》可提取角色思维模型（如温斯顿在极权下保持独立判断的策略）。

## 生成的指令结构（统一入口）

每个生成的指令必须包含：
- Overview：一句话定位
- Core Philosophy：3-5 条核心原则
- CRITICAL PRINCIPLES：不可违反的红线
- When to Use / When NOT to Use：边界声明

然后根据类型追加专属章节。

## 支持格式及转换

- `.md` / `.txt`：直接读取
- `.epub`：Python zipfile 提取 HTML（见 references/epub-convert.md）
- `.pdf`：`pdftotext -layout file.pdf /tmp/book_to_skill.txt`

## 质量验证 Checklist

1. Overview 一句话能说清？
2. CRITICAL PRINCIPLES 是否 actionable？
3. 有没有编造的命令/API？
4. When NOT to Use 写了吗？
5. Pitfalls 表格非空？

## 示例输出

输入《1984》→ 输出 doublethink-detection：识别信息控制、叙事操纵与正统思想压制，包含 5 个思维模型（双重思想、鸭话、思想罪、忘怀洞、二加二等于四）和决策框架。
