# Paper Penalties ⚽✏️

A hand-drawn penalty shootout for two phones, based on the paper game we play at home.

The goal is split into 9 boxes. The shooter secretly picks a box, the keeper secretly picks where to dive, and both phones show the kick at the same moment. Everything looks like it was drawn on a page of a school exercise book: pencil lines, crayon colouring, and a cut-out goalie on a lolly stick.

```
+---+---+---+
| 1 | 2 | 3 |
+---+---+---+
| 4 | 5 | 6 |
+---+---+---+
| 7 | 8 | 9 |
+---+---+---+
```

## Play

**▶ https://bezoon5.github.io/Paper-Penalties/** (once GitHub Pages is switched on, see below)

- **Play the computer:** single player on one phone.
- **Two phones:** one phone taps **Host a game** and gets a 4-letter code. The other phone opens the same page, taps **Join a game** and types the code. Both phones need an internet connection to find each other.

Tip: in Safari tap **Share → Add to Home Screen** (or **Install app** in Chrome on Android). The game then gets its own icon and opens full screen.

## Rules

### House rules (default)
- The shooter picks a box from 1 to 9.
- The keeper dives to a side box (1, 4, 7, 3, 6 or 9) or **stays in the middle**.
- A side box saves that exact box only.
- Staying in the middle saves 2, 5 and 8.
- 5 kicks each, finishing early once one side can't catch up. If it's level after 5 each, it goes to sudden death.

### Pro rules (optional tick box)
- **Corners can miss.** Top corners (1, 3) go over or hit the bar 1 time in 4. Bottom corners (7, 9) go wide or hit the post 1 time in 10.
- **Fingertip saves.** A side dive has a 50% chance of tipping away a shot in the box directly above or below it.
- In a two-phone game the host's choice is used, and both phones always get the same result.

Under perfect play, house rules give about 86% goals and Pro rules about 70% (real shootouts are around 75%).

## Teams

| | Penalty takers | Goalkeeper |
|---|---|---|
| **Reds** (host / you vs computer) | Red shirts | Green kit |
| **Blues** (joining phone / computer) | Blue shirts | Yellow kit |

Takers wear shirt numbers 1–11, shuffled for each match.

## Sound

The crowd, whistle, kick, net, horn and victory fanfare are all generated live in the browser with the Web Audio API, so there are no audio files. **Sound** and **crowd** can each be switched off in the game. On iPhone, the silent switch must be off to hear anything.

## How it works

- **One file.** The game is a single `index.html` with no build step: HTML, CSS, SVG drawing and JavaScript.
- **Hand-drawn look.** The pitch, players and scoreboard are SVG drawn in code with wobbly pencil strokes and crayon-scribble fills, so nothing is an image file.
- **Two-phone play:**
  - On GitHub Pages and other ordinary websites, phones connect directly to each other with [PeerJS](https://peerjs.com/) (WebRTC). The free PeerJS cloud server is only used to introduce the two phones.
  - The game picks a connection automatically. Opened as a Claude artifact, it uses Claude's built-in shared-page connection instead.
- **Keeping both phones in step:**
  - Each phone shares only "locked in" until both players have chosen. After that, both picks are revealed.
  - Each phone works out the result itself from the same picks.
  - Pro rules' random misses and fingertip saves come from a dice roll seeded by the game code and kick number, so both phones always roll the same.

## Running it yourself

Any static web server works. Locally:

```bash
python3 -m http.server 8000
# then open http://localhost:8000
```

To test two-phone play on one computer, open the page in two browser tabs.

### Publish with GitHub Pages
1. In the repository, go to **Settings → Pages**.
2. Under **Build and deployment**, set **Source** to *Deploy from a branch*.
3. Choose **main** and **/ (root)**, then **Save**.
4. After a minute or two the game is live at `https://bezoon5.github.io/Paper-Penalties/`.

## Files

```
index.html             the whole game
manifest.webmanifest   lets phones install it to the home screen
icons/                 app icons (SVG + PNG)
```

## Known limits

- If a phone reloads in the middle of a two-phone match, that match is lost. Leave and host a new game.
- Two-phone play needs an internet connection to pair (even on the same Wi-Fi). Some strict networks block WebRTC connections.
- The fonts (Cabin Sketch, Patrick Hand) load from Google Fonts. Offline, the game falls back to the phone's own fonts.

## Ideas for later

- A "super dive" each keeper can use once per match
- No repeating the same box twice in a row
- Family tournament mode for 3 or more players
- Lifetime stats for each player
