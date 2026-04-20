<div align="center">

# Novel Flow / 小说流

[![Trae](https://img.shields.io/badge/Built%20for-Trae-blue)](https://trae.ai)
[![License](https://img.shields.io/badge/License-MIT-green)](LICENSE)
[![Skills](https://img.shields.io/badge/Skills-6-purple)](#特性)
[![Styles](https://img.shields.io/badge/Styles-3-orange)](#写作风格)

**AI 辅助长篇小说写作系统**

6 个协作 Skill，从灵感到定稿全流程覆盖。
去 AI 味 · 风格引擎 · 结构化审查 · 防漂移机制

**[English](README.md)**

</div>

---

## 快速开始

**Trae 用户：** 将 `skills` 和 `shared` 文件夹直接放到你项目的 `.trae` 目录下即可。

```
你的项目/
└── .trae/
    ├── skills/     ← 复制进来
    └── shared/     ← 复制进来
```

**其他 AI 工具：** 直接告诉 AI：
```
安装这个 skill：https://github.com/ZhangDongyang800/novel-flow-one-by-one.git
```

## 使用流程

1. 对 AI 说出你的想法（什么都行，甚至两个字"小说"），AI 会逐个问你题材、主角、世界观等问题，你只需要做选择题（选 A 还是选 B）
2. 确认生成的 `project.md`（项目设定）和角色卡
3. AI 自动生成章节大纲 `outline.md`，你确认章节路线
4. AI 逐场景写正文，每 300-500 字自动检查 AI 味和排版问题
5. 你确认草稿后，AI 执行六维审查（事件推进、主角变化、记忆点、节奏、情绪、钩子）
6. 审查通过 → 自动同步设定变更 → 写下一章；不通过 → 修改后重新审查

## 写作风格

|     风格     | 适合类型                           | 核心特征                       |
| :----------: | ---------------------------------- | ------------------------------ |
|  **冷白描**  | 现实主义、历史、悬疑、战争         | 克制、情感内敛       |
| **系统爽文** | 系统流、升级流、都市逆袭、玄幻修仙 | 憋屈→反转→爽、打脸升级         |
| **怪诞悬疑** | 规则怪谈、无限流、克苏鲁、智斗     | 规则设计、信息不对称、认知入侵 |

## 目录结构

```
novel-flow/
├── skills/
│   ├── novel-orchestrator/   # 总控调度
│   ├── novel-brainstorm/     # 灵感收束
│   │   └── templates/        # project.md · 人物卡.md
│   ├── novel-outline/        # 章节规划
│   │   └── templates/        # outline.md
│   ├── novel-draft/          # 逐场景写作
│   │   ├── templates/        # guide.md · chapter-xxx.md
│   │   └── styles/           # 冷白描 · 系统爽文 · 怪诞悬疑
│   ├── novel-review/         # 六维审查
│   └── novel-update/         # 设定同步
└── shared/
    ├── file-contracts.md     # 文件契约（数据字典）
    └── state-rules.md        # 状态流转规则
```

## 常见问题

**Q：AI 没有激活 skill，直接开始写了。**
A：检查 `skills/` 和 `shared/` 文件夹是否直接放在 `.trae/` 目录下，路径必须是 `.trae/skills/novel-orchestrator/SKILL.md`，不能多套一层文件夹。

**Q：生成的文字还是有 AI 味。**
A：正常。AI 模型有固有的写作习惯，skill 系统通过规则和自检大幅减少 AI 味，但无法 100% 消除。发现 AI 味时直接指出来，审查 skill 会捕捉并修正。

**Q：文中的数字/逻辑算错了（比如利息算错）。**
A：AI 模型的数学能力有限。skill 里虽然有"必须验算"的规则，但不能完全依赖。涉及数字的内容自己再核对一遍。

**Q：每章结尾感觉很重复。**
A：skill 现在包含"读者视角重读"自检，会主动发现重复。如果还是出现了，直接告诉 AI："这个结尾和上一章太像了，换一种。"

**Q：故事偏离了最初的设定。**
A：update skill 会在每章写完后自动同步设定变更。如果还是偏了，检查 `project.md`——AI 可能悄悄改了设定但没记录。

**Q：brainstorm 问的问题太多了。**
A：任何一步都可以说"跳过"或"这个无所谓"，系统会用默认值继续。

## License

[MIT](LICENSE)
