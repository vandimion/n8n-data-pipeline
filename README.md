# Basic n8n Data Pipeline (MySQL)

A simple ETL workflow built in n8n. Fetches crypto price data from a public API every 6 hours, transforms it, and loads it into MySQL.

## Prerequisites
- Docker
- n8n running on port 5678
- MySQL running and reachable from n8n

## Setup
1. Import `workflows/crypto-prices-etl-mysql.json` into n8n.
2. Create a MySQL credential in n8n (Credentials → New → MySQL) with your DB connection details.
3. Assign that credential to both MySQL nodes in the workflow.
4. Run once manually to confirm it works, then activate/publish the workflow.

## Pipeline Steps
- **Extract**: HTTP Request to CoinGecko API
- **Transform**: Code node cleans and reshapes data, filters out malformed entries
- **Load**: Ensures the `crypto_prices` table exists, then inserts new rows into MySQL