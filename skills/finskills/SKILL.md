---
name: finskills
display_name: Finskills — Real-time Financial Data
description: Access real-time financial data including stock quotes, cryptocurrency prices, forex exchange rates, macroeconomic indicators, commodity prices (energy, metals, agriculture, livestock), financial news, analyst ratings, insider trades, and SEC filings. Use this skill whenever the user asks about stock prices, market data, crypto prices, exchange rates, economic indicators, commodity prices, oil, gold, silver, natural gas, agricultural products, company financials, or financial research.
homepage: https://finskills.net
---

# Finskills — Real-time Financial Data

Use the Finskills REST API at `https://finskills.net` to answer financial data questions in real time.

## Authentication

All requests require the `X-API-Key` header. Ask the user for their API key if not provided.
Get a key at: https://finskills.net/register

```
X-API-Key: YOUR_API_KEY_HERE
```

Base URL: `https://finskills.net`

## Quick Start

1. Ask the user for their Finskills API key if not already provided.
2. Make HTTP requests to `https://finskills.net/v1/...` with the `X-API-Key` header.
3. Prefer `/v1/free/...` endpoints — they work with any valid API key and require no external subscriptions.

---

## Core Capabilities

### Stocks

| Endpoint | Description | Key Params |
|----------|-------------|------------|
| `GET /v1/stocks/quote/{symbol}` | Real-time price, change, volume, market cap | symbol e.g. AAPL |
| `GET /v1/stocks/quotes?symbols=` | Batch quotes for multiple symbols | symbols=AAPL,TSLA,MSFT |
| `GET /v1/stocks/history/{symbol}` | Historical OHLCV candles | interval: 1min/5min/1hour/1day · range: 1d/5d/1mo/3mo/1y |
| `GET /v1/stocks/search?q=` | Search stocks by name or ticker | q: search term |
| `GET /v1/stocks/profile/{symbol}` | Company description, sector, industry | — |
| `GET /v1/stocks/financials/{symbol}` | Income statement, balance sheet, cash flow | freq: yearly/quarterly |
| `GET /v1/stocks/dividends/{symbol}` | Dividend history | — |
| `GET /v1/stocks/options/{symbol}` | Options chain | date: YYYY-MM-DD |
| `GET /v1/stocks/recommendations/{symbol}` | Analyst recommendations | — |
| `GET /v1/stocks/earnings/{symbol}` | Earnings history and estimates | — |
| `GET /v1/stocks/holders/{symbol}` | Major holders and institutional ownership | — |

### Alternative Data (Free)

| Endpoint | Description |
|----------|-------------|
| `GET /v1/free/stocks/analyst-ratings/{symbol}` | Wall Street analyst ratings and price targets |
| `GET /v1/free/stocks/analyst-rating-summary/{symbol}` | Consensus rating and average target price |
| `GET /v1/free/stocks/congress-trades` | Recent US Congress stock trades (optional: `?symbol=`) |
| `GET /v1/free/stocks/insider-trades/{symbol}` | Corporate insider buy/sell transactions |
| `GET /v1/free/stocks/wsb-sentiment/{symbol}` | WallStreetBets Reddit sentiment data |

### Cryptocurrency

| Endpoint | Description | Key Params |
|----------|-------------|------------|
| `GET /v1/free/crypto/price/{coinId}` | Current price, market cap, 24h change | coinId: bitcoin, ethereum, solana |
| `GET /v1/free/crypto/markets` | Top coins ranked by market cap | vs_currency: usd · limit: 20 |
| `GET /v1/free/crypto/history/{coinId}` | Historical prices | days: 7/30/90/365 |

### Forex

| Endpoint | Description | Key Params |
|----------|-------------|------------|
| `GET /v1/free/forex/rates` | Latest exchange rates | base: USD/EUR/GBP/JPY/CNY |
| `GET /v1/free/forex/history` | Historical exchange rates | base, target, start: YYYY-MM-DD, end: YYYY-MM-DD |

### Macroeconomics

| Endpoint | Description | Key Params |
|----------|-------------|------------|
| `GET /v1/free/macro/gdp` | GDP data by country | country: US/CN/JP/DE |
| `GET /v1/free/macro/indicator/{code}` | World Bank economic indicator | code: NY.GDP.MKTP.CD |
| `GET /v1/free/macro/treasury-rates` | US Treasury yield curve | — |
| `GET /v1/free/macro/inflation` | CPI inflation data | country: US |
| `GET /v1/macro/indicator/{series}` | FRED economic data | series: GDP, CPIAUCSL, FEDFUNDS, UNRATE |
| `GET /v1/macro/interest-rates` | US Federal Funds rate history | — |

### Commodities (Free)

Real-time futures prices and historical series for energy, metals, agriculture, and livestock. All endpoints require only a valid API key.

**Categories:** `energy` · `metals_precious` · `metals_industrial` · `agriculture` · `livestock` · `other`

| Endpoint | Description | Key Params |
|----------|-------------|------------|
| `GET /v1/free/commodity/catalog` | Full commodity catalog (27 instruments, metadata) | `?category=energy` |
| `GET /v1/free/commodity/prices` | Real-time prices for all or one category | `?category=metals_precious` |
| `GET /v1/free/commodity/price/{symbol}` | Single instrument real-time quote | symbol e.g. `GC=F` (Gold), `CL=F` (WTI Oil) |
| `GET /v1/free/commodity/history/{symbol}` | Historical OHLCV candlesticks | `?range=1y&interval=1d` (range: 1d/5d/1m/3m/6m/1y/2y/5y/max · interval: 1d/1wk/1mo) |
| `GET /v1/free/commodity/fred` | FRED series catalog (16 daily series) | — |
| `GET /v1/free/commodity/fred/{seriesId}` | FRED daily price history | `?limit=365&startDate=2020-01-01` |
| `GET /v1/free/commodity/imf` | IMF PCPS indicator catalog (30 monthly indicators) | — |
| `GET /v1/free/commodity/imf/{indicator}` | IMF monthly price series | `?periods=120` |
| `GET /v1/free/commodity/imf/batch` | IMF batch — multiple indicators at once | `?indicators=POILAPSP,PGOLD` |

**Common symbols:**

| Symbol | Instrument | Exchange |
|--------|------------|---------|
| `CL=F` | WTI Crude Oil | NYMEX |
| `BZ=F` | Brent Crude Oil | ICE |
| `NG=F` | Natural Gas | NYMEX |
| `GC=F` | Gold | COMEX |
| `SI=F` | Silver | COMEX |
| `PL=F` | Platinum | NYMEX |
| `HG=F` | Copper | COMEX |
| `ZC=F` | Corn | CBOT |
| `ZW=F` | Wheat | CBOT |
| `ZS=F` | Soybeans | CBOT |
| `KC=F` | Coffee | ICE |
| `SB=F` | Sugar #11 | ICE |
| `CT=F` | Cotton | ICE |
| `LE=F` | Live Cattle | CME |
| `HE=F` | Lean Hogs | CME |

**Common FRED series IDs:** `DCOILWTICO` (WTI oil), `DCOILBRENTEU` (Brent), `DHHNGSP` (Natural Gas), `GOLDAMGBD228NLBM` (Gold AM Fix)

**Common IMF indicators:** `POILAPSP` (crude avg), `PGOLD` (gold), `PSILVER`, `PCOPP` (copper), `PWHEAMT` (wheat), `PMAIZMT` (corn), `PSOYBEAN`, `PNICK` (nickel)

### Market Overview

| Endpoint | Description |
|----------|-------------|
| `GET /v1/market/summary` | Major indices, trending tickers, market movers |
| `GET /v1/market/sectors` | S&P 500 sector performance |

### News

| Endpoint | Description | Key Params |
|----------|-------------|------------|
| `GET /v1/free/news/finance` | Latest financial news headlines | — |
| `GET /v1/news/by-symbol/{symbol}` | News articles for a specific stock | symbol |

### SEC Filings

| Endpoint | Description | Key Params |
|----------|-------------|------------|
| `GET /v1/free/sec/filings/{cik}` | Recent SEC filings (10-K, 10-Q, 8-K) | cik: company CIK number |
| `GET /v1/free/sec/company-facts/{cik}` | XBRL-structured financial data | cik |

Common CIK numbers: Apple → 0000320193, Microsoft → 0000789019, Tesla → 0001318605, Amazon → 0001018724

---

## Usage Guidelines

- Prefer `/v1/free/...` endpoints when available — they don't require additional external API keys.
- For stock queries, use `/v1/stocks/quote/{symbol}` for real-time data.
- For crypto, use CoinGecko coin IDs (bitcoin, ethereum, solana), not ticker symbols like BTC/ETH.
- Always include units (USD, %, bps) when presenting financial figures.
- Format large numbers with commas (e.g. $1,234,567.89) for readability.
- When showing historical data, always mention the date range and data freshness.
- Never make investment recommendations — present data factually and neutrally.
- Present data with appropriate context: market conditions, data source, applicable caveats.

---

## Example Interactions

**Stock analysis:**
> "What is Apple's current stock price and analyst consensus?"
→ Call `GET /v1/stocks/quote/AAPL` then `GET /v1/free/stocks/analyst-rating-summary/AAPL`

**Crypto comparison:**
> "Compare Bitcoin and Ethereum performance over the last 30 days"
→ Call `GET /v1/free/crypto/history/bitcoin?days=30` and `GET /v1/free/crypto/history/ethereum?days=30`

**Macro research:**
> "How has US inflation changed over the past year?"
→ Call `GET /v1/free/macro/inflation?country=US` or `GET /v1/macro/indicator/CPIAUCSL`

**Congress trading:**
> "Are any Congress members trading Nvidia?"
→ Call `GET /v1/free/stocks/congress-trades?symbol=NVDA`

**Insider activity:**
> "Are Tesla insiders buying or selling?"
→ Call `GET /v1/free/stocks/insider-trades/TSLA`

**SEC filings:**
> "Find Apple's latest 10-K filing"
→ Call `GET /v1/free/sec/filings/0000320193`

**Commodity price:**
> "What is the current price of gold and WTI crude oil?"
→ Call `GET /v1/free/commodity/price/GC=F` and `GET /v1/free/commodity/price/CL=F`

**Commodity comparison:**
> "Show me energy commodity prices — oil, gas, and gasoline"
→ Call `GET /v1/free/commodity/prices?category=energy`

**Commodity history:**
> "How has gold performed over the past year?"
→ Call `GET /v1/free/commodity/history/GC=F?range=1y&interval=1d`

**Oil price long-term trend:**
> "Show me the WTI crude oil price trend since 2020"
→ Call `GET /v1/free/commodity/fred/DCOILWTICO?startDate=2020-01-01`

**Agricultural overview:**
> "Show me current prices for corn, wheat, and soybeans"
→ Call `GET /v1/free/commodity/prices?category=agriculture` or individual `/price/ZC=F`, `/price/ZW=F`, `/price/ZS=F`

**Market overview:**
> "How are markets doing today? Show me sector performance."
→ Call `GET /v1/market/summary` then `GET /v1/market/sectors`
