# 🕸️ Autonomous Web3 Scraper API for AI Agents

A headless, subscription-free web scraping API built exclusively for Autonomous AI Agents and the Machine Economy.

Traditional scraping APIs (Scrapfly, BrightData) require human sign-ups, API keys, and $50/month plans. **AI agents can't do that.**

This API uses the **HTTP 402 Payment Required** standard with the **x402 protocol** on Solana. Your agent pays exactly **0.005 USDC** per scrape directly from its crypto wallet — no accounts, no keys, no humans.

✅ No subscriptions  
✅ No API keys  
✅ No human required  
✅ Always-on — hosted on AWS EC2 (no cold starts)  
✅ x402 protocol — works with `pay` CLI and any x402-compatible agent  

---

## 🔌 API Details

| Field | Value |
|---|---|
| Base URL | `https://ai-scraper-api.duckdns.org` |
| OpenAPI Spec | `https://ai-scraper-api.duckdns.org/openapi.json` |
| Protocol | x402 (HTTP 402 + Solana on-chain payment) |
| Network | Solana Mainnet |
| Token | USDC |
| USDC Mint | `EPjFWdd5AufqSSqeM2qN1xzybapC8G4wEGGkZwyTDt1v` |
| Price | `0.005 USDC` per scrape |
| Infrastructure | AWS EC2 t3.micro — always-on, no cold starts |

---

## 🚀 Features

- **CAPTCHA Bypass:** Extracts clean HTML or Markdown from any website
- **Pay-per-Request:** Costs exactly `0.005 USDC` per scrape
- **Agent Native:** Implements the `x402` protocol (LangChain, AutoGPT, MCP ready)
- **Instant Settlement:** Powered by the Solana blockchain
- **Replay Protection:** Each payment signature can only be used once ✅ Verified
- **Time-bound Payments:** Transactions must be made within the last 5 minutes
- **Float-safe Verification:** Payment amounts checked in raw USDC integer units

---

## ⚡ Quickstart — Using the `pay` CLI (Recommended)

The [Solana Foundation `pay` CLI](https://github.com/solana-foundation/pay) handles the 402 challenge, payment, and retry automatically in one command.

```bash
npm install -g @solana/pay
pay curl -X POST https://ai-scraper-api.duckdns.org/scrape \
  -H "Content-Type: application/json" \
  -d '{"targetUrl": "https://example.com"}'
```

---

## 🔄 How It Works (Manual Flow)

### 1️⃣ Agent Makes a Request

```bash
curl -X POST https://ai-scraper-api.duckdns.org/scrape \
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

### 3️⃣ Agent Pays and Retries

Send `0.005 USDC` to the recipient wallet on Solana, then retry with the transaction signature in the `Payment-Payload` header:

```bash
curl -X POST https://ai-scraper-api.duckdns.org/scrape \
  -H "Content-Type: application/json" \
  -H "Payment-Payload: YOUR_SOLANA_TRANSACTION_SIGNATURE" \
  -d '{"targetUrl": "https://quotes.toscrape.com"}'
```

> **Note:** The legacy `x-payment-signature` header is also accepted for backward compatibility.

### 4️⃣ Data Delivered 📦

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
| Double-spend | Each signature tracked — can never be reused ✅ Verified on mainnet |
| Time expiry | Transactions older than 5 minutes are rejected |
| Exact amount | Raw USDC integer units checked — underpayment rejected |
| Recipient check | Only transfers to the API wallet are accepted |

> **Mainnet verified:** Reusing a valid signature returns `"This payment receipt has already been used."` A fake signature returns `"Scraping failed or invalid transaction."`

---

## 🤖 Compatible Agent Frameworks

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
| Replay protection | ✅ Verified |
| Time-bound | ✅ 5-minute window |
| Uptime | ✅ Always-on (AWS EC2, no cold starts) |

---

## 📬 Get Started

```bash
npm install -g @solana/pay
pay curl -X POST https://ai-scraper-api.duckdns.org/scrape \
  -H "Content-Type: application/json" \
  -d '{"targetUrl": "https://example.com"}'
```

Your agent already knows what to do.
