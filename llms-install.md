# Installing the Katana MCP server

Katana is a remote MCP server. There is nothing to download, build, or run locally, and no API key is needed.

1. Add this entry under `mcpServers` in the MCP settings file (for Cline, `cline_mcp_settings.json`):

```json
"katana": {
  "type": "streamableHttp",
  "url": "https://mcp.katanascreener.com/mcp"
}
```

2. The server requires sign-in with a Katana account (free registration at https://katanascreener.com/). When the client connects, it opens Katana's sign-in page in the browser; the user signs in and clicks Allow. If the client cannot open a browser sign-in, tell the user that Katana needs OAuth sign-in and point them to https://katanascreener.com/en/mcp/.

3. Confirm the connection by calling `list_metrics` with `{"query": "cash"}`. It should return metric keys with Japanese and English names.

Notes for the agent:
- `judge_qualitative` is charged to the user's Katana AI budget. Ask the user before calling it. The other tools are not charged.
- Tool calls are limited per day (Japan time): 50 for registered users, 500 on a paid plan.
- Amounts are in JPY and ratios are decimals. Price-based metrics are as of each fiscal year end, not current prices.
