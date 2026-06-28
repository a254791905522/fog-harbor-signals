# Shrouded Harbor Signals - Gameplay Fact Card

## App Identity
- **App Name**: Shrouded Harbor Signals
- **Bundle ID**: com.rosewood.fogharbor.game
- **Version**: 1.0
- **Platform**: iOS (iPhone only)
- **Minimum iOS**: 15.0
- **Framework**: SpriteKit + Objective-C
- **Orientation**: Portrait only
- **Age Rating**: 4+
- **Network**: Fully offline, no ads, no IAP, no analytics, no tracking

## Core Gameplay Loop
1. A shift begins at a lighthouse station with a set duration (60-120 seconds).
2. Ships approach the harbor one by one (or simultaneously in later levels).
3. Player taps a ship to focus on it; the ship's name, type, and intent are displayed.
4. Player reads the intent (Inbound, Outbound, Anchorage, Distress, Unknown) and taps the matching signal button.
5. If the signal is correct, the ship is guided successfully. If wrong or timed out, a mistake is recorded.
6. Shift ends when all required ships are guided (pass) or mistakes exceed the limit (fail).

## Ships and Signals
**Ship Types** (8): Fishing, Cargo, Tanker, Passenger, Sail, Steam, Naval, Rescue.

**Ship Intents** (5): Unknown, Inbound, Outbound, Anchorage, Distress.

**Signal Buttons** (6): Foghorn, Lamp, Flag, Ack, Warn, SOS.

**Correct Response Mapping** (from FHLevelManager.m):
| Ship Intent | Correct Signal |
|---|---|
| Inbound | Lamp |
| Outbound | Foghorn |
| Anchorage | Flag |
| Distress | SOS |
| Unknown | Ack |
| Danger ship + bad weather + level >= 6 | Warn |

## Level Progression
- **Total Levels**: 50 (5 stations x 10 levels each)
- **Stations**:
  1. Portland Head (Levels 1-10, 1930s) - Foghorn + Lamp, no radar
  2. Boston Harbor (Levels 11-20, 1940s) - Foghorn + Lamp, no radar
  3. Cape Cod (Levels 21-30, 1950s) - Foghorn + Lamp + Radar
  4. Sandy Hook (Levels 31-40, 1950s) - Foghorn + Lamp + Radar
  5. Cape Ray (Levels 41-50, 1960s) - Foghorn + Lamp + Radar
- **Unlock**: Linear; completing level N unlocks level N+1 (stored in NSUserDefaults key `fh_levelProgress`).
- **Tutorials**: Levels 1-3 are tutorials with hint text teaching each signal type.

## Difficulty Scaling
- **Shift Duration**: 60s (level 1) to 120s (level 10), increasing with station progress.
- **Ships to Guide**: 2 (tutorial) to 5 (advanced).
- **Max Mistakes**: 0 (tutorials) to 3 (advanced).
- **Weather**: Fog -> HeavyRain -> Thunder -> Blizzard, worsening visibility radius (0.35 -> 0.10).
- **Wind Speed**: 2 to 15, increasing ship approach speed.
- **Signal Unlocks**: Lamp (always) -> Foghorn (L2+) -> Flag (L3+) -> Ack (L4+) -> Warn (L6+) -> SOS (L9+).

## Scoring
- No numerical score or star rating system.
- Pass condition: shipsGuided >= shipsToGuide AND mistakes <= maxAllowedMistakes.
- Result panel shows: "Ships guided: X / Y" and "Mistakes: X / Y".

## Game Mechanics
- **Patience Timer**: Each ship has a patience countdown (25s - i*3s). Expires = mistake.
- **Weather Visibility**: Fog (0.35), HeavyRain (0.20), Thunder (0.15), Blizzard (0.10) radius.
- **Radar**: Unlocks at Cape Cod (level 21+). Shows rotating scan line on screen.
- **Morse Code**: Each signal writes to a morse input buffer displayed in HUD.
- **Feedback**: Instant text feedback ("Correct", "Wrong message", "Time out").

## Monetization
- None. No ads, no in-app purchases, no subscriptions.

## Data Collection
- None. All progress saved locally via NSUserDefaults.

## Template Residue Check
- No tw_*, game_01_*, Template, or other template residue found.
- FHPhysicsCategories.h (crane game residue) was deleted as unused.

## Debug UI
- showsFPS = NO
- showsNodeCount = NO
