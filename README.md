# tajachem
Chemicals Typing Game

A browser typing game where you defeat enemies by typing chemical compound names.
Practice the names of alkanes, alkenes, alkynes, alcohols, and aldehydes while you play.

## Play Online

The game is deployed as a static website with GitHub Pages.

1. Open the repository's GitHub Pages URL.
2. Choose a game mode.
3. Type the chemical name shown on an enemy.

## Controls

- Type the chemical name displayed on an enemy.
- `Enter` or `Space`: Attack
- `Back` button or `Esc`: Return to the mode-selection screen
- An enemy reaching the left edge costs one life.
- The game ends when all three lives are lost.

## Game Modes

### Easy

- 10 waves per level
- Level 1: Alkanes
- Level 2: Alkanes + alkenes
- Level 3: Alkanes + alkenes + alkynes
- Level 4: Alkanes + alkenes + alkynes + alcohols
- Level 5: Alkanes + alkenes + alkynes + alcohols + aldehydes
- Clear the fifth level to finish the game.

### Normal

- 20 waves per level
- Uses the same compound progression as Easy.
- Clear the fifth level to finish the game.

### Hard

- 20 waves per level
- Compound numbers continue across levels instead of resetting.
- Alkanes: 1-100
- Alkenes: 1-80
- Alkynes: 1-60
- Alcohols: 1-40
- Aldehydes: 1-20 in level 5
- Clear the fifth level to finish the game.

## Enemy Colors

| Family | Color |
| --- | --- |
| Alkane | Red |
| Alkene | Orange |
| Alkyne | Yellow |
| Alcohol | Green |
| Aldehyde | Blue |

## Built With

- One standalone HTML file
- CSS embedded in the `<style>` section
- Vanilla JavaScript embedded in the `<script>` section

## Files

- `tajachem.html`: Game source
