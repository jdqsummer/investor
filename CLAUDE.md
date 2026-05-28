# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## 项目概述

价值投资书籍创作项目，帮助作者撰写一本关于价值投资的书籍（书名暂定《普通人的长期财富之道》）。项目包含多个 AI 辅助角色、知识库管理系统和内容审核流程。当审核完成后，需要将审核的内容归档到 Obsidian 知识库中。

## 目录结构

```
├── .claude/
│   ├── commands/           # 可执行的 Claude 命令（slash commands）
│   ├── skills/             # Claude Skills（角色技能定义）
│   │   ├── investor-content-generation/   # 内容共创技能
│   │   ├── investor-material-research/    # 素材研究技能
│   │   ├── investor-outline-design/       # 大纲设计技能
│   │   ├── investor-position-analysis/    # 定位分析技能
│   │   ├── investor-text-polish/          # 文字打磨技能
│   │   └── stanley_marks_reviewer/        # 霍华德·马克斯审核技能
│   └── settings.json      # 权限配置
├── agent-rules/
│   ├── kb/                 # 知识库
│   │   ├── 参考资料/       # 经典投资著作摘要
│   │   ├── 我对价值投资的思考/  # 作者个人思考笔记
│   │   ├── 投资笔记/       # 日常投资笔记
│   │   ├── 聪明投资者访谈记录/ # 投资大师访谈
│   │   └── 霍华德·马克斯备忘录/ # Howard Marks 备忘录全集
│   └── kb-books/
│       └── prompts/        # 知识库书籍处理的 prompt 模板（类型识别、概念提取、章节分析等）
├── doc/                    # 文档输出目录
│   ├── investor_content_co_creator/output/    # 章节草稿
│   ├── investor_material_researcher/output/   # 素材报告
│   ├── investor_outline_architect/output/     # 投资大纲
│   ├── investor_position_advisor/output/      # 定位报告
│   ├── investor_polish_master/                # （预留）
│   ├── stanley_marks_reviewer/output/         # 审核报告
│   └── kb-books/                              # 书籍知识库
└── CLAUDE.md
```

## 核心工作流

### 书籍创作
书籍创作遵循以下流水线（按顺序执行）：

1. **定位分析** → `/investor_position_advisor`（确定创作方向和差异化定位）
2. **大纲设计** → `/investor_outline_architect`（搭建章节结构和逻辑框架）
3. **素材研究（可选）** → `/investor_material_researcher --topic="..."`
4. **内容共创** → `/investor_content_co_creator --chapter="第 X 章"`（生成章节草稿）
5. **文字打磨** → `/investor_polish_master --content-path=...`（优化文字、排查漏洞）
6. **马克斯审核** → `/stanley_marks_reviewer`（霍华德·马克斯风格的审核）

### 更新入库
触发词**："更新知识库"、"更新Obsidian"、"
当 Claude 识别到这些触发词时，会将`doc\investor_content_co_creator\output`目录下更改的相关文件内容自动并存入 Obsidian 的仓库中
- 仓库名: iCloud~md~obsidian
- 仓库ID: 38963c3b905540d3
- 存储路径: `Wiki/6_Books/04_创作书籍/普通人的长期财富之道/{章节名}.md`
- 调用 `obsidian-cli` skill 找到对应的章节文件，并读取内容。
- 将更改的文件和内容融入到相关章节中，并保存到`Wiki/6_Books/04_创作书籍/普通人的长期财富之道`对应的章节中。确保格式正确，并更新元数据（如标签、date_modified等）
- 确认写入成功后告知用户，并提供链接或提示如何在 Obsidian 中查看该笔记

## 书籍章节

共 12 章 + 前言 + 简介：
1. 为什么你的投资总是亏钱？
2. 价值投资为何有效？
3. 重新认识财富与复利
4. 能力圈——清楚边界比范围大小重要
5. 护城河——找到好生意
6. 安全边际——买得好等于成功一半
7. 估值艺术——用 50 美分买 1 美元
8. 投资组合——集中与分散的平衡
9. 市场先生——工具而非主人
10. 逆向思维——在恐惧时贪婪
11. 长期持有——在场是唯一胜招
12. 投资即修行——按自己的节奏打球


