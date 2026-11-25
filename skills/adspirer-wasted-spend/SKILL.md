---
name: adspirer-wasted-spend
description: "Find ad spend that is not converting across the connected platforms, such as search terms, keywords, placements, audiences and tired creatives, and propose fixes that are applied only after the user approves. Use when the user asks where budget is being wasted or what to cut."
---

# Wasted-spend review

Load `adspirer-agent`, `adspirer-mcp` and `adspirer-optimize`.

Use the platforms and period the user gave. With none given, cover every connected ad platform for
the last 30 complete days.

1. Call `get_connections_status`. Work only on connected platforms, and confirm the accounts when
   more than one could be meant. Confirm before running across a large number of accounts.
2. Run each platform's wasted-spend read: `analyze_wasted_spend` and `analyze_search_terms` for
   Google Ads, `analyze_meta_wasted_spend`, `analyze_linkedin_wasted_spend` and
   `analyze_tiktok_wasted_spend` for the others, and the equivalent read on any other connected
   platform's router. These are candidates, not guaranteed names: discover each one with
   `list_tools` and `get_tool_schema` first, as `adspirer-mcp` describes.
3. Separate rows with spend and no conversions from rows with a high cost per conversion. Do not
   call a row wasted when the sample is small, when conversions are still arriving, or when
   conversion tracking looks broken.
4. Report the top items by spend with the evidence, the total at stake per currency, and a proposed
   fix for each one: a negative keyword, an exclusion, a pause, or a bid or budget change, with the
   expected effect.

Reading changes nothing. Apply a fix only after the user approves that exact change on that exact
account, following `adspirer-optimize`, and read the result back. Never invent a number: a platform
that could not be read is listed as not available.
