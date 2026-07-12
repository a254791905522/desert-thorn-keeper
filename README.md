# Desert Thorn Keeper

## Overview
Desert Thorn Keeper is a calm, offline cactus care puzzle built with SpriteKit + Objective-C. Tend 50 thorny friends across five cactus families, read symptom events, and choose the matching care action to bloom each plant.

- **Bundle ID**: com.rosewood.desertthornkeeper.game
- **Version**: 1.0
- **Device Support**: iPhone only (iOS 15.0+)
- **Orientation**: Portrait
- **Age Rating**: 4+
- **Network**: Fully offline, no ads, no IAP, no analytics, no tracking

## Gameplay Summary
- 50 levels with linear difficulty scaling
- 5 cactus families (Barrel, Prickly Pear, Moon, Saguaro, Holiday), each with unique optimal ranges
- 6 care actions: Water +5/+15/+25, Fertilizer, Drain, Pest Care
- 10 symptom event types, each with a family-specific correct action
- Tutorial levels (1-3) show care hints; levels 4+ describe symptoms only
- Win condition: growth reaches 100% with health above zero
- Progress saved locally via NSUserDefaults (`CactusGrowProgress`)

## Screenshot Sets
- `screenshots_65/` — 1284x2778 (6.5" display), 5 screenshots, JPEG
- `screenshots_55/` — 1242x2208 (5.5" display), 5 screenshots, JPEG

## Release Files
- `index.html` — Landing page (Support URL)
- `privacy.html` — Privacy Policy page
- `keywords.txt` — App Store keywords (92 chars)
- `GAMEPLAY_FACT_CARD.md` — Source-based gameplay reference
- `PUBLISH_CHECKLIST.md` — Release checklist
- `appstore-review-text.html` — App Store metadata (Format 3)
- `README.md` — This file
- `vercel.json` — Vercel config (cleanUrls=false)
- `.gitignore` — Ignores .vercel

## Deploy
- **Vercel URL**: https://desert-thorn-keeper.vercel.app
- **Privacy URL**: https://desert-thorn-keeper.vercel.app/privacy.html
