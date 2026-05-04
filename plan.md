# MONOREPO_PLAN.md
<!-- Save this file as MONOREPO_PLAN.md at the repository root when plan mode exits. -->
<!-- Audit date: 2026-05-03 | Repository: SchnappAPI/sports-modeling -->

---

# Section 1 — Cross-Reference Index

All factual claims recorded with `file:line`. Occurrences of the same entity are grouped. Depth counted from repository root.

---

## 1.1 Project Identity

| Entity | Value | Source(s) |
|--------|-------|-----------|
| Project name (npm) | `sports-modeling-web` | `web/package.json:2` |
| Project name (GitHub) | `SchnappAPI/sports-modeling` | `docs/CONNECTIONS.md:80`, `web/app/api/refresh-data/route.ts:16-17` |
| Brand name | `Schnapp` (schnapp.bet) | `CLAUDE.md:7`, `web/public/manifest.json:2` |
| Default branch | `main` | `docs/CONNECTIONS.md:81` |
| Repo visibility | private | `docs/CONNECTIONS.md:80` |

---

## 1.2 Stack Versions

| Entity | Value | Source(s) |
|--------|-------|-----------|
| Next.js | `15.2.8` | `web/package.json:16`, `web/README.md:3` |
| React | `^19` | `web/package.json:17` |
| Node.js (engine requirement) | `20.x` | `web/package.json:6` |
| Node.js (Windows laptop) | `24.12.0` | `docs/CONNECTIONS.md:265` |
| TypeScript | `^5` | `web/package.json:28` |
| mssql (npm) | `^11` | `web/package.json:15` |
| tailwindcss | `^3` | `web/package.json:27` |
| Python | `3.12.13` | `docs/CONNECTIONS.md:87` |
| SQLAlchemy | `2.0.49` | `etl/requirements.txt:1` |
| pyodbc | `5.3.0` | `etl/requirements.txt:2` |
| pandas | `3.0.2` | `etl/requirements.txt:3` |
| numpy | `2.4.4` | `etl/requirements.txt:4` |
| requests | `2.33.1` | `etl/requirements.txt:5`, `docs/CONNECTIONS.md:136` |
| nba_api | `1.11.4` | `etl/requirements.txt:6` |
| mlb-statsapi | `1.7.2` | `etl/requirements.txt:7` |
| nflreadpy | `0.1.5` | `etl/requirements.txt:8`, `etl/nfl/README.md:19`, `docs/CONNECTIONS.md:87` |
| pyarrow | `24.0.0` | `etl/requirements.txt:9`, `docs/CONNECTIONS.md:87` |
| scipy | `1.17.1` | `grading/requirements.txt:1` |
| ODBC Driver for SQL Server | `18` (18.6.2.1) | `docs/CONNECTIONS.md:88`, `infrastructure/README.md:55` |
| unixODBC | `2.3.14` | `docs/CONNECTIONS.md:88`, `infrastructure/README.md:55` |
| GitHub Actions runner | `2.334.0` | `infrastructure/README.md:50` |
| claude CLI (Mac) | `2.1.126` | `CLAUDE.md:102`, `docs/CONNECTIONS.md:277` |
| gh CLI (Mac) | `2.92.0` | `CLAUDE.md:102`, `docs/CONNECTIONS.md:278` |
| SQL Server Docker | `2022` | `CLAUDE.md:9`, `docs/CONNECTIONS.md:35`, `infrastructure/README.md:138` |
| Flask | `3.1.3` | `docs/CONNECTIONS.md:172` |
| macOS on Schnapps-MBP | `14.8.5` | `docs/CONNECTIONS.md:84`, `infrastructure/README.md:49` |

---

## 1.3 Environment Variables

| Variable | Value / Default | Referenced In |
|----------|-----------------|---------------|
| `SQL_CONNECTION_STRING` | `Server=localhost,1433;Database=sports-modeling;User Id=sa;Password=...;Encrypt=true;TrustServerCertificate=true;` | `web/lib/db.ts:17`, `docs/CONNECTIONS.md:56`, `infrastructure/README.md:152` |
| `RUNNER_URL` | prod: `https://mac-flask.schnapp.bet`; dev: `http://127.0.0.1:5000`; default in code (stale): `https://live.schnapp.bet` | `web/README.md:22`, `web/app/api/games/route.ts:4`, `web/app/api/live-boxscore/route.ts:13`, `web/app/api/scoreboard/route.ts:6`, `infrastructure/README.md:153` |
| `RUNNER_API_KEY` | `runner-Lake4971` | `web/app/api/games/route.ts:5`, `web/app/api/live-boxscore/route.ts:14`, `web/app/api/scoreboard/route.ts:7`, `docs/CONNECTIONS.md:61`, `infrastructure/README.md:154`, `etl/runner.py:45` |
| `ADMIN_PASSCODE` | `Sports#2026` | `web/app/api/refresh-data/route.ts:27`, `docs/CONNECTIONS.md:57` |
| `AUTH_TOKEN_SECRET` | `schnapp-secret-2026-xk9` (default in code: `fallback-dev-secret-change-me`) | `web/app/api/auth/validate/route.ts:5`, `web/app/api/auth/check/route.ts:5`, `docs/CONNECTIONS.md:58` |
| `ADMIN_REFRESH_CODE` | `GO` | `web/app/api/refresh-data/route.ts:34`, `docs/CONNECTIONS.md:59` |
| `GITHUB_PAT` | fine-grained PAT (expires 2027-03-29) | `web/app/api/refresh-data/route.ts:47`, `web/app/api/refresh-lines/route.ts:8`, `docs/CONNECTIONS.md:62`, `infrastructure/README.md:155` |
| `ODDS_API_KEY` | `e79c9e6b3d9a5e7166602935ee0fb9f6` | `docs/CONNECTIONS.md:63`, `docs/CONNECTIONS.md:252` |
| `AZURE_SQL_SERVER` | now `localhost,1433` | GitHub Actions secret (32 workflows), `etl/db.py`, `infrastructure/README.md:192` |
| `AZURE_SQL_DATABASE` | now `sports-modeling` | GitHub Actions secret (32 workflows), `infrastructure/README.md:192` |
| `AZURE_SQL_USERNAME` | now `sa` | GitHub Actions secret (32 workflows), `infrastructure/README.md:192` |
| `AZURE_SQL_PASSWORD` | SA password from `/Users/schnapp/sql-server.env` | GitHub Actions secret (32 workflows), `infrastructure/README.md:192` |
| `AZURE_SQL_TRUST_CERT` | `yes` | `etl/db.py:7`, `.github/workflows/nba-game-day.yml:36`, `.github/workflows/grading.yml:42` |
| `NBA_PROXY_URL` | `http://bfoopdzv-rotate:eftihw9lhmd7@p.webshare.io:80/` | `docs/CONNECTIONS.md:236`; GitHub Actions secret (6 workflows) |
| `MAC_MCP_AUTH_TOKEN` | (gates shell_exec/read_file/write_file on Mac MCP) | `docs/CONNECTIONS.md:146`, `infrastructure/README.md:114` |
| `GH_PAT` | same value as `GITHUB_PAT` | Mac MCP plist; GitHub Actions secret (0 refs — ORPHAN per `docs/CONNECTIONS.md:107`) |
| `MCP_AUTH_TOKEN` | — | GitHub Actions secret (0 refs — ORPHAN per `docs/CONNECTIONS.md:108`) |
| `CLAUDE_CODE_OAUTH_TOKEN` | 1-year token from `claude setup-token` | `.github/workflows/claude.yml:35`, `docs/CONNECTIONS.md:285` |

---

## 1.4 URLs and Hostnames

| Hostname / URL | Backend | Status |
|---------------|---------|--------|
| `schnapp.bet`, `www.schnapp.bet` | Mac Next.js prod `:3001` via schnapp-mac tunnel | live |
| `prod.schnapp.bet` | Mac Next.js prod `:3001` via schnapp-mac tunnel | live (redundant alias) |
| `dev.schnapp.bet` | Mac Next.js dev `:3000` via schnapp-mac tunnel | live |
| `mac-flask.schnapp.bet` | Mac Flask `:5000` via schnapp-mac tunnel | live |
| `mac-mcp.schnapp.bet/mcp` | Mac MCP `:8765` via schnapp-mac tunnel | live |
| `github-mcp.schnapp.bet` | GitHub MCP proxy `:8766` via schnapp-mac tunnel | live |
| `https://live.schnapp.bet` | — | **DEAD** — DNS deleted 2026-05-01 (`docs/CONNECTIONS.md:203`) |
| `https://mcp.schnapp.bet/mcp` | — | **DEAD** — DNS deleted 2026-05-01 (`docs/CONNECTIONS.md:163`) |
| `sports-modeling-server.database.windows.net` | — | **DELETED** 2026-05-03 (`docs/CONNECTIONS.md:20`) |
| `https://cdn.nba.com/static/json/liveData/scoreboard/todaysScoreboard_00.json` | NBA CDN | public, no auth |
| `https://cdn.nba.com/static/json/liveData/boxscore/boxscore_{game_id}.json` | NBA CDN | public, no auth |
| `https://statsapi.mlb.com/api/v1/game/{game_pk}/withMetrics` | MLB Stats API | public, no auth |
| `https://api.github.com/repos/SchnappAPI/sports-modeling/actions/workflows/{workflow}/dispatches` | GitHub Actions REST | PAT auth |
| Webshare proxy | `http://bfoopdzv-rotate:eftihw9lhmd7@p.webshare.io:80/` | NBA Stats API proxy |

---

## 1.5 Service Configuration

| Service | Managed by | Port | Code | Log path |
|---------|-----------|------|------|----------|
| Next.js prod | `bet.schnapp.web-prod` (launchd) | `127.0.0.1:3001` | `/Users/schnapp/sports-modeling/web` | `web/web-prod.log`, `web/web-prod.err.log` |
| Next.js dev | `bet.schnapp.web` (launchd) | `127.0.0.1:3000` | `/Users/schnapp/sports-modeling/web` | `web/web.log`, `web/web.err.log` |
| Flask live-data | `bet.schnapp.flask` (launchd) | `0.0.0.0:5000` | `etl/runner.py` | `etl/flask.log`, `etl/flask.err.log` |
| Mac MCP | `com.schnapp.macmcp` (launchd) | `127.0.0.1:8765` | `/Users/schnapp/mac-mcp/server.py` | `/Users/schnapp/mac-mcp/mcp.log` |
| Cloudflare tunnel | `com.cloudflare.cloudflared` (system launchd) | — | `schnapp-mac` tunnel ID `844a3714-9bd3-409e-a672-a6840c94e68e` | — |
| GitHub Actions runner | `actions.runner.SchnappAPI-sports-modeling.mac-runner-1` (launchd) | — | `/Users/schnapp/actions-runner/` | `~/Library/Logs/actions.runner.SchnappAPI-sports-modeling.mac-runner-1/` |
| SQL Server 2022 | Docker container `mssql` on Colima | `localhost,1433` | — | — |

---

## 1.6 Database Schemas and Tables

**Schemas:** `nba`, `mlb`, `nfl`, `odds`, `common` — one database (`sports-modeling`), five schemas (`database/README.md:5-11`).

**common.***: `user_codes`, `user_activations`, `demo_config`, `feature_flags`, `teams`, `player_line_patterns`, `daily_grades`, `player_tier_lines`, `ingest_quarantine`, `unmapped_entities`, `data_completeness_log`, `workflow_runs`

**nba.***: `schedule`, `games`, `teams`, `players`, `player_box_score_stats`, `player_passing_stats`, `player_rebound_chances`, `daily_lineups`

**mlb.***: `teams`, `players`, `games`, `batting_stats`, `pitching_stats`, `player_season_batting`, `pitcher_season_stats`, `play_by_play`, `player_at_bats`, `career_batter_vs_pitcher`, `player_trend_stats`

**nfl.***: `games`, `players`, `player_game_stats`, `snap_counts`, `ftn_charting`, `rosters_weekly`, `team_game_stats`

**odds.***: `events`, `game_lines`, `upcoming_events`, `upcoming_game_lines`, `upcoming_player_props`, `event_game_map`, `team_map`, `player_map`

---

## 1.7 GitHub Actions Workflows (active)

| Workflow file | Trigger | Runner | Purpose |
|--------------|---------|--------|---------|
| `deploy-web.yml` | push main `web/**`, workflow_dispatch | mac-runner | Build + deploy Next.js |
| `nba-game-day.yml` | cron `30 9 * * *` + `*/15 0-6` + `*/15 22-23`, workflow_dispatch | mac-runner | Live NBA scoreboard, odds, grading, lineup |
| `nba-etl.yml` | cron `0 9 * * *` | mac-runner | Box scores, PT stats, schedule, rosters |
| `odds-etl.yml` | cron `0 10 * * *`, workflow_dispatch | mac-runner | FanDuel lines; triggers `grading.yml` via workflow_run |
| `grading.yml` | cron `0 11 * * *`, workflow_dispatch, workflow_run (odds-etl) | mac-runner | NBA/MLB prop grading |
| `mlb-etl.yml` | cron `0 9 * * *` | mac-runner | MLB nightly |
| `mlb-grading.yml` | cron `30 11 * * *` | mac-runner | MLB prop grading |
| `mlb-pbp-etl.yml` | workflow_dispatch | mac-runner | Play-by-play loader |
| `nfl-etl.yml` | cron `0 9 * * 2` | mac-runner | NFL weekly |
| `refresh-data.yml` | workflow_dispatch | mac-runner | Full data refresh (intraday mode) |
| `refresh-lines.yml` | cron `0 17,20,23 * * *` | mac-runner | Odds + upcoming grading |
| `compute-patterns.yml` | cron `30 7 * * *` | mac-runner | `common.player_line_patterns` |
| `weekly-calibration.yml` | cron `0 6 * * 0` | mac-runner | Grading calibration |
| `nba-backfill.yml` | workflow_dispatch (dispatched by nba-game-day) | mac-runner | Odds + grade backfill for final games |
| `odds-backfill-weekly.yml` | cron `0 11 * * 1` | mac-runner | Weekly odds backfill |
| `daily-health-report.yml` | scheduled | mac-runner | Data integrity report |
| `retry-incomplete.yml` | scheduled | mac-runner | Retry incomplete data |
| `resolve-mappings.yml` | workflow_dispatch | mac-runner | Odds entity mapping |
| `cleanup-stale-odds.yml` | workflow_dispatch | mac-runner | Clean stale odds rows |
| `retroactive-scan.yml` | workflow_dispatch | mac-runner | Integrity retroactive scan |
| `seed-user-codes.yml` | workflow_dispatch | mac-runner | Seed access codes |
| `grades-migrate.yml` | workflow_dispatch | mac-runner | Schema migration helper |
| `migrate-common-teams.yml` | workflow_dispatch | mac-runner | Schema migration helper |
| `claude.yml` | issue_comment, PR review, issue opened/assigned | ubuntu-latest | Claude Code integration |

Archived workflows (17 in `.github/workflows/_archive/`): mac-mirror variants, investigation utilities, phase-cutover scripts — no active triggers.

---

## 1.8 ADR References

| ADR | Decision | Source |
|-----|----------|--------|
| ADR-0001 | Documentation hierarchy restructure | `docs/README.md:27` |
| ADR-0002 | ETL code files stay flat in `/etl/` | `etl/README.md:23` |
| ADR-0003 | MLB web view spec (6 views) | `web/mlb/README.md`, `docs/ROADMAP.md:21` |
| ADR-0004 | MLB 9-entity data vision | `web/mlb/README.md:3` |
| ADR-0007 | FanDuel bookmaker only | `etl/_shared/README.md:93` |
| ADR-0017 | Opportunity grades | `web/nba/README.md:78` |
| ADR-0019 | SQL Server tuple-IN workaround | `web/mlb/README.md:109` |
| ADR-20260423-1 | KDE tier lines; composite grade 40/40/20 | `database/nba/README.md:85` |
| ADR-20260424-2 | Data integrity framework (3-layer) | `etl/integrity.py`, `etl/_shared/README.md` |
| ADR-20260424-3 | Initiative B streamlining | `etl/_shared/README.md:16` |
| ADR-20260426-2 | Mac-mirror workflow pattern | `infrastructure/README.md:57` |
| ADR-20260427-1 | VM workflows migrated to mac-runner | `infrastructure/README.md:61` |
| ADR-20260501-3 | Initiative B: DRY pass (nfl_etl → etl.db) | `docs/ROADMAP.md:16` |
| ADR-20260501-4 | Initiative C: Observability layer | `docs/ROADMAP.md:17` |
| ADR-20260501-5 | MLB player table accumulate-across-seasons | `docs/ROADMAP.md:18` |
| ADR-20260503-1 | Azure SQL decommission; rename AZURE_SQL_CONNECTION_STRING → SQL_CONNECTION_STRING (web only) | `docs/DECISIONS.md`, `docs/CONNECTIONS.md:23` |

---

## 1.9 Key Path Aliases and Import Patterns

| Path | Resolution | Source |
|------|-----------|--------|
| `@/*` (TypeScript) | `./web/*` | `web/tsconfig.json:17` |
| `from etl.db import get_engine, upsert` | `etl/db.py` | `etl/mlb_etl.py`, `etl/nba_etl.py`, `etl/nfl_etl.py` |
| `from etl.integrity import validate_and_filter, ensure_tables` | `etl/integrity.py` | `etl/nba_etl.py:73-78` |
| `grading/grade_props.py` imports `get_engine` | `etl/db.py` via sys.path hack | `etl/_shared/README.md:46` |

---

# Section 2 — Inconsistencies

## 2.1 Resolved

### R-01 — README.md still claims Azure SQL is a live dependency
- **Conflict:** `README.md:9` says "production web tier still queries Azure SQL Serverless directly (the one remaining Azure dependency)."
- **Reality:** Azure SQL was deleted 2026-05-03. All consumers on local SQL Server since that date.
- **Authoritative source:** `docs/CONNECTIONS.md:20-23`, `docs/CHANGELOG.md` (top entry), `CLAUDE.md:9`. CONNECTIONS.md is a dedicated config file at a more specific path and more recently updated.
- **Resolution:** `README.md:9` is stale — needs one-line update to remove the Azure SQL claim.

### R-02 — `etl/runner.py` claims systemd manages the Flask service
- **Conflict:** `etl/runner.py:24` comment says "Managed by: systemd service `schnapp-flask.service`."
- **Reality:** Flask runs as launchd user agent `bet.schnapp.flask` on Schnapps-MBP (macOS). There is no systemd on the Mac.
- **Authoritative source:** `infrastructure/README.md:83-93`, `docs/CONNECTIONS.md:170`, `CLAUDE.md:9`. Infrastructure README is the dedicated service documentation.
- **Resolution:** `etl/runner.py:24` comment is stale — reflects the decommissioned Azure VM era.

### R-03 — `RUNNER_URL` default in three web API route files points to a deleted hostname
- **Conflict:** `web/app/api/games/route.ts:4`, `web/app/api/live-boxscore/route.ts:13`, `web/app/api/scoreboard/route.ts:6` all default `RUNNER_URL` to `https://live.schnapp.bet`.
- **Reality:** `live.schnapp.bet` DNS was deleted 2026-05-01. Production plists always set `RUNNER_URL=https://mac-flask.schnapp.bet`. The default is never reached in production or dev.
- **Authoritative source:** `infrastructure/README.md:207` explicitly states "default https://live.schnapp.bet is dead code — DNS deleted 2026-05-01."
- **Resolution:** Infrastructure README acknowledges this explicitly. The dead default is harmless as long as the env var is always set, but it creates confusion. Updating the default to `https://mac-flask.schnapp.bet` would eliminate the confusion.

### R-04 — `etl/_shared/README.md` attributes 60s retry wait to "Azure Serverless cold start"
- **Conflict:** `etl/_shared/README.md:46` explains the grading engine's 60s retry wait as needed for Azure Serverless cold starts.
- **Reality:** Azure SQL was deleted 2026-05-03. The retry logic itself is still valid (local SQL Server in a Docker container can also have startup latency), but the stated reason is stale.
- **Authoritative source:** `docs/CHANGELOG.md` (ADR-20260503-1). The behavior is correct; the documented rationale is stale.
- **Resolution:** Update the comment to say "local SQL Server Docker startup" rather than "Azure Serverless cold start."

### R-05 — pyarrow version discrepancy (historical note vs. current pin)
- **Conflict:** `etl/nfl/README.md:20` notes "pyarrow (23.0.1 at first run)." `etl/requirements.txt:9` pins `pyarrow==24.0.0`.
- **Reality:** Not an actual conflict. The README records the version installed when the NFL ETL first ran (2026-04-21). requirements.txt has since been updated to 24.0.0. The README is a historical note, not a pin.
- **Authoritative source:** `etl/requirements.txt` governs the installed version.
- **Resolution:** No action required; both statements are true in context. Optional: update the README historical note to add "(updated to 24.0.0)" for clarity.

### R-06 — GitHub Actions secrets still named `AZURE_SQL_*` despite targeting localhost
- **Conflict:** `AZURE_SQL_SERVER`, `AZURE_SQL_DATABASE`, `AZURE_SQL_USERNAME`, `AZURE_SQL_PASSWORD` are used in 32 workflows but now target `localhost,1433` (local SQL Server).
- **Reality:** This is an intentional naming decision. `docs/CONNECTIONS.md:23` explicitly documents: "GitHub Actions secrets updated 2026-05-03 to target localhost,1433/sa." Names were preserved to avoid updating 32 workflow files. ADR-20260503-1.
- **Authoritative source:** `docs/CONNECTIONS.md:23`, `docs/DECISIONS.md` (ADR-20260503-1).
- **Resolution:** No action required — intentional by ADR-20260503-1.

---

## 2.2 Unresolved

### U-01 — `AZURE_SQL_TRUST_CERT` env var was not renamed alongside the web-tier rename
- **Issue:** ADR-20260503-1 renamed `AZURE_SQL_CONNECTION_STRING` → `SQL_CONNECTION_STRING` for the web tier. The ETL tier still uses `AZURE_SQL_TRUST_CERT` (referenced in `etl/db.py:7` and all 25 mac-runner workflow YAML files as `AZURE_SQL_TRUST_CERT=yes`).
- **The rename was scoped:** ADR-20260503-1 appears to have only renamed the web connection string, not the ETL env vars. Whether `AZURE_SQL_TRUST_CERT` was supposed to be renamed to `SQL_TRUST_CERT` is not stated in any ADR.
- **Why unresolved:** The decision doc does not address the `_TRUST_CERT` variable. Renaming it would require updating `etl/db.py`, all 25 `mac-runner` workflow YAMLs, and the GitHub Actions secret. Not renaming leaves a conceptually misleading `AZURE_*` name pointing at a local container.
- **Human decision required:** Should `AZURE_SQL_TRUST_CERT` be renamed to `SQL_TRUST_CERT` to match the pattern established by `SQL_CONNECTION_STRING`?

### U-02 — Sensitive credentials in plaintext in `docs/CONNECTIONS.md` (checked into repo)
- **Issue:** The following credentials appear in plaintext in `docs/CONNECTIONS.md`, which is committed to the repository:
  - `ODDS_API_KEY`: `e79c9e6b3d9a5e7166602935ee0fb9f6` (`:252`)
  - `NBA_PROXY_URL` with embedded password: `http://bfoopdzv-rotate:eftihw9lhmd7@p.webshare.io:80/` (`:236`)
  - `AUTH_TOKEN_SECRET`: `schnapp-secret-2026-xk9` (`:58`)
  - `ADMIN_PASSCODE`: `Sports#2026` (`:57`)
  - `RUNNER_API_KEY`: `runner-Lake4971` (`:61`, also in `web/app/api/games/route.ts:5`)
  - `SQL_CONNECTION_STRING` with SA password (`:56`)
- **Context:** The repo is private (`docs/CONNECTIONS.md:80`). The author appears to have made an explicit decision to store operational context in version control for a single-developer private repo.
- **Why unresolved:** This is a security posture decision, not a technical inconsistency. For a solo-developer private repo the risk is low; for a paid-subscription product with user data, the risk profile changes.
- **Human decision required:** Should `docs/CONNECTIONS.md` be moved to a gitignored file, or should credentials be replaced with references to their GitHub Actions secret names and Mac plist locations (retaining operational context without storing the literal values)?

### U-03 — `grading/` imports from `etl.db` without a formal dependency declaration
- **Issue:** `grading/grade_props.py` adds the repo root to `sys.path` and imports `from etl.db import get_engine`. This is a runtime path hack, not a declared package dependency. The `grading/requirements.txt` contains only `scipy==1.17.1` and makes no reference to `etl`.
- **Why unresolved:** In the current flat-single-machine setup this works fine. It becomes a problem if `grading/` ever runs in a separate environment or if `etl/db.py` is moved.
- **Human decision required:** Should `etl/db.py` (and `etl/integrity.py`) be extracted into a shared internal package (e.g., `packages/data/`) that both `etl/` and `grading/` can declare as a proper dependency?

---

# Section 3 — Current State Assessment

## 3.1 What actually exists

The repository is already physically structured as a monorepo — multiple workloads under a single git root — but has no formal workspace tooling at the root level:

- **One npm package:** `web/package.json` is the only `package.json`. There is no root-level `package.json` and no workspace declarations (no `workspaces` field, no `pnpm-workspace.yaml`, no `turbo.json`).
- **No Python package structure:** Python code is managed with a flat `etl/requirements.txt` and a separate `grading/requirements.txt`. There is no `pyproject.toml`, no `uv.lock`, and no Python workspace tooling. The `etl/` directory functions as an implicit Python package only through `sys.path` manipulation.
- **No shared tooling config at root:** No root-level `tsconfig.json`, no `eslint.config.js`, no `prettier.config.js`, no `Makefile`, no root `README` that documents workspace commands.

The repo tree:

```
/
├── .claude/                   # Claude Code config (gitignored except settings/skills/etc.)
├── .github/
│   └── workflows/             # 26 active + 17 archived workflow YAMLs
├── CLAUDE.md                  # Root session instructions (depth 1)
├── README.md                  # Stale (Azure SQL ref)
├── .gitignore
├── docs/                      # Project-wide docs hub
│   ├── README.md              # Doc router
│   ├── SESSION_PROTOCOL.md
│   ├── CHANGELOG.md
│   ├── DECISIONS.md
│   ├── CONNECTIONS.md         # Infra + credentials reference
│   ├── ROADMAP.md
│   ├── HEALTH.md
│   └── GLOSSARY.md / PRODUCT_BLUEPRINT.md / etc.
├── infrastructure/
│   └── README.md              # Infra docs only (no code)
├── database/
│   ├── README.md              # DB docs only (no .sql files)
│   ├── _shared/README.md
│   ├── nba/README.md
│   ├── mlb/README.md
│   └── nfl/README.md
├── etl/                       # Python ETL — flat per ADR-0002
│   ├── db.py                  # Shared: SQLAlchemy engines + upsert
│   ├── integrity.py           # Shared: 3-layer data integrity framework
│   ├── runner.py              # Flask live-data proxy (conceptually a microservice)
│   ├── odds_etl.py
│   ├── nba_etl.py
│   ├── nba_live.py
│   ├── mlb_etl.py
│   ├── mlb_play_by_play.py
│   ├── nfl_etl.py
│   ├── game_day_gate.py
│   ├── lineup_poll.py
│   ├── record_run.py
│   ├── requirements.txt       # All ETL deps (pinned)
│   ├── _shared/README.md      # Docs only
│   ├── nba/README.md          # Docs only
│   ├── mlb/README.md          # Docs only
│   └── nfl/README.md          # Docs only
├── grading/
│   ├── grade_props.py         # Grading engine; imports from etl.db via sys.path hack
│   └── requirements.txt       # scipy only
├── mcp/
│   └── server.py              # Legacy VM MCP code (kept for reference; not deployed)
└── web/                       # Next.js 15 app
    ├── package.json           # The only package manifest in the repo
    ├── next.config.mjs
    ├── tsconfig.json
    ├── tailwind.config.ts
    ├── middleware.ts
    ├── README.md
    ├── app/                   # Next.js App Router routes + 37 API routes
    ├── components/            # React components (NBA-dominated)
    ├── lib/                   # Shared TS utilities (db.ts, queries.ts, etc.)
    ├── _shared/               # Cross-sport component work-in-progress
    ├── nba/README.md          # Docs only
    ├── mlb/README.md          # Docs only
    ├── nfl/README.md          # Docs only
    └── public/
```

## 3.2 What is tangled or ambiguous

**etl/runner.py lives in the wrong home.** `runner.py` is a Flask HTTP service (a microservice) but lives in `etl/`. It shares the Python venv with ETL but has no ETL logic — it proxies NBA CDN endpoints. Conceptually it belongs in `services/` or `flask/`.

**grading/ is a half-extracted package.** `grading/` has its own requirements file but imports `etl.db` via a `sys.path` hack. It is neither fully independent nor a proper sub-package of `etl/`. The grading engine is the only consumer of `scipy`, making it the primary reason for the split.

**database/ is documentation masquerading as a directory.** All DDL lives inside Python scripts as SQLAlchemy definitions or inline SQL strings. The `database/` directory has only README files. There are no `.sql` migration files, no schema versioning, no way to reconstruct the schema from this directory alone.

**web/_shared/ is aspirational.** It exists with an invariant ("shared components never import from sport-specific folders") but NBA components still live under sport-specific paths. The directory is structurally correct but unused in practice.

**CLAUDE.md hierarchy is root-only.** The root `CLAUDE.md` is comprehensive (200+ lines) but every sport and component gets a README with an INVARIANTS section that carries equivalent authority. There is no per-package `CLAUDE.md` to scope session instructions. Claude Code sessions always load the full root CLAUDE.md regardless of what part of the repo is being edited.

**`mcp/` is dead code.** `mcp/server.py` was the VM-era MCP. The Mac MCP lives at `/Users/schnapp/mac-mcp/server.py` (outside the repo). The repo copy serves only as reference documentation.

**Sport status is asymmetric.** NBA is live with 24+ API routes and ~20 components. MLB is in development with 9 API routes and all UI inline (no component extraction yet). NFL has ETL (idle, no consumer) and no web layer. This creates implicit dependencies — `web/lib/queries.ts` and `web/lib/signals.ts` are NBA-specific despite sitting in a "shared" `lib/` directory.

**Implicit conventions that are inconsistently followed:**

1. *Sport-scoped subdirectories for docs:* `etl/nba/`, `web/nba/`, `database/nba/` are all docs-only; code is flat in `etl/`. This is consistent but non-obvious.
2. *`_shared/` naming for cross-sport code:* Used in both `web/_shared/` and `etl/_shared/` but neither is complete — only the latter has any meaningful content (just docs).
3. *`todayCT()` vs `todayLocal()`:* NBA API routes use Central Time (`todayCT()`); MLB date controls use browser-local time (`todayLocal()`). Documented in READMEs but inconsistent and may confuse future contributors.
4. *ETL scripts self-add `etl/` parent to sys.path:* `nba_etl.py:73-78` shows a sys.path manipulation pattern for cross-file imports. Some scripts do this; the convention is undocumented at root level.

---

# Section 4 — Proposed Structure

## 4.1 Design principles

The existing layout is close to correct. The goal is to **formalize what already exists** rather than invent new structure. Key decisions:

1. **Keep `etl/` flat** (ADR-0002). Do not create `etl/nba/`, `etl/mlb/`, `etl/nfl/` code subdirectories. Docs subdirectories stay.
2. **Extract the implicit shared Python package** (`etl/db.py` + `etl/integrity.py`) into `packages/data/` so `grading/` can declare a real dependency.
3. **Promote `runner.py` to `services/flask/`** to signal that it is a service, not an ETL script.
4. **Add root workspace config** (package.json with `workspaces: ["web"]`) to make the npm side formal.
5. **Add Python workspace tooling** at root level (a root `requirements.txt` or a `pyproject.toml` with `[tool.uv.workspace]`) to make cross-package Python deps explicit.
6. **Add CLAUDE.md files at package level** to scope Claude Code sessions.
7. **Promote `database/` to hold actual DDL** — one `.sql` bootstrap file per schema, generated from current state.

## 4.2 Target directory tree

```
/                                  # monorepo root
├── CLAUDE.md                      # Root: session protocol, stack overview, global rules
├── README.md                      # Updated: remove stale Azure SQL ref
├── .gitignore
├── package.json                   # NEW: workspaces: ["web"]; no deps
├── pyproject.toml                 # NEW: uv workspace config; members: ["packages/data", "etl", "grading"]
│
├── .github/
│   └── workflows/                 # Unchanged; _archive/ stays
│
├── docs/                          # Unchanged; project-wide docs hub
│   └── (all existing .md files)
│
├── infrastructure/
│   └── README.md                  # Unchanged
│
├── packages/                      # NEW top-level directory for shared packages
│   └── data/                      # NEW: extracted from etl/db.py + etl/integrity.py
│       ├── CLAUDE.md              # NEW
│       ├── pyproject.toml         # name = "schnapp-data", version = "0.1.0"
│       ├── __init__.py
│       ├── db.py                  # MOVED from etl/db.py
│       └── integrity.py           # MOVED from etl/integrity.py
│
├── etl/                           # Python ETL — flat per ADR-0002; imports from packages/data
│   ├── CLAUDE.md                  # NEW
│   ├── pyproject.toml             # UPDATED: depends on schnapp-data
│   ├── requirements.txt           # UPDATED: remove db/integrity deps; add packages/data ref
│   ├── runner.py                  # MOVED to services/flask/runner.py (see below)
│   ├── odds_etl.py
│   ├── nba_etl.py
│   ├── nba_live.py
│   ├── mlb_etl.py
│   ├── mlb_play_by_play.py
│   ├── nfl_etl.py
│   ├── game_day_gate.py
│   ├── lineup_poll.py
│   ├── record_run.py
│   ├── _shared/README.md          # Updated: remove Azure Serverless cold-start note
│   ├── nba/README.md
│   ├── mlb/README.md
│   └── nfl/README.md
│
├── grading/                       # Grading engine; now declares packages/data dependency
│   ├── CLAUDE.md                  # NEW
│   ├── pyproject.toml             # UPDATED: depends on schnapp-data
│   ├── requirements.txt           # UPDATED: scipy only; packages/data via workspace
│   └── grade_props.py             # UPDATED: replace sys.path hack with proper import
│
├── services/                      # NEW top-level directory for runtime services
│   └── flask/                     # NEW: Flask live-data proxy
│       ├── CLAUDE.md              # NEW
│       └── runner.py              # MOVED from etl/runner.py; update comment re: launchd
│
├── database/                      # Schema docs + bootstrap DDL
│   ├── CLAUDE.md                  # NEW
│   ├── README.md                  # UPDATED: note bootstrap .sql files
│   ├── _shared/
│   │   ├── README.md
│   │   └── bootstrap.sql          # NEW: common.* DDL (extracted from Python scripts)
│   ├── nba/
│   │   ├── README.md
│   │   └── bootstrap.sql          # NEW: nba.* DDL
│   ├── mlb/
│   │   ├── README.md
│   │   └── bootstrap.sql          # NEW: mlb.* DDL
│   └── nfl/
│       ├── README.md
│       └── bootstrap.sql          # NEW: nfl.* DDL
│
├── mcp/
│   └── server.py                  # Unchanged; reference only (VM-era code)
│
└── web/                           # Next.js 15 app; unchanged internally except cleanup
    ├── CLAUDE.md                  # NEW
    ├── package.json               # UPDATED: minor — ensure "engines" key stays
    ├── next.config.mjs            # UPDATED: fix stale RUNNER_URL default
    ├── app/
    │   └── api/
    │       ├── games/route.ts     # UPDATED: fix stale RUNNER_URL default
    │       ├── live-boxscore/route.ts  # UPDATED: fix stale RUNNER_URL default
    │       └── scoreboard/route.ts    # UPDATED: fix stale RUNNER_URL default
    ├── components/
    ├── lib/
    ├── _shared/
    ├── nba/README.md
    ├── mlb/README.md
    ├── nfl/README.md
    └── public/
```

## 4.3 What moves where and why

| Item | Current | Target | Reason |
|------|---------|--------|--------|
| `etl/db.py` | `etl/db.py` | `packages/data/db.py` | Shared by both `etl/` and `grading/`; extracts the cross-package dependency |
| `etl/integrity.py` | `etl/integrity.py` | `packages/data/integrity.py` | Same reason — used by multiple ETL scripts, logically part of the shared layer |
| `etl/runner.py` | `etl/runner.py` | `services/flask/runner.py` | It is a Flask service, not an ETL script; the wrong directory signals the wrong mental model |
| Root `package.json` | does not exist | `/package.json` | Makes the npm workspace formal |
| Root `pyproject.toml` | does not exist | `/pyproject.toml` | Makes the Python workspace formal; replaces sys.path hacks |
| `database/*/bootstrap.sql` | does not exist | `database/*/bootstrap.sql` | Makes the schema derivable from the repo, not just from running Python scripts |
| `*/CLAUDE.md` | does not exist (root only) | per-package | Scopes Claude Code sessions; avoids loading 200-line root CLAUDE.md for every task |

## 4.4 What does not move

- All workflow YAMLs — they reference `etl/` and `grading/` paths directly; a coordinated update of all 25 `mac-runner` workflows is needed when paths change, making this a risk-bearing step that should be explicitly sequenced.
- `web/` internal structure — the Next.js app is organized correctly; no structural change needed.
- `docs/` — unchanged; it is the project-wide documentation hub.
- `mcp/` — kept as reference; no active deployment.

---

# Section 5 — CLAUDE.md Hierarchy Plan

Seven `CLAUDE.md` files: one root (exists), six new ones at package/service level.

---

## 5.1 `/CLAUDE.md` (root, EXISTS — update only)

**Purpose:** Project-wide session protocol for Claude Code sessions across all packages.

**Architecture:** Root of a multi-package monorepo on Schnapps-MBP (Intel Mac, macOS 14.8). Production runs entirely on this Mac via launchd agents and a local SQL Server 2022 Docker container. GitHub Actions on `mac-runner-1` handles all Python ETL. No cloud compute.

**Paths:** `docs/README.md`, `docs/SESSION_PROTOCOL.md`, `docs/CHANGELOG.md`, `docs/CONNECTIONS.md`, `docs/DECISIONS.md`

**Conventions:** Tag taxonomy `[sport][component]`; INVARIANTS sections in component READMEs are authoritative; ADR identifier format `ADR-YYYYMMDD-N`.

**Workflows:**
- Web: `npm run build` → commit → push → `gh workflow run deploy-web.yml`
- ETL: syntax check → commit → push → `gh workflow run <workflow>.yml`
- No Python locally on Windows laptop (ThreatLocker)

**Settings and environment:** All secrets in launchd plists or GitHub Actions secrets. Never hardcode. See `docs/CONNECTIONS.md`.

**Memory:**
- Azure fully decommissioned 2026-05-03. No Azure resources exist. Do not suggest Azure.
- `AZURE_SQL_*` secret names in GitHub Actions are intentional — values updated, names preserved (ADR-20260503-1).
- `runner.py` now lives in `services/flask/` (post-migration). Launchd plist path and `etl/flask.log` references must be updated if plist is not updated simultaneously.
- `grading/grade_props.py` imports from `packages/data` (post-migration). No sys.path hack.

**Rules:**
- Never rewrite a component README in full — section edits only.
- Never commit without a CHANGELOG entry.
- Never run Python locally on the corporate Windows laptop.
- Never run destructive commands without explicit confirmation in the same turn.

*Updates needed to existing root CLAUDE.md:*
- Update stack description to reflect `services/flask/runner.py` location (post-migration).
- Update stack description to reflect `packages/data/` (post-migration).
- Remove/replace reference to `etl/runner.py` in Flask service description.

---

## 5.2 `/web/CLAUDE.md` (NEW)

**Purpose:** Next.js 15 web application serving schnapp.bet — NBA (live), MLB (in development), NFL (not started).

**Architecture:** Single Next.js App Router application. All sport pages (`/nba`, `/mlb`, `/nfl`) and 37 API routes live here. Database access via `mssql` (`lib/db.ts`); live-data via Flask proxy (`lib/` API routes reading `RUNNER_URL`). Auth via HMAC tokens (`lib/auth-context.tsx`, `/api/auth/*`). Feature flags from `common.feature_flags` with 60s TTL cache (`lib/feature-flags.ts`). Maintenance gate in `middleware.ts`.

**Paths:**
- DB connection: `lib/db.ts:17` (`SQL_CONNECTION_STRING`)
- Shared queries: `lib/queries.ts`
- Signals logic: `lib/signals.ts`
- Middleware: `middleware.ts`
- NBA API routes: `app/api/games/`, `app/api/grades/`, `app/api/player/`, etc.
- MLB API routes: `app/api/mlb-games/`, `app/api/mlb-player/`, etc.

**Conventions:**
- `todayCT()` for server-side date defaults (API routes); `todayLocal()` for client-side date controls (MLB).
- `RUNNER_URL` and `RUNNER_API_KEY` always from `process.env` — never hardcode.
- Shared components go in `_shared/`; never import from sport-specific folders within `_shared/`.

**Workflows:**
```bash
cd web
npm run build          # must pass before any commit
npm run dev            # local dev on :3000
gh workflow run deploy-web.yml  # deploy to production
```

**Settings and environment:**
- `SQL_CONNECTION_STRING` — MSSQL connection string (required)
- `RUNNER_URL` — Flask base URL (prod: `https://mac-flask.schnapp.bet`)
- `RUNNER_API_KEY` — Flask auth key
- `GITHUB_PAT` — fine-grained PAT for workflow dispatch
- `ADMIN_PASSCODE`, `AUTH_TOKEN_SECRET`, `ADMIN_REFRESH_CODE`, `ODDS_API_KEY`
- All set in launchd plists; see `docs/CONNECTIONS.md:56-63`

**Memory:**
- `https://live.schnapp.bet` is dead code as default for `RUNNER_URL`. DNS deleted 2026-05-01. Default should be `https://mac-flask.schnapp.bet` (post-migration fix).
- Both `bet.schnapp.web` (port 3000) and `bet.schnapp.web-prod` (port 3001) share the same `web/.next/` build directory. Rebuilding affects both.
- Any new env var must be added to BOTH plist files simultaneously.

**Rules:**
- `npm run build` must pass before any commit touching `web/`.
- Never hardcode `RUNNER_URL`, `SQL_CONNECTION_STRING`, or any credential.
- Cache-Control headers for each API route are specified in `next.config.mjs` — check there before adding inline headers.

---

## 5.3 `/etl/CLAUDE.md` (NEW)

**Purpose:** Python ETL pipeline for NBA, MLB, and NFL — fetches from public and authenticated APIs, upserts into local SQL Server 2022 Docker container.

**Architecture:** Flat Python module directory (ADR-0002). All scripts at `etl/*.py`. Shared database utilities in `packages/data/` (post-migration). Runs exclusively in GitHub Actions on `mac-runner-1` (label: `mac-runner`). Never runs locally on Windows laptop (ThreatLocker).

**Paths:**
- Shared DB utilities: `packages/data/db.py` (post-migration; was `etl/db.py`)
- Data integrity: `packages/data/integrity.py` (post-migration; was `etl/integrity.py`)
- NBA: `etl/nba_etl.py`, `etl/nba_live.py`, `etl/lineup_poll.py`
- MLB: `etl/mlb_etl.py`, `etl/mlb_play_by_play.py`
- NFL: `etl/nfl_etl.py`
- Odds: `etl/odds_etl.py`
- Gate/utility: `etl/game_day_gate.py`, `etl/record_run.py`
- Venv: `/Users/schnapp/venv` (Python 3.12.13)

**Conventions:**
- All scripts use `get_engine()` from `packages/data.db` (not `etl.db` post-migration).
- All scripts import `validate_and_filter` from `packages/data.integrity` when using the 3-layer integrity framework.
- `fast_executemany=True` for bulk upserts; `False` for long-VARCHAR staging tables.
- FanDuel only (`bookmakers=fanduel`) for all Odds API calls (ADR-0007).
- `minutes` column (not `min` — SQL Server reserved word).

**Workflows:**
```bash
# Syntax check (safe on Mac, not Windows)
python -c "import ast; ast.parse(open('etl/script.py').read())"
# Trigger ETL
gh workflow run nba-etl.yml
gh workflow run mlb-etl.yml
gh workflow run odds-etl.yml
# Monitor
gh run watch
```

**Settings and environment:** `AZURE_SQL_SERVER`, `AZURE_SQL_DATABASE`, `AZURE_SQL_USERNAME`, `AZURE_SQL_PASSWORD` (GitHub Actions secrets; target `localhost,1433`), `AZURE_SQL_TRUST_CERT=yes`, `ODDS_API_KEY`, `NBA_PROXY_URL`. See `docs/CONNECTIONS.md`.

**Memory:**
- GitHub Actions secret names are `AZURE_SQL_*` by design — values target localhost (ADR-20260503-1). Do not rename without updating all 25+ mac-runner workflow YAMLs.
- `AZURE_SQL_TRUST_CERT=yes` is required for the local SQL Server Docker container (self-signed cert). This is intentional.
- PT stats (`leaguedashptstats`) do NOT require the NBA proxy. All other `stats.nba.com` calls do.
- `nflreadpy.config.update_config(cache_mode='off')` must be called at start of `nfl_etl.py` — GitHub Actions runners have no persistent filesystem.

**Rules:**
- Never add code subdirectories under `etl/` — files stay flat (ADR-0002).
- All ETL is idempotent (MERGE, not INSERT). No destructive loads without an explicit `--backfill` flag.
- `record_run.py` must be called at end of every scheduled workflow for observability.

---

## 5.4 `/grading/CLAUDE.md` (NEW)

**Purpose:** Kernel density estimation (KDE) grading engine for NBA (and MLB) prop lines — produces composite grades, tier lines, and outcome resolution stored in `common.daily_grades` and `common.player_tier_lines`.

**Architecture:** Single script `grade_props.py`. Depends on `packages/data.db` for SQL Server connection (post-migration; was `etl.db` via sys.path hack). Runs in GitHub Actions on `mac-runner-1`. Triggered by `grading.yml` (scheduled, workflow_dispatch, and workflow_run on `odds-etl` success). Has a self-redispatch loop for backfill mode.

**Paths:**
- Engine: `grading/grade_props.py`
- DB shared: `packages/data/db.py` (post-migration)
- Calibration: lives in `common.daily_grades` outcomes

**Conventions:**
- Composite grade formula: `0.40 * momentum + 0.40 * (hit_rate_60 * 100) + 0.20 * pattern_grade` (ADR-20260423-1). Weights renormalize if any component is NULL.
- KDE window: composite ≥ 80 → last 15 games; 50-79 → last 30 games; < 50 → full season.
- `KDE_MIN_GAMES = 10` — do not lower without revalidation (`database/nba/README.md:227`).
- Engine uses `get_engine_slow(max_retries=3, retry_wait=60)` — required for NVARCHAR(MAX) safety.

**Workflows:**
```bash
# Trigger grading (upcoming mode)
gh workflow run grading.yml
# Trigger backfill with date
gh workflow run grading.yml -f mode=backfill -f date=2026-05-01
# Outcomes resolution
gh workflow run grading.yml -f mode=outcomes
```

**Settings and environment:** Same `AZURE_SQL_*` secrets as `etl/`. No additional secrets.

**Memory:**
- `grading/requirements.txt` only contains `scipy`. The `packages/data` dependency is declared in `pyproject.toml` (post-migration), not in `requirements.txt`.
- Backfill redispatch: `grading.yml` re-dispatches itself until `grade_props.py` outputs "Backfill: nothing to do." — exits loop on `cancelled` OR `failure` OR `DONE=true` (ADR-20260501-6).
- Blowout dampening: applies to points and combo markets only when pre-game spread ≥ 10.5.

**Rules:**
- Never call `grade_props.py` with both `--mode backfill` and `--mode upcoming` in the same run.
- `grade_rows` and `tier_rows` from `grade_props_for_date` BOTH require upsert calls — skipping either corrupts the grade chain (`database/nba/README.md:228`).

---

## 5.5 `/services/flask/CLAUDE.md` (NEW)

**Purpose:** Flask HTTP proxy service that exposes live NBA CDN data (scoreboard and boxscore) to the Next.js web app at `mac-flask.schnapp.bet`.

**Architecture:** Single file `runner.py`. Runs as launchd user agent `bet.schnapp.flask` on Schnapps-MBP at `0.0.0.0:5000`. Exposed publicly via Cloudflare tunnel `schnapp-mac` at `https://mac-flask.schnapp.bet`. The web tier calls this service via `RUNNER_URL` env var.

**Paths:**
- Service code: `services/flask/runner.py`
- Launchd plist: `~/Library/LaunchAgents/bet.schnapp.flask.plist`
- Logs: `services/flask/flask.log`, `services/flask/flask.err.log`
  *(plist paths must be updated from `etl/flask.log` when runner.py is moved — see Migration Plan step 3)*

**Conventions:**
- `/ping` is unauthenticated by design (used by health checks and Mac MCP `flask_status`).
- `/scoreboard` and `/boxscore` require `X-Runner-Key` header matching `RUNNER_API_KEY`.
- NBA CDN calls require no proxy, no auth — public endpoints.

**Workflows:**
```bash
# Restart after code changes
launchctl kickstart -k gui/$UID/bet.schnapp.flask
# Or via Mac MCP
# mac_mcp.flask_restart()
```

**Settings and environment:**
- `RUNNER_API_KEY = runner-Lake4971` (set in plist `EnvironmentVariables`)

**Memory:**
- This service was previously at `etl/runner.py`. If any workflow YAML references `etl/runner.py` by path, it must be updated when this move occurs.
- The `runner.py` comment about "systemd service" is stale — it referenced the Azure VM era. The service runs under launchd, not systemd.

**Rules:**
- Never add ETL logic to this service — it is a CDN proxy only.
- Never require auth on `/ping` — it is used by infrastructure health checks.

---

## 5.6 `/packages/data/CLAUDE.md` (NEW)

**Purpose:** Shared Python package providing SQL Server database connectivity (`db.py`) and the three-layer data integrity framework (`integrity.py`) used by both `etl/` and `grading/`.

**Architecture:** Internal package, not published to PyPI. Installed into the shared venv at `/Users/schnapp/venv` via `pip install -e packages/data` (or `uv` workspace sync). Consumers: `etl/*.py`, `grading/grade_props.py`.

**Paths:**
- `packages/data/db.py` — `get_engine()`, `get_engine_slow()`, `record_workflow_run()`, `upsert()`
- `packages/data/integrity.py` — `validate_and_filter()`, `ensure_tables()`

**Conventions:**
- Three engine variants: `get_engine` (fast_executemany=True, retry_wait=45s), `get_engine_slow` (fast_executemany=False, retry_wait=45s), grading's own `get_engine` override (fast_executemany=False, retry_wait=60s for NVARCHAR(MAX) safety and Docker startup latency).
- `upsert()` uses MERGE via temp table `#stage_{table}`. MERGE source must be deduplicated; trailing semicolons required (SQL Server).
- BIT columns require `CAST(col AS INT)` before `SUM()`.
- `DELETE` not `TRUNCATE` (FK constraints block TRUNCATE).

**Settings and environment:** Reads `AZURE_SQL_SERVER`, `AZURE_SQL_DATABASE`, `AZURE_SQL_USERNAME`, `AZURE_SQL_PASSWORD`, `AZURE_SQL_TRUST_CERT` from environment. Connection string: `mssql+pyodbc://{user}:{pw}@{server}/{db}?driver=ODBC+Driver+18+for+SQL+Server&Encrypt=yes&TrustServerCertificate={trust}`.

**Memory:**
- This package was extracted from `etl/db.py` and `etl/integrity.py`. If you need to look at git history for these files, check git log for the old path `etl/db.py`.
- The three-layer integrity framework writes to `common.ingest_quarantine` (L1), `common.unmapped_entities` (L2), `common.data_completeness_log` (L3).

**Rules:**
- This package has no external consumers (not on PyPI). Breaking changes are coordinated changes across `etl/` and `grading/`.
- Never add sport-specific logic here — only infrastructure shared by all sports.

---

## 5.7 `/database/CLAUDE.md` (NEW)

**Purpose:** Schema documentation and bootstrap DDL for all five schemas: `nba`, `mlb`, `nfl`, `odds`, `common`.

**Architecture:** Documentation-primary directory. `database/*/bootstrap.sql` files contain the DDL to recreate each schema from scratch (generated from current state, not a migration chain). The canonical live schema is the SQL Server Docker container on Schnapps-MBP at `localhost,1433`. Changes to schema happen in Python (SQLAlchemy `create_table` / `ALTER TABLE ADD COLUMN`) or via ad-hoc scripts; the `.sql` files are updated to match after any schema change.

**Paths:**
- `database/_shared/bootstrap.sql` — `common.*` and `odds.*` DDL
- `database/nba/bootstrap.sql` — `nba.*` DDL
- `database/mlb/bootstrap.sql` — `mlb.*` DDL
- `database/nfl/bootstrap.sql` — `nfl.*` DDL
- Per-schema READMEs carry authoritative INVARIANTS sections

**Conventions:**
- Naming: schemas lowercase; tables and columns snake_case; PKs surrogate INT with UQ on business keys.
- Every fact table has `created_at DATETIME2 DEFAULT GETUTCDATE()`.
- Column named `minutes` not `min` (SQL Server reserved word).

**Workflows:**
```bash
# Ad-hoc DB access (Mac only)
python /tmp/query.py  # write script to /tmp/, run with /Users/schnapp/venv/bin/python
# pyodbc: server=localhost,1433, database=sports-modeling, uid=sa, TrustServerCertificate=yes
```

**Memory:**
- There is no migration chain. Schema changes are applied directly and then the bootstrap `.sql` files are updated to reflect the new state. If you need to reconstruct the schema on a new machine, use the bootstrap files AND the BACPAC at `/Users/schnapp/azure-sql-backups/` as a data restore point.
- `common.feature_flags.maintenance_mode = 1` was the state at the BACPAC snapshot time (2026-04-26). It was flipped to 0 on the Mac container. Do not set it back to 1 unless intending a maintenance window.

**Rules:**
- One database (`sports-modeling`), five schemas. Do not create a sixth schema without an ADR.
- Schemas map to sport names; cross-sport data goes in `common` or `odds`.

---

# Section 6 — Migration Plan

Steps are ordered by dependency. Risk level is marked **[HIGH]**, **[MEDIUM]**, or **[LOW]**.

---

## Step 1 — Fix stale docs and dead code (no path changes, no risk) **[LOW]**

**Before:** `README.md:9` claims Azure SQL is live; `etl/runner.py:24` says systemd; three API routes default to deleted hostname; `etl/_shared/README.md` attributes retry wait to "Azure Serverless."

**After:** All four documentation/code issues corrected to reflect current reality.

**Changes:**
1. `README.md:9` — remove sentence about Azure SQL being a live dependency. Replace with: "ETL and web both target a local SQL Server 2022 Docker container on Schnapps-MBP."
2. `etl/runner.py:24` — update comment from "Managed by: systemd service `schnapp-flask.service`" to "Managed by: launchd user agent `bet.schnapp.flask` on Schnapps-MBP."
3. `web/app/api/games/route.ts:4`, `web/app/api/live-boxscore/route.ts:13`, `web/app/api/scoreboard/route.ts:6` — change default from `'https://live.schnapp.bet'` to `'https://mac-flask.schnapp.bet'`.
4. `etl/_shared/README.md` — update retry wait rationale from "Azure Serverless cold start" to "SQL Server Docker container startup latency."

**Breaks during transition:** Nothing. These are comment/default-value fixes.

**Order dependencies:** None — can be done first.

---

## Step 2 — Add root package.json (npm workspace) **[LOW]**

**Before:** No root `package.json`. `web/` is the only npm package, with no workspace linkage.

**After:** Root `package.json` declares `workspaces: ["web"]`. This formalizes the npm side without changing any behavior.

**Changes:**
```json
// /package.json (new file)
{
  "name": "sports-modeling",
  "private": true,
  "workspaces": ["web"],
  "engines": { "node": ">=20" }
}
```

**Breaks during transition:** Nothing. The `deploy-web.yml` workflow runs `npm ci` from the `web/` subdirectory; this is unaffected by a root `package.json` with no scripts.

**Order dependencies:** None — can be done in any order.

---

## Step 3 — Move `etl/runner.py` → `services/flask/runner.py` **[MEDIUM]**

**Before:** Flask service at `etl/runner.py`. Launchd plist references `etl/runner.py`. Log files at `etl/flask.log` and `etl/flask.err.log`.

**After:** Flask service at `services/flask/runner.py`. Plist updated. Log references updated.

**Changes:**
1. Create `services/flask/` directory.
2. Move `etl/runner.py` → `services/flask/runner.py`.
3. Update `~/Library/LaunchAgents/bet.schnapp.flask.plist`:
   - Change `ProgramArguments` path from `.../etl/runner.py` to `.../services/flask/runner.py`.
   - Change `StandardOutPath` from `etl/flask.log` to `services/flask/flask.log`.
   - Change `StandardErrorPath` from `etl/flask.err.log` to `services/flask/flask.err.log`.
4. Reload the launchd agent: `launchctl kickstart -k gui/$UID/bet.schnapp.flask`.
5. Update `infrastructure/README.md:84` to reference new path.
6. Update `CLAUDE.md` Flask service path reference.
7. Add `services/flask/CLAUDE.md`.

**Breaks during transition:**
- The Flask service will be briefly unavailable during the plist reload (typically < 2 seconds for launchd restart).
- The Mac MCP `flask_restart` and `flask_status` tools call `launchctl` by label (`bet.schnapp.flask`) — they are unaffected by the file path change.
- Any GitHub Actions workflow that references `etl/runner.py` by path must be identified (grep workflows for `runner.py`) and updated.

**Risk:** The plist edit + launchctl reload is a live service change. Do it during a period with no active NBA games. Verify with `curl http://127.0.0.1:5000/ping` immediately after.

**Order dependencies:** Step 1 should precede this (so the comment in runner.py is fixed before it moves).

---

## Step 4 — Extract `packages/data/` (shared Python package) **[MEDIUM]**

**Before:** `etl/db.py` and `etl/integrity.py` are imported via sys.path hack by `grading/grade_props.py`. No formal package declaration.

**After:** `packages/data/` is an installable Python package. `etl/` and `grading/` import from `schnapp_data` (or `packages.data`). The sys.path hack is removed.

**Changes:**
1. Create `packages/data/` directory.
2. Copy `etl/db.py` → `packages/data/db.py`, `etl/integrity.py` → `packages/data/integrity.py`.
3. Add `packages/data/__init__.py` (can be empty).
4. Add `packages/data/pyproject.toml`:
   ```toml
   [project]
   name = "schnapp-data"
   version = "0.1.0"
   requires-python = ">=3.12"
   dependencies = ["sqlalchemy>=2.0", "pyodbc>=5"]
   ```
5. Install into venv: `pip install -e packages/data` (run on Mac).
6. Update all `from etl.db import ...` statements in `etl/*.py` and `grading/grade_props.py` to `from schnapp_data.db import ...`.
7. Update all `from etl.integrity import ...` statements to `from schnapp_data.integrity import ...`.
8. Remove sys.path manipulation in `etl/nba_etl.py:73-78` and `grading/grade_props.py`.
9. Update `grading/requirements.txt` to remove any `etl/` path reference (add comment pointing to `packages/data`).
10. Delete `etl/db.py` and `etl/integrity.py` (after verifying all consumers updated).
11. Add `packages/data/CLAUDE.md`.
12. Update all GitHub Actions workflow YAMLs that activate the venv to add `pip install -e packages/data` (or add it to the runner's venv setup script).

**Breaks during transition:**
- Between step 2 (copy files) and step 6 (update imports), both old and new paths exist simultaneously. This is safe.
- After step 10 (delete originals), any workflow that hasn't had its venv updated will fail. Coordinate the venv update (step 12) and the import update (steps 6-8) in a single commit so all workflows use the new path simultaneously.
- GitHub Actions venv at `/Users/schnapp/venv` must be updated: `pip install -e packages/data`. This is a manual step on Schnapps-MBP.

**Risk:** All ETL and grading workflows import `etl.db`. If any workflow runs between the deletion of `etl/db.py` and the venv update, it will fail with `ModuleNotFoundError`. To avoid this: do not delete `etl/db.py` until after the venv has been updated and at least one full workflow cycle has succeeded.

**Order dependencies:** Step 1 must precede (so stale doc references are cleaned before the move). Step 3 (runner.py move) is independent and can be done before or after.

---

## Step 5 — Add Python workspace config (pyproject.toml) **[LOW]**

**Before:** Python packages are managed with flat `requirements.txt` files. No root workspace tooling.

**After:** Root `pyproject.toml` declares a `uv` workspace; `etl/` and `grading/` have their own `pyproject.toml` with declared dependencies.

**Changes:**
1. Add root `pyproject.toml`:
   ```toml
   [tool.uv.workspace]
   members = ["packages/data", "etl", "grading"]
   ```
2. Add `etl/pyproject.toml`:
   ```toml
   [project]
   name = "schnapp-etl"
   version = "0.1.0"
   requires-python = ">=3.12"
   dependencies = ["schnapp-data", "sqlalchemy>=2.0", "pandas>=3", "requests>=2.33", "nba_api>=1.11", "mlb-statsapi>=1.7", "nflreadpy>=0.1", "pyarrow>=24", "numpy>=2.4", "pyodbc>=5"]
   ```
3. Add `grading/pyproject.toml`:
   ```toml
   [project]
   name = "schnapp-grading"
   version = "0.1.0"
   requires-python = ">=3.12"
   dependencies = ["schnapp-data", "scipy>=1.17"]
   ```

**Breaks during transition:** None — `requirements.txt` files remain and the venv already has everything installed. The `pyproject.toml` files are additive declarations that enable `uv sync` as an alternative; they do not break the existing `pip install -r` approach used by GitHub Actions.

**Order dependencies:** Step 4 (packages/data creation) must precede this, as `pyproject.toml` references `schnapp-data`.

---

## Step 6 — Generate database bootstrap SQL files **[LOW]**

**Before:** `database/` contains only README documentation. The schema cannot be reconstructed from the repo without running Python scripts.

**After:** `database/*/bootstrap.sql` contains the DDL for each schema, generated from the current live container.

**Changes:**
1. Write a Python script to `sys.stdout` the current schema DDL from `sys.dm_sql_modules` or `INFORMATION_SCHEMA` for each schema.
2. Run the script against the local SQL Server container.
3. Write the output to `database/_shared/bootstrap.sql`, `database/nba/bootstrap.sql`, `database/mlb/bootstrap.sql`, `database/nfl/bootstrap.sql`.
4. Add `database/CLAUDE.md`.
5. Note in each bootstrap file: "Generated from production container 2026-05-03. Apply in dependency order: common/odds before sport schemas."

**Breaks during transition:** None — these are additive files.

**Order dependencies:** None — can be done in any order.

---

## Step 7 — Add per-package CLAUDE.md files **[LOW]**

**Before:** Only root `CLAUDE.md` exists. Claude Code sessions always load 200+ lines of global context regardless of which package is being edited.

**After:** Six new `CLAUDE.md` files at `web/`, `etl/`, `grading/`, `services/flask/`, `packages/data/`, `database/`.

**Changes:** Write each `CLAUDE.md` per the specifications in Section 5 above.

**Breaks during transition:** None — additive files. The root `CLAUDE.md` should also be updated to note the package-level CLAUDE.md files in its session protocol.

**Order dependencies:** Steps 3, 4, and 6 should precede their respective CLAUDE.md files so the paths referenced are accurate.

---

## Step 8 — Resolve U-01: rename `AZURE_SQL_TRUST_CERT` → `SQL_TRUST_CERT` (OPTIONAL) **[HIGH]**

**Before:** ETL uses `AZURE_SQL_TRUST_CERT` alongside `AZURE_SQL_*` server/db/user/pass secrets. Named `AZURE_*` but targeting a local container.

**After:** Renamed to `SQL_TRUST_CERT` to match the pattern established by `SQL_CONNECTION_STRING`.

**Changes:**
1. Update `packages/data/db.py` (was `etl/db.py`) — change `os.getenv('AZURE_SQL_TRUST_CERT', 'no')` to `os.getenv('SQL_TRUST_CERT', 'yes')` (note: default changes to `yes` since local SQL Server always needs it).
2. Update all 25 `mac-runner` workflow YAMLs — change `AZURE_SQL_TRUST_CERT: yes` to `SQL_TRUST_CERT: yes`.
3. Add `SQL_TRUST_CERT` as a GitHub Actions repository variable (not secret — it's not sensitive); remove the per-workflow hardcoding.

**Breaks during transition:** All 25 workflows must be updated atomically. Any workflow that runs between step 1 (db.py update) and step 2 (workflow YAML updates) will fail because it passes `AZURE_SQL_TRUST_CERT` which the updated code no longer reads. Coordinate in a single commit.

**Risk:** HIGH — touches 25 workflow files plus core database code. Do not do this as part of the same commit as any other migration step. **Requires human decision on whether to proceed (see U-01 in Section 2).**

**Order dependencies:** Must follow Step 4 (packages/data extraction) since `db.py` will have been moved.

---

## Step 9 — Resolve U-02: credentials in CONNECTIONS.md (OPTIONAL, requires human decision) **[MEDIUM]**

**Before:** Six categories of sensitive credentials appear in plaintext in `docs/CONNECTIONS.md` (checked into private repo).

**Option A — Redact to references:** Replace literal values with references like `"<see GitHub Actions secret ODDS_API_KEY>"` or `"<see launchd plist EnvironmentVariables>"`. Preserves operational docs without storing secrets.

**Option B — Gitignore CONNECTIONS.md:** Move `docs/CONNECTIONS.md` to a gitignored path; maintain a `docs/CONNECTIONS.md.template` with placeholder values in version control.

**Option C — Accept current state:** Private repo, single developer, accept the risk.

**Risk:** MEDIUM — Option A is safe and additive (just text replacements). Option B breaks the project invariant that `docs/CONNECTIONS.md` is the source of truth for all session context.

**Breaks during transition (Option A):** None — text replacements only.

**Order dependencies:** None — independent of all other steps.

---

## Sequencing Summary

```
Step 1 (stale docs)     → Step 3 (move runner.py)
Step 1 (stale docs)     → Step 4 (packages/data)
Step 4 (packages/data)  → Step 5 (pyproject.toml)
Step 4 (packages/data)  → Step 8 (rename TRUST_CERT) [optional, HIGH risk]
Step 3 (move runner.py) → Step 7 (CLAUDE.md for services/flask)
Step 4 (packages/data)  → Step 7 (CLAUDE.md for packages/data)
Step 6 (bootstrap SQL)  → Step 7 (CLAUDE.md for database)

Steps 2, 6, 9 are independent — no blocking dependencies.
Steps 3 and 4 are independent of each other.
```

Safe order for a single working session:
1 → 2 → 6 → 3 → 4 → 5 → 7 (Steps 8 and 9 require human decisions; do separately.)

---

# Summary of Key Findings

## Most important findings

1. **The repo is already a well-structured informal monorepo.** The main gap is the absence of root-level workspace tooling (no root `package.json`, no `pyproject.toml`). The physical structure is sound and ADR-0002's "flat ETL" decision should be preserved.

2. **`grading/grade_props.py` has a sys.path hack** that imports `etl.db` without a formal dependency declaration. This is the highest-priority structural defect — it will break if `etl/db.py` is ever moved without a coordinated update of `grading/`.

3. **`etl/runner.py` is a Flask service living in the ETL directory.** This misleads contributors into treating it as an ETL script. Moving it to `services/flask/` is a clean win.

4. **Three web API route files default `RUNNER_URL` to a deleted hostname** (`https://live.schnapp.bet`, DNS deleted 2026-05-01). These defaults are harmless in production (env var is always set) but are confusing and should be updated.

5. **`database/` has no DDL.** The schema can only be reconstructed by reading Python scripts and SQLAlchemy models scattered across `etl/`. Adding bootstrap `.sql` files closes this gap.

6. **`CLAUDE.md` hierarchy is root-only.** A 200+ line root CLAUDE.md loads for every session regardless of scope. Per-package `CLAUDE.md` files would make sessions faster to orient and more accurate in their guidance.

---

## Human decisions required before migration can proceed

| # | Decision | Stakes |
|---|----------|--------|
| U-01 | Rename `AZURE_SQL_TRUST_CERT` → `SQL_TRUST_CERT`? | Touches 25 workflow YAMLs + core db code; must be atomic |
| U-02 | Remove plaintext credentials from `docs/CONNECTIONS.md`? | Security posture choice for a private repo with user data |
| U-03 | Extract `packages/data/` now vs. defer? | Structural improvement vs. disruption to working ETL |

Steps 1, 2, 3, 6, and 7 carry no meaningful risk and can proceed immediately without these decisions.
