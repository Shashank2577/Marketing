# GETTING-STARTED.md
# Complete Step-by-Step Setup Guide
**For Marketing + GrowthOS repos — verified links, current programs**
*Last verified: May 2026 by Cleo 🐾*

---

## Overview — What You're Setting Up

| Repo | What it does | Time to set up |
|------|-------------|----------------|
| **Marketing** | Posts to LinkedIn, Twitter, Reddit, blogs — autonomous | ~60 min |
| **GrowthOS** | SEO audits, funding research, grants, traction tracking — autonomous | ~45 min |

**Total: ~2 hours. Then both run forever without you.**

---

# PART 1 — MARKETING REPO SETUP
**Repo: github.com/Shashank2577/Marketing**

---

## Step 1 — Create Brand Accounts
*~20 minutes. Do this first — everything else depends on it.*

### 1.1 Twitter/X — Brand accounts
1. Open **twitter.com** → click Sign Up
2. Create account: `sovixhq@proton.me` (use a separate email)
   - Username: `@sovixhq`
   - Display name: `Sovix`
   - Bio: `Self-hosted Kubernetes observability. Datadog-free. → portal.sovix.xyz`
   - No real name, no personal photo — use your product logo or abstract avatar
3. Repeat for Spreix:
   - Username: `@spreixhq`
   - Bio: `AI meeting intelligence that actually understands context. → app.spreix.xyz`

> **Why separate email:** Keeps brand identity clean. Use Proton Mail (free) or a new Gmail.

### 1.2 LinkedIn Company Pages
1. Go to **linkedin.com/company/setup/new/**
2. Create company: `Sovix`
   - Website: `https://portal.sovix.xyz`
   - Industry: Computer Software
   - Size: 1-10 employees
   - Tagline: `Kubernetes observability without the Datadog bill`
3. Repeat for `Spreix` → `https://app.spreix.xyz`

> **Note:** You need a personal LinkedIn account to create company pages, but the company page is separate from your personal profile. Colleagues won't see the connection unless they look specifically.

### 1.3 Reddit Brand Account
1. Go to **reddit.com** → Create account
   - Username: `SovixOfficial`
   - Email: `sovixhq@proton.me` (same brand email)
2. Add karma first before posting: spend 1-2 days upvoting and making small comments in r/devops before posting brand content. Reddit flags new accounts with 0 karma.

### 1.4 Dev.to Account
1. Go to **dev.to** → Sign up with GitHub or email
   - Username: `sovix-engineering`
   - Bio: `Engineering blog for Sovix — self-hosted K8s observability`
2. Settings → Account → API Keys → Generate new key → copy it

### 1.5 Hashnode Blog
1. Go to **hashnode.com** → Sign up
   - Create blog: `sovix.hashnode.dev`
2. Account Settings → Developer → Personal Access Tokens → Generate → copy it

---

## Step 2 — Set Up Buffer (LinkedIn + Twitter posting)
*~10 minutes. This is what lets me post automatically.*

1. Go to **buffer.com** → Sign up free
2. Connect channels:
   - Click **Add a Channel** → LinkedIn → Select "Sovix" company page
   - Click **Add a Channel** → Twitter/X → Login as `@sovixhq`
   - Repeat for Spreix (LinkedIn company page + `@spreixhq` Twitter)
3. Get API token:
   - Go to **buffer.com/developers/apps** → Create an App
   - App name: `Cleo-Marketing-Bot`
   - After creating → copy the **Access Token**
4. Send me the token:
```bash
openclaw secrets set BUFFER_TOKEN=your_access_token_here
```

> **Buffer free plan:** 3 channels, 10 scheduled posts. Paid ($6/mo/channel) removes limits. Start free.

---

## Step 3 — Set Up Reddit API
*~5 minutes. Lets me post community replies as the brand.*

1. Log in as `u/SovixOfficial` on reddit.com
2. Go to **reddit.com/prefs/apps** → scroll down → click **"create another app"**
   - Name: `sovix-community-bot`
   - Type: **script**
   - Description: `Community management bot`
   - Redirect URI: `http://localhost:8080`
3. Click **Create app** → you'll see `client_id` (under the app name) and `client_secret`
4. Send me the credentials:
```bash
openclaw secrets set REDDIT_CLIENT_ID=your_client_id
openclaw secrets set REDDIT_CLIENT_SECRET=your_client_secret
openclaw secrets set REDDIT_USERNAME=SovixOfficial
openclaw secrets set REDDIT_PASSWORD=your_reddit_password
```

---

## Step 4 — Install SocialFlow (Autonomous CMO Engine)
*~15 minutes. The core engine that posts to 12 platforms.*

```bash
cd ~/.openclaw/workspace/Marketing
git clone https://github.com/inbharatai/SocialFlow engine/socialflow
cd engine/socialflow/backend
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
playwright install chromium
```

Configure:
```bash
cp .env.example .env
nano .env
```

Set these values in `.env`:
```
AI_PROVIDER=gemini
GEMINI_API_KEY=your_key       # Get free at: aistudio.google.com
HEADLESS=true
```

Start:
```bash
python main.py
# Dashboard at http://localhost:8000
```

In the dashboard:
- Go to **Brand Kit** → upload Sovix logo, set colors, set tone: `"Direct, technical, no-fluff. Engineering voice."`
- Go to **Accounts** → add LinkedIn (login via browser), Twitter (login via browser)

---

## Step 5 — Install marketmenow (Reddit + Twitter Engagement)
*~10 minutes.*

```bash
cd ~/.openclaw/workspace/Marketing
git clone https://github.com/thearnavrustagi/marketmenow engine/marketmenow
cd engine/marketmenow
bash setup.sh
cp .env.example .env
```

Set in `.env`:
```
REDDIT_SESSION=your_session_cookie    # Get from browser after logging in as SovixOfficial
REDDIT_USERNAME=SovixOfficial
GEMINI_API_KEY=your_key               # Same key as above
```

Set up brand profiles:
```bash
# For Sovix:
uv run mmn project add sovix
# Fill in: name=Sovix, url=portal.sovix.xyz, targets: r/devops r/kubernetes r/sre r/selfhosted

# For Spreix:
uv run mmn project add spreix
# Fill in: name=Spreix, url=app.spreix.xyz, targets: r/productivity r/PKMS r/Notion
```

---

## Step 6 — Install linkedin-skills
*~5 minutes. LinkedIn-specific posting with viral hooks.*

```bash
cd ~/.openclaw/workspace/Marketing
git clone https://github.com/sergebulaev/linkedin-skills skills/linkedin-skills
cd skills/linkedin-skills
pip install requests python-dotenv
```

Set up Publora (free LinkedIn publishing API):
1. Go to **app.publora.com/signup** → Sign up free (15 posts/month free)
2. Click **Channels** → **Add Channel** → LinkedIn → authorize Sovix company page
3. Click **Settings** (bottom left) → **API** → **Create Key** → copy `sk_...`
4. Go back to **Channels** → click your LinkedIn account → copy the `linkedin-...` ID

```bash
cp .env.example .env
nano .env
# Set:
# PUBLORA_API_KEY=sk_your_key
# LINKEDIN_PLATFORM_ID=linkedin-your_id
```

---

## Step 7 — Add All Secrets to OpenClaw

Run these once (replace with your actual values):

```bash
openclaw secrets set GEMINI_API_KEY=your_gemini_key
openclaw secrets set BUFFER_TOKEN=your_buffer_token
openclaw secrets set REDDIT_CLIENT_ID=your_id
openclaw secrets set REDDIT_CLIENT_SECRET=your_secret
openclaw secrets set REDDIT_USERNAME=SovixOfficial
openclaw secrets set REDDIT_PASSWORD=your_password
openclaw secrets set DEVTO_API_KEY=your_devto_key
openclaw secrets set HASHNODE_TOKEN=your_hashnode_token
openclaw secrets set PUBLORA_API_KEY=sk_your_key
openclaw secrets set LINKEDIN_PLATFORM_ID=linkedin-your_id
```

---

## Marketing Repo ✅ DONE

After this, every day automatically:
- 7:00 AM → Posts written for LinkedIn + Twitter (both brands)
- 7:30 AM → Published via SocialFlow/Buffer
- 9:00 AM → Reddit community scan + replies posted
- 1:00 PM → Afternoon Reddit + HN scan
- 4:00 PM → Blog published to Dev.to + Hashnode (Mon/Thu)

---
---

# PART 2 — GROWTHSOS REPO SETUP
**Repo: github.com/Shashank2577/GrowthOS**

---

## Step 8 — Install SEO Skills
*~15 minutes.*

```bash
cd ~/.openclaw/workspace/GrowthOS/skills

# Main SEO engine (24 skills, runs audits, schema, backlinks, GEO)
git clone --depth 1 https://github.com/AgriciDaniel/claude-seo.git

# Marketing audit (CRO, copy, competitor intel, landing pages)
git clone https://github.com/zubair-trabzada/ai-marketing-claude.git
cd ai-marketing-claude && ./install.sh && pip install reportlab && cd ..
```

---

## Step 9 — Install Founder Skills (Pitch + Validation)
*~10 minutes.*

```bash
cd ~/.openclaw/workspace/GrowthOS/skills

# Pitch deck review, market sizing, IC simulation, competitive positioning
git clone https://github.com/lool-ventures/founder-skills.git
cd founder-skills && uv sync && cd ..

# Validation layer: hypothesis register, gap analysis, GTM
git clone https://github.com/BellaBe/strategy-os.git
```

---

## Step 10 — Connect Google Search Console (Free SEO Data)
*~10 minutes. Gives you keyword rankings, impressions, CTR.*

1. Go to **search.google.com/search-console** → Add property
   - Add `portal.sovix.xyz` → verify via DNS TXT record (add in your domain registrar)
   - Add `app.spreix.xyz` → same
2. Go to **console.cloud.google.com** → Create new project: `GrowthOS-SEO`
3. Enable APIs: Google Search Console API + PageSpeed Insights API
4. Create OAuth 2.0 credentials → download `credentials.json`
5. Run setup:
```bash
cd ~/.openclaw/workspace/GrowthOS/skills
git clone https://github.com/acamolese/google-search-console-mcp.git gsc-mcp
cd gsc-mcp && pip install -r requirements.txt
```
6. Add secrets:
```bash
openclaw secrets set GOOGLE_CLIENT_ID=your_id
openclaw secrets set GOOGLE_CLIENT_SECRET=your_secret
```

---

## Step 11 — Apply for Cloud Credits
*Priority order — start with easiest, no incorporation needed.*

### Week 1 — Apply today

**AWS Activate (up to $100K)**
- URL: **aws.amazon.com/startups** → click "Apply now"
- Requirements: Working website, company email, describe your product
- Apply TWICE: once for Sovix (`portal.sovix.xyz`), once for Spreix (`app.spreix.xyz`)
- Time: 30 min per application
- Decision: 1-2 weeks

**GCP for Startups (up to $350K for AI-first)**
- URL: **cloud.google.com/startup/apply**
- Tiers:
  - Pre-funded: $2,000 (instant, just sign up)
  - Seed-Series A: $200K standard / $350K for AI-first
- Apply as AI-first startup (both Sovix and Spreix use AI)
- Apply TWICE: once per product domain
- Time: 20 min per application

**Microsoft for Startups Founders Hub (up to $150K Azure)**
- URL: **portal.startups.microsoft.com/signup**
- Requirements: Company email, working product URL
- Apply TWICE: once per product
- Time: 15 min per application
- Includes: Azure credits + GitHub Copilot + Microsoft 365

**Azure Founders Hub**
- Same as Microsoft for Startups — same portal as above
- If you apply via Microsoft for Startups, Azure credits are included

### Week 2 — After basic landing pages live

**DigitalOcean Startups**
- URL: **digitalocean.com/startups** → "Apply now" form
- Requirements: Company website, under $10M raised
- Credits: varies (typically $500-1000 for solo applicants, more via accelerator)
- Also get: free GPU droplets at $1.90/hr for 12 months

**Anthropic for Startups ($25K Claude credits)**
- URL: Apply via YC/Antler/accelerator (preferred) OR email `startups@anthropic.com`
- Best path: Apply to Antler India first → Antler has Anthropic credits in their perks ($1M+ in AI perks)

**OpenAI Startup Credits ($25K)**
- URL: **openai.com/startups** → application form
- Easiest via: accelerator referral (Antler/YC)

### Use these immediately (no approval needed)

| Service | What to do | Link |
|---------|-----------|------|
| Google AI Studio / Gemini | Just sign up → free tier | aistudio.google.com |
| Groq (100K tokens/day free) | Sign up → instant | console.groq.com |
| Together AI ($25 free) | Sign up → instant | api.together.xyz |
| Mistral | Sign up → free tier | console.mistral.ai |
| Neon (Postgres, free) | Sign up → free tier | neon.tech |
| Supabase (free tier) | Sign up → free tier | supabase.com |
| Cloudflare Workers (100K req/day free) | Sign up → free tier | cloudflare.com |

---

## Step 12 — Apply for Accelerators (India)

**Antler India AI Residency — HIGHEST PRIORITY**
- What: ₹4 Crore (~$470K) for 11% equity + $1M in AI perks
- URL: **antler.co/location/india** → Apply button
- Format: In-person residency in Bangalore, 3 weeks
- Decision: 3 weeks from application
- Next cohort: Check site for dates (runs 2-3x per year)
- Note: Sovix + Spreix are exactly what they back (AI, SaaS, DevTools)

**100X.VC (India, rolling)**
- What: ₹25L ($30K) for iSAFE (standard terms)
- URL: **100x.vc/apply**
- Rolling applications, decisions monthly

**Pioneer (remote, weekly)**
- What: $5K/month grant + no equity for early-stage projects
- URL: **pioneer.app**
- Apply weekly — global leaderboard, voting community

**Better Capital (India, rolling)**
- What: $200K for 7-10% equity
- URL: **bettercapital.us** → Apply
- Rolling applications

---

## Step 13 — India Government Programs

**Step 1 (required for all India grants): DPIIT Startup Recognition**
- URL: **startupindia.gov.in** → Register → Apply for DPIIT Recognition
- Requirements: Incorporated entity (Pvt Ltd or LLP), less than 10 years old, under ₹100Cr turnover
- Cost: Free
- Time: 2-4 weeks processing
- Benefit: Unlocks all government grants, tax exemptions, fast-track patents

**NASSCOM 10K Startups**
- URL: **nasscom.in/10000startups** → Apply
- Benefits: Mentoring, cloud credits, co-working, investor connects
- Rolling applications

**Startup India Seed Fund (₹50L = ~$60K)**
- URL: **seedfund.startupindia.gov.in**
- Requires: DPIIT recognition first
- Apply through DPIIT-recognized incubators

---

## Step 14 — Launch on Traction Channels

**Hacker News — Show HN**
- Post: Monday-Wednesday, 9-11 AM EST (9:30 PM - 11:30 PM IST)
- Use exact drafts from: `GrowthOS/traction/playbook.md`
- Only post once per product

**Product Hunt**
- URL: **producthunt.com/posts/create**
- Find a hunter: Search PH for DevOps/observability hunters with followers
- Schedule launch day: Tuesday or Wednesday (best traffic)
- Notify your network day-of for upvotes

**Submit to Directories (free backlinks + discovery)**
Submit to all of these — takes 5 min each:

| Directory | Link | Type |
|-----------|------|------|
| BetaList | betalist.com/submit | Beta products |
| AlternativeTo | alternativeto.net/recommend/ | Alternatives listing |
| G2 | g2.com/products/new | Software reviews |
| StackShare | stackshare.io/submissions/new | Dev tools |
| DevHunt | devhunt.org | Dev tools |
| SaaSHub | saashub.com | SaaS listing |
| There's An AI For That | theresanaiforthat.com/submit | AI tools (Spreix) |
| Futurepedia | futurepedia.io/submit-tool | AI tools (Spreix) |
| StartupIndia listing | startupindia.gov.in | India startups |

**CNCF Landscape (Sovix — high value)**
- URL: **github.com/cncf/landscape** → open a PR to add Sovix
- This gets Sovix in front of every Kubernetes user globally
- Requirements: Open source repo, working product

---

## Step 15 — Add Final Secrets to OpenClaw

```bash
# Google Search Console
openclaw secrets set GOOGLE_CLIENT_ID=your_id
openclaw secrets set GOOGLE_CLIENT_SECRET=your_secret

# Optional: DataForSEO for live SERP data (free trial)
# Sign up at dataforseo.com
openclaw secrets set DATAFORSEO_LOGIN=your_login
openclaw secrets set DATAFORSEO_PASSWORD=your_pass

# Optional: Apify for LinkedIn scraping ($5/mo free credit)
# Sign up at console.apify.com → Settings → API tokens
openclaw secrets set APIFY_TOKEN=your_token
```

---

# Summary Checklist

## Accounts to create
- [ ] Twitter `@sovixhq` + `@spreixhq`
- [ ] LinkedIn company pages: Sovix + Spreix
- [ ] Reddit `u/SovixOfficial`
- [ ] Dev.to `sovix-engineering`
- [ ] Hashnode `sovix.hashnode.dev`
- [ ] Buffer account → connect all 4 social accounts
- [ ] Publora account → connect LinkedIn company pages

## Credits to apply (Week 1)
- [ ] AWS Activate for Sovix → aws.amazon.com/startups
- [ ] AWS Activate for Spreix → aws.amazon.com/startups
- [ ] GCP for Sovix → cloud.google.com/startup/apply
- [ ] GCP for Spreix → cloud.google.com/startup/apply
- [ ] Microsoft for Startups for Sovix → portal.startups.microsoft.com/signup
- [ ] Microsoft for Startups for Spreix → portal.startups.microsoft.com/signup

## Immediate free credits (no approval)
- [ ] Google AI Studio → aistudio.google.com
- [ ] Groq → console.groq.com
- [ ] Together AI → api.together.xyz
- [ ] Neon → neon.tech

## Accelerators (apply ASAP)
- [ ] Antler India AI Residency → antler.co/location/india ← **highest priority**
- [ ] Pioneer → pioneer.app ← **weekly, apply now**
- [ ] 100X.VC → 100x.vc/apply
- [ ] Better Capital → bettercapital.us

## India grants (after incorporating)
- [ ] DPIIT Startup Recognition → startupindia.gov.in ← **required for all others**
- [ ] NASSCOM 10K → nasscom.in/10000startups

## Secrets to set in OpenClaw
- [ ] GEMINI_API_KEY
- [ ] BUFFER_TOKEN
- [ ] REDDIT_CLIENT_ID + SECRET + USERNAME + PASSWORD
- [ ] DEVTO_API_KEY
- [ ] HASHNODE_TOKEN
- [ ] PUBLORA_API_KEY + LINKEDIN_PLATFORM_ID
- [ ] GOOGLE_CLIENT_ID + GOOGLE_CLIENT_SECRET

---
*This file is maintained by Cleo 🐾. URLs verified May 2026.*
