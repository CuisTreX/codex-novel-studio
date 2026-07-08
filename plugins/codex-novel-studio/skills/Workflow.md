# Workflow — Codex Novel Studio v1.0

> 版本: 1.1  
> 最后更新: 2026-07-08  
> 状态: 强制流程

---

## 1. 总工作流

```
Novel Architect ──→ Character Bible
       │                    │
       ├────────────────────┤
       │                    │
       ▼                    ▼
 World Bible ────────── Novel Writer
       │                    │
       ├────────────────────┤
       │                    ▼
       │           Novel Editor (Round 1-4 + QA追踪 + 回归测试)
       │                    │
       ├────────────────────┤
       │                    ▼
       │        Translation Editor (可选)
       │                    │
       └────────────────────┘
               交付
```

---

## 2. 阶段定义

### Phase 0: 项目初始化
**参与者**: Novel Architect  
**输入**: 创作需求  
**输出**: ProjectID、项目目录、初始 Story Bible、spaces.md、dagang.md  

1. 确定 ProjectID。
2. 创建项目目录结构（参考 Shared_Rules.md 第 2.2 节）。
3. 创建 **spaces.md** 初稿——根据故事概要预设重要空间的布局与陈设。
4. 创建 **dagang.md**——用户后续输入新设定/草稿的入口文件。
5. 执行市场分析，确定商业定位。
6. 撰写 Story Bible 初稿。
7. 执行创新检查。

**门槛条件**:
- [ ] 商业定位明确
- [ ] 目标受众清晰
- [ ] 创新检查通过（无重大相似度风险）
- [ ] Story Bible 初稿完成
- [ ] spaces.md 初稿完成

---

### Phase 1: 角色与世界观构建
**参与者**: Character Bible + World Bible（并行）  
**输入**: Story Bible 初稿  
**输出**: Character Bible 初稿、World Bible 初稿、Timeline 初稿  

**Character Bible 工作内容**:
1. 解析 Story Bible 确定角色列表。
2. 为每个角色撰写完整档案（参考 Character_Template.md）。
3. 建立角色关系图。
4. 设计每个角色的成长树。

**World Bible 工作内容**:
1. 解析 Story Bible 确定世界观范围。
2. 撰写文明体系总览。
3. 建立科技树（参考 World_Template.md）。
4. 设计地理位置和空间结构。
5. 完善 **spaces.md** ——根据详细设定补充所有场景空间布局。

**门槛条件**:
- [ ] 所有主要角色完成心理画像
- [ ] 角色成长路径明确
- [ ] 文明体系逻辑自洽
- [ ] 科技树可追溯演化路径
- [ ] 时间线初稿零冲突
- [ ] spaces.md 覆盖全部主要场景

---

### Phase 2: 试写与风格校准
**参与者**: Novel Writer  
**输入**: Character Bible、World Bible、Timeline、spaces.md  
**输出**: 试写章节（3 章）  

1. 校准文学风格（参考 04_Novel_Writer.md 文学风格融合规则）。
2. 撰写第 1-3 章（严格按六步流程执行）。
3. 提交 Novel Editor 初审。

**门槛条件**:
- [ ] 风格一致性检验通过
- [ ] 试写章节通过 Novel Editor 逻辑审查

---

### Phase 3: 正文创作
**参与者**: Novel Writer  
**输入**: 校准后的风格和设定  
**输出**: 各章节正文（逐章交付）  

1. 按章节规划逐章输出（严格按六步流程执行）。
2. 每章提交 Novel Editor 初审。
3. Chapter Goal / Conflict / Payoff / Foreshadow / Emotion Curve / Character Arc 六项指标全部标注。
4. **每章完成后**: 通知 World Bible 更新时间线，通知 Character Bible 更新角色状态。

**每章门槛条件**:
- [ ] 六项指标完整标注
- [ ] 与前章设定一致
- [ ] 空间描写与 spaces.md 一致
- [ ] 节奏指标在阈值内

---

### Phase 4: 编辑评审
**参与者**: Novel Editor  
**输入**: 完成的全部正文  
**输出**: QA 报告（10 大维度）、编辑批注、问题追踪  

**四轮审查**:

| 轮次 | 名称 | 审查内容 | 时间安排 |
|------|------|----------|----------|
| 1 | 逻辑审查 | 10 大 QA 维度（人设/时间/情节/对话/伏笔/称呼/场景/物品/情感/世界观） | 每章完成后立即 |
| 2 | 文学审查 | AI 味 / 重复句式 / 模板化语言 / 结构化句式 / 三连排比 / 表达重复统计 | 全文完成后 |
| 3 | 商业审查 | 章节爽感 / 悬念 / 高潮 / 人物讨喜度 / 弃书风险 | 全文完成后 |
| 4 | 出版审查 | 英文版地道性 / 中文版文学性 / 翻译腔 / AI 语言 / 语法拼写 | 全文完成后 |

**问题追踪**:
- 每轮发现的问题分配 QA ID，按 BLOCKER/CRITICAL/MAJOR/MINOR 分级。
- Novel Writer 修正后提交回归验证。
- 回归测试: 重新检查所有 OPEN 状态的问题。

**门槛条件**:
- [ ] 四轮审查全部完成
- [ ] 无 BLOCKER/CRITICAL 级别问题
- [ ] 商业审查均分 ≥ 7/10
- [ ] 无弃书风险

---

### Phase 5: 创译（可选）
**参与者**: Translation Editor  
**输入**: 编辑后的最终中文版正文  
**输出**: 英文版正文  

1. 文化转换 — 中国特有文化元素转为北美读者可理解的等效元素。
2. 对白重写 — 使对话符合英语母语者的表达习惯。
3. 节奏调整 — 调整句式长度和段落结构适配英语阅读节奏。
4. 幽默与俚语调整 — 替换为北美读者能理解的幽默和俚语。
5. 最终润色。

**门槛条件**:
- [ ] 英文版读起来完全不像翻译
- [ ] 经母语者水平检验

---

## 3. 同步机制

### 3.1 dagang.md 同步
当用户修改了 dagang.md 并要求更新/同步时:
1. 读取 dagang.md 中的 `## 待更新内容` 段落。
2. 识别新剧情、新人物、新空间或设定变更。
3. 冲突检测: 检查新设定是否与已写章节冲突。
4. 同步更新 outline.md / timeline.md / characters.md / spaces.md。
5. 归档: 将待更新内容重命名为"已更新"保留原始。

### 3.2 反向同步
当用户要求"按章节回归大纲"时:
1. 读取已写章节正文。
2. 提取关键情节、时间点和人物信息。
3. 对比当前 outline.md / timeline.md / characters.md / spaces.md。
4. 补充大纲中缺失的章节细节、完善时间线、补充人物成长节点、把正文中已稳定出现的空间布局补入 spaces.md。

---

## 4. 迭代规则

### 4.1 回到前一阶段的条件
- Novel Editor 发布 BLOCKER 级别问题: 退回 Phase 3。
- Novel Architect 发现商业定位偏差: 退回 Phase 0。
- Character Bible 或 World Bible 需要重大修改: 退回 Phase 1。

### 4.2 紧急修改通道
- 单处文本修正不涉及设定变化的，由 Novel Editor 直接修改。
- 涉及设定变化的，需通知相关 Skill 同步更新。

---

## 5. 交付标准

| 交付物 | 责任 Skill | 格式 | 截止条件 |
|--------|-----------|------|----------|
| Story Bible | Novel Architect | Markdown | Phase 0 完成 |
| spaces.md + dagang.md | Novel Architect | Markdown | Phase 0 完成 |
| Character Bible | Character Bible | Markdown (每人一文件) | Phase 1 完成 |
| World Bible | World Bible | Markdown | Phase 1 完成 |
| Timeline | World Bible | Markdown | Phase 1 完成 |
| Dictionary | Novel Architect | Markdown | Phase 1 完成 |
| 各章正文 | Novel Writer | Markdown | Phase 3 完成 |
| QA 报告 | Novel Editor | Markdown | Phase 4 完成 |
| 英文版（可选） | Translation Editor | Markdown | Phase 5 完成 |

---

## 变更日志
| 版本 | 日期 | 变更内容 | 发起人 |
|------|------|----------|--------|
| 1.1 | 2026-07-08 | 新增 spaces.md、dagang.md 初始化和同步流程；新增反向同步机制；完善 QA 追踪与回归测试流程 | CNS-Foundation |
| 1.0 | 2026-07-08 | 初始版本 | CNS-Foundation |
