# Memory Spec — Codex Novel Studio v1.0

> 版本: 1.1  
> 最后更新: 2026-07-08  
> 状态: 强制规范

---

## 1. 概述

Memory Spec 定义了 Codex Novel Studio 六个 Skill 之间的数据存储、引用和同步协议。目标是保证所有协作组件共享一致的项目数据，杜绝信息孤岛和版本分歧。

---

## 2. 存储架构

### 2.1 物理层
- 所有项目数据以 Markdown（.md）文件存储在 `{ProjectID}/` 目录中。
- 每个项目一个目录，目录命名与 ProjectID 一致。
- 目录结构（强制执行）:

```
{ProjectID}/
├── meta.md                           # 项目元信息
├── story_bible.md                    # Story Bible（Novel Architect 维护）
├── outline.md                        # 结构化大纲（Novel Architect 维护）
├── timeline.md                       # 时间线（World Bible 维护）
├── characters.md                     # 角色索引（Character Bible 维护）
├── spaces.md                         # 空间布局（World Bible 维护，写作时强制对照）
├── dagang.md                         # 用户草稿/新设定入口（用户直接修改）
│
├── character_bible/
│   ├── index.md                      # 角色索引（自动生成）
│   ├── CH-001.md                     # 角色 001 完整档案
│   ├── CH-002.md
│   └── ...
├── world_bible/
│   ├── index.md                      # 世界观总览
│   ├── civilization.md               # 文明体系
│   ├── tech_tree.md                  # 科技树
│   ├── economy.md                    # 经济体系
│   ├── society.md                    # 社会结构
│   └── locations/
│       ├── index.md                  # 地点索引
│       ├── LOC-001.md
│       └── ...
├── chapters/
│   ├── chapter_index.md              # 章节索引与规划
│   ├── chapter_001.md
│   ├── chapter_002.md
│   └── ...
├── references/
│   └── writing-style.md              # 写作风格规范细则
├── dictionary.md                     # 术语词典
└── changelog.md                      # 项目级变更日志
```

### 2.2 逻辑层
数据分为五个逻辑库，由不同 Skill 负责维护:

| 逻辑库 | 文件位置 | 维护者 | 读取者 |
|--------|----------|--------|--------|
| Story Bible | `story_bible.md` + `meta.md` | Novel Architect | 全部 |
| Character Bible | `characters.md` + `character_bible/` | Character Bible | Novel Writer, Novel Editor, Translation Editor |
| World Bible | `world_bible/` + `timeline.md` + `spaces.md` | World Bible | Novel Writer, Novel Editor, Translation Editor |
| User Draft | `dagang.md` | 用户 | Novel Architect（同步用）|
| Chapter Storage | `chapters/` | Novel Writer | Novel Editor, Translation Editor |

---

## 3. 命名规范

### 3.1 标识符规则
- ProjectID: `CNS-{YYYY}-{NNN}`（例: `CNS-2026-001`）
- 角色: `{ProjectID}-CH-{NNN}`
- 地点: `{ProjectID}-LOC-{NNN}`
- 科技: `{ProjectID}-TECH-{NNN}`
- 事件: `{ProjectID}-EV-{NNN}`
- 章节: `{ProjectID}-CHP-{NNN}`
- 时间节点: `{ProjectID}-TM-{NNN}`
- 术语: `{ProjectID}-TERM-{NNN}`
- 质量问题: `{ProjectID}-QA-{NNN}`

### 3.2 文件命名
- 角色档案: `CH-{NNN}.md`
- 地点档案: `LOC-{NNN}.md`
- 章节文件: `chapter_{NNN}.md`
- 空间布局: `spaces.md`（单文件，按空间名分节）

---

## 4. 引用协议

### 4.1 跨文件引用格式
所有文件间的引用必须使用统一格式:

```
[引用: {文件名}/{节路径}] 或
[引用: {ProjectID}-{实体类型}-{NNN}]
```

示例:
- `[引用: world_bible/tech_tree.md/#聚变动力]`
- `[引用: CNS-2026-001-CH-003]`
- `[引用: character_bible/CH-001.md/#核心信念]`
- `[引用: spaces.md/#飞船主控室]`

### 4.2 无歧义原则
- 禁止在正文中重新描述已存储在引用源中的信息。
- 仅使用引用标识，并附简要上下文说明。
- 违反此原则的文本将在 Novel Editor 第一轮审查中标记。

---

## 5. 同步协议

### 5.1 写入锁
- 同一时间只有一个 Skill 可以写入一个文件。
- 写入前必须检查 `changelog.md` 中该文件的最后修改时间。
- 如果发现并发写入冲突，后写入者必须合并前写入者的变更。

### 5.2 变更广播
- 对 Character Bible 或 World Bible 中任何文件的修改，必须更新 `changelog.md`。
- 变更日志条目格式:

```
| {日期} {时间} | {版本号} | {修改文件} | {变更摘要} | {发起 Skill} |
```

### 5.3 dagang.md 同步协议
- dagang.md 是用户输入新设定/草稿的唯一入口。
- 同步时只读取 `## 待更新内容` 段落中的内容。
- 同步完成后，将该段落重命名为 `## 已更新内容（更新时间：{YYYY-MM-DD}）`，并保留用户原始稿。
- 创建新的空白 `## 待更新内容` 段落作为下次同步入口。

### 5.4 反向同步
- 当用户要求"按章节回归大纲"时，从 chapters/ 中提取章节内容，反向更新 outline.md / timeline.md / characters.md / spaces.md。
- 反向同步后需在 changelog.md 中记录。

### 5.5 定期完整性检查
- 每完成 10 章或每 30 天（以先到者为准），运行一次完整性检查。
- 检查内容:
  1. 所有引用的角色 ID 是否存在对应的角色档案文件。
  2. 所有引用的地点 ID 是否存在对应的地点档案文件。
  3. 所有时间线引用是否在 `timeline.md` 中可查。
  4. 所有科技引用是否在 `tech_tree.md` 中可查。
  5. 所有空间引用是否在 `spaces.md` 中可查。
- 不一致项记录在 `changelog.md` 中并标注 `[完整性违规]`。

---

## 6. 备份与恢复

### 6.1 自动备份
- 每完成一个 Phase，对项目目录执行全量备份。
- 备份存储位置: `{ProjectID}/backups/`。
- 备份文件命名: `backup_{YYYYMMDD}_{Phase编号}.tar.gz`。

### 6.2 回滚流程
1. 确定回滚目标版本（从 `changelog.md` 追溯）。
2. 从备份中提取目标版本的项目文件。
3. 在 `changelog.md` 中记录回滚操作。
4. 通知所有 Skill 清除本地缓存。

---

## 7. 数据完整性规则

### 7.1 强引用检查
- 任何文件中出现的角色 ID、地点 ID、科技 ID 必须在对应档案中存在。
- 孤儿引用（引用了不存在的 ID）是 BLOCKER 级别问题，必须立即修复。

### 7.2 时间线一致性
- `timeline.md` 是时间事实的唯一来源。
- 所有章节中的时间标注必须与 `timeline.md` 严格一致。
- 误差范围: ±0。不允许近似值。

### 7.3 空间一致性
- `spaces.md` 是空间布局事实的唯一来源。
- 所有章节中的空间描写必须与 `spaces.md` 严格一致。
- 违反此规则视为 MAJOR 级别问题。

### 7.4 成长路径连续性
- 每个角色在 `character_bible` 中的成长树节点，必须按照时间线顺序排列。
- 每个成长节点必须至少有一个触发事件引用。

---

## 变更日志
| 版本 | 日期 | 变更内容 | 发起人 |
|------|------|----------|--------|
| 1.1 | 2026-07-08 | 新增 spaces.md、dagang.md 存储协议；新增 dagang.md 同步协议和反向同步；新增 QA 问题 ID 规范；增加空间一致性条款 | CNS-Foundation |
| 1.0 | 2026-07-08 | 初始版本 | CNS-Foundation |
