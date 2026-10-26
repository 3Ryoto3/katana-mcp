<p align="center"><img src="assets/logo.png" width="96" height="96" alt="Katana"></p>

# Katana — Japan Stock Screener MCP

Connect your AI assistant to [Katana](https://katanascreener.com/en/mcp/) and screen every listed company in Japan (about 3,800) from a conversation: financial conditions, 10-year aggregates, custom formulas, words in annual securities reports, and qualitative judgment from the report text.

This repository is a setup kit for Claude Code, Cursor, Gemini CLI, and Cline. It contains connection settings and skills only. The Katana server itself runs at `https://mcp.katanascreener.com/mcp` and is not part of this repository.

[日本語は下にあります](#日本語)

## Before you use it

- Sign-in with a Katana account (free registration) is required. Your client opens Katana's sign-in page the first time it connects.
- Tool calls are limited per day (Japan time): 50 for registered users, 500 on a paid plan.
- Qualitative judgment (`judge_qualitative`) uses the same AI budget as Search with AI on katanascreener.com. The other tools do not use it.
- Data comes from annual securities reports on EDINET (Financial Services Agency of Japan) and is updated every morning.

## Tools

| Tool | What it does |
|---|---|
| `list_metrics` | Metric catalog: keys, Japanese and English names, units, missing counts, and the syntax for period aggregates and custom formulas |
| `list_preset_screens` | Published preset screens (Graham, Piotroski, Magic Formula and others) |
| `screen_companies` | Filter all companies by financial conditions, period aggregates, custom formulas, and words in annual reports |
| `company_financials` | One company's latest metrics and up to 10 fiscal years of financials |
| `read_filing` | Passages from the main sections of one company's latest annual report, revenue share by segment, and the EDINET link |
| `judge_qualitative` | Judge companies against yes/no questions from their annual reports; returns pass, review, or fail with the passage behind it |

## Install

Server URL: `https://mcp.katanascreener.com/mcp` (Streamable HTTP, OAuth sign-in)

### Claude Code

Server only:

```bash
claude mcp add --transport http katana https://mcp.katanascreener.com/mcp
```

Then choose Katana in `/mcp` to sign in.

Server and skills, as a plugin:

```
/plugin marketplace add 3Ryoto3/katana-mcp
/plugin install katana@katana-mcp
```

### Cursor

[Add to Cursor](cursor://anysphere.cursor-deeplink/mcp/install?name=katana&config=eyJ1cmwiOiJodHRwczovL21jcC5rYXRhbmFzY3JlZW5lci5jb20vbWNwIn0=), or add this to `~/.cursor/mcp.json`:

```json
{
  "mcpServers": {
    "katana": { "url": "https://mcp.katanascreener.com/mcp" }
  }
}
```

This repository is also a Cursor plugin (`.cursor-plugin/plugin.json`, `mcp.json`, `skills/`).

### Gemini CLI

```bash
gemini extensions install https://github.com/3Ryoto3/katana-mcp
```

Then run `/mcp auth katana` to sign in.

### Cline

Add this to `cline_mcp_settings.json`, or ask Cline to install from this repository ([llms-install.md](llms-install.md)):

```json
{
  "mcpServers": {
    "katana": { "type": "streamableHttp", "url": "https://mcp.katanascreener.com/mcp" }
  }
}
```

### Other clients

Any client that supports remote MCP servers with OAuth can connect to `https://mcp.katanascreener.com/mcp`. Steps for Claude and ChatGPT are on [katanascreener.com/en/mcp/](https://katanascreener.com/en/mcp/).

## Skills

| Skill | Use it to |
|---|---|
| [`screen-by-hypothesis`](skills/screen-by-hypothesis/SKILL.md) | Turn an idea or a company profile into conditions and screen the whole market |
| [`verify-with-filings`](skills/verify-with-filings/SKILL.md) | Check a shortlist against what the annual reports state (`read_filing`, `judge_qualitative`) |
| [`company-ten-years`](skills/company-ten-years/SKILL.md) | Look at one company over 10 years with its annual report sections |

## Example requests

- "Using Katana, find companies across Japan growing on data center cooling demand"
- "Using Katana, find companies whose profit would rise most from interest income as rates go up"
- "Show Toyota (7203)'s 10-year operating income and cash flow from Katana"

## Links

- Setup and details: https://katanascreener.com/en/mcp/
- Privacy policy: https://katanascreener.com/en/privacy.html
- Terms of service: https://katanascreener.com/en/terms.html
- Support: katanascreener@gmail.com

Katana is for informational purposes only and is not a recommendation or solicitation to buy or sell any securities. Investment decisions are your own responsibility.

## License

The files in this repository are under the [MIT License](LICENSE). The Katana server, its data, and katanascreener.com are not covered by this license and are not included here.

---

## 日本語

刀（[katanascreener.com](https://katanascreener.com/mcp/)）をAIにつなぎ、日本の上場企業約3,800社を会話から探すためのキット。財務条件・10年の期間集計・その場で作る数式・有価証券報告書の語で絞り込み、有報の本文から定性判定もできる。

このリポジトリは Claude Code・Cursor・Gemini CLI・Cline 用の接続設定とスキルだけを含む。刀のサーバー本体は `https://mcp.katanascreener.com/mcp` で動いており、このリポジトリには含まれない。

- 利用には刀のアカウント（無料登録）でのログインが必要です。初回接続時に刀のログイン画面が開きます。
- ツールの呼び出しは1日（日本時間）あたり、登録者50回・課金者500回までです。
- 定性判定（`judge_qualitative`）は、刀の「AIで探す」と同じAI予算を使います。ほかのツールは使いません。
- データは金融庁EDINETの有価証券報告書から作り、毎朝更新しています。

導入方法は上の [Install](#install) を参照。Claude と ChatGPT での接続手順は [katanascreener.com/mcp/](https://katanascreener.com/mcp/) にある。

刀は情報提供のみを目的としており、特定の金融商品の売買を推奨・勧誘するものではありません。投資に関する最終判断はご自身の責任で行ってください。

ライセンス：このリポジトリのファイルはMITライセンス。刀のサーバー・データ・katanascreener.com はこのライセンスの対象外で、ここには含まれない。
