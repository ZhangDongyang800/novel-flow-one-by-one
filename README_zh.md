<div align="center">

# Novel Flow / 小说流

[![Trae](https://img.shields.io/badge/Built%20for-Trae-blue)](https://trae.ai)
[![License](https://img.shields.io/badge/License-MIT-green)](LICENSE)
[![Skills](https://img.shields.io/badge/Skills-6-purple)](#特性)
[![Styles](https://img.shields.io/badge/Styles-3-orange)](#写作风格)

**AI 辅助长篇小说写作系统**

6 个协作 Skill，从灵感到定稿全流程覆盖。
去 AI 味 · 风格引擎 · 结构化审查 · 防漂移机制

[快速开始](#快速开始) · [使用流程](#使用流程) · [写作风格](#写作风格)

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

## License

[MIT](LICENSE)
