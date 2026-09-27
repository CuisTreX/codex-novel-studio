# codex-novel-studio 发布包

版本: 0.1.0+codex.20260805153353
发布日期: 2026-08-05
来源: F:\CodeX\codex-novel-studio-plugin\plugins\codex-novel-studio

## 包内容
- .codex-plugin/plugin.json — 插件清单
- skills/ — 16 个小说写作技能文件（架构、人设、世界观、写作、编辑、翻译及各类模板）

## 安装方式（在 Codex 中）
1. 解压后得到 codex-novel-studio/ 目录，放入插件源目录（如仓库的 plugins/ 下）。
2. 确认 marketplace 指向该目录后执行：
   codex plugin add codex-novel-studio@<marketplace-name>
3. 在新开的会话中使用该插件（新会话才会加载新 skill）。

## 校验
已通过 plugin-creator 的 validate_plugin.py 校验。
