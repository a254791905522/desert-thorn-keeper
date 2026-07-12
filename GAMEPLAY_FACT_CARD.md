# Desert Thorn Keeper - Gameplay Fact Card

## App Identity
- **App Name**: Desert Thorn Keeper
- **Bundle ID**: com.rosewood.desertthornkeeper.game
- **Version**: 1.0
- **Platform**: iOS (iPhone only)
- **Minimum iOS**: 15.0
- **Framework**: SpriteKit + Objective-C
- **Orientation**: Portrait only
- **Age Rating**: 4+
- **Network**: Fully offline, no ads, no IAP, no analytics, no tracking
- **Product Name**: DesertThornKeeper (Xcode target: CactusGrow)

## Core Gameplay Loop
1. Player starts a level from the main menu or level select screen (50 levels total).
2. A potted cactus from one of five families is presented with health=100, growth=0, and resource values (water, nutrient, pest, sun, wind) initialized to family-specific ranges.
3. Growth progress fills automatically over time based on the level's time limit (60s at L1, 180s at L50, linear interpolation).
4. The cactus cycles through five growth stages: Root Check -> Soil Balance -> Growth Prep -> Plant Inspection -> Bloom Push. Each stage lasts 3.2-4.4 seconds depending on difficulty.
5. From the Growth Prep stage onward, symptom events trigger randomly. Each symptom has one correct care action that depends on the cactus family.
6. The player taps one of six care buttons: Water +5, Water +15, Water +25, Fertilizer, Drain Soil, Pest Care.
7. A correct action during an event restores health and advances the cycle. A wrong action during an event ends the level immediately.
8. Health drains continuously while a symptom event is active. If health reaches zero or the event timer expires, the level fails.
9. Victory occurs when growth progress reaches 100% AND health is above zero. Progress is saved and the next level unlocks.

## Cactus Families (5 families, cycle by `(level-1) % 5`)

| Family | optimalWater | optimalSun | optimalWindMax | growthRate | waterDrain | sunDrift | windDrift |
|--------|-------------|-----------|---------------|-----------|-----------|---------|----------|
| Barrel Cactus | 1.0 - 10.0 | 58.0 - 92.0 | 78.0 | 4.8 | 0.42 | 1.15 | 0.58 |
| Prickly Pear | 8.0 - 24.0 | 44.0 - 82.0 | 68.0 | 4.4 | 0.52 | 0.92 | 0.72 |
| Moon Cactus | 16.0 - 34.0 | 30.0 - 62.0 | 54.0 | 4.0 | 0.60 | 1.05 | 0.86 |
| Saguaro Sprout | 4.0 - 16.0 | 64.0 - 96.0 | 62.0 | 4.2 | 0.46 | 1.24 | 0.78 |
| Holiday Cactus | 22.0 - 42.0 | 24.0 - 58.0 | 48.0 | 3.9 | 0.68 | 0.76 | 0.92 |

**Difficulty scaling** (`difficulty = MIN(1.0, (level-1)/49.0)`):
- growthRate += difficulty * 0.6
- waterDrainRate += difficulty * 0.18
- windDriftRate += difficulty * 0.20

## Care Actions (6 buttons)

| Action | Display Name | Effect |
|--------|-------------|--------|
| water_5 | Water +5 | water = MIN(100, water + 5) |
| water_15 | Water +15 | water = MIN(100, water + 15) |
| water_25 | Water +25 | water = MIN(100, water + 25) |
| fertilizer | Fertilizer | nutrient = MIN(100, nutrient + 24) |
| drain | Drain Soil | water = MAX(0, water - 12) |
| pest | Pest Care | pestPressure = MAX(0, pestPressure - 32) |

## Symptom Events (10 event types)

Each event has a family-specific correct action. Events trigger from the Growth Prep stage onward.

| Event | Title | Message |
|-------|-------|---------|
| mild_dry | Heat Wrinkle | Ribs look tighter and the skin has lost its usual gloss. |
| deep_wilt | Deep Wilt | Lower ribs fold inward and the pot feels unusually light. |
| soil_crust | Crusted Soil | The soil pulls from the pot edge and looks hard across the top. |
| wet_base | Wet Foot | The surface stays shiny and a damp ring forms under the pot. |
| pale_crown | Pale Crown | New growth is yellow-green and the crown has stopped pushing. |
| bud_stall | Bud Stall | A tiny bud holds its shape for days without opening. |
| scar_specks | Scar Specks | Tiny marks spread around the areoles and young spines. |
| soft_base | Soft Base | The lower stem looks darker and the base feels too soft. |
| sun_blotch | Sun Blotch | A pale patch appears on the sun-facing side after a bright spell. |
| wind_scuff | Wind Scuff | Fine dusty scratches gather on the wind-facing ribs. |

## Level Progression
- **Total Levels**: 50 (5 pages x 10 levels per page in level select)
- **Tutorial Levels**: 1-3 (display the correct care hint during symptom events)
- **Normal Levels**: 4+ (describe symptoms only, player must infer the correct action)
- **Level Time Limit**: 60s (L1) to 180s (L50), linear interpolation
- **Cycle Stages**: 5 stages per level (Settle, FirstWater, LightTraining, Airflow, BloomPush)
- **Stage Duration**: MAX(3.2, 4.4 - difficulty) seconds per stage
- **Event Count**: 3 (L1) up to 3-10 (L50), formula: `3 + (level-1)*7/49`
- **Initial Event Delay**: 11-16s (L1) to 2.5-5s (L50)
- **Event Duration**: 3.0-5.0 seconds
- **Cycle Patterns**: 5 patterns (selected by `(level-4) % 5` for L4+), L1-3 use Pattern 0

## Scoring System
- **No stars, no coins**. The game uses a binary win/lose outcome.
- **Win Condition**: growthProgress >= 100.0 AND health > 0.0
- **Growth Progress**: Time-based, `MIN(100, elapsed / growthDuration * 100)`
- **Health Changes**:
  - Correct cycle action: +4.0 (cap 100)
  - Correct event action: +8.0 (min 68, cap 100)
  - Event active: drains at `MAX(12, health) / eventRemaining` per second
  - All safe + no event: +0.45 per second
  - Wrong event action or timeout: health = 0 (level fails)

## Safety Ranges (cactus color changes when unsafe)
- waterIsSafe: optimalWaterMin <= water <= optimalWaterMax
- sunIsSafe: optimalSunMin <= sun <= optimalSunMax
- windIsSafe: wind <= optimalWindMax
- nutrientIsSafe: 45.0 <= nutrient <= 92.0
- pestOK: pestPressure <= 70.0

## Resource Drift (per second, during update)
- water -= (waterDrainRate + sunStress*0.42 + windStress*0.32) * dt
- nutrient -= (0.18 + difficulty*0.08) * dt
- pestPressure += (0.18 + difficulty*0.14 + windStress*0.18) * dt
- sun += sunDriftRate * dt (only increases)
- wind += windDriftRate * dt (only increases)

Note: sun and wind drift upward only and cannot be directly reduced by the player.

## Monetization
- None. No ads, no in-app purchases, no subscriptions.

## Data Collection
- None. All progress saved locally via NSUserDefaults.
- **Progress key**: `CactusGrowProgress` (NSInteger, default 1)
- **Music key**: `CactusGrowMusic` (BOOL, default YES)
- **Sound key**: `CactusGrowSound` (BOOL, default YES)
- **Haptics key**: `CactusGrowHaptics` (BOOL, default YES)

## Template Residue Check
- No tw_*, game_01_*, Template, or other template residue found.
- Cactus part assets (cactus_part_arm/body/flower/pot/root/spines) exist in the asset catalog but are not loaded by code; the game uses a single `cactus_potted` sprite. These are design-phase remnants, not template residue.

## Debug UI
- showsFPS = NO
- showsNodeCount = NO
- prefersStatusBarHidden = YES
- scaleMode = SKSceneScaleModeAspectFill
