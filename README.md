# 🕸️ Autonomous Web3 Scraper API for AI Agents

Welcome to the **Web3 Scraper API** — a headless, subscription-free web scraping tool designed exclusively for Autonomous AI Agents and the Machine Economy.

Traditional web scraping APIs (like Scrapfly or BrightData) require human intervention: signing up, managing API keys, and paying $50/month subscriptions. **AI agents can't do that.**

This API uses the **HTTP 402 (Payment Required)** standard built on the **x402 protocol** with Solana. Your AI agent pays exactly **0.005 USDC** per scrape directly from its crypto wallet — no accounts, no keys, no humans.

✅ No subscriptions  
✅ No API keys  
✅ No human required  
✅ x402 protocol — works with `pay` CLI and any x402-compatible agent  

---

## 🚀 Features

- **CAPTCHA Bypass:** Extracts clean HTML or Markdown from any website
- **Pay-per-Request:** Costs exactly `0.005 USDC` per scrape
- **Agent Native:** Implements the `x402` protocol (LangChain, AutoGPT, MCP ready)
- **Instant Settlement:** Powered by the Solana blockchain
- **Replay Protection:** Each payment signature can only be used once
- **Time-bound Payments:** Transactions must be made within the last 5 minutes

---

## 🔌 API Details

| Field | Value |
|---|---|
| Base URL | `https://ai-scraper-api-4dkl.onrender.com` |
| Protocol | x402 (HTTP 402 + Solana on-chain payment) |
| Network | Solana Mainnet |
| Token | USDC |
| USDC Mint | `EPjFWdd5AufqSSqeM2qN1xzybapC8G4wEGGkZwyTDt1v` |
| Price | `0.005 USDC` per scrape |

---

## ⚡ Quickstart — Using the `pay` CLI (Recommended)

The easiest way to call this API is with the [Solana Foundation `pay` CLI](https://github.com/solana-foundation/pay). It handles the 402 challenge, payment, and retry automatically in one command.

```bash
npm install -g @solana/pay
pay --dev curl -X POST https://ai-scraper-api-4dkl.onrender.com/scrape \
  -H "Content-Type: application/json" \
  -d '{"targetUrl": "https://example.com"}'
```

---

## 🔄 How It Works (Manual Flow)

### 1️⃣ Agent Makes a Request

```bash
curl -X POST https://ai-scraper-api-4dkl.onrender.com/scrape \
  -H "Content-Type: application/json" \
  -d '{"targetUrl": "https://quotes.toscrape.com"}'
```

### 2️⃣ Server Responds with 402

**HTTP/1.1 402 Payment Required**

```
WWW-Authenticate: Payment v=0,a=0.005,t=EPjFWdd5AufqSSqeM2qN1xzybapC8G4wEGGkZwyTDt1v,p=solana,r=<RECIPIENT_WALLET>
```

**Response body:**

```json
{
  "error": "Payment Required",
  "message": "Please pay 0.005 USDC to access this API.",
  "x402": {
    "protocol": "x402",
    "amount": "0.005",
    "token": "EPjFWdd5AufqSSqeM2qN1xzybapC8G4wEGGkZwyTDt1v",
    "network": "solana",
    "recipient": "<RECIPIENT_WALLET>"
  }
}
```

---

### 3️⃣ Agent Pays and Retries

The agent sends `0.005 USDC` to the recipient wallet on Solana, then retries the request with the transaction signature in the `Payment-Payload` header:

```bash
curl -X POST https://ai-scraper-api-4dkl.onrender.com/scrape \
  -H "Content-Type: application/json" \
  -H "Payment-Payload: YOUR_SOLANA_TRANSACTION_SIGNATURE" \
  -d '{"targetUrl": "https://quotes.toscrape.com"}'
```

> **Note:** The legacy `x-payment-signature` header is also accepted for backward compatibility.

---

### 4️⃣ Data Delivered 📦

The API verifies the on-chain transaction and returns the scraped content:

```json
{
  "success": true,
  "data": "<scraped HTML or Markdown content>"
}
```

---

## 🔒 Security

| Protection | Detail |
|---|---|
| Double-spend | Each transaction signature is tracked — can never be reused ✅ Confirmed |
| Time expiry | Transactions older than 5 minutes are rejected |
| Exact amount | Checks raw USDC integer units — underpayment rejected |
| Recipient check | Only transfers to the API wallet are accepted |

> **Replay protection verified:** Reusing a valid signature returns `"This payment receipt has already been used."` Submitting a fake signature returns `"Scraping failed or invalid transaction."` Both tested on mainnet.

---

## 🤖 Compatible Agent Frameworks

Works out-of-the-box with any tool that supports x402:

- [Solana Foundation `pay` CLI](https://github.com/solana-foundation/pay)
- [x402-fetch](https://www.npmjs.com/package/x402-fetch) npm package
- LangChain with x402 integration
- AutoGPT with x402 plugin
- Any MCP-enabled agent with x402 support

---

## ⚡ Quick Summary

| Feature | Value |
|---|---|
| Pricing | `0.005 USDC` per request |
| Auth | None (payment-based) |
| Protocol | x402 (HTTP 402 + Solana) |
| Payment header | `Payment-Payload: <tx_signature>` |
| Output | HTML or Markdown |
| Replay protection | ✅ |
| Time-bound | ✅ 5-minute window |

---

## 📬 Get Started

```bash
npm install -g @solana/pay
pay --dev curl -X POST https://ai-scraper-api-4dkl.onrender.com/scrape \
  -H "Content-Type: application/json" \
  -d '{"targetUrl": "https://example.com"}'
```

Your agent already knows what to do.
