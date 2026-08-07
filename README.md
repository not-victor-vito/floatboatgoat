# Float Boat Goat Scorer

A single-page scorer for the five-game extended version of Float Boat Goat. No build step, no dependencies, no backend. Everything lives in `index.html`.

## The games

| Game | Words |
| --- | --- |
| 1 | float / boat / goat |
| 2 | rode / toed / hoed |
| 3 | block / cock / stock |
| 4 | steed / feed / mead |
| 5 | flag / wag / stag |

All five run concurrently and independently.

## How to use it

1. The two players are fixed as **GAV** (orange) and **GIN** (teal). See "Changing the players" below to edit them.
2. When someone calls a word, tap that word on their row. It fills with their colour.
3. Tapped the wrong one? Tap it again to un-claim it. There is no undo history, the toggle is the undo.
4. When a player has all three words in a game, that card is covered by a "wins the round" panel. Tap **Score it** to confirm.
5. Confirming adds 1 to that player's overall total and 1 to their tally for that game, then clears only that game's board. The other four games keep their progress untouched.
6. **Reset everything** at the bottom needs two taps. The first tap arms it and turns it red, the second wipes all scores and boards. It disarms itself after four seconds if you do not follow through.

While a win is waiting to be confirmed, that game's buttons are locked so a bump in the car cannot change the result. The other games stay live.

### Scoring display

- The two big numbers at the top are total rounds won across all five games. The header stays stuck to the top of the screen as you scroll.
- The small orange-blue pair on each game card is that game's own record, player 1 first.

## Important: state is per device

The page holds its state in memory only. That means:

- Opening it on two phones gives you two separate scoreboards that do not talk to each other. Pick one phone as the scorekeeper.
- Reloading the page, or the browser dropping the tab from memory while your phone is locked for a long time, will clear the scores.

If you want the scores to survive a reload, that is a small change to save state into the browser's local storage. Ask and it can be added.

## Hosting it on GitHub Pages

From Windows, in the folder containing `index.html`:

```
git init
git add .
git commit -m "Float Boat Goat scorer"
git branch -M main
git remote add origin https://github.com/YOUR-USERNAME/floatboatgoat.git
git push -u origin main
```

Create the empty `floatboatgoat` repository on GitHub first (public), then on the repo page go to **Settings** > **Pages**, set **Source** to "Deploy from a branch", branch `main`, folder `/ (root)`, and save.

After a minute or two the site is live at:

```
https://YOUR-USERNAME.github.io/floatboatgoat/
```

Send that link to your friend. On an iPhone, Share > Add to Home Screen gives it an icon and opens it without the browser chrome, which leaves more room for the game cards.

### Alternatives if GitHub feels like too much

- Email or message the `index.html` file to yourself and open it from your phone's Files app. Works fully offline, which matters if the drive goes through patchy coverage.
- Drag the file onto [netlify.com/drop](https://app.netlify.com/drop) for an instant public URL with no account required for the first deploy.

## Changing the players

Names are set in one place near the top of the script block in `index.html`:

```js
var NAMES = ['GAV', 'GIN'];
```

Keep them short, three or four characters, since they double as the row tag on every game card.

## The goat art

The goats are hand-drawn inline SVG defined once as a `<symbol id="goat">` near the top of `<body>`, then reused everywhere via `<use href="#goat">`. Nothing is fetched from the internet, so there are no licences to worry about, nothing breaks offline, and it stays crisp at any size. To restyle it, edit the fill colours in that symbol: `#fbf3e4` is the face, `#c8a04a` the horns, `#5b4636` the outline.

## Changing the games

The word sets are defined near the top of the script block in `index.html`:

```js
var GAMES = [
  { words: ['float', 'boat', 'goat'] },
  ...
];
```

Add, remove, or edit entries and the page rebuilds itself around them. Each game needs exactly three words for the win detection to work as written.
