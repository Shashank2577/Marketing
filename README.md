# Marketing Engine 🚀
**Autonomous marketing for Sovix + Spreix — and every future product.**

Run by Cleo 🐾. Zero human effort required after one-time setup.

---

## Architecture

```
Marketing/
├── engine/           ← SocialFlow (6-agent autonomous CMO)
├── skills/           ← OpenClaw skills (LinkedIn, SEO, Reddit)
├── brands/           ← Brand configs per product
│   ├── sovix/        ← Sovix brand kit + content
│   └── spreix/       ← Spreix brand kit + content
├── content/          ← Generated content library
│   ├── posts/        ← LinkedIn + Twitter drafts
│   ├── threads/      ← Reddit + HN threads
│   └── blogs/        ← Dev.to / Hashnode articles
├── credentials/      ← .gitignored — API keys only
└── SETUP.md          ← One-time setup guide
```

---

## What runs automatically (4x per day)

| Time IST | Agent | Action |
|----------|-------|--------|
| 7:00 AM | Creator | Write LinkedIn + Twitter posts for both brands |
| 7:30 AM | Publisher | Post via SocialFlow (LinkedIn, Twitter, Threads) |
| 9:00 AM | Scout | Scan Reddit r/devops r/kubernetes r/sre r/productivity r/PKMS |
| 9:30 AM | Community | Post replies to relevant threads as brand |
| 1:00 PM | Scout | Afternoon scan — HN, Reddit, trending topics |
| 1:30 PM | Community | Post afternoon replies |
| 4:00 PM | Creator | Write blog article (Mon/Thu — 4 articles/week) |
| 4:30 PM | Publisher | Publish to Dev.to + Hashnode |
| 9:00 PM | Analyst | Daily performance report → Telegram |

---

## Stack (all free / pay-per-use only)

| Tool | Purpose | Cost |
|------|---------|------|
| **SocialFlow** | 6-agent CMO: Scout→Planner→Creator→Reviewer→Publisher→Analyst | Free (self-hosted) |
| **marketmenow** | Reddit + Twitter engagement, content capsules, repurposing | Free |
| **linkedin-skills** | LinkedIn posts, comments, viral hook formulas | Free |
| **Publora** | LinkedIn publishing API | Free (15 posts/mo) / $9 paid |
| **Apify** | LinkedIn read (posts, comments, engagers) | Free ($5 credit/mo) |
| **Reddit PRAW** | Reddit OAuth API | Free |
| **Dev.to API** | Blog publishing | Free |
| **Hashnode API** | Blog publishing | Free |
| **Gemini API** | AI content generation (via SocialFlow) | Free tier |

**Total cost: $0/month to start. <$10/month at scale.**

---

## Adding a new product

```bash
cp -r brands/sovix brands/my-new-product
# Edit brands/my-new-product/brand.yaml with new product details
# SocialFlow picks it up automatically on next run
```

---

## Setup

See [SETUP.md](./SETUP.md) — one hour, done forever.
