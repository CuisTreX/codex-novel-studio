# Codex Novel Studio

一套给 Codex（同样适用于 Claude Code 等 AI Agent）使用的**中文长篇小说创作工作流插件**：从需求收集 → 大纲架构 → 人设圣经 → 世界观圣经 → 正文写作 → 编辑修订 → 翻译润色，全流程技能化，配套一整套模板与记忆规范，专门对抗长篇创作中的三大顽疾——**写飞、人设崩塌、前后矛盾**。

## 技能一览

| 技能文件 | 作用 |
| --- | --- |
| `00_User_Input_Prompt.md` | 创作需求收集引导，先问清楚再动笔 |
| `01_Novel_Architect.md` | 大纲架构：分卷、分章、节奏曲线 |
| `02_Character_Bible.md` | 人设圣经：角色档案、关系网、成长线 |
| `03_World_Bible.md` | 世界观圣经：设定、规则、地理与势力 |
| `04_Novel_Writer.md` | 正文写作：按大纲逐章产出，保持文风一致 |
| `05_Novel_Editor.md` | 编辑修订：一致性校对、伏笔回收检查 |
| `06_Translation_Editor.md` | 翻译润色：多语言版本输出 |

配套模板：`Story_Bible_Template`（故事圣经）、`Character_Template`（人设）、`World_Template`（世界观）、`Timeline_Template`（时间线）、`Dictionary_Template`（名词词典）、`Dagang_Template`（大纲）、`Spaces_Template`（场景空间），以及贯穿全程的 `Workflow.md`（工作流编排）、`Memory_Spec.md`（记忆规范）、`Shared_Rules.md`（共享写作规则）。

## 目录结构

```
.agents/plugins/marketplace.json      # 本地插件市场清单
plugins/codex-novel-studio/           # 插件本体
  ├─ .codex-plugin/plugin.json        # 插件清单
  └─ skills/                          # 全部技能与模板
release/                              # 发布包（zip + 发布说明）
```

## 安装（Codex CLI）

1. 将 `plugins/codex-novel-studio/` 放入你的插件源目录（或解压 `release/` 中的发布包）；
2. 确认 `marketplace.json` 指向该目录；
3. 执行：

```bash
codex plugin add codex-novel-studio@<marketplace-name>
```

4. **新开会话**后生效（已开会话不会加载新插件）。

## 使用

新会话中直接说：

> 我想用 Codex Novel Studio 开始一部新小说，请先展示创作需求模板并引导我填写。

插件会从需求收集开始，一步步带你走完整个创作流程。

## 版本

当前版本：`0.1.0+codex.20260820133407`，已通过 plugin-creator 的 `validate_plugin.py` 校验。
