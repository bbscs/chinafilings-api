# ChinaFilings API & MCP Server (CNINFO)

**The China Equivalent of SEC EDGAR** — Real-time official **CNINFO** China A-share corporate filings (SSE / SZSE / BSE), classified into actionable trading events with **AI English investor impact takeaways, sentiment scores (`-1.0` to `+1.0`), direct PDF links**, and native **HTTPS Model Context Protocol (MCP)** support.

- **Live HTTPS Demo & Portal**: https://appropriations-rocky-feels-releases.trycloudflare.com
- **Interactive OpenAPI Docs**: https://appropriations-rocky-feels-releases.trycloudflare.com/docs

## Key Features

- **Direct CNINFO Official Disclosures** (refreshed every 10 minutes from Shanghai infrastructure, zero scraping fragility)
- **8 Actionable Event Categories**: `earnings`, `buyback`, `insider` (buy/sell/pledge), `ma` (M&A/related-party), `dividend`, `regulatory` (inquiries/penalties), `contract`, `general`
- **AI Institutional Enrichment**: English headline (`title_en`), 1-sentence investor impact takeaway (`impact_en`), sentiment (`bullish`/`neutral`/`bearish`) + score (`-1.0` to `+1.0`)
- **Dual Protocol**:
  - REST JSON / low-token Markdown (`/v1/filings`, `/v1/events`, `/v1/company/{symbol}`, `/v1/search`)
  - Native **HTTPS Streamable HTTP MCP Server** (`POST /mcp`) with 4 tools: `get_cn_filings`, `get_company_filings`, `get_event_signals`, `search_cn_filings`

## Quick Start (HTTPS MCP Server)

Add this directly to **Cursor**, **Claude Desktop**, or any MCP client using the public demo key (`150 req/day`):

```json
{
  "mcpServers": {
    "chinafilings": {
      "url": "https://appropriations-rocky-feels-releases.trycloudflare.com/mcp",
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
  "https://appropriations-rocky-feels-releases.trycloudflare.com/v1/events?lang=en&limit=5"
```
