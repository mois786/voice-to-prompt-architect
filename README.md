# Voice-to-Prompt Architect

A personal-use, mobile-first web app starter with a Cloudflare Worker API proxy and a React UI.

## Included
- Prompt workspace with Hindi/Hinglish-friendly input and editable transcript
- Provider profiles and custom OpenAI-compatible / Anthropic API endpoints
- Model discovery (`GET /models` where supported), manual model IDs
- Free / Paid / Unknown labels (never assumes free)
- Per-task model selection and explicit paid-fallback consent
- Projects and per-project Context Ledger stored locally in the browser
- Prompt history and export
- Cloudflare Worker backend proxy so provider keys are not placed in frontend source

## Important limits
- This starter does not make provider APIs unlimited. Provider quotas, rate limits, and billing still apply.
- Browser speech recognition depends on browser/device support and may send audio to the browser's speech service.
- This project has not been deployed or live-tested from this environment.
- For real private use, configure Cloudflare secrets and an access gate before sharing the URL.

## Local development
Install Node.js 20+, then:
1. `npm install`
2. `npm run dev`

## Cloudflare deployment
1. Create a GitHub repository and upload this project.
2. In Cloudflare, create a Workers & Pages project connected to that GitHub repository.
3. Build command: `npm run build`
4. Build output directory: `dist`
5. Deploy the Worker using Wrangler (`npx wrangler deploy`) or Cloudflare's supported build workflow.
6. Add provider credentials as Worker secrets, or use the in-app provider settings only after implementing an authenticated server-side credential vault. Never put long-lived API keys in public frontend variables.
7. Protect the site with Cloudflare Access or an equivalent authentication layer before using it privately.

## API security note
This starter routes provider calls through `/api/proxy`. For production, replace the demo session mechanism with Cloudflare Access/JWT validation and a server-side encrypted credential store. The UI currently keeps entered keys in session memory only and sends them to the Worker per request; it does not persist them to localStorage. Do not deploy as a public service without adding authentication and rate limiting.
