# steam-trends-mcp

[![Steam Trends](https://img.shields.io/badge/Steam%20Trends-1B2838?style=flat-square)](https://trendsmcp.ai/steam-trends)
[![MCP](https://img.shields.io/badge/MCP-compatible-blue?style=flat-square)](https://modelcontextprotocol.io)
[![Works with Claude](https://img.shields.io/badge/Claude-supported-orange?style=flat-square)](https://trendsmcp.ai/mcp-server-for-claude)
[![Works with Cursor](https://img.shields.io/badge/Cursor-supported-purple?style=flat-square)](https://trendsmcp.ai/mcp-server-for-cursor)

> **Steam player trend data for AI assistants**
> Track concurrent player counts and game momentum for any title on Steam. Player trend data reveals which games are growing, which are declining, and when major launches or updates are driving spikes.

**Full docs and live demo:** [https://trendsmcp.ai/steam-trends](https://trendsmcp.ai/steam-trends)

Part of **[Trends MCP](https://trendsmcp.ai)** -- the MCP server for live trend data across 12+ sources.
See the main repo: [https://github.com/trendsmcp/trends-mcp](https://github.com/trendsmcp/trends-mcp)

---

## Get started in 2 steps

**Step 1:** Get your free API key at **[trendsmcp.ai](https://trendsmcp.ai)**
100 requests/day, no credit card required.

**Step 2:** Add to your AI client (replace `YOUR_API_KEY`):

[**+ Add to Cursor (one click)**](cursor://anysphere.cursor-deeplink/mcp/install?name=trends-mcp&config=eyJ1cmwiOiAiaHR0cHM6Ly9hcGkudHJlbmRzbWNwLmFpL21jcCIsICJ0cmFuc3BvcnQiOiAiaHR0cCJ9)

**Cursor / Windsurf / Cline** &nbsp; (`~/.cursor/mcp.json` or equivalent)
```json
{
  "mcpServers": {
    "trends-mcp": {
      "url": "https://api.trendsmcp.ai/mcp",
      "transport": "http",
      "headers": { "Authorization": "Bearer YOUR_API_KEY" }
    }
  }
}
```

**VS Code / GitHub Copilot** &nbsp; (`.vscode/mcp.json`)
```json
{
  "servers": {
    "trends-mcp": {
      "type": "http",
      "url": "https://api.trendsmcp.ai/mcp",
      "headers": { "Authorization": "Bearer YOUR_API_KEY" }
    }
  }
}
```

**Claude Desktop** &nbsp; (`claude_desktop_config.json`)
```json
{
  "mcpServers": {
    "trends-mcp": {
      "url": "https://api.trendsmcp.ai/mcp",
      "transport": "http",
      "headers": { "Authorization": "Bearer YOUR_API_KEY" }
    }
  }
}
```

**Claude.ai** (browser) &nbsp; Settings -> Connectors -> Add custom connector:
```
https://api.trendsmcp.ai/mcp
```

---

## Example query

After connecting, ask your AI:
```
get_trends(keyword='Counter-Strike 2', source='steam', data_mode='weekly')
```

---

## Available tools

| Tool | What it does |
|------|-------------|
| `get_trends` | Time-series for a keyword on this source |
| `get_growth` | Growth % over 1W, 1M, 3M, 6M, 1Y periods |
| `get_top_trends` | What is trending right now on this source |
| `get_ranked_trends` | Top topics ranked by volume |

---

## FAQ

### What Steam data does Trends MCP return?

Normalized concurrent player count trends (0-100 scale) for any game on Steam. Returns weekly time series, growth rates, and peak player data. Useful for tracking game momentum before and after launches, updates, or sales events.

### How do I identify a game for the query?

Use the game's display name as it appears on Steam -- for example 'Counter-Strike 2', 'Palworld', or 'Elden Ring'. The MCP server resolves the name to the correct Steam App ID automatically.

### What is a concurrent player count?

The number of players actively in-game at the same time, tracked by Steam. Peak concurrent players (PCU) is a standard metric for measuring a game's popularity and live engagement level.

### How is this useful for investment or market research?

Game studios, investors, and analysts use Steam player trends to gauge a title's commercial momentum, identify breakout games early, and track how a game retains players over time.

### How far back does the data go?

Up to 5 years of weekly data, giving you full launch history, seasonal cycles, and long-term retention trends for any game on Steam.

---

## All data sources

Trends MCP covers 12+ sources in one connection:
Google Search, YouTube, TikTok, Reddit, Amazon, Wikipedia,
News Sentiment, Web Traffic, App Downloads, Steam, npm, and more.

Browse all: [https://trendsmcp.ai/data-sources](https://trendsmcp.ai/data-sources)


---

## Also works as a Python client

Same API key works directly in Python — no MCP host needed.

```bash
pip install steam-trends-mcp
```

```python
import os
from steam_trends_mcp import TrendsMcpClient, SOURCE

client = TrendsMcpClient(api_key=os.environ["TRENDSMCP_API_KEY"])

series  = client.get_trends(source=SOURCE, keyword="your keyword")
growth  = client.get_growth(source=SOURCE, keyword="your keyword", percent_growth=["1M", "3M", "12M"])
top     = client.get_top_trends(type="Steam", limit=10)
```

Full Python docs: [trendsmcp.ai/docs](https://trendsmcp.ai/docs)
---

## License

MIT &copy; [Trends MCP](https://trendsmcp.ai)