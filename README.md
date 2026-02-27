# delist-hk-monitor

一个可复用的 OpenClaw Skill，用于监控港交所（HKEX）私有化/撤销上市相关公告，并更新 DelistHK 的 Obsidian 文档。

## 文件说明
- `SKILL.md`：Skill 源定义文件
- `delist-hk-monitor.skill`：打包后的 Skill 文件

## 功能范围
- 使用固定筛选条件检索港交所私有化/撤销上市公告
- 增量判重（避免重复处理）
- 更新 `index.md`、`logs/YYYY-MM-DD.md`、`companies/*.md`、`fail-log.md`
- 通过 Discord 私聊发送汇报

## 安装 / 使用

### 方式 A：从 Release 下载（推荐）
1. 打开 Releases 页面：`https://github.com/Keningz/delist-hk-monitor-skill/releases`
2. 下载 `delist-hk-monitor.skill`
3. 在你的 OpenClaw 环境中导入/安装该 `.skill`

### 方式 B：直接使用源码
- 将 `SKILL.md` 放入你的 skill 目录：`delist-hk-monitor/SKILL.md`
- 运行前请先按你的环境修改路径与通知目标。

## 注意事项
- 该 Skill 默认偏向 Kening 的 DelistHK 工作流（HKEX 筛选 + Obsidian 目录 + Discord 汇报）。
- 如果你要 fork 到自己的环境，建议先调整：
  1) Obsidian 路径
  2) 消息通知目标（频道/用户）
