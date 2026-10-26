---
name: screen-by-hypothesis
description: Turn an investment hypothesis or a description of the companies the user wants into Katana conditions and screen every listed company in Japan. Use when the user asks to find Japanese stocks that fit an idea, a theme, or a company profile.
---

# Screen Japanese companies from a hypothesis

Requires the Katana MCP server (`https://mcp.katanascreener.com/mcp`) and a signed-in Katana account.

1. If the hypothesis is ambiguous in a way that would change which companies qualify, ask the user one or two short questions first. Otherwise go ahead.
2. Find the metrics you need with `list_metrics` (search by key, Japanese name, or English name). Where useful, use period aggregates (`annual__<metric>__<mean|median|min|max|cagr|latest>__<years>`) and custom formulas in `custom_metrics`.
3. For business keywords, add `word_conditions` with the word as written in Japanese annual reports (for example `データセンター`). Optionally limit a word to one section.
4. Run `screen_companies`. Show the user the conditions you used, the number of matching companies, and the data timestamp.
5. If too many or too few companies remain, adjust one condition at a time and say what you changed.
6. Offer the next step: judge the shortlist against the annual reports (the `verify-with-filings` skill), or look at one company's history (the `company-ten-years` skill).

Notes:
- Amounts are in JPY and ratios are decimals (0.5 = 50%).
- Price-based metrics are as of each fiscal year end, not current prices.
- Null means unavailable, which is different from zero.
- For debt in formulas, use `interest_bearing_debt`.
- `list_preset_screens` returns published screens (Graham, Piotroski, Magic Formula and others); pass an id as `preset` to start from one.
- Reply in the language the user wrote in.
