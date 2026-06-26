# 🌍 Opportunity — Global Market Intelligence

> Describe any app concept → discover which countries already have a validated solution → find where the market gap is yours to capture.

---

## What it does

Enter a brief description of an app idea. Opportunity uses **Claude (Anthropic AI)** to analyze the global market and return:

- **✅ Validated Markets** — Countries where similar solutions already operate, with real app/company names and market maturity
- **🎯 Opportunity Markets** — Countries where this type of solution is absent, with an opportunity score (1–10) and market context
- **💡 Global Insights** — Strategic patterns and timing observations

---

## Deploy in 10 minutes

### Prerequisites

| Tool | Why |
|---|---|
| Node.js 18+ | Run locally |
| Git | Version control |
| Anthropic API key | Powers the AI research ([get one free](https://console.anthropic.com)) |
| GitHub account | Host the code |
| Vercel account | Deploy (free tier works) |

---

### Step 1 — Download the code

**Option A: Clone (if already on GitHub)**
```bash
git clone https://github.com/YOUR_USERNAME/opportunity.git
cd opportunity
```

**Option B: Start fresh**
```bash
mkdir opportunity && cd opportunity
# Copy all project files here
```

---

### Step 2 — Install dependencies

```bash
npm install
```

---

### Step 3 — Set up your API key

```bash
cp .env.example .env.local
```

Open `.env.local` in any editor and paste your key:

```env
ANTHROPIC_API_KEY=sk-ant-api03-XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX
```

> 🔑 Get your key at [console.anthropic.com](https://console.anthropic.com) → API Keys → Create Key

---

### Step 4 — Run locally

```bash
npm run dev
```

Open **[http://localhost:3000](http://localhost:3000)** — it should work immediately.

Try the example prompts or type your own app idea.

---

### Step 5 — Push to GitHub

```bash
git init
git add .
git commit -m "feat: initial Opportunity project"
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/opportunity.git
git push -u origin main
```

> Replace `YOUR_USERNAME` with your GitHub username. Create the repo at [github.com/new](https://github.com/new) first (no need to initialize with README).

---

### Step 6 — Deploy to Vercel

#### Option A: Vercel website (recommended for beginners)

1. Go to [vercel.com](https://vercel.com) and sign in
2. Click **"Add New… → Project"**
3. Click **"Import"** next to your `opportunity` repo
4. In the **"Environment Variables"** section, add:
   - **Name:** `ANTHROPIC_API_KEY`
   - **Value:** `sk-ant-api03-...`
5. Click **Deploy** 🚀

Vercel builds and deploys in ~60 seconds. You get a live URL like `opportunity-xyz.vercel.app`.

#### Option B: Vercel CLI

```bash
npm install -g vercel
vercel

# Answer the prompts:
# Set up and deploy? → Y
# Which scope? → your account
# Link to existing project? → N
# What's your project's name? → opportunity
# In which directory is your code? → ./
# Override settings? → N
```

Then add your API key:
```bash
vercel env add ANTHROPIC_API_KEY production
# Paste your key when prompted
vercel --prod
```

---

### Step 7 — Your app is live ✅

Vercel gives you:
- **Production URL:** `https://opportunity-xxx.vercel.app`
- **Automatic deploys** every time you push to `main`
- **Preview deploys** for every pull request

---

## Project structure

```
opportunity/
├── app/
│   ├── page.tsx              # Main page — idle / loading / results / error
│   ├── layout.tsx            # Root layout + metadata
│   ├── globals.css           # Tailwind base + custom animations
│   └── api/research/
│       └── route.ts          # ← Claude API call (Edge runtime, 2 min timeout)
├── components/
│   ├── ResearchForm.tsx      # Input form with optional fields
│   ├── ResultsDisplay.tsx    # Country cards — validated markets + opportunities
│   └── LoadingState.tsx      # Animated radar loading screen
├── lib/
│   └── types.ts              # Shared TypeScript types
├── .env.example              # Copy → .env.local, add your API key
└── README.md
```

---

## Develop with Claude Code

After cloning and installing, open the project in Claude Code:

```bash
claude
```

Example prompts to extend the app:

- *"Add a button to export results as a CSV file"*
- *"Add a filter to show only opportunities with score ≥ 7"*
- *"Add a second tab to compare two app concepts side by side"*
- *"Translate the entire UI to Spanish"*
- *"Add a world map that highlights validated countries in green and opportunities in amber"*
- *"Save search history using Supabase so users can revisit past analyses"*

---

## Optional: enable live web search

By default Opportunity uses **Claude's training data** — fast (15–20 s), accurate for established categories, works on the free Vercel plan.

To get **more current data** with live internet searches:

1. Add to `.env.local` (local) or Vercel environment variables (production):
   ```env
   ENABLE_WEB_SEARCH=true
   ```
2. Research will take 30–90 seconds
3. ⚠️ Vercel Hobby plan times out at 60 s on Edge functions — for reliable web search, upgrade to **Vercel Pro** (which allows up to 300 s) or deploy elsewhere (Railway, Fly.io, self-hosted)

---

## Troubleshooting

| Problem | Fix |
|---|---|
| `ANTHROPIC_API_KEY` error | Check the key in `.env.local` starts with `sk-ant-` |
| Build fails | Run `npm install` and check Node.js is ≥ 18 |
| Research always fails | Check Vercel function logs → Deployments → your deploy → Functions |
| Timeout on Vercel | Enable web search only with Pro plan; without it, 15–20 s is fine |
| JSON parse error | Rare — retry; if persistent, check the `extractJSON` fn in `route.ts` |

---

## What to build next

- [ ] Persist searches with Supabase (add `npm install @supabase/supabase-js`)
- [ ] Export results as PDF or CSV
- [ ] Side-by-side comparison of two concepts
- [ ] Interactive world map (react-simple-maps or Recharts)
- [ ] Competitor deep-dive per country (second Claude call)
- [ ] Shareable result links via unique IDs
- [ ] Multi-language UI

---

## License

MIT — use it however you want.
