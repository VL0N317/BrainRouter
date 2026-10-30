# BrainRouter 🧠

**One chat box, multiple AI models. You type, it picks the right model.**

**Live:** [brainrouter.co.in](https://brainrouter.co.in) · [brain-router.vercel.app](https://brain-router.vercel.app)

<!-- TODO: add a screenshot or a 10-15 sec GIF of a prompt being routed. Put it right here. -->
<!-- ![BrainRouter demo](docs/demo.gif) -->

I kept switching between ChatGPT, Claude, and Gemini depending on the task, and it got annoying. BrainRouter makes that choice for you. A fast classifier model reads each message, determines which model is best suited, and routes it there. A dynamic routing badge above each response and an active roster in the sidebar show every decision and the reason behind it.

Started as a college project. I kept building it because I think the idea works.

---

## How routing works

1. You send a message.
2. A fast classifier (the router) receives the query with a system prompt telling it to reply with JSON only:

   ```json
   {"model": "claude", "reason": "Technical programming & code logic"}
   ```

3. The app parses that decision and calls the corresponding provider's API.
4. The response appears in chat with a routing badge, and the active model pulses in the sidebar roster.

| Task | Model / Engine | Provider |
|---|---|---|
| Code, debugging & technical questions | Claude (3.5 Sonnet / Haiku 4.5) | Anthropic / OpenRouter |
| General conversation & structured Q&A | GPT-4o mini | OpenAI / OpenRouter |
| Casual chat, humor & witty banter | Grok 2 / 4.5 | xAI / OpenRouter |
| Research, math & deep reasoning | Gemini Flash-Lite / 2.5 | Google AI Studio / OpenRouter |
| Ultra-fast lookups & reasoning | GPT-OSS 120B / LLaMA | Groq LPU Engine |
| Image generation | Pollinations / Stability | Built-in / Stability AI |

### Dual-Layer Routing Engine

BrainRouter uses a two-tier routing system to balance intelligence and speed:

1. **AI Semantic Router**: When a Gemini, Groq, or OpenRouter key is configured, an LLM performs deep semantic intent classification in structured JSON.
2. **Instant Heuristic Fallback (< 1 ms)**: If keys are missing, network is slow, or provider limits are reached, a built-in regex and pattern matcher takes over immediately. It categorizes code keywords, math proofs, jokes, and image requests so routing **never fails or lags**.

### Performance

- **Groq LPU Router**: ~190 ms classification latency
- **Gemini Flash-Lite Router**: ~1.4 s classification latency
- **Local Heuristic Fallback**: < 1 ms (instant)
- **Groq 120B Inference**: ~68 ms completion time (500+ tokens/s)

---

## Features

- **Dynamic multi-model routing** across 6 specialized AI models and generators
- **Visual routing badges** showing the active model, its accent color, and the routing rationale
- **Live sidebar model roster** that illuminates and pulses the active model in real time
- **Zero-config free tier**: works out of the box with zero API keys required
- **1-Click Auto Setup**: pre-configures and securely saves keys into `localStorage` via `#setup` tokens
- **Local API key manager**: keys stay strictly in your browser and are never stored on any server
- **Built-in image generator** powered by Pollinations.ai (free high-res image rendering)
- **Sign in with Google or email** with local message limit tracking

---

## Running it

It's a single `index.html` file. Download it and open it in any browser:

```bash
open index.html
```

Or serve locally:

```bash
python3 -m http.server 3000
```

### Free & Optional API Keys

BrainRouter works out of the box using a free public fallback. For instant speed and unlimited quotas, open the **API Keys** panel (top right) and paste any of these free keys:

- **Google Gemini** (100% Free · Router & Reasoning) → [aistudio.google.com](https://aistudio.google.com/app/apikey)
- **Groq Cloud** (100% Free · 500+ tokens/s on Groq LPUs) → [console.groq.com](https://console.groq.com/keys)
- **OpenRouter** (Universal key · access Claude, GPT-4o, Grok & free models) → [openrouter.ai/keys](https://openrouter.ai/keys)
- **Direct Keys** (Optional): Anthropic Claude, OpenAI, xAI Grok, Stability AI

Keys are saved exclusively in your browser's `localStorage` and sent directly to provider endpoints via client-side HTTPS. They never touch any server of mine.

### Google sign-in (if you fork this)

1. Go to [console.cloud.google.com](https://console.cloud.google.com) and create a project.
2. APIs & Services → Credentials → Create OAuth Client ID → Web application.
3. Add your domain to the authorized JavaScript origins.
4. Replace `YOUR_GOOGLE_CLIENT_ID_HERE` in `index.html` with your client ID.

---

## Tech stack

- **Frontend**: Vanilla HTML5, CSS3, modern ES6+ JavaScript. Single-file architecture, zero build tools, zero dependencies.
- **Typography**: Google Fonts (Inter, Lora, JetBrains Mono)
- **Auth**: Google Identity Services (OAuth 2.0)
- **AI Providers**: Google AI Studio, Groq Cloud, OpenRouter, Anthropic, OpenAI, xAI, Pollinations.ai
- **Hosting**: Vercel with custom domain ([brainrouter.co.in](https://brainrouter.co.in))

---

## Known limitations

I'd rather list these than have you find them:

- **Usage limits are enforced client-side.** The message counter lives in `localStorage`, so it can be cleared. The paywall popup is a prototype.
- **Client-side direct API calls.** Calls are made directly from the browser, which requires CORS or browser-friendly endpoints (handled via direct headers, OpenRouter, or free proxy). A production app should hold keys in a serverless proxy.
- **No sync across devices yet.** Chat history lives in your current browser session.
- **Router accuracy is probabilistic.** Like all LLM classifications, edge cases can occasionally route to an alternative model.

---

## Roadmap

- [x] Dual-layer intent routing (AI router + instant local heuristic fallback)
- [x] Client-side 1-click API key manager in `localStorage`
- [x] Zero-config free tier fallback
- [x] Groq LPU sub-second inference engine integration
- [x] In-chat dynamic routing badges and real-time active roster pulse
- [ ] Serverless backend on Vercel: keys held server-side, usage limits enforced for real
- [ ] Database for accounts and chat history across devices
- [ ] Stripe payments for Pro plan
- [ ] Support for local models via WebLLM or local Ollama instances

---

## Author

**P Dheeraj** ([@VL0N317](https://github.com/VL0N317)), Bangalore

Feedback or collaboration: open an issue or reach out through [brainrouter.co.in](https://brainrouter.co.in).
