# STACK-RESEARCH.md
# Best Proven OSS for Reach, SEO & Social Media Posts
**Research date: May 2026 | Maintained by Cleo 🐾**

---

## TL;DR — What We're Using and Why

After researching 30+ tools across GitHub topics `seo-automation`, `social-media-automation`, and ClawhHub (52K tools, 180K users), here's the verdict:

**For social posting** → `social-ai-team` replaces SocialFlow as primary. SocialFlow stays as the publisher/scheduler layer. Both serve different roles.

**For SEO** → `30x-seo` + `topic-cluster-architect` replace `claude-seo`. 30x-seo is deeper, faster to install (one command), and has 24 skills vs 19.

**For Reddit/community** → `marketmenow` stays. Nothing beats it for agentic Reddit engagement.

---

## 1. SOCIAL MEDIA — Tool-by-Tool Verdict

### ✅ KEEP: SocialFlow (`inbharatai/SocialFlow`)
- **Stars:** High activity, updated Apr 2026
- **What it does:** 6-agent CMO pipeline — Scout → Planner → Creator → Reviewer → Publisher → Analyst
- **Unique value:** Posts to 12 platforms using Playwright (no API needed for LinkedIn, Reddit, Medium). Has Brand Kit, GPT Image 1.5, content calendar.
- **Why keep:** Best autonomous *publisher*. Once configured, it posts without any input.
- **Weakness:** Heavyweight, complex setup. Overkill for content creation alone.
- **Role in stack:** Scheduler + publisher layer

### 🆕 ADD: social-ai-team (`stevenflanagan1/social-ai-team`)
- **Stars:** Active, updated May 2026
- **What it does:** 10 Claude Code skills that act as a full social media team
  - `/brand-onboarding` → captures brand voice + visual identity once
  - `/content-calendar` → monthly content plan with pillar ratios
  - `/caption-writer` → 6 storytelling frameworks, platform-native
  - `/linkedin-writer` → first-person, insight-led, LinkedIn-native format
  - `/x-writer` → 280-char enforced, standalone hooks
  - `/threads-writer` → 500-char, opinion-led
  - `/social-creative-designer` → branded visuals via Nano Banana (AI image MCP)
  - `/publisher` → schedules via Blotato
  - `/social-performance-review` → monthly review, feeds back into next month
- **Why add:** Content *quality* is better than SocialFlow. SocialFlow posts fast; social-ai-team posts *well*. The feedback loop (performance review → content calendar) is unique.
- **Install:**
  ```bash
  git clone https://github.com/stevenflanagan1/social-ai-team.git
  cd social-ai-team && bash install.sh
  ```
- **Role in stack:** Content creation + quality layer

### ✅ KEEP: marketmenow (`thearnavrustagi/marketmenow`)
- **Stars:** Active, updated Apr 2026
- **What it does:** Agentic Reddit + Twitter outbound marketing. Finds threads, generates relevant replies, posts as brand.
- **Why keep:** Nothing else does authentic community engagement at this level. ClawCompatible = works natively with OpenClaw.
- **Role in stack:** Community engagement + inbound from Reddit/HN

### ✅ KEEP: linkedin-skills (`sergebulaev/linkedin-skills`)
- **Stars:** Active, updated Apr 2026
- **What it does:** LinkedIn-specific skills — human-sounding posts, comments that get noticed, feed analysis, publishing cadence
- **Why keep:** Complements social-ai-team's `/linkedin-writer`. Good for personal profile posting (Shash's own profile) vs company page.
- **Role in stack:** Personal LinkedIn presence (Shash as founder)

### ❌ SKIP: Somiibo bots (twitter-bot, linkedin-bot, instagram-bot)
- Mass-follow/like/comment spam bots
- High ban risk, no AI, no quality. Not what we want.

### ❌ SKIP: social-media-caption-generator-claude (`rediumvex`)
- Good for Instagram Reels/TikTok captions
- Sovix + Spreix are B2B → LinkedIn/Twitter/Reddit is the channel, not TikTok
- Skip unless B2C social becomes a priority

---

## 2. SEO — Tool-by-Tool Verdict

### 🔄 REPLACE: claude-seo → 30x-seo (`norahe0304-art/30x-seo`)

**Why replace:**
| Feature | claude-seo | 30x-seo |
|---------|-----------|---------|
| Skills | 19 | 24 |
| Install | `bash install.sh` | `npx skills add norahe0304-art/30x-seo` (1 command) |
| AI Overviews / GEO | Basic | Full GEO + LLM citation tracking |
| Content decay detection | No | Yes |
| Cannibalization detection | No | Yes |
| SEO drift monitoring | No | Yes |
| AI visibility (ChatGPT/Claude/Perplexity) | No | Yes (DataForSEO) |
| No API needed | 12 skills | 19/24 skills |
| 2026 ready | Partial | Yes (September 2025 QRG) |

**30x-seo key skills for Sovix/Spreix:**
- `/seo technical` → crawlability, Core Web Vitals, structured data
- `/seo content-brief` → analyzes top 10 SERP, generates content briefs
- `/seo programmatic` → scale comparison pages (Sovix vs Datadog, Spreix vs Notion)
- `/seo competitor-pages` → "Datadog alternative" / "Notion alternative" pages (high intent)
- `/seo ai-visibility` → track if Sovix/Spreix appear in ChatGPT/Claude/Perplexity answers
- `/seo geo` → optimize for AI Overviews
- `/seo content-decay` → detect which pages are losing ranking

**Install:**
```bash
npx skills add norahe0304-art/30x-seo
# Optional: configure DataForSEO for live SERP data
echo -n "email:password" | base64 > ~/.config/dataforseo/auth
```

### 🆕 ADD: topic-cluster-architect (`x0u0an/topic-cluster-architect`)
- **What it does:** Builds pillar page + topic cluster strategy from site URL, competitors, existing content. Outputs 30/60/90-day execution roadmap.
- **Why add:** Neither 30x-seo nor claude-seo does strategic content *architecture*. This fills the gap between "what's wrong" (audit) and "what to write" (content brief).
- **Perfect use case:**
  - Give it `portal.sovix.xyz` + competitors (groundcover.com, datadog.com) → get pillar pages + cluster structure
  - Give it `app.spreix.xyz` + competitors (notion.so, otter.ai) → get pillar pages + cluster structure
- **Install:**
  ```bash
  npx skills add x0u0an/topic-cluster-architect
  ```

### ✅ KEEP: claude-seo (`AgriciDaniel/claude-seo`) — as secondary
- Has GEO optimization, PDF/HTML reporting, Google APIs integration, competitor comparison page generator
- Keep for: `/seo geo`, `/seo google report`, `/seo competitor-pages`
- The ecosystem (claude-blog + banana) makes it worth having alongside 30x-seo

### ✅ KEEP: ai-marketing-claude (`zubair-trabzada/ai-marketing-claude`)
- 15 marketing skills: CRO audits, copy, email sequences, ad campaigns
- Complements SEO work — once you have traffic, this converts it
- Keep for landing page copy + conversion optimization

---

## 3. THE FULL OPTIMIZED STACK

```
SOCIAL MEDIA LAYER
├── social-ai-team         → Content creation (quality, brand voice, feedback loop)
├── SocialFlow             → Publishing (12 platforms, autonomous, Brand Kit)
├── marketmenow            → Community (Reddit/Twitter engagement, agentic)
└── linkedin-skills        → Personal brand (Shash's personal LinkedIn)

SEO LAYER
├── 30x-seo                → Primary SEO engine (24 skills, AI visibility, decay)
├── topic-cluster-architect → Content architecture (pillar pages, 90-day roadmap)
├── claude-seo             → Secondary (GEO, PDF reports, Google APIs)
└── ai-marketing-claude    → Conversion (CRO, landing pages, copy)

CONTENT → SOCIAL FLOW
topic-cluster-architect    → What to write (strategy)
        ↓
30x-seo content-brief      → How to write it (SERP-optimized brief)
        ↓
social-ai-team             → Write it (LinkedIn/Twitter/Threads versions)
        ↓
SocialFlow                 → Publish it (12 platforms, scheduled)
        ↓
marketmenow                → Amplify it (Reddit threads, community replies)
        ↓
30x-seo monitor            → Track rankings (GSC)
30x-seo ai-visibility      → Track AI mentions (ChatGPT/Claude/Perplexity)
```

---

## 4. WHAT TOOLS WE DON'T HAVE (GAPS)

| Gap | Best OSS option | Worth adding? |
|-----|----------------|---------------|
| Blog writing (long-form SEO) | `AgriciDaniel/claude-blog` | Yes — pairs with 30x-seo content briefs |
| AI image generation for content | `AgriciDaniel/banana-claude` | Yes — needed for social-ai-team visuals |
| YouTube automation | `darkzOGx/youtube-automation-agent` | Later — not priority now |
| Email newsletter | No great OSS option | Use Resend (free tier) manually for now |
| HN/Reddit trend monitoring | Built into marketmenow | Covered |
| Competitor social monitoring | `spacesdrive/twiligent` | Nice to have — local analytics dashboard |

---

## 5. IMMEDIATE ACTIONS

### Update Marketing repo — add missing tools
```bash
cd ~/.openclaw/workspace/Marketing/engine

# Add social-ai-team (content quality layer)
git clone https://github.com/stevenflanagan1/social-ai-team.git

# Add claude-blog (long-form SEO content)
git clone https://github.com/AgriciDaniel/claude-blog.git

# Add banana-claude (AI image generation for social)
git clone https://github.com/AgriciDaniel/banana-claude.git
```

### Update GrowthOS repo — replace/upgrade SEO layer
```bash
cd ~/.openclaw/workspace/GrowthOS/skills

# Remove old claude-seo (or keep alongside)
# Add 30x-seo (primary)
npx skills add norahe0304-art/30x-seo

# Add topic-cluster-architect (strategy layer)
npx skills add x0u0an/topic-cluster-architect
```

### One-time SEO setup for both products
Run these once after setup:
```
# In Claude Code:
/topic-cluster-architect
# → URL: portal.sovix.xyz
# → Business: Self-hosted Kubernetes observability platform
# → Audience: DevOps engineers, SREs, Platform engineers
# → Goal: Leads / signups
# → Competitors: groundcover.com, datadog.com, grafana.com

/topic-cluster-architect
# → URL: app.spreix.xyz
# → Business: AI meeting intelligence and note-taking SaaS
# → Audience: Founders, PMs, consultants, remote teams
# → Goal: Signups
# → Competitors: otter.ai, fireflies.ai, notion.so
```

---

## 6. FREE TIER LIMITS (KNOW BEFORE YOU HIT THEM)

| Tool | Free limit | When you'll hit it |
|------|-----------|-------------------|
| Gemini API (AI Studio) | 1M tokens/day | Never for 2 brands |
| Groq | 100K tokens/day | ~50 posts/day |
| Buffer | 3 channels, 10 queued posts | After 10 posts queued |
| Blotato | 15 posts/month | Week 1 |
| DataForSEO | $0 free trial, ~$50/mo after | After free credits |
| Playwright (via SocialFlow) | Unlimited | Never — local browser |

**Workaround for Buffer/Blotato limits:**
- Use SocialFlow's Playwright mode (no API = no limits) for the actual posting
- Use Buffer/Blotato only for scheduling queue management

---

*Research by Cleo 🐾 | github.com/Shashank2577/Marketing*
