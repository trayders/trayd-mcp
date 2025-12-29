# Trayd - Robinhood Portfolio Intelligence for Claude Code

Connect Claude Code to your Robinhood account. View positions, analyze performance, and optionally execute trades with explicit confirmations.

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
5. Start analyzing!

## What You Can Do

### Portfolio Analysis (Read-Only)
```
"What's my portfolio worth?"
"Show my current positions and today's P&L"
"What's my exposure by sector?"
"Which positions moved most today?"
"Get me a quote on NVDA"
```

### Trade Execution (Requires Confirmation)
```
"Buy 10 shares of AAPL" → Shows preview → Requires explicit confirmation
"Place a limit order for TSLA at $400" → Shows full order details → Confirm to execute
"Cancel my open orders"
```

## Features

### Portfolio Intelligence
- **Portfolio Overview** - Equity, cash, buying power at a glance
- **Position Analysis** - All holdings with cost basis, current value, P&L
- **Real-time Quotes** - Current prices for any ticker
- **Order Tracking** - View all open/pending orders

### Trade Execution (Optional)
- **Market Orders** - Buy/sell at market price
- **Limit Orders** - Set your price
- **Order Management** - Cancel open orders
- **Explicit Confirmation** - Every trade shows full preview before execution

## Safety & Security

### Authentication
- **OAuth 2.1 with PKCE** - Industry-standard secure auth
- **Google Sign-in** - No passwords stored by Trayd
- **Robinhood Phone 2FA** - Native Robinhood security required

### Data Security
- **Memory-Only Storage** - Tokens never written to disk
- **Session Isolation** - Each user's data completely separate
- **Auto-Wipe** - All tokens cleared on server restart or logout

### Trade Safety
- **Explicit Confirmation Required** - Every order shows full details before execution
- **Order Preview** - Ticker, side, quantity, order type displayed before confirm
- **Audit Trail** - All actions logged with timestamps
- **Read-Only Default** - Portfolio viewing requires no special permissions

## Tools Available

### Read-Only Tools
| Tool | Description |
|------|-------------|
| `check_login_status` | Check if Robinhood is linked |
| `get_portfolio` | Portfolio summary (equity, cash, buying power) |
| `get_positions` | All stock positions with P&L |
| `get_open_orders` | Pending orders |
| `get_quote` | Stock quote for a ticker |
| `get_price` | Latest price |

### Execution Tools (Require Confirmation)
| Tool | Description |
|------|-------------|
| `link_robinhood` | Link your Robinhood account |
| `place_order` | Buy/sell with explicit confirmation |
| `cancel_order` | Cancel an open order |
| `logout` | Unlink Robinhood (wipes token immediately) |

## Example Conversations

### Portfolio Analysis
```
You: What's my portfolio looking like?

Claude: Your portfolio summary:
  • Total Equity: $229,956
  • Cash: $2,021
  • Positions: 12

  Top Holdings:
  1. NVDA - 1,353 shares @ $187.79 (+$13,038 gain)
  2. AAPL - 500 shares @ $273.84 (+$5,230 gain)
  3. GOOGL - 100 shares @ $313.26 (+$2,100 gain)
```

### Trade Execution (with confirmation)
```
You: Buy 10 shares of AAPL

Claude: Order Preview:
  • Action: BUY
  • Symbol: AAPL
  • Quantity: 10 shares
  • Type: Market Order
  • Estimated Cost: ~$2,738

  Do you want to place this order? (yes/no)

You: yes

Claude: ✅ Order placed successfully
  Order ID: abc123...
```

## Troubleshooting

**Browser doesn't open for auth?**
→ Type `/mcp` in Claude Code, select `trayd`, click "Authorize"

**Phone notification not received?**
→ Make sure Robinhood app is installed and you're logged in. Try again.

**"Authentication required" error?**
→ Run `/mcp` to re-authenticate (tokens expire on server restart)

## Privacy & Compliance

- Your Robinhood credentials are sent directly to Robinhood, never stored by Trayd
- Access tokens exist only in server memory
- No trading data is logged or stored permanently
- Full token wipe on logout or server restart

**This tool is not affiliated with Robinhood Markets, Inc.**

**Not financial advice.** This tool helps you interact with your own brokerage account. All investment decisions are your own.

## Support

- Issues: [GitHub Issues](https://github.com/trayders/trayd-mcp/issues)
- Email: team@trayd.ai

## License

MIT
