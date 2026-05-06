# 🕸️ Autonomous Web3 Scraper API for AI Agents

Welcome to the **Web3 Scraper API** — a headless, subscription-free web scraping tool designed exclusively for Autonomous AI Agents and the Machine Economy.

Traditional web scraping APIs (like Scrapfly or BrightData) require human intervention: signing up, managing API keys, and paying $50/month credit card subscriptions. **AI agents can't do that.**

This API uses the **HTTP 402 (Payment Required) standard** built on Solana Pay. Your AI agent pays exactly **0.0005 USDC** per scrape directly from its crypto wallet. No subscriptions. No API keys. No human required.

## 🚀 Features
* **Perfect CAPTCHA Bypass:** Extracts clean HTML/Markdown from any website.
* **Pay-per-Request:** Costs exactly `0.0005 USDC` per scrape.
* **Agent Native:** Uses the `x402` protocol. Built for LangChain, AutoGPT, and MCP.
* **Instant Settlement:** Powered by the Solana blockchain.

## 🔌 API Details
* **Base URL:** `https://ai-scraper-api-4dkl.onrender.com`
* **Network:** Solana Mainnet
* **Accepted Token:** USDC (`EPjFWdd5AufqSSqeM2qN1xzybapC8G4wEGGkZwyTDt1v`)

---

## 🛠️ How it Works (The HTTP 402 Protocol)

This API uses a Challenge-Response payment flow.

### 1. The Agent Requests Data
The agent sends a `POST` request with the target URL.
```bash
curl -X POST https://ai-scraper-api-4dkl.onrender.com/scrape \
-H "Content-Type: application/json" \
-d '{"targetUrl": "https://quotes.toscrape.com"}'
