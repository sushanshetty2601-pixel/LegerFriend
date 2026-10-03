# LedgerFriend 📚✨
### *A Private, Local AI Financial Bookkeeper Built for a Small Business Friend*

> **Weekend Hackathon Theme:** *Build for a Friend*  
> **Core Innovation:** Dual-Core Deterministic Accounting Engine powered by Local Open-Source AI (Ollama + Qwen 2.5 / Gemma 2) with 100% offline data sovereignty and zero mathematical hallucination risk.

---

## 🔗 Live Demo Links

| Access Method | Link / Path | Note |
|---|---|---|
| **📱 Public Demo (Phones & Any Device)** | **[https://a1553164a0942b.lhr.life](https://a1553164a0942b.lhr.life)** | **Live public HTTPS link** (Works anywhere on mobile/PC!) |
| **🌐 Local Web Demo** | **[http://localhost:8080](http://localhost:8080)** | On your current laptop (port 8080) |

> ⚡ **Quick Test Tip:** Open on any phone or laptop, tap **"⚡ Load Demo Shop"** in the top header to instantly populate a month of realistic business transactions, then view the **3 Final Accounts (Trading, P&L, Balance Sheet)** and run the **AI Accuracy Benchmark**!

---

## 🌟 The Story: Who Was This Built For?

Meet **Anita Sharma**, who runs *Anita's Stationery & Xerox*, a small neighborhood shop. Like millions of sole proprietors:
- She knows how to sell goods, but dreads formal bookkeeping terminology (*"Dr. Real Account, Cr. Nominal Account..."*).
- She cannot afford ₹15,000–₹25,000/year subscription fees for complex enterprise software like Tally Prime or QuickBooks.
- She has fierce concerns about privacy: She **never** wants her daily cash balance, bank transactions, and customer credit books uploaded to cloud servers owned by tech conglomerates.
- She visits a Chartered Accountant (CA) once a year with shoeboxes of crumpled receipts, stressed about whether her accounts will balance.

**LedgerFriend was built for Anita.** It gives her a friendly, private companion on her laptop that lets her speak or type in natural language (*"Ramesh ko ₹5,000 ka maal udhaar becha"* or *"Paid shop rent ₹12,000 via bank transfer"*), translates it into double-entry accounting, and generates the **3 Final Accounts (Trading Account, Profit & Loss Account, and Balance Sheet)** ready to hand to her CA.

---

## 🛡️ The AI Dilemma: *"AI Makes Mistakes — What Should We Do?"*

Large Language Models (LLMs) are notorious for arithmetic hallucinations and unpredictability. If an AI hallucinates ₹500 as ₹5,000 or invents an account, a business's tax filing and balance sheet are ruined.

### The Solution: The Dual-Core Safety Architecture

LedgerFriend enforces a strict separation of concerns:

```
[ Natural Language / Voice Note ]
               │
               ▼
┌───────────────────────────────┐
│     LOCAL OPEN-SOURCE AI      │  <-- Classifies Intent & Extracts Entities ONLY
│  (Ollama: Qwen 2.5 / Gemma 2) │      (Date, Amount, Party, Transaction Type)
│     ZERO ARITHMETIC TRUST     │      *Never does math. Never touches debits/credits directly.*
└──────────────┬────────────────┘
               │ Structured Proposal
               ▼
┌───────────────────────────────┐
│ HUMAN-IN-THE-LOOP CONFIRMATION│  <-- Translates into plain, human English:
│   "Anita, Ramesh owes you     │      "Cash doesn't change. Ramesh owes ₹5,000.
│    ₹5,000. Is this right?"    │       Sales increases by ₹5,000. Correct?"
└──────────────┬────────────────┘
               │ Confirmed
               ▼
┌───────────────────────────────┐
│ DETERMINISTIC DOUBLE-ENTRY    │  <-- Fixed Accounting Rules (Integer-paise arithmetic)
│         CORE ENGINE           │      • Debit ALWAYS equals Credit
│                               │      • Bank overdrafts classify as Current Liabilities
└──────────────┬────────────────┘      • Immutable reversals (No silent overwrites)
               │
   ┌───────────┴───────────┐
   ▼                       ▼
[ General Ledger & TB ]  [ 3 Final Accounts: Trading, P&L, Balance Sheet ]
```

1. **AI Never Does Arithmetic:** The AI extracts the facts (Party, Amount, Transaction Type). The accounting engine uses integer paise (₹1 = 100 paise) in strict double-entry code where Debits $\equiv$ Credits is an invariant.
2. **Human-in-the-Loop Verification:** Before posting, the owner sees a plain-language summary explaining the economic reality of the transaction.
3. **The 3 Types of Suspense Accounts (Zero Guesswork):**
   When an entry is ambiguous, LedgerFriend **never guesses**. It quarantines it into one of three standard accounting suspense categories:
   - **Type 1: Unidentified Receipts / Payments** (Mystery UPI credits without bill or party info).
   - **Type 2: Trial Balance Balancing Differences** (Clerical discrepancies held until CA reconciliation).
   - **Type 3: Banking & Dishonour Suspense** (Cheques deposited in clearing, bounced cheques, overdraft disputes).
4. **Immutable Audit Trail:** Entries are never deleted or silently modified. If a correction is needed, a complete double-entry **Reversal Entry** is generated so the CA has an untampered audit trail.
5. **Sole Proprietorship Scope Check:** Explicitly restricts scope to single-owner businesses. Rejects Partnerships, LLPs, and Companies that require corporate statutory filings and share capital allocation.

---

## 🚀 Key Features

- 🎙️ **Voice Entry (Web Speech API):** Speak naturally in Hindi, English, or Hinglish: *"5000 ka maal Ramesh ko udhaar becha"*.
- 🤖 **Dual-Mode AI Engine:**
  - **Local Ollama Integration:** Connects to `http://127.0.0.1:11434` running local open-source models (`qwen2.5:7b`, `gemma2:2b`, `llama3.2:3b`).
  - **Zero-Cloud In-Browser Heuristic Fallback:** If Ollama is not yet running, a built-in offline accounting rule engine ensures the user and judges can test transactions immediately without setup friction.
- 📒 **General Journal:** Complete double-entry original records with ledger folio, debits, credits, and 1-click reversals.
- 📑 **General Ledger:** Interactive T-accounts with real-time running balances and Dr/Cr closing indicators.
- ⚖️ **Trial Balance:** Live columnar equilibrium verification.
- 📈 **The 3 Final Accounts:**
  1. **Trading Account:** Calculates Cost of Goods Sold (COGS) and **Gross Profit / Loss**.
  2. **Profit & Loss Account:** Factors operating expenses, depreciation, bank charges, and calculates **Net Profit / Loss**.
  3. **Balance Sheet:** Proper classification of Fixed Assets (less Accumulated Depreciation), Current Assets (Inventory, Debtors, Bank, Cash), Liabilities (Creditors, Bank Loan, **Bank Overdraft**), and Capital (Initial Capital + Net Profit - Drawings). Balanced verification badge!
- 📉 **Depreciation Calculator:** Straight Line Method (SLM) & Written Down Value (WDV) calculator for shop equipment and furniture.
- 🧪 **Live Textbook Benchmark Suite:** Evaluates 15 diverse textbook accounting problems on-the-fly and prints a verifiable Accuracy & Safety Scorecard for hackathon judges!
- 📑 **CA Audit Export:** 1-Click CSV export for Journal and printable CA Audit Dossier.

---

## ⚡ Quick Start

### 1. Launch the Web Application
Open the live demo:
👉 **[http://localhost:8080](http://localhost:8080)**

Or start a local Python server if launching manually:
```bash
python -m http.server 8080
```

### 2. Connect Local Open-Source AI (Optional, Recommended)
1. Install [Ollama](https://ollama.com/).
2. Pull and run your favorite open model:
   ```bash
   ollama run qwen2.5:7b
   # or
   ollama run gemma2:2b
   ```
3. Open LedgerFriend, go to **Setup & CA Export**, and click **Test Ollama Connection**.

*(Note: Even if Ollama is not running, LedgerFriend's built-in offline rules parser automatically handles your input, so you can test immediately!)*

### 3. Test With 1 Click
Click **"⚡ Load Demo Shop"** in the top navigation bar to instantly populate Anita's Stationery with a month of realistic transactions (sales, purchases, rent, loan, depreciation, drawings, closing stock).

### 4. Run the Judge Benchmark
Go to **AI Benchmark** and click **"▶ Run 15-Transaction Benchmark"** to see live accuracy scores against textbook accounting cases.

---

## 💡 Why Open Innovation Matters Here

| Requirement | Why Closed SaaS / Cloud LLMs Fail | Why LedgerFriend & Open AI Succeed |
|---|---|---|
| **Confidentiality & Privacy** | Small businesses must not upload daily cash, debts, and profit margins to proprietary servers. | **100% on-device.** Financial data lives strictly in local browser storage and local Ollama inference. |
| **Offline Reliability** | Small shops in semi-urban India often face intermittent internet. | Works completely offline on a laptop with zero internet access. |
| **Operating Cost** | Cloud LLM APIs charge per token and SaaS tools charge monthly fees. | **₹0 forever.** Open-weight models run locally with no recurring costs. |
| **Model Customizability** | Closed models change behavior without warning, breaking structured schemas. | Open models (Qwen, Gemma, Llama) can be version-locked, quantized (4-bit), or fine-tuned for regional accounting terms. |

---

## 👥 Built with Care
Built for friends running small businesses who deserve the power of modern AI without sacrificing their privacy, their financial accuracy, or their peace of mind.
