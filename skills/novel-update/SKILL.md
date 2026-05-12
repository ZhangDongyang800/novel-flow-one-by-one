---
name: novel-update
description: |
  每章 review 通过后自动调用。更新 project.md canon、outline.md 状态、
  章节文件定稿摘要、角色卡变更记录。不做审查，只做同步。
---

# Novel Update

review 通过后的收尾工作。不做审查，只做同步——把章节产出中的事实变化反映到 project.md、outline.md 和角色卡中。

<HARD-GATE>
除非 novel-review 明确判定当前章为"通过"（pass），否则不得调用本 skill。不得做任何创作判断——本 skill 仅将章节产出中的事实同步到 project.md 和 outline.md。违反此规则意味着要么为未经批准的内容更新 canon，要么在 review 流程之外做了创作决策。
</HARD-GATE>

## 反模式："这一章不需要更新 canon"

每一章在 review 通过后都必须经过这个流程。即使本章没有引入新设定、新角色、世界观变化，你仍然需要完整执行更新流程——至少要更新 outline 状态为 done 并写入定稿摘要。因为"没有变化"而跳过更新，正是导致 outline 状态脱节、章节摘要缺失的原因，后续将无法追踪项目进展。一个没有 canon 变更的章节会很快完成这个流程——跳过它不会节省时间，只会造成数据缺口。

---

## 检查清单

你必须按顺序完成以下项目：

1. **读取章节文件** — 读取 `【书名】/第X卷/chapter-xxx.md`（正文）+ `章节/chapter-xxx.md`（目标）+ `project.md` + `outline.md` + `人物/` 文件夹中的角色卡
2. **更新 project.md canon** — 检查设定变更，如有则追加到变更日志
3. **更新角色卡** — 检查角色状态变化，如有则追加到角色卡变更记录
4. **更新 outline.md 状态** — 将当前章状态改为 done
5. **写入定稿摘要** — 在章节文件中写入 2-3 句话定稿摘要
6. **交给 orchestrator** — 调用 novel-orchestrator 推进到下一章

---

## 流程图

```dot
digraph update {
    rankdir=TB;
    node [shape=box, style="rounded,filled", fontsize=10];
    edge [fontsize=9];

    start [label="review 通过\n触发 update", fillcolor="#d5f5e3"];
    read [label="Step 1: 读取上下文", fillcolor="#eaf2f8"];
    canon [label="Step 2: 更新 project.md canon", fillcolor="#eaf2f8"];
    character [label="Step 3: 更新角色卡", fillcolor="#eaf2f8"];
    outline [label="Step 4: 更新 outline.md 状态", fillcolor="#eaf2f8"];
    summary [label="Step 5: 写入定稿摘要", fillcolor="#eaf2f8"];
    handoff [label="Step 6: 交给 orchestrator", fillcolor="#d5f5e3"];

    start -> read -> canon -> character -> outline -> summary -> handoff;
}
```

**终态是调用 novel-orchestrator。** 不要直接调用 novel-draft 开始下一章——更新完成后始终通过 novel-orchestrator 进行路由。

---

## 流程

### Step 1: 读取上下文

**目标：** 获取更新所需的所有信息。

1. 读取 `【书名】/第X卷/chapter-xxx.md`（正文）
2. 读取 `章节/chapter-xxx.md`（目标 + 结构标记）
3. 读取 `project.md`（当前设定）
4. 读取 `outline.md`（当前卷章节列表）
5. 读取 `人物/` 文件夹中的角色卡（当前角色状态）

**验证点：** 正文、章节文件、project.md、outline.md、角色卡已获取。

---

### Step 2: 更新 project.md canon

**目标：** 检查正文是否有设定变更，如有则记录。

扫描正文，检查是否有以下变更：
- 新角色正式登场
- 新地点/组织/物品首次出现
- 主角能力/状态变化
- 世界规则被揭示或修正

**操作：**
- 如有变更 → 追加到 project.md 的「变更日志」section
- 如无变更 → 跳过

**禁止：** 不修改 project.md 的初始设定 section。

**验证点：** 变更日志已更新（如有变更），初始设定未被修改。

---

### Step 3: 更新角色卡

**目标：** 检查正文是否有角色状态变化，如有则记录到对应角色卡。

扫描正文，检查是否有以下角色相关变更：
- 新角色正式登场（如无对应角色卡，则创建新角色卡）
- 角色关系变化（如敌友关系转变、新联盟等）
- 角色能力/状态变化（如获得新能力、受伤、心态转变等）

**操作：**
- 如有变更 → 追加到对应 `人物/[角色名].md` 的「变更记录」section
- 新角色登场 → 在 `project.md` 的「变更日志」中记录"新角色：[角色名]，待创建角色卡"，由用户确认后通过 orchestrator 路由到 novel-brainstorm 创建
- 如无变更 → 跳过

**禁止：** 不修改角色卡的初始设定 section。

**验证点：** 角色卡变更记录已更新（如有变更），初始设定未被修改。

---

### Step 4: 更新 outline.md 状态

**目标：** 将当前章状态标记为完成。

1. 将当前章的状态从 reviewing/done 改为 done（如尚未更新）
2. 检查当前卷是否所有章都是 done
   - 是 → 在 outline.md 中标注"当前卷已完成"

**验证点：** 当前章状态为 done，卷完成状态已标注（如适用）。

---

### Step 5: 写入定稿摘要

**目标：** 在章节文件中记录本章定稿摘要。

在 `章节/chapter-xxx.md` 的「定稿摘要」section 写入 2-3 句话摘要。

摘要内容：
- 本章关键事件
- 角色状态变化
- 引入的新元素

不含正文。

**验证点：** 定稿摘要已写入章节文件。

---

### Step 6: 交给 orchestrator

**目标：** 将控制权交回 orchestrator 推进到下一章。

调用 `novel-orchestrator` 推进到下一章。

**验证点：** orchestrator 已被调用。

---

## 核心原则

- **初始设定只读** — 只追加变更日志，不修改 project.md 和角色卡的初始设定 section
- **最小化且事实性** — 变更日志只记录事实，不做评价
- **始终更新状态** — 即使没有 canon 变更，也要更新 outline 状态和定稿摘要
- **不做创作判断** — 不做任何创作判断，只做同步

## 反模式清单

| 错误行为 | 正确做法 |
|----------|----------|
| 修改 project.md 初始设定 | 只追加变更日志 |
| 修改角色卡初始设定 | 只追加变更记录 |
| 跳过更新因为"没有变化" | 至少更新状态和摘要 |
| 在变更日志中写评价 | 只记录事实 |
| 不更新 outline 状态 | 每次都更新 |

## 交叉引用

### 上游

- **`novel-review`**：review 判定为"通过"后触发本 skill。
- **`novel-orchestrator`**：路由到本 skill 执行更新。

### 下游

- **`novel-orchestrator`**：更新完成后交给 orchestrator 推进到下一章。

### 关键文件

| 文件 | 职责 |
|------|------|
| `章节/chapter-xxx.md` | 输入：本章目标；输出：定稿摘要 + 状态更新 |
| `【书名】/第X卷/chapter-xxx.md` | 输入：正文（扫描设定变更） |
| `project.md` | 输入：当前设定；输出：变更日志追加 |
| `人物/[角色名].md` | 输入：当前角色状态；输出：变更记录追加（如有变更） |
| `outline.md` | 输入：当前卷章节列表；输出：状态更新 + 卷完成标注 |
