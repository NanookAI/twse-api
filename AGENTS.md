# Agent instructions — twse-api

This repo is a Claude Code plugin containing one skill: `skills/twse-api/`,
a reference for the Taiwan Stock Exchange OpenAPI (https://openapi.twse.com.tw).
There is no application code, build step, or test suite — the deliverables are
the markdown files themselves.

## Layout

- `skills/twse-api/SKILL.md` — main skill: API conventions, quick start,
  task→endpoint cheat sheet. Keep it under ~150 lines; details belong in
  `references/`.
- `skills/twse-api/references/*.md` — one file per official API category
  (7 files, 143 endpoints total). Each endpoint entry lists the exact JSON
  response keys and keeps the official Chinese title as an HTML comment.
- `.claude-plugin/plugin.json` — plugin metadata. Bump `version` on any
  skill content change.
- `.skillignore` / `.clawhubignore` — keep packaging limited to `SKILL.md`
  + `references/` (README/CLAUDE/AGENTS must stay excluded).

## Conventions

- Skill content is written in **English**; Chinese text from the official
  API docs is preserved as comments (`<!-- 上市個股日成交資訊 -->`) or inline
  where the Chinese IS the data (e.g. `/opendata` endpoints return
  Traditional-Chinese JSON keys like `公司代號` — never translate those keys).
- Endpoint data comes from `https://openapi.twse.com.tw/v1/swagger.json`.
  When updating, regenerate from the spec rather than hand-editing entries,
  and spot-check field keys against live API responses (the spec and reality
  have matched so far, but verify — e.g. `curl .../exchangeReport/STOCK_DAY_ALL`).
- Facts stated in SKILL.md were verified live: no endpoint takes parameters,
  all values are strings, dates are ROC-era (`1150706` = 2026-07-06),
  `FMSRFK_ALL`/`FMNPTK_ALL` return current-period aggregates only (not
  history). Re-verify before changing any of these claims.

## Publishing

- **ClawHub**: `clawhub skill publish ./skills/twse-api --slug twse-api
  --name "TWSE API" --version <next>`. Known issue: CLI v0.23.1 misreports
  the registry's async-publish response (`status: "pending"`) as
  `skillId: invalid value; versionId: invalid value` — the publish actually
  went through; the security scan takes minutes to ~1 hour. Confirm with
  `clawhub inspect twse-api`, don't retry.
- **Plugin marketplace**: distributed via the NanookAI/skills marketplace
  repo, which references this repo. Push a version bump here, then update
  the marketplace entry.
