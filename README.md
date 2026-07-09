# TWSE API Skill

A [Claude Code](https://claude.com/claude-code) skill for the official
**Taiwan Stock Exchange (TWSE) OpenAPI** (臺灣證券交易所開放資料 API,
https://openapi.twse.com.tw). It teaches the AI how to query all **143
endpoints** — free, no API key, no registration.

## What's covered

| Category (原分類) | Endpoints | Contents |
|---|---|---|
| Securities Trading (證券交易) | 36 | Daily OHLC quotes, P/E · dividend yield · P/B, margin balances, block trades, day trading, attention/disposition stocks, market calendar |
| Corporate Governance (公司治理) | 56 | Company profiles, insider/director holdings, material news, dividends, shareholder meetings, 21 ESG datasets |
| Financial Statements (財務報表) | 30 | Monthly revenue, income statements & balance sheets by industry format, profitability summaries |
| Indices (指數) | 5 | TAIEX, Taiwan 50, Formosa Index histories |
| Broker Data (券商資料) | 9 | Securities firm directories, personnel, monthly financials |
| Warrants (權證) | 3 | Warrant issuance and trading stats |
| Miscellaneous (其他) | 4 | TWSE news/events, government bonds, funds |

The skill also documents the pitfalls an AI needs to know: ROC (民國) date
format, Chinese vs. English JSON keys, comma-formatted number strings,
snapshot-only data (no historical query parameters), and the TWSE/TPEx split.

## Installation

### ClawHub

```
clawhub install twse-api
```

Skill page: https://clawhub.ai/skills/twse-api

### Claude Code (plugin marketplace)

This plugin is distributed through the [NanookAI/skills](https://github.com/NanookAI/skills)
marketplace. Inside Claude Code, run:

```
/plugin marketplace add NanookAI/skills
/plugin install twse-api@nanookai-skills
```

The skill is then available in every project, and `/plugin marketplace update`
picks up new versions.

### Manual

Copy `skills/twse-api/` into your project's `.claude/skills/` directory
(or `~/.claude/skills/` for all projects).

## Usage

Once installed, just ask Claude about Taiwan stocks — the skill triggers
automatically. Examples:

- "台積電今天的收盤價和本益比是多少?"
- "Get the TAIEX index history and plot the last month"
- "列出上市公司股利分派情形,找出殖利率最高的 10 檔"

## Repository layout

```
skills/twse-api/
├── SKILL.md           # Main skill: conventions, quick start, task→endpoint cheat sheet
└── references/        # Per-category endpoint catalogs with exact JSON response keys
```

Endpoint data is derived from the official Swagger spec
(`https://openapi.twse.com.tw/v1/swagger.json`) and verified against live
API responses. Chinese endpoint titles from the official docs are preserved
as comments.

## License

[MIT](LICENSE)
