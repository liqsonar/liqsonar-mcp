# LiqSonar MCP server

**Website: [liqsonar.com](https://liqsonar.com) · Docs: [liqsonar.com/api-docs#mcp](https://liqsonar.com/api-docs#mcp)**

<img src="assets/logo.png" alt="LiqSonar" width="96" align="right">

Live crypto futures market data for Claude, ChatGPT, Cursor, Gemini CLI and other MCP clients: order-flow signals, detected pumps and dumps, estimated liquidation levels, large order book walls and a cross-exchange verdict on whether price moves with or against the order flow.

LiqSonar is a hosted service. This repository holds only the connection configs and the registry metadata; there is no server code to run.

- Endpoint: `https://liqsonar.com/mcp` (Streamable HTTP)
- Auth: OAuth 2.1 with dynamic client registration and PKCE (works as a custom connector in Claude and ChatGPT), or a Pro API key as `Authorization: Bearer lsk_...`
- Data: all Binance USDT futures pairs, plus Bybit, OKX, Bitget, MEXC and Hyperliquid
- Official MCP Registry: `com.liqsonar/liqsonar`
- Access: a LiqSonar Pro account ($9/month, 3-day free trial without a card)

## Tools

| Tool | What it returns |
|---|---|
| `get_signals` | Recent order-flow signals: CVD divergences, absorption, buy/sell pressure, CVD flips, funding extremes, volume spikes |
| `get_pumps` | Detected pumps and dumps with prices, volume surge, open interest change, liquidations and an AI summary |
| `get_liquidation_levels` | Estimated long and short liquidations per price bin within ±12% of the price for one pair |
| `get_order_book_walls` | Large resting limit orders with size, distance from the price and how long they have stood |
| `get_verdict` | Whether price moves with or against the order flow on Binance, Bybit, OKX and Bitget |
| `get_signal_stats` | Track record of each signal type at 15 minutes, 1 hour and 4 hours |
| `get_my_alerts` | The signed-in user's LiqSonar alerts |
| `get_my_watchlist` | The signed-in user's watchlist with prices |
| `get_my_wall_watches` | Order book walls the signed-in user tracks |

All tools are read-only.

## Connect

**Claude (claude.ai, Desktop):** Settings → Connectors → Add custom connector → `https://liqsonar.com/mcp`, then sign in to LiqSonar.

**Claude Code:**

```bash
claude mcp add --transport http liqsonar https://liqsonar.com/mcp
```

**Cursor, Windsurf, Cline and other `mcpServers` clients:**

```json
{
  "mcpServers": {
    "liqsonar": {
      "type": "http",
      "url": "https://liqsonar.com/mcp"
    }
  }
}
```

**Gemini CLI:**

```bash
gemini extensions install https://github.com/liqsonar/liqsonar-mcp
```

**With an API key** instead of OAuth, add `"headers": { "Authorization": "Bearer lsk_YOUR_KEY" }`. Keys are created on [liqsonar.com/api-docs](https://liqsonar.com/api-docs).

## Example prompts

- "Is the BTC move organic or against the order flow right now?"
- "Show the biggest order book walls on SOLUSDT within 2% of the price."
- "Where are the liquidation clusters for ETH over the last 3 days?"
- "Which pumps did LiqSonar catch in the last few hours, and what dumped after?"

## Files

- `server.json` — entry in the official MCP Registry
- `.mcp.json`, `mcp.json` — client config
- `gemini-extension.json` — Gemini CLI extension
- `.claude-plugin/plugin.json`, `.cursor-plugin/plugin.json` — Claude Code and Cursor plugin manifests
- `llms-install.md` — install steps for AI agents

## Links

- Privacy policy: [liqsonar.com/privacy](https://liqsonar.com/privacy)
- Terms: [liqsonar.com/terms](https://liqsonar.com/terms)
- Contact: hello@liqsonar.com
