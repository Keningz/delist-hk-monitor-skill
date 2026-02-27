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

## Install / Use

### Option A: Download from Release
1. Open Releases: `https://github.com/Keningz/delist-hk-monitor-skill/releases`
2. Download `delist-hk-monitor.skill`
3. Import/install this `.skill` in your OpenClaw environment.

### Option B: Use source directly
- Copy `SKILL.md` into your skill folder as `delist-hk-monitor/SKILL.md`
- Ensure paths/targets in the skill match your own environment before running.

## Notes
- This skill is opinionated for Kening's DelistHK workflow (HKEX filters + Obsidian structure + Discord reporting).
- If you fork for your own setup, adjust Obsidian path and message target first.
