# Darkroom rename: name research

26 October 2026. Why rename: "Darkroom" is Bergen Co.'s photo editor (29k ratings) and The Darkroom Lab's film app, and a competing vault is already called "Photo Vault - Darkbox". The site cannot rank on its own brand name.

Method: searches of apps.apple.com and play.google.com for each name, then a wider web search for companies, products, domains and trademarks. Direct App Store, Play, WHOIS and USPTO lookups were blocked by this environment's network policy, so the last step (below) still has to be done by hand.

Brief: keep the darkroom / film-developing world the app already uses (frames, develop, fixer tray, contact sheet), short, ownable, works as "<Name>: Private Photo Vault".

## Shortlist (no app, company or product found)

| Name | Meaning | App Store | Play | Web / brands | Notes |
|---|---|---|---|---|---|
| **Unexposed** | Film that has never seen light: photos nobody has seen | none | none | none (only a `juju unexpose` CLI command) | Strongest: one word, film term and privacy promise at once |
| **Keep Dark** | What you do with undeveloped film | none (closest: "Keep Black", an Apple TV screen dimmer) | none | none | Friendly, imperative; two words |
| **Lightsafe** | Darkroom term for light-tight containers | none | none | none (closest: LiveSafe, LinkSafe) | Clear "safe" signal for search |
| **Blackslide** | The slide that protects a film holder from light | none | none | none (closest: BLACKSLATE7 clapperboard app) | Ties to the slide-to-draw pattern |

## Rejected (taken)

| Name | Taken by |
|---|---|
| Safelight | Safelight: Darkroom Timer; Safelight Project; Safelight Imaging |
| Latent | Latent: Pro Camera Studio; Latent Roll; Latent Studio; Latente |
| Darkslide | DarkSlide Skateboard Tricks (App Store) |
| Lightproof | LibreOffice's Lightproof grammar checker |
| Stop Bath | an App Store developer account named "Stop Bath" |
| Silverbox | SilverBox (Play); Silver Box KTV app |
| Shadowbox | ShadowBox apps (App Store and Play) |
| Undeveloped, Boltplate | clear, but weak as brands |

## Before committing to a name (must do by hand)

1. App Store Connect → My Apps → New App: type the exact name. It is rejected if another developer holds it.
2. Domains: `<name>.app` / `.com` / `get<name>.com` at a registrar (Cloudflare Registrar, since the site is on Cloudflare).
3. Trademarks: USPTO Trademark Search (classes 9 and 42), EUIPO eSearch, UK IPO. Search the exact word and close spellings.
4. Handles: X, Instagram, TikTok, GitHub.
