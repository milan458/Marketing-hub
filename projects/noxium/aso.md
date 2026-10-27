# Noxium: App Store optimization (ASO)

Draft, 27 October 2026. Facts come from `darkroom-website/site.json`. Nothing here has been checked against real search-volume data yet. Before submitting, pull Google volumes for the candidate words with gum ([gum-runbook.md](./gum-runbook.md) §1) and check App Store popularity with Apple Ads keyword suggestions.

## 1. What Apple searches

| Field | Limit | Indexed for search? | Notes |
|---|---|---|---|
| App name | 30 | Yes, strongest | |
| Subtitle | 30 | Yes | |
| Keyword field | 100 | Yes | Comma-separated, no spaces. Don't repeat words from the name or subtitle; Apple combines words across fields |
| Screenshot captions | n/a | Reported yes since mid-2025 (OCR), weaker than the name | Third-party reports, not Apple documentation |
| In-app purchase names, developer name | | Yes | |
| Promotional text (170), description | | No (App Store) | Write them for people, not for ranking |
| Custom product pages | up to 70 | Can replace the default page for keywords you assign | Keywords must come from the keyword field, not name/subtitle |

Apple's App Review Guideline 2.3.7: no competitor app names or trademarks in metadata. So "Keepsafe", "Private Photo Vault" (as a brand) etc. stay out of keywords; the website guides cover those searches instead.

## 2. Metadata draft (US English)

**Name** (27/30): `Noxium: Private Photo Vault`

**Subtitle**, two options to test (product page optimization can't test text, so pick one, then compare search impressions after 4 weeks):
- A (30/30): `Hide Pictures, Encrypted Album`
- B (29/30): `Hide Pics & Videos, Encrypted`

**Keyword field** with subtitle A (98/100):
```
secret,hidden,locker,lock,safe,gallery,video,decoy,calculator,secure,keep,pattern,password,lockbox
```
Why these: "hidden", "secret", "locker", "lock", "safe", "gallery" form the common vault phrases ("secret photo album", "photo locker", "hidden gallery") together with "photo"/"album" from the name and subtitle. "decoy", "calculator" and "pattern" are real features (decoy vault; Calculator lookalike icon is Pro). "password" catches "password protect photos". If subtitle B wins, swap `video` for `album,pictures` and drop `lockbox`.

**Extra locale for the US store:** the US store is widely reported to also index the Spanish (Mexico) localization. Add a Spanish (Mexico) localization with *different* English words in its keyword field (e.g. `iphone,ipad,pics,encryption,albums,stash,conceal,protect,personal,lockscreen`) only if the Spanish name/subtitle still read naturally. Verify this behavior before relying on it.

**Promotional text** (not indexed, editable without review), launch version:
> New: Noxium is the new name for Darkroom. Photos only you can see, encrypted on your iPhone and backed up to your own iCloud.

**In-app purchase display names:** `Noxium Pro Monthly`, `Noxium Pro Yearly`, `Noxium Pro Lifetime` (already in `site.json`). Leave them plain.

## 3. Screenshots (the conversion lever)

Most visitors decide from the first three. One promise per shot, caption at the top, in the App Store voice. Captions double as weak keywords, so use the words people search.

| # | Caption | Shows |
|---|---|---|
| 1 | Hide photos behind a pattern only you know | The bolt plate with a pattern drawn |
| 2 | Encrypted on your iPhone. Not even we can see them | Vault grid |
| 3 | Moves to your new iPhone. Draw your pattern, it's back | Restore screen |
| 4 | A decoy vault for when someone's watching | Second pattern opening a harmless vault |
| 5 | No ads. No account. Data Not Collected | Privacy label / settings |
| 6 | Hide videos and Live Photos in full quality | Video in vault |
| 7 | Free for 150 photos. Pro when you need more | Plans |

Check each claim against `site.json` facts before export. Test order 1–3 with **Product Page Optimization** (App Store Connect → Product Page Optimization) once there's enough traffic (a few thousand page views per variant).

## 4. Custom product pages (after launch)

Build three, each with keywords assigned from the keyword field and matching campaign links from the website:
1. **Decoy** (keywords: decoy, secret): screenshot 4 first. Link from `/guides/what-is-a-decoy-vault`.
2. **Calculator / hidden icon** (keywords: calculator, hidden): Pro icon shots first. Link from the planned `/guides/calculator-vault-apps`.
3. **New iPhone** (keywords: safe, secure): restore shot first. Link from `/guides/move-photo-vault-to-new-iphone`.

## 5. Ratings and reviews

- Ask with `RequestReviewAction` / `SKStoreReviewController` after a moment of success (e.g. first successful restore, or the 20th photo imported), never at first launch or after an error. Apple caps it at 3 prompts a year.
- Reply to every review in App Store Connect in the first months, especially 1★ about lost patterns: point to the recovery phrase.
- Never incentivize reviews (guideline 5.6.1 territory). No `aggregateRating` on the website until real ratings exist.

## 6. Monthly ASO routine (first Monday, with the SEO monthly)

1. App Store Connect → App Analytics: impressions from Search vs Browse, page views, conversion rate.
2. Apple Ads (even with a tiny budget) → search terms report: which real queries show the app. Move winners into the keyword field; drop words with no impressions.
3. Update the keyword field only with an app update (it ships with a version).
4. Log changes below with the date so effects can be read 4 weeks later.

| Date | Field | Change | Result after 4 weeks |
|---|---|---|---|
| | | | |
