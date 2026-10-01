# Stock Research Tool

An AI-powered stock research tool that provides instant, comprehensive analysis of any publicly traded company using real-time market data and large language models.

---

## What It Does

Enter any stock ticker and get:

- **Company Overview** — What the company does and how it makes money
- **Financial Health Assessment** — Revenue, margins, earnings analysis
- **Valuation Analysis** — Is the stock cheap or expensive relative to its fundamentals and 52-week range
- **Key Risks** — Main risks an investor should consider
- **Investment Verdict** — Plain English summary for retail investors
- **Q&A** — Ask any follow-up question about the stock in natural language

---

## How It Works

```
User enters ticker (e.g. AAPL, TSLA, NVDA)
        ↓
yfinance fetches real-time market data
(price, P/E, EPS, revenue, margins, 52-week range, sector)
        ↓
Claude LLM generates structured 5-section analysis
        ↓
User asks follow-up questions in natural language
        ↓
LLM answers using the fetched data and prior analysis as context
```

---

## Tech Stack

| Component | Technology |
|-----------|------------|
| Market Data | yfinance (real-time, free) |
| LLM | Anthropic Claude (Haiku) |
| Embeddings | HuggingFace sentence-transformers (all-MiniLM-L6-v2) |
| Vector Store | FAISS |
| Orchestration | LangChain |
| Frontend | Gradio |

---

## Example Output — AAPL

**Input:** `AAPL`

**Fetched Data (live from yfinance):**
- Current Price: $330.32
- 52-Week Range: $243.42 — $345.34
- Market Cap: $4.82T
- P/E Ratio: 37.84
- EPS: $8.73
- Revenue: $466.8B
- Profit Margin: 27.6%
- Sector: Technology

**AI-Generated Analysis:**

> **COMPANY OVERVIEW**
> Apple Inc. designs and manufactures premium consumer electronics including iPhones, MacBooks, iPads, and wearables, alongside a growing services ecosystem including the App Store, Apple Music, and iCloud.
>
> **FINANCIAL HEALTH**
> Excellent. $4.8T market cap, $467B annual revenue, and a 27.6% profit margin — Apple converts over a quarter of every sales dollar into profit, reflecting fortress-like fundamentals.
>
> **VALUATION**
> Premium. P/E of 37.84 vs. market average of ~20. Trading near its 52-week high at $330, suggesting limited near-term upside from current levels.
>
> **KEY RISKS**
> High valuation leaves little room for earnings misses. Mature smartphone market limits hardware growth. Significant China manufacturing and revenue exposure. Regulatory scrutiny on App Store practices.
>
> **VERDICT**
> World-class company at a world-class price. Strong fundamentals, but consider waiting for a pullback toward $290-300 for a better entry point unless you have a 5+ year horizon.

**Follow-up Q&A:**

> **Q:** Should I buy this stock today?
> **A:** Not the ideal entry point. The stock is near its 52-week high with a P/E of 37.84 — you're paying a premium with limited upside. Consider waiting for a 5-10% pullback or dollar-cost averaging if you're a long-term holder. Apple's business quality is not in question; the issue is current price, not fundamentals.

---

## Features

- Works with any US-listed ticker on NYSE or NASDAQ
- Real-time data fetched live on every query — no stale cache
- Structured 5-section analysis: overview, health, valuation, risks, verdict
- Natural language Q&A grounded in actual fetched data
- Clean Gradio interface — no setup required for end users
- No account or login required to use

---

## Architecture

**Data Layer**
yfinance pulls live fundamentals and price data for any ticker entered — current price, 52-week range, P/E, EPS, revenue, profit margins, sector, and business description.

**Analysis Layer**
The fetched data is passed to Claude via a structured prompt engineered to produce consistent, investor-readable output across five sections. Prompt design ensures the model grounds its analysis in the actual numbers rather than general knowledge.

**Q&A Layer**
The generated analysis is chunked, embedded using sentence-transformers, and indexed in a FAISS vector store. Follow-up questions retrieve the most semantically relevant context chunks before Claude generates a response — keeping answers grounded in the specific stock's data rather than hallucinated generalities.

**Interface Layer**
Gradio provides a clean two-panel UI: ticker input and analysis output on top, follow-up Q&A below. Designed to deploy to Hugging Face Spaces with environment-variable API key injection.

---

## Limitations

- US-listed stocks only (NYSE, NASDAQ)
- Fundamental data sourced from yfinance — some metrics may reflect last reported quarter, not real-time earnings
- Analysis is based on quantitative data only — does not incorporate recent news, earnings call sentiment, or qualitative developments
- Not financial advice — for research and educational purposes only

---

## Author

**Karthik Velavarthypathi**

[LinkedIn](https://www.linkedin.com/in/karthikvhs) | [Medium](https://medium.com/@hsaikarthikv) | [GitHub](https://github.com/saikarthik0809)
