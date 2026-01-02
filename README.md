# Trayd - Trade Robinhood from Claude Code

Connect Claude Code to your Robinhood account. Analyze your portfolio, get real-time quotes, and execute trades—all through conversation.

![MCP](https://img.shields.io/badge/MCP-Compatible-blue)
![License](https://img.shields.io/badge/license-MIT-green)

![Demo](demo.gif)

## Quick Start

```bash
claude mcp add --transport http trayd https://mcp.trayd.ai/mcp --scope user
```

Then in Claude Code:
1. Type `/mcp` → select `trayd` → click **Authorize**
2. Sign in with Google
3. Say: *"Link my Robinhood account"*
4. Approve on your phone
5. Start trading!

## What You Can Do

### 📊 Portfolio Analysis
```
"What's my portfolio worth?"
"Which positions are up today? Which are down?"
"What's my biggest winner this week?"
"Show me everything that's down more than 5%"
```

### 📈 Real-Time Market Data
```
"What's NVDA trading at?"
"Get me a quote on AAPL"
"Check the price of TSLA"
```

### 💰 Trade Execution
```
"Buy 10 shares of AAPL"
"Place a limit order for TSLA at $400"
"Set 5 ladder buys for NVDA from $180-$175"
"Set stop losses on all my positions at -5%"
```

### 🔥 Complex Operations (One Sentence)
```
"Sell half of my TSLA position"
"What's my biggest loser today? Sell it."
"Cancel all my open orders and show me what's left"
"Buy $500 worth of each: AAPL, GOOGL, MSFT"
```

> **Note:** Market orders work during regular hours (9:30 AM - 4 PM ET). Extended hours (pre-market & after-hours) require limit orders—this is a Robinhood policy.

### Why Trayd?
Instead of clicking through dozens of screens:
```
Setting 5 ladder limit orders manually:
  Open app → Search NVDA → Buy → Limit → $180 → 10 shares → Submit
  → Search NVDA → Buy → Limit → $178.75 → 10 shares → Submit
  → Search NVDA → Buy → Limit → $177.50 → 10 shares → Submit
  → Search NVDA → Buy → Limit → $176.25 → 10 shares → Submit
  → Search NVDA → Buy → Limit → $175 → 10 shares → Submit
  (50+ clicks, 5 minutes)

With Trayd:
  "Set 5 ladder buys for NVDA from $180-$175"
  (1 sentence, 10 seconds)
```

## Security Model

### How Your Credentials Flow

```
You → Claude Code → Trayd Server → Robinhood API
         ↓              ↓
    (MCP token)    (Your RH credentials
                   passed through to RH,
                   NEVER stored by us)
```

**Important to understand:**
- Your Robinhood email/password pass through our server to Robinhood's API
- We **never log, store, or persist** your password - it goes directly to Robinhood
- After login, Robinhood returns access tokens which we hold **in memory only**
- Tokens are wiped on: logout, server restart, or container redeployment

### What We Store (and Don't)

| Data | Stored? | Where | Duration |
|------|---------|-------|----------|
| Robinhood password | **NO** | Never touches disk | Passed through, then discarded |
| Robinhood access token | Yes | Server memory only | Until logout/restart |
| Your trades/positions | **NO** | Not logged | Fetched live from RH |
| Your Google identity | Yes | Via Clerk | For auth only |

### Authentication
- **OAuth 2.1 with PKCE** - Industry-standard secure auth flow
- **Google Sign-in via Clerk** - We don't handle Google passwords
- **Robinhood Phone 2FA** - Native Robinhood security, you approve on your phone

### Infrastructure
- **AWS ECS Fargate** - Containerized, isolated execution
- **Cloudflare Tunnel** - DDoS protection, no exposed ports
- **HTTPS everywhere** - All traffic encrypted

## Example Conversations

### Check Your Portfolio
```
You: What's my portfolio worth?

Claude: Your Robinhood portfolio:
  • Total Equity: $45,230.82
  • Cash Available: $2,156.33
  • Buying Power: $2,156.33
```

### View Positions
```
You: Show my positions

Claude: Your current holdings:

  NVDA - 50 shares
  • Avg Cost: $127.45 → Current: $137.01
  • Market Value: $6,850.50
  • P&L: +$478.00 (+7.5%)

  AAPL - 100 shares
  • Avg Cost: $178.23 → Current: $254.49
  • Market Value: $25,449.00
  • P&L: +$7,626.00 (+42.8%)
```

### Get a Quote
```
You: What's TSLA trading at?

Claude: TSLA (Tesla Inc) - $421.06
  • Bid: $421.05 × 100
  • Ask: $421.08 × 200
  • Day Range: $415.02 - $428.50
  • Volume: 42.3M
```

### Place a Trade
```
You: Buy 5 shares of GOOGL at $191

Claude: I'll place a limit order to buy 5 shares of GOOGL at $191.00.

  [Calls place_order tool]

  ✓ Limit order placed successfully
  • Order ID: 67890-abcdef
  • Buy 5 GOOGL @ $191.00 limit
```

### Cancel an Order
```
You: Cancel my GOOGL order

Claude: [Calls cancel_order tool]

  ✓ Order cancelled successfully
```

## Troubleshooting

| Issue | Solution |
|-------|----------|
| Browser doesn't open for auth | Type `/mcp` → select `trayd` → click "Authorize" |
| Phone notification not received | Ensure Robinhood app is installed and you're logged in |
| "Authentication required" error | Run `/mcp` to re-authenticate |
| Market order rejected after hours | Use limit orders (Robinhood policy for extended hours) |

## FAQ

**Is this safe?**

Yes, and here's why you can verify it yourself:

1. **Phone 2FA on every login** - Robinhood sends a notification to your phone. Nothing happens unless you tap "Approve". You control access.

2. **Your Claude is honest to you** - This MCP runs through *your* Claude Code. Ask Claude "Am I logged in to Robinhood?" or "Is my Robinhood linked?" anytime. Claude will honestly tell you your connection status because it's *your* assistant.

3. **Instant logout, verified by Claude** - Say "Logout from Robinhood" and all credentials are immediately wiped from memory. Then ask Claude "Am I still connected?" - it will confirm you're logged out. No trust required—verify it yourself.

**Why should I trust you?**

You don't have to trust us blindly—you can verify:
- **Phone approval required** - We can't access your account without you tapping Approve
- **Ask Claude to verify** - Your Claude Code honestly reports your connection status
- **Logout = instant wipe** - Say "logout" and ask Claude to confirm you're disconnected
- **Server restarts wipe everything** - Tokens only exist in memory, never on disk

**What if something goes wrong with a trade?**
You are responsible for all trades placed through your account. We provide the interface; you make the decisions. Always verify orders before confirming.

## Risks & Disclaimers

**Please read before using:**

- **USE AT YOUR OWN RISK** - This software is provided "as is" without warranty
- **NOT FINANCIAL ADVICE** - We don't provide investment recommendations
- **YOU ARE RESPONSIBLE** - For all trades and decisions made through this tool
- **NO LIABILITY** - We are not liable for any losses, bugs, or issues
- **BETA SOFTWARE** - This is early-stage software; expect rough edges

**By using Trayd, you acknowledge:**
1. You understand the security model and accept the risks
2. You are solely responsible for your trading decisions
3. You will not hold Trayd liable for any losses
4. You understand this is not affiliated with Robinhood

---

**Not affiliated with Robinhood Markets, Inc.**

**Not financial advice.** This tool helps you interact with your own brokerage account. All investment decisions are yours.

## Support

- Email: team@trayd.ai
- GitHub: [trayders/trayd-mcp](https://github.com/trayders/trayd-mcp/issues)

## License

MIT
