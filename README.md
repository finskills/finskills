# Finskills — Real-time Financial Data Skill

> An AI skill that gives Claude and other assistants real-time access to stock quotes, cryptocurrency prices, forex rates, macroeconomic indicators, analyst ratings, insider trades, financial news, and SEC filings.

[![Anthropic Skills](https://img.shields.io/badge/Anthropic-Skills-blueviolet)](https://github.com/anthropics/skills)
[![License: Apache-2.0](https://img.shields.io/badge/License-Apache_2.0-blue.svg)](LICENSE)

## Why Finskills?

| Feature | Description |
|---------|-------------|
| **Real-time Data** | Live market quotes, not static training data |
| **7 Data Categories** | Stocks · Crypto · Forex · Macro · News · Filings · Sentiment |
| **Free Tier** | Most endpoints work with any valid API key at no cost |
| **Standard Format** | Follows [Anthropic SKILL.md](https://github.com/anthropics/skills) specification |

## Quick Start

### 1. Get an API Key

Register at [finskills.net/register](https://finskills.net/register) — free tier available.

### 2. Install the Skill

Choose one of the methods below:

#### Claude Code (npx)

```bash
npx skills add yushuyang/finskills
```

#### Claude.ai (Project Knowledge)

1. Open [claude.ai](https://claude.ai) → select or create a Project
2. Go to **Project Knowledge** → click **Add content**
3. Download [`SKILL.md`](skills/finskills/SKILL.md) and upload it as project knowledge

#### Cursor

```bash
# Download into Cursor rules directory
mkdir -p .cursor/rules
curl -o .cursor/rules/finskills.mdc https://finskills.net/SKILL.md
```

#### VS Code Copilot

```bash
# Add to project-level Copilot instructions
mkdir -p .github
curl -o .github/copilot-instructions.md https://finskills.net/SKILL.md
```

#### Manual Download

```bash
curl -O https://finskills.net/SKILL.md
```

### 3. Set Your API Key

When prompted, provide your API key. It will be sent as the `X-API-Key` header on all requests.

### 4. Start Querying

Ask natural language questions — no special commands needed.

## Example Prompts

| You ask | Endpoints called |
|---------|-----------------|
| "What's Apple's stock price and analyst consensus?" | `/v1/stocks/quote/AAPL` + `/v1/free/stocks/analyst-rating-summary/AAPL` |
| "Compare Bitcoin and Ethereum over the last 30 days" | `/v1/free/crypto/history/bitcoin?days=30` + `/v1/free/crypto/history/ethereum?days=30` |
| "What's the USD/EUR exchange rate trend this year?" | `/v1/free/forex/history?base=USD&target=EUR` |
| "Show US GDP growth and inflation for the last 5 years" | `/v1/free/macro/gdp?country=US` + `/v1/free/macro/inflation?country=US` |
| "Find Tesla's latest 10-K SEC filing" | `/v1/free/sec/filings/0001318605` |
| "Are any Congress members trading NVIDIA?" | `/v1/free/stocks/congress-trades?symbol=NVDA` |
| "Show me sector performance and market movers today" | `/v1/market/summary` + `/v1/market/sectors` |
| "Are Tesla insiders buying or selling?" | `/v1/free/stocks/insider-trades/TSLA` |

## Supported Data Categories

- **Stocks** — Real-time quotes, historical OHLCV, company profiles, financials, dividends, options, earnings, holders
- **Alternative Data** — Analyst ratings, Congress trades, insider transactions, WallStreetBets sentiment
- **Cryptocurrency** — Prices, market rankings, historical data (CoinGecko IDs: bitcoin, ethereum, solana…)
- **Forex** — Live exchange rates, historical rate data
- **Macroeconomics** — GDP, inflation, Treasury yields, FRED economic series, interest rates
- **Market Overview** — Major indices, sector performance, trending tickers
- **News** — Financial headlines, stock-specific news
- **SEC Filings** — 10-K, 10-Q, 8-K filings, XBRL structured data

## How It Works

```
You ask a question
        ↓
SKILL.md tells Claude which endpoint to call
        ↓
Claude sends HTTP request to Finskills API (with X-API-Key header)
        ↓
Finskills returns real-time JSON data
        ↓
Claude formats a contextualized answer
```

## Project Structure

```
finskills/
├── LICENSE
├── README.md
└── skills/
    └── finskills/
        └── SKILL.md          ← The skill definition file
```

## MCP Support

Finskills also supports the **Model Context Protocol (MCP)** for direct tool-based integration:

```
MCP Endpoint: https://finskills.net/mcp
Transport: Streamable HTTP (SSE)
```

See [finskills.net/mcp](https://finskills.net/mcp) for MCP documentation.

## Links

- **Website**: [finskills.net](https://finskills.net)
- **API Docs**: [finskills.net/documentation](https://finskills.net/documentation)
- **Skill Page**: [finskills.net/skill](https://finskills.net/skill)
- **MCP Docs**: [finskills.net/mcp](https://finskills.net/mcp)
- **Register**: [finskills.net/register](https://finskills.net/register)
- **Anthropic Skills Spec**: [github.com/anthropics/skills](https://github.com/anthropics/skills)

## License

[Apache License 2.0](LICENSE)
