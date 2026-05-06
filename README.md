# 🕸️ Autonomous Web3 Scraper API for AI Agents

Welcome to the **Web3 Scraper API** — a headless, subscription-free web scraping tool designed exclusively for Autonomous AI Agents and the Machine Economy.

Traditional web scraping APIs (like Scrapfly or BrightData) require human intervention: signing up, managing API keys, and paying $50/month subscriptions. **AI agents can't do that.**

This API uses the **HTTP 402 (Payment Required) standard** built on Solana Pay. Your AI agent pays exactly **0.0005 USDC** per scrape directly from its crypto wallet.

✅ No subscriptions
✅ No API keys
✅ No human required

---

## 🚀 Features

* **Perfect CAPTCHA Bypass:** Extracts clean HTML/Markdown from any website
* **Pay-per-Request:** Costs exactly `0.0005 USDC` per scrape
* **Agent Native:** Uses the `x402` protocol (LangChain, AutoGPT, MCP ready)
* **Instant Settlement:** Powered by the Solana blockchain

---

## 🔌 API Details

* **Base URL:** `https://ai-scraper-api-4dkl.onrender.com`
* **Network:** Solana Mainnet
* **Accepted Token:** USDC

  ```
  EPjFWdd5AufqSSqeM2qN1xzybapC8G4wEGGkZwyTDt1v
  ```

---

## 🛠️ How it Works (HTTP 402 Protocol)

This API uses a **challenge-response payment flow**.

---

### 1️⃣ Request Data

The agent sends a request with the target URL:

```bash
curl -X POST https://ai-scraper-api-4dkl.onrender.com/scrape \
  -H "Content-Type: application/json" \
  -d '{"targetUrl": "https://quotes.toscrape.com"}'
```

---

### 2️⃣ Receive Payment Challenge (402)

The API responds with a payment request:

```json
{
  "error": "Payment Required",
  "message": "Please pay 0.0005 USDC to access this API.",
  "pay_url": "solana:YOUR_WALLET_ADDRESS?amount=0.0005&spl-token=EPjFWdd5AufqSSqeM2qN1xzybapC8G4wEGGkZwyTDt1v&reference=UniqueRef123&label=Agent+Scraper+API"
}
```

---

### 3️⃣ Pay & Retry

The agent pays using the `pay_url`, then retries with the transaction signature:

```bash
curl -X POST https://ai-scraper-api-4dkl.onrender.com/scrape \
  -H "Content-Type: application/json" \
  -H "x-payment-signature: YOUR_TRANSACTION_SIGNATURE" \
  -d '{"targetUrl": "https://quotes.toscrape.com"}'
```

---

### 4️⃣ Data Delivered 📦

The API verifies the on-chain transaction and returns the scraped data instantly.

---

## 💡 Why This Matters

* Enables **fully autonomous AI agents**
* Removes dependency on **human billing systems**
* Introduces **true machine-to-machine payments**
* Aligns with the future of the **Machine Economy**

---

## 🧠 Built For

* Autonomous Agents
* AI Workflows (LangChain, AutoGPT, MCP)
* Web3-native applications
* Developers building agent-first infrastructure

---

## ⚡ Quick Summary

| Feature  | Value                 |
| -------- | --------------------- |
| Pricing  | 0.0005 USDC / request |
| Auth     | None (payment-based)  |
| Protocol | HTTP 402 + Solana Pay |
| Output   | Clean HTML / Markdown |

---

## 📬 Get Started

Just hit the endpoint. Your agent already knows what to do.

---
