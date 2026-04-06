# X / Twitter Engagement Reference

## Tool: xurl

CLI at `/opt/homebrew/bin/xurl`. Authenticated as `@broomva_tech`.

```bash
xurl mentions -n 10                    # Recent mentions
xurl search "QUERY" -n 5              # Search tweets
xurl post "TEXT"                       # Standalone post
xurl reply TWEET_ID "TEXT"            # Reply (engagement-gated — see 403 section)
xurl quote TWEET_ID "TEXT"            # Quote-tweet (always works)
xurl timeline --max-results 10        # Own timeline
```

## The 403 Constraint

X API v2 enforces `reply_settings` per tweet. The API returns:
```
403: Reply to this conversation is not allowed because you have not been 
     mentioned or otherwise engaged by the author.
```

**Root cause**: High-profile accounts often set restricted reply settings. The X app uses internal v1.1 endpoints that bypass this. The API cannot.

**Same constraint on QTs**: Some accounts also restrict quote-tweets via the same mechanism.

## Engagement Ladder

```
Level 1 — Quote-tweet (unconditional)
  xurl quote TWEET_ID "text"
  → Works on all accounts with public tweets
  → Best for adding insight to big threads without needing engagement

Level 2 — Wait for engagement
  → Target comments on their thread/mentions → they'll see and may reply
  → Once they reply or mention @broomva_tech → API replies fully unlocked

Level 3 — App reply (manual)
  → @broomva replies from X app directly
  → Creates engagement chain (they've "engaged" us via thread context)
  → Bot can now continue via API in same conversation

Level 4 — DM (for serious collaboration)
  → For @PolicyLayer, @Evolvent_AI type opportunities
  → Done manually from app
```

## Search Queries (run every loop)

```bash
xurl search "agent memory OR event sourcing agent" -n 5
xurl search "rust agent architecture OR rust LLM" -n 5
xurl search "x402 payment agent OR micropayment agent" -n 5
xurl search "agent identity OR soul file DID" -n 5
xurl search "agent homeostasis OR cognitive drift" -n 5
xurl search "MCP model context protocol agent" -n 5
xurl search "agent operating system OR agent OS kernel" -n 5
```

## Post Templates

### Standalone insight (1/day, 8-10am ET)
```
{single concrete architectural claim}

{3-4 line explanation with specific detail}

{one-line implication or open question}
```

Max 280 chars. URL counts as 23 chars. Leave 257 chars for body.

### Reply (when API-gated accounts engage us)
```
{acknowledge their specific point in 1 sentence}
{add the architectural angle that extends it}
{optional: question that invites next reply}
```
Under 280 chars. No link unless directly relevant.

### Quote-tweet
```
{their core claim restated more precisely}

{how Life OS implements or validates this:}
{module name + specific mechanism}

{one-line implication}
```
Under 240 chars (leave room for quoted tweet).

## Daily Limits

| Action | Limit | Timing |
|--------|-------|--------|
| Quote-tweets | 3/day max | Stagger: 9:07, 13:23, 18:41 ET |
| Standalone posts | 1/day | 8-10am ET optimal |
| Replies (API-gated) | Unlimited when unlocked | Immediate when mention comes in |
| Searches | Unlimited | Run each loop |

**Stagger timing**: post at odd minutes (9:07, not 9:00) to avoid looking automated.

## Active Thread IDs

Update this table as threads evolve:

| Thread / Conv ID | Account | Topic | Status |
|-----------------|---------|-------|--------|
| `2041105216469193047` | @jeremie_strand | Agent security, confused deputy, FsPolicy | Active — deep technical |
| `2041087024162070651` | @Evolvent_AI | World model going public | Active — move to DM |
| `2040985943365005602` | @PolicyLayer | Governance collab | Active — DM sent |
| `2041209680974733684` | @PsudoMike | Bi-temporal Lago | Active — ongoing |

## Content Angles by Module

| Module | X angle | Example post opening |
|--------|---------|---------------------|
| Lago | Bi-temporal, event sourcing | "event sourcing isn't a database pattern. it's a correctness guarantee." |
| Arcan | OperatingMode, agent loop | "LLM is the CPU. Arcan is the OS that actually runs the loop." |
| Autonomic | HysteresisGate, cognitive drift | "the first sign an agent is running unattended isn't bad output. it's cognitive drift." |
| Anima | Soul file, DID, identity | "the soul file is not your agent's identity. it's a config. anyone with write access owns the values." |
| Nous | Dual-eval, calibration | "confidence scores are self-referential loops. the model rates its own certainty." |
| Praxis | FsPolicy, confused deputy | "the confused deputy problem: agent trusted to do X, attacker uses that trust to authorize Y." |
| Haima | x402, micropayments | "x402: agent hits endpoint, gets HTTP 402, pays from wallet, retries. zero human." |
| Spaces | A2A, distributed | "agents need a nervous system, not just tool calls. Spaces is the communication substrate." |
