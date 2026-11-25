---
name: adspirer-write-ad-copy
description: "Write on-brand ad copy for a named platform and campaign, using the brand voice, the campaign's current ads and keywords, and real search terms. Use when the user asks for headlines, descriptions, primary text or new ad variants for a specific campaign."
---

# Write ad copy

Load `adspirer-agent`, `adspirer-mcp` and `adspirer-creative`, plus the platform's own skill for its
character limits.

Use the platform and campaign the user named. If either is missing, ask.

1. If `BRAND.md` exists and is an Adspirer brand workspace, read it for brand voice and audience,
   and `STRATEGY.md` for messaging directives. Otherwise ask for the voice in a sentence or two.
2. Read the campaign's current ads and keywords (`get_campaign_structure` on Google; the
   equivalent read on the platform's router elsewhere).
3. On paid search, read what people actually search (`analyze_search_terms`).
4. Call `suggest_ad_content` where the platform's router lists it, and treat its output as
   suggestions to filter, not final copy.
5. Write at least five headline and description options that follow the brand voice, stay inside
   each field's limit, and are grounded in the performance data. Show the character count for each.
6. Present the options and wait.

Tool names here are candidates: discover each with `list_tools` and `get_tool_schema` first.
Writing copy changes nothing in the account. Updating a live ad is a separate, explicit yes for that
ad on that account, following `adspirer-creative`.
