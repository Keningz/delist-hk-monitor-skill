# delist-hk-monitor

Reusable OpenClaw skill for monitoring HKEX privatization/delisting announcements and updating DelistHK Obsidian docs.

## Files
- `SKILL.md` — source skill definition
- `delist-hk-monitor.skill` — packaged artifact

## Scope
- HKEX title search with fixed filters for privatization/delisting
- Incremental detection
- Update `index.md`, `logs/YYYY-MM-DD.md`, `companies/*.md`, `fail-log.md`
- Discord DM reporting
