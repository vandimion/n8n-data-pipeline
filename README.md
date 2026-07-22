# Basic n8n Data Pipeline (MySQL)

A simple ETL workflow built in n8n. Fetches crypto price data from a public API every 6 hours, transforms it, and loads it into MySQL.

## Prerequisites
- Docker
- n8n running on port 5678
- MySQL running and reachable from n8n

## Setup
1. Install Docker.
2. Clone this repo and run: **docker-compose up -d**
This starts both MySQL and n8n on a shared network, no manual Docker commands needed.
3. Open n8n at http://localhost:5678 and create your local account.
4. Import `workflows/crypto-prices-etl-mysql.json` (paste the JSON directly onto the canvas, Ctrl+V).
5. n8n strips credentials on export for security, so you'll need to create one MySQL credential in n8n:
   - Host: `mysql` (the service name in docker-compose.yml)
   - Database: `crypto_data`
   - User: `root`
   - Password: `yourpassword` (change this in docker-compose.yml before running, ideally)
   - Port: `3306`
6. Apply that credential to both MySQL nodes in the workflow.
7. Click "Execute Workflow" to test, then publish/activate it to run automatically every 6 hours.

## Pipeline Steps
- **Extract**: HTTP Request to CoinGecko API
- **Transform**: Code node cleans and reshapes data, filters out malformed entries
- **Load**: Ensures the `crypto_prices` table exists, then inserts new rows into MySQL