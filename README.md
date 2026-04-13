# BrainRouter 🧠

so basically this is my college project but i actually think its a pretty solid idea so i built it properly lol

live at → **[brainrouter.co.in](https://brainrouter.co.in)**

---

## what is it

its a single web app that has multiple AI models connected to it — and instead of you having to choose which one to use, it just... figures it out for you. you type something and Gemini 1.5 Flash reads your message and routes it to whichever model is best for that specific task.

like if you ask it to write code it sends it to Claude. if you wanna have a casual chat it goes to Grok. if you need something researched properly it uses Gemini. image generation goes to Stability AI. you get the idea.

---

## the models and what they do

| model | what its good at |
|-------|-----------------|
| Gemini 1.5 Flash | routing every message + deep reasoning |
| GPT-4o mini | general conversation and Q&A |
| Grok | casual chat, humor, real-time stuff |
| Claude | code, debugging, anything technical |
| Stability AI | generating images from text |

---

## how the routing works

every time you send a message, before anything else happens, it hits the Gemini API with a system prompt that tells it to return a JSON object like:

```json
{"model": "claude", "reason": "user is asking to write a python script"}
```

then based on that it calls whichever API is needed. the whole routing step takes like half a second which is why i picked Gemini Flash specifically — its fast.

---

## features

- smart routing (the whole point)
- sign in with Google or email
- 20 free messages as a guest, 100 after you sign up
- API keys saved to localStorage so you dont have to re-enter them every session
- routing log on the right side shows you every decision it made and why
- paywall popup after 20 messages (built this in because why not, could actually make this real)

---

## setup / running it locally

its literally one HTML file so just download it and open it in your browser. thats it.

for it to actually work you need API keys:

- **Gemini** (required, this is the router) → [aistudio.google.com](https://aistudio.google.com)
- **OpenAI** → [platform.openai.com](https://platform.openai.com)
- **Grok** → [console.x.ai](https://console.x.ai)
- **Claude** → [console.anthropic.com](https://console.anthropic.com)
- **Stability AI** → [platform.stability.ai](https://platform.stability.ai)

paste them in the settings panel (the icon in the top right) and youre good

---

## google sign-in setup (if you're forking this)

1. go to console.cloud.google.com
2. new project → APIs & Services → Credentials → OAuth Client ID → Web application
3. add your domain to authorized JavaScript origins
4. copy the client ID
5. find `YOUR_GOOGLE_CLIENT_ID_HERE` in the HTML and replace it

---

## tech stack

honestly its just vanilla HTML, CSS and JavaScript. no frameworks, no build tools, no node_modules folder with 400MB of dependencies. one file. i kind of like that about it

the only external things are:
- Google Fonts (Lora + DM Sans)
- Google Identity Services (for OAuth)
- the actual AI APIs

---

## why i built this

i kept switching between ChatGPT, Claude, Gemini etc depending on what i needed to do and it was annoying. the idea is that you shouldnt have to know which AI is good at what — it should just know. 

also it was a college project and i wanted to build something that could actually be a real product one day and not just a thing i submit and forget about

---

## future plans (maybe)

- actual backend with a proper database instead of localStorage
- user history saved across devices  
- more models (Mistral, Llama, etc)
- a proper Pro plan with Stripe payments
- mobile app version

---

## made by

vl0n317 — project, 2026

if you wanna reach out or collab → brainrouter.co.in
