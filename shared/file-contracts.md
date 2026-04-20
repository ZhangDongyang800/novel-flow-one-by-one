# 文件数据契约 (File Contracts)

> 本规范定义了小说流项目中每个文件的严格字段规范。
> 所有 skill 必须按本契约读写文件，不得自行发明字段或格式。

---

## 1. project.md

**所有者：** `novel-brainstorm`（初始化）、`novel-update`（canon 更新）

### 1a. 必填 section（初始化时填写）

```markdown
# [书名]

## 核心 Premise
> 一句话：谁 + 在什么处境 + 必须做什么 + 否则会怎样
> 开篇策略：XXX

## 主题
> 一句话：这个故事最终想探讨什么

## 角色与关系
> 详细角色信息见 `人物/` 文件夹

- **[主角名字]** → `人物/[主角名字].md`（主角）
- **[配角名字]** → `人物/[配角名字].md`（与主角关系：XX）

## 世界观硬规则
- 规则 1：
- 规则 2：
- ...

## 核心冲突
- 主线冲突：
- 冲突升级方向：

## 写作风格
- 叙事视角：
- 文风要求：
- 节奏偏好：
- 禁止事项：

## 字数规划
- 全书目标：
- 每章目标（默认 2300 字左右，用户可修改）：
```

**字段约束：**

| section | 约束 |
|---------|------|
| 核心 Premise | 必须恰好一句话，格式为"谁 + 在什么处境 + 必须做什么 + 否则会怎样"。可选追加"开篇策略"行 |
| 主题 | 一句话，描述故事最终想探讨什么。可写"待定" |
| 角色与关系 | 角色名字列表，详细信息在 `人物/` 文件夹。至少 1 个主角 + 1 个配角。配角必须标注与主角关系 |
| 世界观硬规则 | 至少 1 条，最多 7 条 |
| 核心冲突 | 必须包含：主线冲突 + 升级方向 |
| 写作风格 | 必须包含：叙事视角、文风要求、节奏偏好、禁止事项 |
| 字数规划 | 必须包含：全书目标 + 每章目标（默认 2300 字左右，用户可修改） |

### 1b. 运行时 section（review 通过后由 novel-update 追加）

```markdown
## 变更日志
> 每次 canon 更新时追加，格式：[chapter-xxx] 变更内容
```

### 1c. 禁止事项

- 不允许在 `project.md` 中删除或修改已确认的初始设定
- 新增事实只能追加到「变更日志」
- 修正原始设定必须保留原文并标注修正原因，格式：

```markdown
~~原文内容~~ → 修正后内容（[chapter-xxx] 修正原因）
```

---

## 2. outline.md

**所有者：** `novel-outline`

### 2a. 必填 section

```markdown
# [项目名称] 大纲

## 全书主线摘要
> 2-3 句话概括整个故事的方向（可随写作调整）

## 当前卷：第 [N] 卷

### 卷目标
> 本卷要完成什么（1-2 句话）

### 章节列表
| 章节 | 任务说明 | 结构标记 | 状态 |
|------|---------|---------|------|
| chapter-001 | [一句话任务说明] | setup | planned |
| chapter-002 | [一句话任务说明] | build | planned |
| chapter-003 | [一句话任务说明] | climax | planned |
| chapter-004 | [一句话任务说明] | fallout | planned |
| ... | | | |

## 后续方向

### 第 [N+1] 卷
> 1-2 句话粗略方向

### 第 [N+2] 卷
> 1-2 句话粗略方向

## 已完成卷摘要

### 第 1 卷
> 2-3 句话实际走向
```

### 2b. 字段约束

| 字段 | 约束 |
|------|------|
| 全书主线摘要 | 2-3 句话，覆盖起承转合 |
| 卷目标 | 1-2 句话，具体到可执行 |
| 任务说明 | 每章恰好一句话，具体到可执行（不是"日常"，而是"主角在集市偶遇神秘商人，获得第一个线索"） |
| 结构标记 | 必填，每章一个，取值范围：`setup` / `build` / `climax` / `fallout` |
| 状态 | 必填，取值范围：`planned` / `drafting` / `reviewing` / `done` / `blocked` |
| 后续方向 | 每卷 1-2 句话，标注仅为"种子" |
| 已完成卷摘要 | 每卷 2-3 句话实际走向，基于已完成章节的定稿 |

### 2c. 结构标记说明

| 标记 | 含义 | 在卷中的位置 |
|------|------|-------------|
| `setup` | 建立场景、引入角色/冲突 | 卷的开头部分 |
| `build` | 推进冲突、升级张力 | 卷的中段 |
| `climax` | 高潮、关键转折点 | 卷的关键节点 |
| `fallout` | 收束、余波、为下一阶段铺垫 | 卷的结尾部分 |

每卷应包含至少一个 `setup`、一个 `climax`、一个 `fallout`，`build` 可以有多个。

---

## 3. 章节/chapter-xxx.md

**所有者：** `novel-draft`（草稿）、`novel-review`（审查）

### 3a. frontmatter（严格格式）

```yaml
---
id: chapter-001
volume: 1
status: drafting
review_round: 0
canon_changed: false
source_outline_version: 1
updated_at: 2026-04-13
---
```

**字段约束：**

| 字段 | 类型 | 必填 | 说明 |
|------|------|------|------|
| `id` | string | 是 | 章节标识符，格式 `chapter-NNN` |
| `volume` | integer | 是 | 所属卷号 |
| `status` | enum | 是 | 取值：`planned` / `drafting` / `reviewing` / `done` / `blocked` |
| `review_round` | integer | 是 | 已经历的审查轮次，初始为 0 |
| `canon_changed` | boolean | 是 | 本章是否有 canon 变更，初始为 `false` |
| `source_outline_version` | integer | 是 | 基于哪个版本的 outline 写的，每次 outline 更新递增 |
| `updated_at` | date | 是 | 最后更新日期，格式 `YYYY-MM-DD` |

### 3b. 必填 section

```markdown
# Chapter [XXX]: [章节标题]

## 本章目标
> 从 outline 继承的任务说明 + 结构标记

## 修改意见
> review skill 填写

## 定稿摘要
> review 通过后填写：本章关键事件摘要（2-3 句话），不含正文
```

### 3c. 修改意见格式（严格）

```markdown
## 修改意见

**review_status:** pass / minor_fix / rewrite_required / reject
**review_severity:** minor / structural

### 判定依据
1. [具体问题]
2. ...

### 建议修改
1. [具体修改建议]
2. ...
```

**判定约束：**

| review_status | review_severity | 含义 |
|---------------|----------------|------|
| `pass` | — | 通过，无需修改 |
| `minor_fix` | `minor` | 小修，问题不超过 3 个，改 1 轮直接过 |
| `rewrite_required` | `structural` | 重写，指出核心问题（1-2 个），最多重写 1 次 |
| `reject` | — | 回退，方向性错误，建议调整 outline |

---

## 4. project-state.md

**所有者：** `novel-orchestrator`

### 4a. frontmatter（严格格式）

```yaml
---
current_volume: 1
current_chapter: chapter-003
project_status: in_progress
blocked_reason:
last_skill: draft
updated_at: 2026-04-13
---
```

**字段约束：**

| 字段 | 类型 | 必填 | 说明 |
|------|------|------|------|
| `current_volume` | integer | 是 | 当前卷号 |
| `current_chapter` | string | 是 | 当前章节 id，格式 `chapter-NNN` |
| `project_status` | enum | 是 | 取值：`not_started` / `in_progress` / `completed` |
| `blocked_reason` | string | 是 | 阻塞原因，为空表示未阻塞。有值时状态强制为 `blocked` |
| `last_skill` | enum | 是 | 最后执行的 skill，取值：`brainstorm` / `outline` / `draft` / `review` / `update` |
| `updated_at` | date | 是 | 最后更新日期，格式 `YYYY-MM-DD` |

### 4b. blocked_reason 取值规范

| 值 | 含义 |
|----|------|
| （空） | 未阻塞 |
| `direction_error` | 方向性错误（review 回退） |
| `canon_conflict` | canon 一致性严重冲突 |
| `user_pause` | 用户主动暂停 |

---

## 5. 【书名】/第X卷/chapter-xxx.md

**所有者：** `novel-draft`（写入草稿）、`novel-review`（定稿更新）

### 5a. 格式

```markdown
# Chapter [XXX]: [章节标题]

> 纯正文，无元数据，可直接复制

[正文内容]
```

**约束：**
- 无 frontmatter
- 无元数据、无任务说明、无修改意见
- 只包含纯正文，可直接复制使用
- 目录以 `project.md` 中的项目名称命名，按卷号组织子文件夹
- review 通过后，正文为最终定稿版本

---

## 6. 人物/[角色名].md

**所有者：** `novel-brainstorm`（创建）、`novel-update`（运行时追加变更记录）

### 6a. 必填 section（初始化时填写）

```markdown
# [角色名字]

## 基本信息
- 身份：
- 与主角关系：

## 核心特质
- 核心驱动力：
- 核心恐惧：
- 关键特征：

## 变更记录
> 角色状态变化时追加，格式：[章节] 变化内容
```

**字段约束：**

| section | 约束 |
|---------|------|
| 基本信息 | 必须包含：身份。主角可省略"与主角关系"，配角必须包含 |
| 核心特质 | 必须包含：核心驱动力、核心恐惧、关键特征 |
| 变更记录 | 运行时由 novel-update 追加，格式为 `[章节] 变化内容` |

### 6b. 禁止事项

- 不允许删除或修改已确认的初始设定
- 新增角色状态变化只能追加到「变更记录」
- 修正原始设定必须保留原文并标注修正原因

---

## 7. 文件间引用关系

```
project.md ← novel-brainstorm 创建，novel-update 追加 canon
    ↓ 读取
人物/[角色名].md ← novel-brainstorm 创建，novel-update 追加变更记录
    ↓ 读取
outline.md ← novel-outline 创建和更新
    ↓ 读取任务说明
章节/chapter-xxx.md ← novel-draft 创建，novel-review 更新
    ↓ 正文直接写入
【书名】/第X卷/chapter-xxx.md ← novel-draft 写入草稿，novel-review 定稿更新
    ↑ 状态同步
project-state.md ← novel-orchestrator 维护
    ↑ review 通过后调用 novel-update 更新 canon 和 outline 状态
```

---

## 8. 状态值枚举汇总

所有文件中出现的 status/status 字段必须使用以下枚举值：

| 字段 | 允许值 |
|------|--------|
| 章节文件 frontmatter.status | `planned` / `drafting` / `reviewing` / `done` / `blocked` |
| outline.md 章节列表状态 | `planned` / `drafting` / `reviewing` / `done` / `blocked` |
| project-state.md.project_status | `not_started` / `in_progress` / `completed` |
| project-state.md.blocked_reason | （空）/ `direction_error` / `canon_conflict` / `user_pause` |
| project-state.md.last_skill | `brainstorm` / `outline` / `draft` / `review` / `update` |
| outline.md 结构标记 | `setup` / `build` / `climax` / `fallout` |
