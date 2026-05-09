# SETUP.md — One-Time Setup (~60 minutes)
**Do this once. Marketing runs forever after.**

---

## Step 1: Create brand accounts (20 min)

### Twitter/X
1. Go to twitter.com → Create Account
2. Username: `@sovixhq` (and `@spreixhq` separately)
3. Bio: "Self-hosted Kubernetes observability. Datadog-free. → portal.sovix.xyz"
4. No real name, no photo — use brand logo or abstract avatar

### LinkedIn Company Pages
1. linkedin.com/company/create
2. Create "Sovix" company page → sovix.xyz
3. Create "Spreix" company page → app.spreix.xyz
4. Category: Computer Software
5. No personal profile needed — company pages are brand-only

### Reddit
1. reddit.com → create account: `u/SovixOfficial`
2. This account posts in r/devops, r/kubernetes, r/sre as the brand

### Dev.to + Hashnode
1. dev.to → sign up as "Sovix Engineering"
2. hashnode.com → sign up, create blog at sovix.hashnode.dev

---

## Step 2: Install SocialFlow (15 min)

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
# Edit .env:
AI_PROVIDER=gemini
GEMINI_API_KEY=your_key_here     # free at aistudio.google.com
HEADLESS=true                     # server mode
```

Start:
```bash
python main.py
# Dashboard: http://localhost:8000
```

---

## Step 3: Install marketmenow for Reddit + Twitter (10 min)

```bash
cd ~/.openclaw/workspace/Marketing
git clone https://github.com/thearnavrustagi/marketmenow engine/marketmenow
cd engine/marketmenow
bash setup.sh

# Add brand profile for Sovix:
cd engine/marketmenow
uv run mmn project add sovix

# Add brand profile for Spreix:
uv run mmn project add spreix
```

Configure Reddit:
```bash
# .env inside marketmenow:
REDDIT_SESSION=your_session_cookie    # from browser after login
REDDIT_USERNAME=SovixOfficial
```

---

## Step 4: Install linkedin-skills (5 min)

```bash
cd ~/.openclaw/workspace/Marketing
git clone https://github.com/sergebulaev/linkedin-skills skills/linkedin-skills
cd skills/linkedin-skills
pip install requests python-dotenv
```

Configure Publora (free publishing API):
```bash
# 1. Sign up at app.publora.com (free)
# 2. Connect LinkedIn company page
# 3. Get API key from Settings > API
cp .env.example .env
# Edit .env:
PUBLORA_API_KEY=sk_your_key
LINKEDIN_PLATFORM_ID=linkedin-your_id
APIFY_TOKEN=your_apify_token    # optional, from console.apify.com
```

---

## Step 5: Get API keys (10 min)

### Gemini (free AI)
- go.google.com/aistudio → Get API Key → free

### Dev.to
- dev.to/settings/extensions → Generate API key

### Hashnode
- hashnode.com/settings/developer → Generate token

### Reddit OAuth
- reddit.com/prefs/apps → create app → script type
- Save: client_id, client_secret

### Apify (optional, $5/mo free credit)
- console.apify.com → sign up → Settings → API tokens

---

## Step 6: Add secrets to OpenClaw

```bash
openclaw secrets set GEMINI_API_KEY=your_key
openclaw secrets set DEVTO_API_KEY=your_key
openclaw secrets set HASHNODE_TOKEN=your_key
openclaw secrets set REDDIT_CLIENT_ID=your_id
openclaw secrets set REDDIT_CLIENT_SECRET=your_secret
openclaw secrets set REDDIT_USERNAME=SovixOfficial
openclaw secrets set PUBLORA_API_KEY=sk_your_key
openclaw secrets set LINKEDIN_PLATFORM_ID=linkedin-your_id
```

---

## Done ✅

From this point:
- SocialFlow runs autonomously (posts to LinkedIn, Twitter, Threads)
- marketmenow scans Reddit 4x/day and posts replies
- Cleo writes all content via OpenClaw crons
- You get a daily Telegram report at 9 PM IST

**You never touch marketing again.**
