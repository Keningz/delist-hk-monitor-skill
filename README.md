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

## Git / GitHub workflow

### Branch
- Default branch: `main`

### Push normal updates
```bash
git add .
git commit -m "update skill"
git push origin main
```

### Create a version tag (when you want to publish a version)
```bash
git tag v1.0.0
git push origin v1.0.0
```

Tag convention:
- `v1.0.0` major release
- `v1.0.1` patch fix
- `v1.1.0` minor feature

### CI packaging
This repo includes GitHub Actions workflow:
- `.github/workflows/package-skill.yml`
- Triggered on `SKILL.md` changes (or manual trigger)
- Produces `delist-hk-monitor.skill` as an artifact

### Repository
- https://github.com/Keningz/delist-hk-monitor-skill
