# Noxium: launch plan

Draft, 27 October 2026. Status: version 1.0 is in App Store review; getnoxium.app is in waitlist mode. "L" below is launch day (the day the app goes live). Pick it, don't let it happen: in App Store Connect set the version to **Manually release this version**, so approval and launch are separate.

Goal for the first 90 days: installs from search (App Store and Google), a first base of honest ratings, and Noxium being the name AI engines give for "encrypted photo vault for iPhone with no account". Budget assumption: one developer, near-zero paid spend.

## The one-line story

> Noxium is the new name for Darkroom: a photo vault for iPhone and iPad that opens with a pattern only you know. Encrypted on your device, backed up to your own iCloud, moves to a new iPhone without losing a photo. No ads, no account.

Angles, by audience:
- **Everyday iPhone users:** "Your photos never get lost, even on a new phone." The main complaint in competitor 1★ reviews (lost photos, paywalls, ads) is the hook.
- **Privacy people (r/privacy, Privacy Guides):** no account, Data Not Collected, Argon2id + AES-256-GCM, nobody can reset a pattern. Be ready for "is it open source?" and pattern-entropy questions; answer plainly.
- **Apple press and newsletters:** a Nocturne-designed indie app with a drawable lock, a decoy vault and an emergency-erase pattern.

## Phase 0: before approval (now)

- [ ] Finish the website move (`SEO-PLAYBOOK.md` §1a) and Search Console / Bing setup (§2). Every week the site is indexed before launch helps.
- [ ] Off-site profiles with the one-line sentence (`SEO-PLAYBOOK.md` §3): X, Reddit bio, GitHub, Privacy Guides forum, AlternativeTo (list once live).
- [ ] Final ASO metadata and screenshots (`aso.md`).
- [ ] Press kit page or folder: icon, 5 screenshots, the one-line story, the facts block, founder contact. No quotes from people who didn't say them.
- [ ] Record two 15–30 s screen videos: drawing the pattern to open the vault, and the decoy pattern opening a harmless vault. Usable as App Preview, on X/TikTok/Reels, and in the Product Hunt gallery.
- [ ] Write the Show HN / blog post draft: "How a 5×5 pattern becomes an encryption key" (Argon2id parameters, what's encrypted, what isn't, the threat model from the homepage). Technical honesty is the whole pitch here.

## Phase 1: approval to L (aim for 2–3 weeks)

- [ ] **App Store featuring nomination** (App Store Connect → Featuring → Nominations → App Launch). Apple asks for the planned date at least 3 weeks ahead. No guarantee, but it costs nothing.
- [ ] Consider a **pre-order** if L is more than a week away: the App Store page goes live early, so waitlist links and press can point to it.
- [ ] Pick L on a Tuesday–Thursday. Avoid Apple event weeks and the US Thanksgiving week.
- [ ] Email press 7–10 days before L with an embargo and an offer/promo code for Pro: Apple-focused sites with tips lines, indie-app newsletters, privacy newsletters. Short, personal, one link. Run the journalist-pitch prompt from this repo, then cut it in half.
- [ ] Product Hunt: create the page in advance (maker profile, gallery, first comment written). Launch it on L or L+1, at 00:01 PT.
- [ ] Line up the launch-day email to the waitlist (the site's waitlist list): what changed (the Darkroom → Noxium rename), the App Store link, one request: "if it's useful, a rating helps a lot."

## Phase 2: launch day (L)

1. Release the version in App Store Connect. Wait until the page loads in the US store.
2. Website: in `darkroom-website/site.json` set `"release": "live"`, `"appStoreId"`, `"providerToken"`; build; ask Milan to deploy; run `tools/indexnow.py` (`SEO-PLAYBOOK.md` §1).
3. Send the waitlist email.
4. Post: X thread with the pattern video; Product Hunt; r/iosapps and other subreddits that allow developer posts (read each one's self-promotion rules that day; r/privacy generally doesn't allow it). Always say you're the developer.
5. Show HN with the technical post (L or L+1, a weekday morning US time). Stay in the thread for the first hours and answer everything.
6. Update off-site profiles with the App Store link; list on AlternativeTo.

## Phase 3: weeks 1–4

- **Ratings:** in-app prompt after a success moment (`aso.md` §5). Reply to every review.
- **Apple Ads:** small daily budget for 2–4 weeks on exact match: "noxium", "darkroom vault", and 10–15 category terms ("photo vault", "hide photos", "secret photo album", "photo locker", "private photo vault"). Goal is learning which terms convert, not scale. Stop terms whose cost per install is above what a Pro conversion is worth.
- **Daily answers** (`SEO-PLAYBOOK.md` §4) continue; now a guide link can end with the App Store link where it fits.
- **First update** (1.0.1) within 2–3 weeks: fixes from reviews, plus the first keyword-field revision based on Apple Ads search terms.
- **AI visibility:** run the 7 monthly questions in ChatGPT, Perplexity, Google AI Overviews, Claude and Copilot; log in `SEO-PLAYBOOK.md` §12. Check whether engines mix Noxium up with Bergen Co.'s Darkroom.

## Phase 4: days 30–90

- Custom product pages for decoy, calculator icon and new-iPhone intents (`aso.md` §4).
- Product Page Optimization test of the first screenshot.
- Second content cluster on the site: iPad, hidden apps, calculator vaults (backlog rows 14–16).
- A seasonal moment: new-iPhone season (September) and the holidays are when people move phones and lose vault photos. Plan a "moving your vault to a new iPhone" push for those.
- After 10+ real ratings: consider `aggregateRating` in the site's JSON-LD.
- Post-mortem at day 90 with the numbers below; decide where the next quarter's hours go.

## What to measure

| When | Metric | Where |
|---|---|---|
| Weekly | Impressions, page views, conversion rate (page view → install), by source (Search, Browse, Web referrer, App referrer) | App Store Connect → App Analytics |
| Weekly | Installs by website page and button (`ct` campaign tokens) | App Store Connect → Analytics → Sources → Campaigns |
| Weekly | Free → Pro conversion, trial starts, refunds | App Store Connect → Subscriptions / Sales |
| Weekly | Ratings count and average, crash-free sessions | App Store Connect, Xcode Organizer |
| Monthly | Google/Bing clicks to guides; AI citations | `SEO-PLAYBOOK.md` §8, §12 |

Set targets after week 2 with real data; don't invent them now.

## Rules that apply to every launch asset

- Facts from `site.json` only. If a claim isn't there, check the app code before using it.
- No invented testimonials, ratings, user counts or "as seen in" logos.
- Competitor statements dated and sourced.
- Disclose being the developer every time.
