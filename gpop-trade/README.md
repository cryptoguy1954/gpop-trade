# TradeDesk — Deployment Guide

## What's in this folder

```
tradedesk-netlify/
├── index.html                  ← Your trading app
├── netlify.toml                ← Netlify configuration
├── netlify/functions/
│   └── claude.js               ← Serverless API proxy (keeps your key secure)
└── README.md                   ← This file
```

---

## Step 1 — Get Your Anthropic API Key

1. Go to **console.anthropic.com**
2. Sign up or log in
3. Click **API Keys** in the left sidebar
4. Click **Create Key** → give it a name like "TradeDesk"
5. Copy the key (starts with `sk-ant-...`) — save it somewhere safe, you only see it once

**Cost:** ~$0.02 per article processed. Both shows daily for a month ≈ $1.20 total.

---

## Step 2 — Deploy to Netlify

### Option A — Drag and Drop (Easiest)
1. Go to **app.netlify.com** and sign up for free
2. Click **Add new site** → **Deploy manually**
3. Drag this entire `tradedesk-netlify` **folder** onto the upload zone
4. Netlify deploys in ~30 seconds — you get a live URL like `amazing-trader-123.netlify.app`

### Option B — GitHub (Best for future updates)
1. Push this folder to a GitHub repo
2. In Netlify: **Add new site** → **Import from Git** → connect your repo
3. Future updates: just push to GitHub and Netlify auto-deploys

---

## Step 3 — Add Your API Key to Netlify

This is the key step that makes the AI features work:

1. In Netlify, go to your site → **Site configuration** → **Environment variables**
2. Click **Add a variable**
3. Key: `ANTHROPIC_API_KEY`
4. Value: paste your `sk-ant-...` key
5. Click **Save**
6. Go to **Deploys** → click **Trigger deploy** → **Deploy site**

Your API key now lives securely on Netlify's servers — never exposed in the browser.

---

## Step 4 — You're Live!

Open your Netlify URL and test:
- Paste Gareth's Game Plan article → click **Process with AI**
- Paste Trading the Close notes → click **Process with AI**
- Go to **⚡ Intelligence** → click **Generate Analysis**

---

## Updating the App

If you get an updated `index.html` from Claude:
- **Drag & drop:** Re-drag the whole folder to Netlify
- **GitHub:** Replace `index.html` and push — auto-deploys

The `netlify.toml` and `netlify/functions/claude.js` files rarely need to change.

---

## Troubleshooting

**"Error processing show notes"**
→ Check that `ANTHROPIC_API_KEY` is set in Netlify environment variables and you triggered a redeploy after adding it.

**"Method not allowed"**
→ Make sure you're accessing the deployed Netlify URL, not opening index.html directly from your computer.

**Charts not loading**
→ TradingView widgets require a live URL — they won't work when opening the file locally either.
