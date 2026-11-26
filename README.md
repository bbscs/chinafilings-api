# ChinaFilings API & MCP Server (CNINFO)

**The China Equivalent of SEC EDGAR** — Real-time official **CNINFO** China A-share corporate filings (SSE / SZSE / BSE), classified into actionable trading events with **AI English investor impact takeaways, sentiment scores (`-1.0` to `+1.0`), direct PDF links**, and native **HTTPS Model Context Protocol (MCP)** support.

- **Live HTTPS Demo & Portal**: https://filings.cnpulse.cn
- **RapidAPI Marketplace**: https://rapidapi.com/liyangxiao/api/chinafilings-china-a-share-filings-event-signals
- **Interactive OpenAPI Docs**: https://filings.cnpulse.cn/docs

## Key Features

- **Direct CNINFO Official Disclosures** (refreshed every 10 minutes from Shanghai infrastructure, zero scraping fragility)
- **8 Actionable Event Categories**: `earnings`, `buyback`, `insider` (buy/sell/pledge), `ma` (M&A/related-party), `dividend`, `regulatory` (inquiries/penalties), `contract`, `general`
- **AI Institutional Enrichment**: English headline (`title_en`), 1-sentence investor impact takeaway (`impact_en`), sentiment (`bullish`/`neutral`/`bearish`) + score (`-1.0` to `+1.0`)
- **Annual Report Supply-Chain Extraction**: Top-5 customer & supplier concentration, disclosed entity names, related-party share, and exact CNINFO PDF page citations
- **Dual Protocol**:
  - REST JSON / low-token Markdown (`/v1/filings`, `/v1/events`, `/v1/company/{symbol}`, `/v1/search`, `/v1/supply-chain/{symbol}`)
  - Native **HTTPS Streamable HTTP MCP Server** (`POST /mcp`) with 5 tools: `get_cn_filings`, `get_company_filings`, `get_event_signals`, `search_cn_filings`, `get_supply_chain`

## Quick Start (HTTPS MCP Server)

Add this directly to **Cursor**, **Claude Desktop**, or any MCP client using the public demo key (`150 req/day`):

```json
{
  "mcpServers": {
    "chinafilings": {
      "url": "https://filings.cnpulse.cn/mcp",
      "headers": {
        "X-API-Key": "cf_demo_public_readonly"
      }
    }
  }
}
```

## Quick Start (REST API)

```bash
curl -H "X-API-Key: cf_demo_public_readonly" \
  "https://filings.cnpulse.cn/v1/events?lang=en&limit=5"

curl -H "X-API-Key: cf_demo_public_readonly" "https://filings.cnpulse.cn/v1/supply-chain/300750"
```

## MCP Tools

| Tool | Description |
| :--- | :--- |
| `get_cn_filings` | Retrieve latest real-time China A-share corporate filings from CNINFO (SSE / SZSE / BSE) |
| `get_company_filings` | Retrieve official CNINFO filings and AI English enrichment for a specific A-share company symbol |
| `get_event_signals` | Query classified actionable event signals (`earnings`, `buyback`, `insider`, `ma`, `dividend`, `regulatory`, `contract`, `general`) with sentiment scores |
| `search_cn_filings` | Full-text search across China A-share CNINFO corporate filings |
| `get_supply_chain` | Extract Top-5 Customer & Top-5 Supplier concentration numbers, disclosed entity names (when non-anonymized), related-party share, and exact CNINFO PDF page citations directly from a China A-share company's official annual report (`symbol`, optional `year`) |

## REST API Endpoints

| Endpoint | Description |
| :--- | :--- |
| `GET /v1/filings` | List latest official CNINFO A-share corporate filings with AI English enrichment and direct PDF links |
| `GET /v1/events` | Filter actionable trading event signals across 8 categories with sentiment scores (`-1.0` to `+1.0`) |
| `GET /v1/company/{symbol}` | Retrieve filings and event signals for a specific China A-share stock symbol |
| `GET /v1/search` | Search A-share corporate filings by keyword |
| `GET /v1/supply-chain/{symbol}` | Extract Top-5 Customer & Top-5 Supplier concentration numbers, disclosed entity names, related-party share, and exact CNINFO PDF page citations from official annual reports. Optional query params: `year` (e.g. `2025`) and `format=json\|markdown` |
