# Adspirer Advertising Agent for Antigravity

Run your ad campaigns from Antigravity. Adspirer connects the agent to your live ad accounts on Google Ads, Meta Ads (Facebook and Instagram), TikTok Ads, LinkedIn Ads, Microsoft Advertising (Bing), Amazon Ads, Walmart Connect and ChatGPT Ads through Adspirer's hosted MCP server, so you can research keywords, plan, launch and optimize campaigns, and report on ROAS, ACoS, CPA and CTR without leaving the conversation. New campaigns are created paused, and every change that affects spend needs your approval.

## Use it for

- **Paid search:** Google Ads Search and Performance Max, Microsoft Advertising, keyword research with live CPC and search volume, negative keywords and search-term reports.
- **Paid social:** Facebook and Instagram ads, TikTok in-feed video and Spark Ads, LinkedIn B2B lead generation, and YouTube and Demand Gen campaigns.
- **Retail media:** Amazon Sponsored Products, Sponsored Brands and Sponsored Display, and Walmart Connect Sponsored Products, with ACoS and bid management.
- **Reporting:** cross-platform spend, conversions, ROAS, CPA, CTR and CPC, with pacing against budget.
- **Optimization:** find wasted spend, shift budget to what converts, catch creative fatigue, and audit conversion tracking before you scale.
- **Ad copy:** headlines, descriptions and primary text written to each platform's limits and your brand voice.

## Install

**Antigravity app:** open **Customizations**, find **Adspirer Advertising Agent** in the
Marketplace, and install it.

**Antigravity CLI:**

```text
agy plugin install https://github.com/Adspirer/adspirer-antigravity-plugin
```

**Manual:** clone this repository into your plugins folder.

```text
git clone https://github.com/Adspirer/adspirer-antigravity-plugin ~/.gemini/config/plugins/adspirer-advertising-agent
```

Then sign in: open **Customizations**, then **Installed**, then **MCP Servers**, and choose
**Authenticate** next to the Adspirer server. Sign in to Adspirer in the browser, then connect the
accounts you want to work on at [adspirer.ai/connections](https://adspirer.ai/connections). No
API key or client secret is required. An Adspirer account is required, and plan usage limits apply.

## Get started

Ask:

```text
How did my ads do across every platform in the last 30 days?
Find spend that is not converting on Google and Meta, and propose fixes.
Research keywords for my product and plan a Google Search campaign.
Write five new headlines for my best Search campaign in our brand voice.
```

Or start with a skill by name:

| Skill | What it does |
| --- | --- |
| `/adspirer-setup` | Connect your accounts, get a first look, and optionally build a brand workspace |
| `/adspirer-status` | Connected accounts and remaining plan usage |
| `/adspirer-performance-review` | Cross-platform scorecard with the top problems and next actions |
| `/adspirer-wasted-spend` | Spend that is not converting, with a fix proposed for each item |
| `/adspirer-write-ad-copy` | On-brand copy for a named platform and campaign |
| `/adspirer-launch` | Plan and build a campaign, created paused for your review |

Add a platform and period if you want, for example `/adspirer-performance-review last 7 days`.

## What it covers

| Area | Capabilities |
| --- | --- |
| Ad platforms | Google, Meta, TikTok, LinkedIn, Microsoft, Amazon, Walmart Connect and ChatGPT Ads: campaigns, budgets, bids, keywords, audiences, creative and reporting |
| Research | Keyword research, search-term mining, and public competitor ads |
| Measurement | Conversion-tracking audit and funnel diagnosis, plus Google Analytics 4, Search Console and Tag Manager when you connect them |
| Reporting | Scorecards, a local dashboard file, and email or Slack digest drafts that are sent only after you approve each one |

Available operations depend on the platforms you connect and on your Adspirer plan.

## What's included

- **Skills** (`skills/`): the entry points above, plus `adspirer-agent`, `adspirer-mcp`,
  `adspirer-optimize`, `adspirer-keywords`, `adspirer-creative`, `adspirer-competitors`,
  `adspirer-dashboard`, `adspirer-digest`, `adspirer-docs`, one skill per ad platform
  (`adspirer-google-ads`, `adspirer-meta-ads`, `adspirer-tiktok-ads`, `adspirer-linkedin-ads`,
  `adspirer-microsoft-ads`, `adspirer-amazon-ads`, `adspirer-walmart-ads`, `adspirer-chatgpt-ads`),
  `adspirer-google-analytics`, `adspirer-search-console`, `adspirer-tag-manager`, and the read-only
  `adspirer-ads-manager-sign-in` and `adspirer-ads-manager-browser`, which the agent loads when a
  request needs them.
- **A rule** (`rules/adspirer-advertising-agent.md`) that loads only for advertising requests and
  holds the agent to paused creation and approval before spend.
- **The Adspirer MCP server** connection (`mcp_config.json`).

The hosted server is the source of truth for tool names and schemas. The skills teach the agent to
discover the current tools and their parameters instead of hardcoding every operation.

## Safety

- **Created paused.** Every new campaign is created paused and does not spend until you resume it.
- **Approval before spend.** Creating, resuming, deleting, and changing budgets, bids, keywords or
  targeting happen only after you approve that exact change on that exact account in the conversation.
- **Readback.** After a write, the agent reads the object back and reports what actually exists,
  including partial failures.
- **No purchases.** The agent never buys, upgrades or renews a plan or paid feature. If a plan limit
  is reached, it stops and explains the limit.
- **Confirmation first** before quota-heavy runs, such as reporting on every account.
- **Nothing sent without a yes.** Email and Slack digests are drafts until you approve that draft
  and destination.
- **No credentials in chat.** The optional ads-manager check is read-only, and you sign in yourself.
- **Honest numbers.** Currency, dates and data freshness are stated; missing data is never reported
  as zero; totals are never summed across currencies; competitor research covers public ads only.
- **Your files.** A brand workspace (`BRAND.md`, `STRATEGY.md`) is written only when you ask for
  one, and existing files are never overwritten.

## MCP and authentication

```json
{
  "mcpServers": {
    "adspirer": {
      "url": "https://mcp.adspirer.com/mcp"
    }
  }
}
```

The server speaks Streamable HTTP. Authentication uses OAuth 2.1 with PKCE and dynamic client
registration, so Antigravity handles the browser sign-in and the plugin contains no API keys,
tokens, client secrets, or configuration variables. Ad-platform credentials stay server-side with
Adspirer and are scoped to the accounts you connect.

## Network and execution surface

The plugin's only MCP server is `https://mcp.adspirer.com/mcp`. It contains no hooks, scripts,
telemetry, local executables, or bundled server code. Skills and the rule are Markdown guidance.
Beyond the Adspirer server, the skills may ask the agent to read Adspirer's public documentation at
`adspirer.com/docs`, to read your own website or a competitor's public pages during campaign
research, and, only if you ask for the ads-manager check and your host provides a browser, to view
an ads manager you sign in to yourself.

## Privacy, support, and source

- Privacy policy: [adspirer.com/privacy](https://www.adspirer.com/privacy)
- Terms: [adspirer.com/terms](https://www.adspirer.com/terms)
- Documentation: [adspirer.com/docs](https://www.adspirer.com/docs)
- Support: [support@adspirer.com](mailto:support@adspirer.com) for help installing, signing in or using this plugin. See [SUPPORT.md](SUPPORT.md).
- Issues: [github.com/Adspirer/adspirer-antigravity-plugin/issues](https://github.com/Adspirer/adspirer-antigravity-plugin/issues)

## License

MIT. See [LICENSE](LICENSE).
