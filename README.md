# FraudShield AI — Pause. Check. Protect.

FraudShield AI is an educational digital-payment safety prototype. It reviews SMS, WhatsApp messages and payment-request text for common warning signs: urgency, requests for OTP/UPI PIN/passwords, unexpected rewards, KYC pressure and suspicious links.

It provides an explainable indicator score (0–100), a Low / Medium / High band, matched warning signs and safe next steps. When configured, Google Gemini adds a plain-language explanation. Without an API key, the local rule engine still works.

> **Important:** This is a hackathon prototype, not a bank, antivirus or fraud-confirmation service. A low score does not guarantee safety; a high score does not prove fraud.

## Features
- Paste and analyse message text.
- Transparent Python pattern checks and risk indicator score.
- Matched warning signs and safe next steps.
- Optional Gemini-generated explanation.
- Sample messages for a quick demonstration.
- No bank login, UPI connection, or payment execution.

## Technology stack
- Frontend: HTML5, CSS3, vanilla JavaScript
- Backend: Python 3, Flask
- Optional AI model: Google Gemini `gemini-2.5-flash`
- SDK/API: Google's `google-genai` Python SDK, Gemini `generate_content`
- Local analysis: Python regular expressions and weighted rules
- Environment variables: `python-dotenv`

The local rule engine calculates the score. Gemini adds explanation only; it does not override the score.

## Project structure
```text
FraudShield_AI/
├── app.py
├── requirements.txt
├── .env.example
├── .gitignore
├── README.md
├── DEMO_VIDEO_SCRIPT.md
├── sample_messages.txt
├── templates/index.html
└── static/
    ├── app.js
    └── style.css
```

## How to run the application

1. Install Python 3.10 or newer.
2. Open a terminal in this folder.
3. Create a virtual environment:

**Windows PowerShell**
```powershell
python -m venv .venv
.venv\Scripts\Activate.ps1
```
**Windows CMD**
```bat
python -m venv .venv
.venv\Scripts\activate.bat
```
**macOS/Linux**
```bash
python3 -m venv .venv
source .venv/bin/activate
```
4. Install packages:
```bash
pip install -r requirements.txt
```
5. Optional Gemini setup: copy `.env.example` to `.env`, then add your own key:
```text
GEMINI_API_KEY=your_real_key_here
GEMINI_MODEL=gemini-2.5-flash
```
You can run without a key; local analysis remains enabled. Never commit `.env` or expose your API key.
6. Start:
```bash
python app.py
```
7. Open `http://127.0.0.1:5000`.

## Demo steps
1. Click **Suspicious sample**.
2. Click **Analyse message**.
3. Show the score and detected warning signs.
4. Explain the AI explanation / local fallback.
5. Click **Ordinary sample** and compare.
6. Explain that a low score is not a safety guarantee.

## API endpoint
`POST /api/analyze`

Request JSON:
```json
{"message":"Your account will be blocked. Share your OTP now."}
```
Response fields: `score`, `level`, `summary`, `reasons`, `ai_explanation`, `ai_enabled`, `disclaimer`.

## AI model and APIs used
- Model: Google Gemini `gemini-2.5-flash` (configurable via `GEMINI_MODEL`)
- SDK: `google-genai`
- API call: `client.models.generate_content(...)`
- Purpose: explain detected warning signs in plain language and suggest safe verification steps.
- Fallback: local Python rules work if the API key is missing or Gemini is unavailable.

## Privacy and limitations
Do not paste real OTPs, UPI PINs, passwords, card/account numbers or private messages. The app does not connect to bank/UPI systems. If Gemini is configured, the message text is sent to Gemini for explanation; review Google's API terms before using it. Pattern checks can miss new scam styles or flag legitimate messages. It does not verify the sender, domain ownership or transaction authenticity.

## Future improvements
Multilingual analysis, consent-based OCR, URL reputation checks, labelled test data and measured false-positive/false-negative rates.

Built as an Arthaton 2026 hackathon prototype.
