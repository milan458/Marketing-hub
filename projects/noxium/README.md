# Noxium in the Marketing-hub

Noxium photo vault (iPhone/iPad, formerly Darkroom) is the first product we run through this repo. Website: getnoxium.app (repo `milan458/darkroom-website`). App: version 1.0 submitted to App Store review in October 2026.

| File | What it is |
|---|---|
| [aso.md](./aso.md) | App Store metadata draft (name, subtitle, keywords, screenshots, custom product pages, ratings) |
| [launch-plan.md](./launch-plan.md) | Launch timeline from now to day 90, channel by channel |
| [naming-research.md](../darkroom/naming-research.md) | How the name Noxium was picked |

## What this repo is (and isn't) good for

It's a library of about 2,400 copy-paste prompts (forked from AiCMO's Marketing Prompt Collection). About 1,800 of them are written for B2B SaaS: pipelines, ICPs by job title, sales enablement. None cover ASO or a consumer iOS launch. Use the prompts as **checklists and frameworks**, not as sources of truth:

- Swap B2B words for ours: "buyer" → "iPhone user worried about private photos", "pipeline" → "installs", "ICP job title" → the person and the moment ("just got a new iPhone", "kid borrows my phone").
- Several prompts ask the model to *predict* AI citations, search volumes or "estimated lift". Those numbers are guesses. Measure for real instead (Search Console, App Store Connect, the monthly AI visibility log in `SEO-PLAYBOOK.md` §12).
- Anything a prompt produces for the website still follows the website's `CLAUDE.md`: facts from `site.json`, no invented ratings or testimonials, competitor claims dated and sourced.

## Prompts worth running for Noxium

**GEO (AI answer engines)**
- `03_Content-&-Creative/GEO-AIO-GEN-AI-Optimization/AI-Chatbot-Citation-Share-Of-Voice-Testing-Engine.md`: use Step 1 only to build the monthly question set; then ask the real engines and log results in `SEO-PLAYBOOK.md` §12.
- `03_Content-&-Creative/GEO-AIO-GEN-AI-Optimization/GEO-Content-Optimizer.md`: run on an existing guide before the Thursday refresh.
- `03_Content-&-Creative/GEO-AIO-GEN-AI-Optimization/Structured-Data-Schema-Markup-&-AI-Parsing-Intelligence-Engine.md`: audit against what `tools/build.py` already emits (MobileApplication, FAQPage, Article, BreadcrumbList).
- `03_Content-&-Creative/GEO-AIO-GEN-AI-Optimization/AI-Powered-LLM-Brand-Monitoring-&-Reputation-Intelligence-Engine.md`: after launch, to watch whether engines still confuse Noxium with Darkroom (Bergen Co.).

**SEO**
- `05_Analytics-&-Performance/SEO-&-Organic-Performance-Analytics/Keyword-Research-&-Search-Intent-Mapping-Intelligence-Engine.md`: feeds the keyword backlog (`SEO-PLAYBOOK.md` §10). Verify volumes in a real tool.
- `02_Product-Marketing/Positioning-&-Messaging/Competitive-Comparison-Page-&-SEO-Displacement-Intelligence-Engine.md`: structure for the next "X vs Y" and "X alternatives" guides.
- `03_Content-&-Creative/GEO-AIO-GEN-AI-Optimization/Topical-Authority-AI-Search-Dominance-Engine.md`: to plan the next cluster (iPad, hidden apps, calculator vaults).

**Positioning and launch**
- `02_Product-Marketing/Positioning-&-Messaging/Jobs-To-Be-Done-Research-&-Messaging-Translation-Engine.md`: feed it competitor 1★ review themes (already counted in `SEO-PLAYBOOK.md` §10).
- `02_Product-Marketing/Positioning-&-Messaging/Message-Testing-Validation.md`: before choosing screenshot captions.
- `02_Product-Marketing/Go-To-Market-Strategy/Product-Launch-Go-To-Market-Blueprint.md`: cross-check `launch-plan.md`.
- `06_Market-Specific-Playbooks/B2C-Marketing/AI-Powered-B2C-Full-Funnel-Brand-Growth-&-Consumer-Acquisition-Intelligence-Engine.md`: the only consumer full-funnel prompt.
- `03_Content-&-Creative/Viral-Content-Ideation-Creation-Transformation/Generate-Viral-Hooks.md`: hooks for short videos of the pattern unlock and decoy vault.
- `03_Content-&-Creative/Press-Release-&-PR/AI-Powered-B2B-Journalist-Pitch-Engineering-&-Earned-Media-Coverage-Intelligence-Engine.md`: adapt for indie-app press pitches.
