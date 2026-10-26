---
name: company-ten-years
description: Look at one Japanese listed company's financials over up to 10 fiscal years with Katana, together with its annual report sections. Use when the user names a company or securities code and wants its history, trend, or a closer look.
---

# Look at one company over 10 years

Requires the Katana MCP server (`https://mcp.katanascreener.com/mcp`) and a signed-in Katana account.

1. Identify the 4-character securities code (for example `7203`). If you only have a name, find it with `screen_companies` or ask the user.
2. Run `company_financials` with `years: 10`. Pass `fields` (metric keys from `list_metrics`) when the user is interested in specific items; otherwise the main P/L, cash flow, and balance sheet items are returned.
3. Show the figures as a table by fiscal year, and point out turning points, losses, and missing years. Null means unavailable, not zero.
4. If the user wants to know why the numbers moved or what the business does, read the relevant sections with `read_filing` (business description, issues, risks, management discussion, R&D, capital expenditures, dividend policy, and more), plus revenue share by segment.
5. For anything after the latest annual report, check the company's latest earnings results and announcements, and give the date of each source.

Amounts are in JPY and ratios are decimals. Price-based metrics are as of each fiscal year end, not current prices. Reply in the language the user wrote in.
