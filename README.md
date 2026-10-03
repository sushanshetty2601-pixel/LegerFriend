# LedgerFriend
### Describe the transaction. Review the entry. Understand your books.

LedgerFriend is an experimental bookkeeping assistant for Indian sole proprietors, built for the **Hacktoberfest 2026 Weekend Challenge: Build for a Friend**.

The idea is simple: a small-business owner should be able to describe a transaction in ordinary language, review the proposed accounting treatment, and generate organised books without manually repeating the same information across multiple reports.

**AI suggests the transaction details. Fixed accounting rules generate the entries. A human approves what gets posted.**

> Prototype only. Not production accounting software, tax advice, or a replacement for a Chartered Accountant.

## 🔗 Shared Demo

[**Demo Link👈**](https://velvety-malasada-97c155.netlify.app/)

This is a shared development demo, not a permanent production deployment. Availability may depend on the development server and tunnel remaining online.

**Please use fictional transactions only. Do not enter bank details, customer information, or confidential financial records.**

The public interface being available does not guarantee that AI inference is available.

In the original browser-to-Ollama architecture, a request to `localhost` refers to the visitor’s own computer—not the developer’s laptop. A public website tunnel alone does not make the developer’s local model available to visitors.

## 👤 Who I’m Building For

The intended user is an Indian sole proprietor who is a Friend, Who finds it difficult to keep everyday transactions organised and translate them into accounting records.

I do not want to invent a user testimonial. The project becomes more useful when its design is based on one real person’s workflow.

## 💡 How the Idea Started

I initially explored student-focused projects such as notes-to-quiz tools and a group-chat-to-task-list assistant.

However, I wanted to build something different and connected to a practical problem: small-business bookkeeping.

My first idea was much larger:

> What if an owner could describe sales, purchases, expenses, and other transactions, and AI could prepare the journal, ledger, trial balance, and final accounts?

That immediately raised the most important question:

**What happens when the AI makes a mistake?**

Instead of trusting the model to perform the entire accounting process, I separated language understanding from accounting logic.

I also narrowed the scope. This version targets **sole proprietorships using INR**, not partnerships, LLPs, companies, or non-profits.

## 🧠 The Design: AI Suggests, Rules Calculate

The transaction flow is:
text

Owner describes one transaction

↓

Local model proposes structured details

↓

Application validates fields and supported types

↓

Owner reviews the proposal

↓

Fixed rules generate a debit/credit preview

↓

Owner explicitly confirms

↓

Journal, ledger, trial balance, and draft reports update

For example:
text

Today, the owner introduced INR 20000 in cash

into the business as capital. No tax applies.

The expected accounting entry is:
text

Debit: Cash ₹20,000

Credit: Owner’s capital ₹20,000

The model does not directly post entries or decide the accounting engine’s arithmetic.

**A balanced entry is not necessarily a correct entry.** The wrong classification can still produce equal debits and credits, so human review remains essential.

## ✨ Prototype Features

### Transaction entry

- Plain-language transaction descriptions.
- Local AI integration through Ollama.
- Manual entry when AI is unavailable.
- A fixed list of supported transaction types.
- Journal preview and explicit confirmation before posting.

### Accounting views

- Journal.
- General ledger.
- Trial balance.
- Draft trading account.
- Draft profit and loss account.
- Draft balance sheet.

### Supported examples

- Cash, bank, and credit sales.
- Purchases of goods for resale.
- Operating expenses.
- Owner’s capital and drawings.
- Bank receipts against existing customer debts.
- Bank payments against existing supplier debts.
- Equipment purchases through bank.
- Bank loan receipts.
- Transfers between cash and bank.
- Manually reviewed depreciation amounts.
- Period-end closing-stock adjustments.

### Review and export

- Unposted “Needs review” queue.
- Reversal entries rather than editing posted entries in place.
- Journal CSV export.
- JSON snapshot export.

A review queue is **not** a suspense account. Unclear transactions should not automatically create accounting entries.

## 🛡️ Safety Measures—and Their Limits

The prototype uses:

- Integer-paise arithmetic rather than floating-point rupee calculations.
- Fixed transaction-to-account rules.
- Date and amount validation.
- Balanced journal-entry checks.
- Certain balance checks, including preventing negative cash.
- Human confirmation before posting.
- Reversal records that retain the original entry.

These measures reduce some error risks. They do not establish complete accounting correctness.

Important limitations:

- AI can still misunderstand the transaction.
- Users can approve incorrect suggestions.
- Rule-based code can contain bugs.
- Aggregate customer/supplier balances do not validate individual party balances.
- Browser storage can be modified or deleted.
- The application does not provide a tamper-proof audit trail.

## 🛠️ How I Built It

I started with a lightweight, single-page application using:

| Component | Role |
|---|---|
| HTML | Application structure and forms |
| CSS | Responsive dashboard and report styling |
| JavaScript | Validation, posting rules, reports, and AI requests |
| Browser localStorage | Prototype data persistence |
| Ollama | Local model serving |
| Qwen2.5 | Open-weight language model for transaction parsing |
| VS Code | Editing and local development |
| Python HTTP server / VS Code Live Server | Serving the interface locally |

I installed and experimented with:

- `qwen2.5:3b`
- `qwen2.5:1.5b`

The smaller model was explored to reduce hardware demands. Smaller size does not guarantee adequate accounting classification accuracy.

### AI-assisted development tools

I used AI assistance to explore the idea, generate and revise code, and troubleshoot integration problems.

Tools used during the development process included:

- **Backboard:**  I used Backboard to create the **initial project structure and HTML foundation** for LedgerFriend. It helped turn the initial concept into the application's page structure, forms, and overall interface layout, which I then developed and refined further.
- **Antigravity:** I used Antigravity during development for implementation and debugging assistance while testing different approaches and working through application issues.
- **ChatGPT and Claude:** ideation, implementation guidance, and debugging assistance.

Development assistance is distinct from the application’s runtime dependencies.

The documented local inference path is Ollama + Qwen. I should only claim a Backboard runtime integration or a partner-category feature if it is present in the submitted implementation.

## 🔓 Why Open Innovation Matters

### Model choice

An open-weight model allows me to experiment with different sizes and compare speed, memory requirements, and classification quality.

I am not designing the application around one proprietary model endpoint.

### Local inference

The local configuration can process transaction descriptions on the user’s own computer rather than sending them to a hosted inference provider.

After the model and required software are downloaded, the local setup can operate without internet access, provided its local services are running.

### Inspectable behaviour

The accounting rules are ordinary application code. They can be inspected, tested, and changed independently of the model.

The model’s output is treated as a proposal—not as an authoritative accounting record.

### Costs and trade-offs

Local inference avoids a hosted provider’s per-request inference charge, but it is not literally cost-free: it requires hardware, storage, electricity, and setup time.

My experience also exposed the trade-off clearly: local deployment gave me control, but Windows networking and model-runner troubleshooting took substantial effort.

## 🐛 What Went Wrong—and What I Learned

### 1. Model output did not match the expected amount format

For a ₹20,000 capital transaction, the model returned:
text

Inr 20000

The initial validator expected:
text

20000

The application correctly refused to post the invalidly formatted output.

I added narrowly scoped handling for an explicit INR or ₹ prefix while retaining the underlying amount validation.

I avoided simply deleting all non-numeric characters: doing that could turn a foreign-currency amount into an incorrect rupee entry or misread shorthand such as “20k”.

### 2. A successful connection check did not prove inference worked

The app could list installed models while actual generation requests failed.

A connection check only established that Ollama’s API was reachable. It did not prove that the model runner could start and complete the request.

### 3. The model runner failed to open an internal local port

A server log eventually showed:
text

couldn't bind HTTP server socket,

hostname: 127.0.0.1, port: 53337

This explained that particular runner exit: Ollama’s internal inference server could not bind its socket.

Later checks did not show an active connection on that port or a matching Windows excluded-port range at the time they were run.

Those checks did not establish the underlying cause. Security filtering and transient conflicts remained possibilities, not confirmed diagnoses.

The important lesson was:

> Read the server logs before changing models, prompts, or unrelated settings.

### 4. Local AI has multiple moving parts

I learned to distinguish:

- The website’s server.
- Ollama’s public API.
- Ollama’s internal model runner.
- The browser’s permissions and allowed origins.

A working website did not mean the AI service was working. A working AI API did not mean inference was working.

## 🚧 Current Status

The bookkeeping interface and manual-entry workflow were built, and a development demo link has been shared.

During development, basic terminal inference succeeded, but website inference also encountered repeated model-runner crashes.

**Reliable end-to-end AI operation has not been established by the debugging results documented here.**

Before marking the project as fully working, I need to verify:

- [ ] AI parsing completes reliably.
- [ ] Missing information triggers review rather than guessing.
- [ ] Unsupported currencies are safely handled.
- [ ] Journal and report outputs pass repeatable tests.
- [ ] The public demo’s AI behaviour is explained and verified.
- [ ] The intended friend has tried the application.

## ▶️ Running Locally

### 1. Serve the website

From the project folder:
bash

python -m http.server 8000 --bind 127.0.0.1

Open:
text

http://localhost:8000

Alternatively, use VS Code Live Server and consistently use the origin it opens.

### 2. Install Ollama and a model

Install Ollama from:

https://ollama.com/download

For the smaller model:
bash

ollama pull qwen2.5:1.5b

Verify installed model names:
bash

ollama list

### 3. Check the application endpoint

The JavaScript endpoint should match the running Ollama server, for example:
javascript

const OLLAMA = http://127.0.0.1:11434;

If origin configuration is necessary, allow the exact website origin. Avoid running the Ollama desktop service and a second `ollama serve` instance on the same port.

### 4. Configure LedgerFriend

1. Open **Business & AI**.
2. Save the demo business settings.
3. Select an installed model by its exact name.
4. Click **Save model**.
5. Click **Test connection**.
6. Test a fictional transaction and review the proposed entry.

Manual transaction entry does not require Ollama.

## 🧪 Accounting Verification Example

Starting from empty books, enter:

| Transaction | Amount |
|---|---:|
| Owner introduces cash | ₹20,000 |
| Goods purchased with cash | ₹6,000 |
| Cash sale | ₹10,000 |
| Operating expense paid in cash | ₹1,000 |
| Closing-stock adjustment | ₹2,000 |

Expected results:

| Output | Expected value |
|---|---:|
| Cash | ₹23,000 |
| Closing inventory | ₹2,000 |
| Gross profit | ₹6,000 |
| Net profit | ₹5,000 |
| Total assets | ₹25,000 |
| Capital plus profit | ₹25,000 |
| Trial balance total on each side | ₹31,000 |

These are expected results for a test scenario—not a published accuracy benchmark or a claim that all tests passed.

## ⚠️ Scope and Limitations

This prototype is intentionally narrow:

- INR only.
- Sole proprietorships only.
- First bookkeeping period with zero opening balances.
- Periodic inventory accounting.
- No full individual customer/supplier subledgers.
- No GST/TDS calculations or statutory filing.
- No automated tax depreciation.
- No automatic determination of depreciation amounts.
- No comprehensive accrual, prepayment, or bad-debt workflow.
- No multi-currency accounting.
- No comprehensive cheque-dishonour or bills-of-exchange workflow.
- No implementation of “three types of suspense”.
- No encrypted storage provided by the application.
- No JSON restore workflow.

Browser data belongs to the browser profile and website origin. Changing from `localhost:8000` to another hostname or port creates a different storage context.

Closing or clearing browser storage, sharing a device, or exposing an exported snapshot can affect data availability and privacy.

## 🗺️ Next Steps

1. Stabilise local model inference.
2. Validate the workflow with one real business owner.
3. Add automated accounting and validation tests.
4. Add deterministic safeguards for unsupported currencies.
5. Improve ambiguity handling and transaction explanations.
6. Introduce reviewed customer/supplier subledgers.
7. Add secure backup and restore.
8. Explore voice entry and multilingual descriptions.
9. Expand accounting coverage only with reviewed rules and tests.

The goal is not to replace a Chartered Accountant.

The goal is to help a small-business owner prepare clearer, better-organised records for review.

## 📜 Licensing

[Add the licence you choose for your own project code and include a matching LICENSE file.]

Ollama, model weights, and other dependencies have their own licences. Using an open-weight model does not automatically license this application’s source code.

## ❤️ Challenge Reflection

This project started with an ambitious question:

> Can AI turn ordinary descriptions of business activity into accounting records?

Building it led to a more useful question:

> How can AI help without being trusted to silently decide everything?

LedgerFriend is my attempt to answer that through local inference, transparent accounting rules, human confirmation, and honest limits.
