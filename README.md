# LinkedIn Autopilot

**AI-powered LinkedIn content machine. 37 agents. 5 teams. Built-in swipe file from 9 legendary copywriters. Zero to autopilot in 5 minutes.**

LinkedIn Autopilot is a fully autonomous content pipeline that researches trends, studies top performers, writes posts in your voice, and publishes on your schedule. It does not post generic AI slop. It studies the DNA of the best copywriters who ever lived and writes like a human who has read everything.

---

## What You Get

- **37 specialized AI agents** organized into 5 coordinated teams
- **28MB swipe file library** from 9 legendary copywriters (Hormozi, Halbert, Ogilvy, and more)
- **Industry presets** for SaaS, Agency, Coach, Realtor, E-commerce, Freelancer, and Custom
- **Interactive setup wizard** that configures everything in 5 minutes
- **Content review dashboard** with approve/edit/reject workflow
- **Auto-posting** via PhantomBuster integration
- **Trend scouting** that monitors influencers and web sources daily
- **Multi-format output**: short posts, long posts, carousels, articles, newsletters
- **Email digests** with daily content summaries
- **Full scheduling engine** with timezone support and retry logic
- **Docker deployment** for set-and-forget operation

---

## Quick Start

### Option A: Docker (Recommended)

```bash
git clone https://github.com/yourorg/linkedin-autopilot.git
cd linkedin-autopilot
python setup.py          # Interactive wizard generates all config
docker-compose up -d     # Start the pipeline
```

### Option B: Local Install

```bash
git clone https://github.com/yourorg/linkedin-autopilot.git
cd linkedin-autopilot
pip install -r requirements.txt
python setup.py          # Interactive wizard
python -m linkedin_autopilot.main   # Start the pipeline
```

Your dashboard will be live at `http://localhost:8080`.

---

## How It Works

LinkedIn Autopilot runs a daily content pipeline powered by 5 specialized agent teams:

```
TREND SCOUTS        CONTENT CREATORS       QUALITY CONTROL
  Monitor web    ->   Write posts      ->   Score & refine
  Track influencers   Match voice            Check brand alignment
  Surface topics      Apply frameworks       Enforce CTA rules

                  PUBLISHING TEAM           ANALYTICS
                    Queue approved   <->   Track performance
                    Auto-post                Feedback loop
                    Retry failures           Optimize
```

**The daily cycle:**

1. **5:30 AM** - Trend scouts scan web sources, influencer feeds, and news
2. **6:00 AM** - Content creators draft posts using trends + your voice config
3. **6:30 AM** - Quality control scores, refines, and queues content
4. **7:00 AM** - Dashboard email digest sent for your review
5. **7:30 AM** - Approved content auto-posts to LinkedIn (or waits for manual approval)
6. **Ongoing** - Analytics track performance and feed back into the system

---

## The Swipe File Library

LinkedIn Autopilot ships with a 28MB curated library of copywriting patterns, hooks, frameworks, and structures from 9 legendary direct-response copywriters:

| Copywriter | What the Agents Learn |
|---|---|
| Alex Hormozi | Value stacking, grand slam offers, lead magnets |
| Gary Halbert | Direct response, urgency, storytelling |
| David Ogilvy | Headlines, brand voice, long-form persuasion |
| Evaldo Albuquerque | Big idea development, belief shifting |
| George Ten | Fascinations, hooks, curiosity gaps |
| Justin Welsh | LinkedIn-native growth, solopreneur systems |
| Dickie Bush | Atomic essays, frameworks, consistency |
| Nicolas Cole | Category design, digital writing |
| Dan Koe | One-person business philosophy |

The agents do not copy these writers. They study the underlying patterns and apply them to your voice and your topics.

---

## Features at a Glance

| Feature | Required API Key | Without It |
|---|---|---|
| AI content generation | Anthropic (required) | N/A |
| Web trend scouting | Serper (optional) | Uses LinkedIn-only trends |
| Influencer monitoring | None | Always active |
| Auto-posting to LinkedIn | PhantomBuster (optional) | Manual posting via dashboard |
| Email digests | Resend (optional) | Dashboard-only review |
| Embedding-based dedup | OpenAI (optional) | Basic text similarity |
| Content dashboard | None | Always active |

---

## Configuration

The setup wizard (`python setup.py`) generates all config files automatically. You can also create them manually using the examples in `config_examples/`.

| File | Purpose |
|---|---|
| `config/business.yaml` | Business identity, voice, positioning, case studies |
| `config/content_calendar.yaml` | Schedule, formats, posting slots |
| `config/influencers.yaml` | Who to monitor for content inspiration |
| `config/trend_sources.yaml` | Web queries and scrape targets |
| `.env` | API keys and secrets (never committed) |

See `config_examples/` for fully documented example files with comments explaining every field.

---

## Industry Presets

The setup wizard includes 7 industry presets that pre-configure content themes, influencer lists, trend queries, and tone defaults:

| Preset | Best For |
|---|---|
| **SaaS / Tech Founder** | Software companies, developer tools, B2B tech |
| **Agency Owner** | Marketing agencies, creative shops, consultancies |
| **Coach / Consultant** | Executive coaches, business consultants, trainers |
| **Realtor** | Real estate agents, investors, property managers |
| **E-commerce / DTC** | Online stores, direct-to-consumer brands, Shopify |
| **Freelancer / Creator** | Solo practitioners, content creators, writers |
| **Custom / Other** | General business (fully customizable) |

Each preset includes curated influencer lists, search queries, sample case studies, and tone recommendations specific to that industry.

---

## API Keys Guide

| Key | Provider | What It Enables | Required? |
|---|---|---|---|
| `ANTHROPIC_API_KEY` | [Anthropic](https://console.anthropic.com/) | All AI content generation | Yes |
| `OPENAI_API_KEY` | [OpenAI](https://platform.openai.com/) | Embedding-based deduplication | No |
| `SERPER_API_KEY` | [Serper](https://serper.dev/) | Web search for trend scouting | No |
| `RESEND_API_KEY` | [Resend](https://resend.com/) | Email digest delivery | No |
| `PHANTOMBUSTER_API_KEY` | [PhantomBuster](https://phantombuster.com/) | Auto-posting to LinkedIn | No |
| `LINKEDIN_PHANTOM_ID` | PhantomBuster | Specific phantom for posting | No |

LinkedIn Autopilot works with just the Anthropic key. Every other integration is optional and gracefully degrades.

---

## Architecture

```
linkedin-autopilot/
├── setup.py                    # Setup wizard entry point
├── setup/
│   ├── wizard.py               # Interactive configuration wizard
│   ├── validators.py           # Input validation helpers
│   └── industry_presets/       # 7 industry YAML presets
├── config/                     # Generated config (gitignored)
│   ├── business.yaml
│   ├── content_calendar.yaml
│   ├── influencers.yaml
│   └── trend_sources.yaml
├── config_examples/            # Documented example configs
├── linkedin_autopilot/
│   ├── main.py                 # Pipeline orchestrator
│   ├── agents/                 # 37 specialized agents
│   ├── teams/                  # 5 agent teams
│   │   ├── trend_scouts/       # Web + influencer monitoring
│   │   ├── content_creators/   # Writing + formatting
│   │   ├── quality_control/    # Scoring + refinement
│   │   ├── publishing/         # Queue + auto-post
│   │   └── analytics/          # Performance tracking
│   └── swipe_library/          # 28MB copywriter pattern library
├── tools/
│   ├── dashboard.py            # Web-based content review
│   ├── posting_queue.py        # Publication queue
│   └── auto_poster.py          # PhantomBuster integration
├── prompts/                    # Agent system prompts
├── docker-compose.yml
├── Dockerfile
├── requirements.txt
└── .env                        # API keys (gitignored)
```

**5 Agent Teams:**

1. **Trend Scouts** (8 agents) - Monitor the web, track influencers, surface relevant topics
2. **Content Creators** (12 agents) - Write posts, articles, carousels, and newsletters
3. **Quality Control** (7 agents) - Score content, check brand alignment, refine copy
4. **Publishing** (5 agents) - Manage the queue, handle scheduling, execute posting
5. **Analytics** (5 agents) - Track engagement, identify patterns, optimize strategy

---

## Dashboard

The built-in dashboard provides:

- Content queue with approve/edit/reject workflow
- Post preview with formatting
- Performance metrics (when analytics are connected)
- Schedule overview
- Agent activity log

Access it at `http://localhost:8080` (or your configured port) after starting the pipeline.

---

## Deployment

**Local development:**
```bash
python -m linkedin_autopilot.main
```

**Docker (production):**
```bash
docker-compose up -d
```

**Server deployment:**
```bash
# Uses systemd service
sudo systemctl start linkedin-autopilot
sudo systemctl enable linkedin-autopilot
```

---

## License

MIT License. See [LICENSE](LICENSE) for details.

---

**Built for people who would rather build their business than spend 2 hours a day writing LinkedIn posts.**
