---
name: verify-with-filings
description: Check a shortlist of Japanese companies against what their latest annual securities reports state, using Katana's read_filing and judge_qualitative. Use after a screen, or when the user asks which of these companies actually do something according to their filings.
---

# Check candidates against annual reports

Requires the Katana MCP server (`https://mcp.katanascreener.com/mcp`) and a signed-in Katana account.

1. Write the questions in English, as yes/no propositions the annual report can support or contradict.
   - One proposition per question; split a hypothesis with several parts into several questions.
   - Put a question that only makes sense if another holds after it (for example, "sells X" before "X is a main source of revenue").
   - Ask about what the filing states as fact (products, customers, orders, capacity plans already decided). Questions about expected growth tend to come back unconfirmed.
   - Optionally add `search_terms`: words as written in Japanese filings, whose passages are read first.
2. Before running `judge_qualitative`, ask the user. It is charged to the user's Katana AI budget; the other Katana tools are not. Wait for the answer.
3. Run `judge_qualitative` with the securities codes and questions. With 200 or more companies it asks for confirmation first; repeat with `confirmed: true` only after the user agrees. If `unjudged_sec_codes` comes back, continue with those codes.
4. Show the companies that passed first, with the passage behind each. Tell the user how many came back as review. Review means the filing did not confirm it, which is not the same as failing; show them if the user asks.
5. For companies the user wants to look into, read the sections with `read_filing` (text is in Japanese as filed; it is not the full filing). Check the latest earnings results and company announcements to see whether each one still fits. Separate supporting, contradicting, and unverified points, and give the date of each source.
6. If the user asks for a link, pass `share` to `judge_qualitative` to get a katanascreener.com link that opens the result in Katana.

Reply in the language the user wrote in.
