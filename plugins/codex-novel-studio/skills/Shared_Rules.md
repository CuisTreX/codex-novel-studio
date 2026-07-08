# Shared Rules — Codex Novel Studio v1.0

> 版本: 1.1  
> 最后更新: 2026-07-08  
> 适用范围: 全部六个 Skill，所有协作场景强制遵守

---

## 1. 核心原则

### 1.1 系统完整性
- 六个 Skill 共享同一套项目数据（Story Bible、Character Bible、World Bible、Timeline、Dictionary、**spaces.md**）。
- 任何 Skill 修改共享数据后，必须通过 Memory_Spec.md 规定的存储协议同步。
- 不允许维护本地副本导致的版本分歧。

### 1.2 引用优先，复述禁止
- 所有涉及的角色信息、世界观设定、时间节点引用，必须直接引用源文档，不得复述或概括。
- 引用格式: `[引用: 文档名/节/行号]`。

### 1.3 增量更新
- 每次修改必须以 Diff 形式记录变更原因、变更时间、变更人（Skill 名称）。
- 变更日志附加在文档末尾的 `## 变更日志` 节。

### 1.4 职责边界
- 每个 Skill 只修改自己负责的文档区域。跨域修改需要发起 Review Request。
- Review Request 格式:
  ```
  Review Request
  发起 Skill: [名称]
  目标文档: [文档名]
  变更内容: [简要描述]
  理由: [为何需要跨域修改]
  ```

### 1.5 信息密度原则
- 所有文档条目必须提供可操作的信息，禁止填充无信息量的模板语言。
- 每个条目需要回答: 这如何影响故事？这如何影响读者体验？

---

## 2. 命名约定

### 2.1 文档标识符
- 每个项目拥有唯一 `ProjectID`，格式: `CNS-{年份}-{序号}` (e.g., `CNS-2026-001`)。
- 角色 ID: `CNS-{ProjectID}-{CH-序号}` (e.g., `CNS-2026-001-CH-01`)。
- 地点 ID: `CNS-{ProjectID}-{LOC-序号}`。
- 事件 ID: `CNS-{ProjectID}-{EV-序号}`。
- 科技条目 ID: `CNS-{ProjectID}-{TECH-序号}`。
- 章节 ID: `CNS-{ProjectID}-{CHP-序号}`。
- 时间节点 ID: `CNS-{ProjectID}-{TM-序号}`。
- 问题/缺陷 ID: `CNS-{ProjectID}-QA-{NNN}`。

### 2.2 文件路径
- 所有项目文件存储在 `{ProjectID}/` 目录下。
- 每个项目包含:
  ```
  {ProjectID}/
  ├── meta.md                   # 项目元信息（书名、类型、主题、POV、写作风格等）
  ├── story_bible.md            # Story Bible
  ├── outline.md                # 结构化大纲
  ├── timeline.md               # 时间线
  ├── characters.md             # 人物总览（索引用）
  ├── spaces.md                 # 空间布局（重要场景的布局预设，避免前后描写矛盾）
  ├── dagang.md                 # 用户输入的草稿/新设定（同步入口）
  │
  ├── character_bible/
  │   ├── index.md              # 角色索引
  │   ├── CH-01.md              # 角色 01 完整档案
  │   ├── CH-02.md
  │   └── ...
  │
  ├── world_bible/
  │   ├── index.md              # 世界观总览
  │   ├── tech_tree.md          # 科技树
  │   ├── civilization.md       # 文明体系
  │   └── locations/
  │       ├── index.md
  │       ├── LOC-001.md
  │       └── ...
  │
  ├── chapters/
  │   ├── chapter_index.md      # 章节索引与规划
  │   ├── chapter_001.md
  │   └── ...
  │
  ├── references/
  │   └── writing-style.md      # 写作风格规范（去 AI 化细则、禁用表达清单等）
  │
  ├── dictionary.md             # 术语词典
  └── changelog.md              # 项目级变更日志
  ```

---

## 3. 质量标准

### 3.1 每个 Skill 输出前的自检清单
- [ ] 是否引用了正确的数据来源？
- [ ] 是否与前序章节/设定保持一致？
- [ ] 是否存在 AI 味、模板化语言？
- [ ] 是否存在冗余或重复内容？
- [ ] 是否满足该 Skill 的专项质量标准？

### 3.2 交叉验证
- Novel Editor 有权要求任何 Skill 重新输出。
- Character Bible 修改角色后，Novel Writer 应检查受影响章节的人物一致性问题。
- World Bible 修改设定后，Novel Architect 应评估对 Story Bible 的影响。
- Novel Writer 输出章节后，**必须**对照 spaces.md 检查空间描写一致性。

### 3.3 表达重复检查（全系统强制）
- 所有正文（含对话）中，同一表达在全文中累计 ≥ 3 次时，后续章节禁用。
- 同一形容词在相邻 3 段内不得重复。
- 全系统禁止出现结构化对比句式（"不是…而是…""不是…是…"）和三连排比句。
- 禁止在小说叙述中使用议论文式逻辑过渡词（"首先…其次…""一方面…另一方面"）。

---

## 4. 信息安全

### 4.1 不可输出项
以下内容仅供内部推理使用，不得出现在任何面向用户的输出中：

- MBTI 类型（仅内部参考）
- 心理模型原始数据
- 未成熟的设定草稿
- 被否决的故事线版本

### 4.2 版本控制
- 所有文档使用语义化版本号: `MAJOR.MINOR.PATCH`
  - MAJOR: 破坏性变更（故事线重写、角色删除）
  - MINOR: 新增内容（新角色、新章节）
  - PATCH: 修正（拼写、格式、微小调整）
- 重大决策（MAJOR 变更）需要 Novel Architect 批准。

---

## 5. 协作协议

### 5.1 阶段门禁
- 每个阶段（设计 → 写作 → 编辑）设有门槛条件。
- 未满足门槛条件的输出不得进入下一阶段。

### 5.2 回滚协议
- 任何变更均可回滚。
- 回滚需要记录:
  - 回滚原因
  - 影响范围
  - 替代方案

### 5.3 争议解决
- 当两个 Skill 存在意见分歧时，由 Novel Architect 综合判断。
- 判断依据: 是否有利于提升读者体验，是否符合商业定位。
- 分歧和处理记录必须归档。

---

## 变更日志
| 版本 | 日期 | 变更内容 | 发起人 |
|------|------|----------|--------|
| 1.1 | 2026-07-08 | 新增 spaces.md、dagang.md 到项目结构；新增表达重复检查 + 问题追踪 ID 规范 | CNS-Foundation |
| 1.0 | 2026-07-08 | 初始版本 | CNS-Foundation |
