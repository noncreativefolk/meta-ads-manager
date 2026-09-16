# meta-ads-manager — Kimi plugin

Ask "what's the status of my campaigns" or "set up a campaign" inside your
Kimi project chat. Kimi interviews you per Meta's setup framework, returns an
execution recommendation, and on your GO builds everything in your Meta ad
account automatically (all PAUSED — nothing spends until you say ACTIVATE).

No custom code to maintain: the plugin points at **Meta's official Ads MCP
server** (`https://mcp.facebook.com/ads`, open beta since Apr 2026) and adds
a SKILL.md playbook that encodes the interview + execution workflow.

## Setup (one-time, ~10 min)

1. **Push this folder to GitHub** (e.g. `noncreativefolk/meta-ads-manager`).
   Nothing secret is in this repo — auth is OAuth, no tokens stored anywhere.
2. **Install into Kimi:**
   - Kimi Work desktop: run the Plugin Builder (`/plugin-builder`), paste the
     repo URL → it registers to your **Personal** plugins tab → click +.
   - or Kimi Code CLI: `/plugins install https://github.com/<you>/meta-ads-manager`
     then `/reload`.
3. **Connect Meta:** first time a Meta tool is called, Kimi runs Meta Business
   OAuth — log in with the profile that administers your ad account. That's
   the only Meta-side touching, ever.
4. **Fill `PROJECT_CONTEXT.md`** and drop it into your Kimi project chat.

## Daily use

- "What's the status of my campaigns?" → performance readout + recommended actions
- "Set up a campaign for [goal]" → grouped interview → execution recommendation
  → reply **GO** → built in Ads Manager, PAUSED → say **ACTIVATE** to go live

## Limits (honest list)

- Meta's official server is in phased beta rollout. If your SG account isn't
  enabled yet, tools return an enablement error. Fallback: a hosted
  third-party Meta Ads MCP (e.g. Pipeboard) — **security-audit before use**,
  per your standing rule — or wait for Meta's rollout.
- Official server creates everything PAUSED by design; ACTIVATE should work
  via status update — if Meta blocks it, it's one toggle in Ads Manager.
- MCP is request/response: nothing runs while the chat is closed. For
  scheduled rules (budget pacing, fatigue auto-pause), add a scheduled-task
  or n8n layer later.
- Some UI-only surfaces (certain Advantage+ flows, billing settings) have no
  API coverage in any solution — Kimi WebBridge can drive your logged-in
  browser for those edge cases.

## Files

- `kimi.plugin.json` — manifest (MCP server + skill registration)
- `skills/meta-ads-copilot/SKILL.md` — the interview/diagnosis/execution playbook
- `PROJECT_CONTEXT.md` — your account defaults, drop into the project chat
