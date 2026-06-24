# BioRivet — AI Diagnostic Platform

Personalized NEET diagnostic reports with Rahul Sir AI prescriptions, shareable student cards, and Hinglish mentor voice.

---

## Your File Structure (what goes on GitHub)

```
biorivet/
├── server.js                  ← Express backend + all API endpoints
├── package.json               ← Node dependencies
├── .gitignore                 ← Keeps .env and node_modules off GitHub
├── .env.example               ← Template for env vars (safe to commit)
├── README.md                  ← This file
└── public/
    └── index.html             ← Your main HTML tool (rename from BioRivet_Diagnostic_Tool_v2.html)
```

> **IMPORTANT:** Rename `BioRivet_Diagnostic_Tool_v2.html` → `public/index.html`  
> The server serves everything from the `public/` folder. The HTML file must be named `index.html` inside `public/`.

---

## Step 1 — Set Up GitHub Repo

### First time (new repo):
```bash
# Inside your project folder
git init
git add .
git commit -m "Initial BioRivet deploy"

# Create repo on github.com, then:
git remote add origin https://github.com/YOUR_USERNAME/biorivet.git
git branch -M main
git push -u origin main
```

### Every update after that:
```bash
git add .
git commit -m "describe what you changed"
git push
```
Render auto-deploys within 2–3 minutes every time you push.

---

## Step 2 — Deploy on Render

1. Go to **https://render.com** → Sign in with GitHub

2. Click **"New +"** → **"Web Service"**

3. Connect your GitHub repo (`biorivet`)

4. Fill in these settings exactly:

| Setting | Value |
|---|---|
| **Name** | `biorivet` (or any name) |
| **Region** | Singapore (closest to India) |
| **Branch** | `main` |
| **Runtime** | `Node` |
| **Build Command** | `npm install` |
| **Start Command** | `node server.js` |
| **Instance Type** | `Free` (to start) |

5. Scroll down to **"Environment Variables"** → Click **"Add Environment Variable"**:

| Key | Value |
|---|---|
| `GEMINI_API_KEY` | your actual Gemini API key |

> Get your Gemini API key from: https://aistudio.google.com/app/apikey

6. Click **"Create Web Service"**

7. Wait 3–5 minutes for first deploy. You'll get a URL like:  
   `https://biorivet.onrender.com`

---

## Step 3 — Verify It's Working

Open your Render URL in browser. You should see the BioRivet tool.

**Test checklist:**
- [ ] Tool loads without errors
- [ ] Upload a question paper PDF → questions extract correctly
- [ ] Upload answer sheet → scoring works
- [ ] Generate AI Prescription → Rahul Sir report appears
- [ ] Click "Generate Shareable Card" → card modal opens
- [ ] Download PNG → saves to device

---

## Common Issues & Fixes

### "Application Error" on Render
- Check Render logs → Dashboard → your service → "Logs" tab
- Most common cause: `GEMINI_API_KEY` not set in environment variables

### Tool loads but AI prescription fails
- Check that `GEMINI_API_KEY` is correct in Render environment variables
- Check Render logs for the exact error message

### Free tier goes to sleep
- Render free tier sleeps after 15 minutes of inactivity
- First request after sleep takes ~30 seconds to wake up
- Fix: upgrade to Starter ($7/month) for always-on, OR use https://uptimerobot.com (free) to ping your URL every 10 minutes and keep it awake

### Port issues
- Never hardcode a port. `server.js` already uses `process.env.PORT || 3000` — this is correct.
- Render sets `PORT` automatically. Do not add `PORT` to your environment variables on Render.

---

## Updating After Changes

```bash
# Make your changes to server.js or public/index.html
git add .
git commit -m "what you changed"
git push
# Render auto-deploys in 2-3 minutes
```

---

## Environment Variables Reference

| Variable | Where to get it | Required |
|---|---|---|
| `GEMINI_API_KEY` | https://aistudio.google.com/app/apikey | Yes |

---

## Local Development

```bash
# Install dependencies
npm install

# Create your local .env file
cp .env.example .env
# Edit .env and add your GEMINI_API_KEY

# Run locally
npm start
# Open http://localhost:3000
```
