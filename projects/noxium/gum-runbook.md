# gum runbook for Noxium

[gum](https://github.com/ehmo/gum) (v2.3.1) is a CLI and MCP server for Google APIs. For Noxium it replaces the guesswork in `aso.md` and `SEO-PLAYBOOK.md` with real Google data:

| Need | gum operation | Auth |
|---|---|---|
| Real search volumes for the keyword backlog and ASO seed terms | `googleads.keywordPlanIdeas.generateKeywordHistoricalMetrics` | Google Ads OAuth; Cloud project needs Basic access |
| New keyword ideas from a seed list or a page URL | `googleads.keywordPlanIdeas.generateKeywordIdeas` | same |
| Queries, clicks, CTR, position by page (the Thursday refresh) | `searchconsole.searchanalytics.query` | Search Console OAuth |
| Is a new guide indexed? | `searchconsole.urlInspection.index.inspect` | same |
| Sitemap status | `searchconsole.sitemaps.list` / `.get` | same |

gum does **not** cover the App Store (Apple has no Google API). For ASO it gives Google web volumes as a proxy for which words people use; confirm App Store popularity with Apple Ads keyword suggestions.

The argument shapes below were validated against the v2.3.1 schema (they get as far as the auth check). They haven't been run against real accounts yet.

## One-time setup (on your Mac, not in a cloud session)

gum logs in through a browser and keeps tokens in the macOS keychain, so it runs where you are.

Run these one line at a time. Use `ehmo/tap/gum`, not plain `gum`, which is Charm's unrelated tool. The dry run prints the files setup would write; the second setup line gives Claude Code the gum skill and MCP server.

```bash
brew tap ehmo/tap https://github.com/ehmo/homebrew-tap
brew install ehmo/tap/gum
gum setup --target claude --features skills,mcp --dry-run
gum setup --target claude --features skills,mcp --yes
```

Google Cloud (one project, e.g. "noxium-marketing"):
1. Enable **Search Console API** and **Google Ads API**.
2. OAuth consent screen: testing mode, add your Google account as a test user.
3. Create an OAuth client, type **Desktop app**.

```bash
printf '%s' "$GOOGLE_OAUTH_CLIENT_SECRET" | gum auth use-oauth-client --client-id "$GOOGLE_OAUTH_CLIENT_ID" --secret-stdin
gum login --service searchconsole
gum read searchconsole.sites.list
```

The last line should list `sc-domain:getnoxium.app`.

Keyword Planner needs a Google Ads account (no spend required) and **Basic access for the Google Cloud project** that owns the OAuth client. Since September 2026 Google grants Google Ads API access per Cloud project, not per developer token: request it in Google Cloud Console → Google Ads API → overview page (the old API Center "Apply for Basic Access" link now opens a form that is only for the App Conversion Tracking API). New Basic applications need the project's OAuth brand verified first. Until access is granted, calls fail with "only approved for use with test accounts"; use the Keyword Planner export in the Google Ads web UI meanwhile.

gum 2.3.1 still asks for a developer token. Google now ignores the token header, but gum may refuse to call without one, so store the one you have:

```bash
printf '%s' "$GOOGLE_ADS_DEVELOPER_TOKEN" | gum auth use-ads-developer-token --stdin
gum login --service googleads
gum config set googleads.customer_id=<10-digit Ads customer id>
gum config set googleads.geo_target_constants=2840
gum config set googleads.language=1000
gum doctor
```

2840 is the United States and 1000 is English. Without these defaults, Keyword Planner returns worldwide, all-language numbers that look like US numbers. Keep them set.

Never paste the client secret or developer token into a chat; use stdin as above.

## 1. Keyword volumes for ASO and the backlog (do now, before the ASO metadata is final)

```bash
gum read googleads.keywordPlanIdeas.generateKeywordHistoricalMetrics --args '{
  "keywords": ["photo vault","private photo vault","hide photos","hidden photos","secret photo album",
               "photo locker","hidden album","lock photos","calculator vault","decoy vault",
               "hide pictures","hide videos iphone","password protect photos","encrypted photo vault",
               "photo vault app","secure photo album","private album","hidden gallery"]
}' --output csv > keyword-volumes-$(date +%F).csv
```

Then ideas from the site itself:

```bash
gum read googleads.keywordPlanIdeas.generateKeywordIdeas --args '{"url":"https://getnoxium.app/","pageSize":200}' --output csv > keyword-ideas-home.csv
gum read googleads.keywordPlanIdeas.generateKeywordIdeas --args '{"keywords":["photo vault","hide photos iphone"],"pageSize":200}' --output csv > keyword-ideas-seed.csv
```

Use the results to:
- Rank the words in the `aso.md` keyword field; swap out words with no volume.
- Pick between subtitle A ("Hide Pictures…") and B ("Hide Pics & Videos…").
- Add rows to the keyword backlog (`SEO-PLAYBOOK.md` §10) with the monthly volume in the row.

Keep the CSVs out of the website repo (or add them to `.assetsignore`), since everything in that folder is public.

## 2. Weekly: Search Console pull (Thursday refresh, `SEO-PLAYBOOK.md` §6)

```bash
gum read searchconsole.searchanalytics.query --args '{
  "siteUrl": "sc-domain:getnoxium.app",
  "body": {"startDate": "<28 days ago>", "endDate": "<yesterday>", "dimensions": ["query","page"], "rowLimit": 1000}
}' --output csv > gsc-$(date +%F).csv
```

Look for pages with impressions but position 5–20 (the refresh candidates), and queries the site ranks for that have no dedicated guide (new backlog rows).

## 3. After publishing a guide (`SEO-PLAYBOOK.md` §9, step 10)

```bash
gum read searchconsole.urlInspection.index.inspect --args '{
  "body": {"inspectionUrl": "https://getnoxium.app/guides/<slug>", "siteUrl": "sc-domain:getnoxium.app"}
}' --output json
```

This only *checks* indexing status; requesting indexing is still the button in Search Console. Don't use gum's `indexing.urlNotifications.publish` for guides: Google limits the Indexing API to job-posting and livestream pages. `tools/indexnow.py` stays the way to ping Bing.

## 4. With Claude Code

After `gum setup --target claude`, ask Claude Code in the website repo things like "pull last 28 days of Search Console for getnoxium.app and list refresh candidates" or "get US volumes for the backlog keywords". It goes through the gum MCP server with the same safety gates: reads run freely, writes need `--allow-write`, deletes need a confirmation token.
