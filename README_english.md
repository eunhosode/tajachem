# TAJACHEM

TAJACHEM is a browser-based typing game. Type the names or molecular formulas of organic compounds to defeat enemies approaching from the right side of the screen.

Customize the base rules by combining modes represented by chemist cards. Each card also has a harder Enhanced mode. The current version uses endless progression, with no bosses or level-up items. You keep advancing through levels until you run out of lives.

## Running the Game

Keep `tajachem.html` and the eight chemist images in the same folder. Open `tajachem.html` in your browser to play. No build step is required.

The game uses the Firebase Web SDK and includes Firebase project initialization, Google sign-in, and online leaderboards backed by Firestore. Use the Firebase CLI to deploy to Firebase Hosting.

## How to Play

1. Start without selecting any cards to play by the base rules.
2. Click or tap a chemist card to select its Standard mode. You can combine multiple Standard modes.
3. Press and hold a card for about 0.6 seconds to select its Enhanced mode. Only one Enhanced mode can be active at a time.
4. Select `게임 시작` (Start Game), then type the correct answer for an enemy and fire.
5. You lose one life each time an enemy reaches you. The game ends when you run out of lives.

To select an Enhanced mode with the keyboard, focus the card and press `Shift + Enter` or `Shift + Space`. You can also use the `강화 모드 바로 선택` (Select Enhanced Mode) menu above the cards.

## Controls

- `Enter` or `Space` after typing an answer — Fire
- `Esc` or `모드 선택` (Mode Select) — End the current run and return to the mode selection screen
- `Caps Lock` has no effect on in-game input.
- You can omit spaces and hyphens from compound names.
- Molecular formulas accept both regular and subscript digits.

In Berzelius Mode, use `Shift` for uppercase letters. In Standard mode, type the entire name in uppercase. In Enhanced mode, alternate uppercase and lowercase letters.

## Scoring and Levels

- Earn 5 points for clearing a wave.
- You start with 3 lives.
- Earn one extra life each time you clear a level.
- Enemies' base speed increases with each level.
- The game continues beyond Level 10.

| Level | Waves | Points Required | Starting Score |
| ---: | ---: | ---: | ---: |
| 1 | 10 | 50 | 0 |
| 2 | 20 | 100 | 50 |
| 3 | 30 | 150 | 150 |
| 4 | 30 | 150 | 300 |
| 5 | 40 | 200 | 450 |
| 6 | 40 | 200 | 650 |
| 7 | 50 | 250 | 850 |
| 8 | 50 | 250 | 1,100 |
| 9 | 60 | 300 | 1,350 |
| 10 | 60 | 300 | 1,650 |
| 11 | 70 | 350 | 1,950 |
| 12 | 70 | 350 | 2,300 |

Starting with Levels 11 and 12, each successive pair of levels requires 10 more waves, or 50 more points, per level. Levels 13 and 14 each require 80 waves (400 points), and Levels 15 and 16 each require 90 waves (450 points).

The base speed multiplier for each level is calculated as follows.

```text
1 + (current level - 1) × 0.10 + (current level - 1)² × 0.006
```

## Base Rules

- Each wave spawns one alkane enemy.
- The carbon count resets to 1 at the start of each level.
- Type the English compound name shown on screen in lowercase.
- A new wave spawns every 2.5 seconds, so multiple waves can be on screen at once.

## Game Modes

| Mode | Standard | Enhanced |
| --- | --- | --- |
| Berzelius Mode | Type the entire name in uppercase. | Alternate uppercase and lowercase letters, as in `MeThAnE`. |
| Hofmann Mode | The first wave is methane. Each subsequent wave randomly selects an alkane, alkene, or alkyne. | Each wave randomly selects an ether, amine, or sulfide. |
| Boyle Mode | The arena is about two-thirds of its default width. | The arena is about half of its default width. |
| Nobel Mode | Clearing a wave before it crosses the two-thirds line slows the next wave. Letting it cross speeds up the next wave. | Each time a wave crosses the two-thirds line, a permanent speed increase is added. |
| Lewis Mode | Two enemies spawn per wave. | Three enemies spawn per wave. |
| Curie Mode | An enemy's name is revealed after it passes the halfway point of the arena. | Enemy names stay hidden throughout the game. |
| Lavoisier Mode | Both names and molecular formulas are accepted. Using the same answer format twice in a row spawns one Wound that requires the other format. | Using the same format twice in a row spawns two fast Wounds. If you repeat a format again while any Wound is still active, you lose a life. |
| Mendeleev Mode | The carbon count carries over between levels. | The carbon count carries over between levels. Use the displayed molecular formula to determine and type the compound name. |

The level-based speed multiplier also applies to Wounds in Lavoisier Mode.

### Combining Modes

- You can select multiple Standard modes at once.
- Selecting an Enhanced mode clears all selected Standard modes.
- Enhanced modes cannot be combined with any other mode.
- When Hofmann and Lewis are combined, the first wave contains only one methane enemy. Each subsequent wave contains two enemies from the same compound class.
- Nobel Mode's speed modifier is multiplied by the level-based speed multiplier.

Selecting one of these exact combinations displays its name in the selection summary and on the game screen. The individual modes' effects stack, and each named combination has its own online leaderboard.

| Selected Modes | Display Name |
| --- | --- |
| Berzelius + Boyle | High Pressure Mode |
| Hofmann + Lewis | Molecular Ensemble Mode |
| Berzelius + Boyle + Nobel | Critical Explosion Mode |
| Curie + Mendeleev | Element X Mode |
| Lavoisier + Mendeleev | Periodic Table Mode |

## Sign-In, Unlocks, and Online Leaderboards

- Guests can play with the base rules. Online scores require sign-in.
- A Firestore user document is created automatically the first time you play after signing in with Google.
- Reaching Levels 2 through 9 unlocks one Standard mode per level, starting with Berzelius and ending with Mendeleev.
- Earn a cumulative score of 30,000 points in a Standard mode to unlock its Enhanced version.
- The leaderboard selector lists base and individual Standard modes first, followed by named combinations and then Enhanced modes.
- Base mode, each individual Standard mode, each of the five named combinations, and each individual Enhanced mode have separate online leaderboards.
- You can play unnamed combinations of Standard modes. Scores from those runs do not count toward an online leaderboard.
- Only the highest score for each account and mode is saved.
- The global leaderboard shows the top 10 players. The personal leaderboard shows your best score and global rank for the selected mode.

Firestore uses the following document paths.

```text
users/{uid}
users/{uid}/modeStats/{modeId}
rankings/{modeId}/entries/{uid}
```

To enable saving player records after sign-in, publish `firestore.rules` in the Firestore **Rules** tab of the Firebase Console or deploy it with the Firebase CLI.

## Project Structure

```text
tajachem/
├─ tajachem.html              # Game UI, styles, and game logic
├─ firestore.rules            # Security rules for player records and leaderboards
├─ README.md
├─ Alfred_Nobel.jpg
├─ Antoine_Lavoisier.jpg
├─ August_W_Hofmann.jpg
├─ Dmitri_Mendeleev.jpg
├─ Gilbert_N_Lewis.jpg
├─ Jöns_Jacob_Berzelius.jpg
├─ Marie_Curie.jpg
└─ Robert_Boyle.jpg
```

## Tech Stack

- CSS and vanilla JavaScript in a single HTML file
- Firebase Web SDK 12.19.0 browser modules
- No external game framework or build tools
- Mouse and touch support on desktop and mobile
- Accessible keyboard controls for card selection and status announcements

## Play

Start with [old.html](old.html) for practice.  
Once you're comfortable with the game, try the [hosted version](https://tajachem-5bcac.web.app/).
