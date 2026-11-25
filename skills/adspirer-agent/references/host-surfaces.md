# Host surfaces: showing work, repeating work, and the browser

This plugin runs in Antigravity. Use what the host actually offers, and don't announce a capability
you have not confirmed in this session. When in doubt, the conversation is the surface.

## Showing work

1. **Do the work first.** The answer comes before the packaging.
2. **A markdown table in the conversation is the default.** A scorecard, a comparison of ad
   variants, or a campaign plan all fit one.
3. **A local file when the user wants something to keep.** Write one self-contained HTML page (or
   a markdown file) in the workspace and tell the user the path. Inline the figures and draw charts
   as SVG or CSS. Don't fetch a chart library, font or image from a third-party host unless the user
   asks. Nothing is published or shared by writing the file.
4. **Ask before anything leaves the conversation.** Ad performance, spend, customer lists and
   lead-form submissions are confidential. Never publish, upload or share a page with account data
   unless the user explicitly says to, and say plainly what would become visible first.

Don't promise a link, a hosted page or a screenshot you can't produce.

## Repeating work

Offer a schedule only if this host actually supports one and the user asks for it. Never say
something is scheduled until a real scheduler confirms it, and never say "I'll keep an eye on it":
the conversation ends when the user closes it.

Good candidates for a cadence: a Monday performance review, a mid-month pacing check, a nudge before
a budget resets.

- Write the prompt so a late run behaves: "only look at today's spend; if it's past 6pm, just
  summarize what changed."
- A scheduled run reads and reports. It never changes spend, and it never sends an email or a Slack
  message. Those need a fresh yes in a live conversation.
- Be conservative about unattended runs: one that writes to an ad account spends real money with
  nobody watching.

### Adspirer's own server-side monitors

Adspirer has monitors and email briefs of its own, under the `monitoring_and_reporting` router:
threshold alerts on ROAS, CPA, spend and CTR, scheduled reports, and async research jobs. Use them
when the host has no scheduler, when the user wants the report to arrive as **email**, or when they
want an alert to keep firing after they close this assistant.

Discovery on that router is free (`{"action": "list_tools"}`), as are `list_monitors`,
`list_scheduled_tasks`, `get_monitor_history` and `test_monitor`. Creating a monitor or a scheduled
brief is a write: confirm the metric, threshold, cadence and recipient with the user first.

## What a scheduled run costs

A scheduled run re-does the work, which means it calls Adspirer tools again. Every run draws on the
user's monthly tool-call quota exactly like a live conversation. A daily review costs roughly thirty
times what a monthly one does.

Pick a cadence the plan can carry, and say what it will cost in calls before setting it up. Weekly is
the right default for a performance review; daily is for accounts spending enough to justify it.
`get_usage_status` is free and shows what's left.

## The browser

The read-only ads-manager check (`adspirer-ads-manager-browser`) needs a browser the agent can
control and the user can take over to sign in. Use it only if this host provides one in this session.
The user signs in themselves; the agent never types or receives a password or a 2FA code. With no
controllable browser, say so once and use the Adspirer API tools instead.
