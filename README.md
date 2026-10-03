# LedgerFriend
### Describe the transaction. Review the entry. Understand your books.

LedgerFriend is a prototype bookkeeping assistant for Indian sole proprietors. It lets a user describe a business transaction in plain language, review the suggested accounting treatment, and generate organised books without manually repeating the same information across reports.

**AI suggests the transaction details. Fixed accounting rules generate the entries. A human approves what gets posted.**

> Prototype only. Not production accounting software, tax advice, or a replacement for a Chartered Accountant.

## Demo

- Live demo: https://a1553164a0942b.lhr.life
- Local app: http://localhost:8080
- Public demo note: this is a development demo, not a permanent production deployment.
- Please use fictional transactions only. Do not enter bank details, customer information, or confidential financial records.

## Who this is for

This project is intended for an Indian sole proprietor who wants a simpler way to record ordinary business activity without dealing with complex accounting jargon and manual repetitive bookkeeping.

## How the idea started

The goal was to combine natural-language input with deterministic accounting rules:

- AI extracts the transaction details.
- Fixed rules create the accounting entry.
- The user reviews and confirms before posting.

This keeps accounting logic transparent and reduces the risk of silent AI mistakes.

## Features

- Plain-language transaction descriptions
- Local AI integration through Ollama
- Manual data entry fallback when AI is unavailable
- Journal, ledger, trial balance, and draft financial statements
- Review queue and reversal workflow
- CSV export and JSON snapshot export

## Safety and limitations

The prototype includes safeguards such as:

- Integer-paise arithmetic instead of floating-point rupee calculations
- Fixed transaction-to-account rules
- Date and amount validation
- Balanced journal-entry checks
- Human confirmation before posting

Important limitations:

- AI can still misunderstand a transaction
- Users can approve an incorrect suggestion
- Rule-based logic can contain bugs
- The app is not a full tax, audit, or compliance system
- Browser storage can be modified or deleted

## Local setup

1. Install Ollama: https://ollama.com/
2. Pull a model such as:
   ```bash
   ollama run qwen2.5:7b
   ```
3. Start the app locally:
   ```bash
   python -m http.server 8080
   ```
4. Open the app in a browser:
   ```text
   http://localhost:8080
   ```

## Tech stack

- HTML, CSS, and JavaScript
- Browser localStorage for prototype data
- Ollama for local AI inference
- Open-source models such as Qwen and Gemma
- VS Code for development

## Current status

This is a demo prototype built to explore local AI-assisted bookkeeping. It is useful for demonstration and development testing, but it is not yet a production-ready accounting system.

## Goal

The project aims to help a small-business owner prepare clearer, better-organised records for review and decision-making without blindly trusting AI-generated accounting entries.
