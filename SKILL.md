---
name: delist-hk-monitor
description: "Monitor HKEX privatization and delisting announcements and maintain the DelistHK Obsidian project files. Use when running manual or scheduled checks for HKEX disclosure announcements with filters 公告及通告 → 重组/股权变动/主要改动/公众持股量/上市地位 → 私有化/撤销或取消证券上市, then update index.md, logs/YYYY-MM-DD.md, companies/*.md, and fail-log.md."
---

# DelistHK Monitor

Use this workflow for Kening's DelistHK project.

## Fixed project paths
- Vault root: `/opt/obsidian-webdav/data/vaults/ClawNotes`
- Project root: `/opt/obsidian-webdav/data/vaults/ClawNotes/Warren/projects/DelistHK`
- Index: `index.md`
- Logs: `logs/YYYY-MM-DD.md`, `logs/fail-log.md`
- Company files: `companies/<5位代码><公司简称>.md`

## Backup rule (mandatory)
Before editing any existing file, create backup:
- `<name>.bak(YYYY-MM-DD-HHMMUTC).md`
- Keep at most 2 backups per source file; if more than 2 exist, delete oldest backups first.

## HKEX browser search steps
1. Open: `https://www1.hkexnews.hk/search/titlesearch.xhtml?lang=zh`
2. Set filters:
   - 标题类别: `公告及通告` (`t1code=10000`)
   - 子类别: `重组/股权变动/主要改动/公众持股量/上市地位` (`t2Gcode=7`)
   - 细分类: `私有化/撤销或取消证券上市` (`t2code=17600`)
3. Set date range (`from`, `to`) as `YYYY/MM/DD`.
4. Click `搜尋`.
5. Parse result rows with fields:
   - 发放时间
   - 股票代码
   - 公司简称
   - 公告标题
   - PDF链接

## Incremental rule
Use unique key:
- `pdf_url + 发布时间 + 股票代码`

If key already exists in history, treat as duplicate.

## File update rules
1. Update `index.md`:
   - If code already in “正在进行的私有化”: update row.
   - If new: append row in “正在进行的私有化”.
   - If title indicates delisted/completed: move row to “已经结束的私有化”.
2. Update company file:
   - If missing, create from `companies/00000案例公司.md` structure.
   - Update latest date, stage, summary, source link, and timeline row.
3. If a fetched document is a scheme/circular/proposal document (e.g., contains `計劃`, `協議安排`, `要約`, `私有化建議`):
   - Read document carefully (prefer direct PDF download + text extraction when browser PDF DOM is unreadable).
   - Extract and write structured terms into company file under offer section:
     - offer structure (cash / share / mixed)
     - cancellation consideration per share (exact official wording)
     - pre-conditions for making proposal/offer
     - implementation conditions (e.g., court meeting thresholds, approvals, waivers)
     - waiver scope (which conditions are non-waivable / waivable)
   - Prefer official announcement wording over media summaries.
4. Write `logs/YYYY-MM-DD.md`:
   - run time, duration, date range, hit count, new count, duplicate count, detail table.
5. On failure, append one row to `logs/fail-log.md`.

## Stage mapping (default)
- 含“每月更新” -> `每月更新`
- 含“法院批准” -> `法院批准`
- 含“法院会议/股东特别大会结果” -> `股东会结果`
- 含“生效/撤销上市地位生效/除牌” -> `已结束` (and move to finished table)
- Otherwise -> `进展更新`

## Execution modes
- Manual run: user provides explicit date range.
- Daily run: derive date range from latest valid `logs/YYYY-MM-DD.md`; fallback to last 30 days if missing or >31 days.

## Discord notification (default)
After each run, send a Discord DM report via `message` tool:
- `channel`: `discord`
- `target`: `channel:1476513117759340615`

Send policy (default):
1. Success with new items: send full summary + item list.
2. Success with zero new items: send `今日无新增私有化公告` + date range.
3. Failure: send `检查失败告警` + failure stage + error summary.

## Output format
Always include:
- searched date range
- total hits
- new items count
- top-level bullets for each new item (if any)
- failure note if any
