# Trayd - Robinhood Trading for Claude Code

Trade stocks on Robinhood using natural language in Claude Code.

![MCP](https://img.shields.io/badge/MCP-Compatible-blue)
![License](https://img.shields.io/badge/license-MIT-green)

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

```
"What's my portfolio worth?"
"Show me my NVDA position"
"Buy 10 shares of AAPL"
"Place a limit order for 5 TSLA at $400"
"Cancel my open orders"
"What's the price of GOOGL?"
```

## Features

- ✅ **Portfolio & Positions** - View equity, cash, all holdings
- ✅ **Real-time Quotes** - Get current prices for any ticker
- ✅ **Market Orders** - Buy/sell at market price
- ✅ **Limit Orders** - Set your price
- ✅ **Order Management** - View and cancel open orders
- ✅ **Secure OAuth 2.1** - Google sign-in, no passwords stored
- ✅ **Phone 2FA** - Robinhood's native security
- ✅ **Memory-only Storage** - Tokens never written to disk

## Security

- 🔐 OAuth 2.1 with PKCE for authentication
- 📱 Robinhood phone approval required for linking
- 🧠 Access tokens stored in memory only (wiped on server restart)
- 🚫 Your Robinhood password is never stored - sent directly to Robinhood

## Tools Available

| Tool | Description |
|------|-------------|
| `check_login_status` | Check if Robinhood is linked |
| `link_robinhood` | Link your Robinhood account |
| `complete_robinhood_link` | Complete phone approval |
| `logout` | Unlink Robinhood (wipes token) |
| `get_portfolio` | Portfolio summary |
| `get_positions` | All stock positions |
| `get_open_orders` | Pending orders |
| `get_quote` | Stock quote for a ticker |
| `get_price` | Latest price |
| `place_order` | Buy/sell (market or limit) |
| `cancel_order` | Cancel an order |

## Troubleshooting

**Browser doesn't open for auth?**
→ Type `/mcp` in Claude Code, select `trayd`, click "Authorize"

**Phone notification not received?**
→ Make sure Robinhood app is installed and you're logged in. Try again.

**"Authentication required" error?**
→ Run `/mcp` to re-authenticate (tokens expire on server restart)

## License

MIT

---

*Not affiliated with Robinhood Markets, Inc.*
