# CRAFT platform (compact deploy build of UPDATE_170)

Same 6-file layout as before:

| File | Purpose |
|---|---|
| `package.json` | dependencies + `npm start` |
| `start.js` | launcher: unpacks `app.pack` into `app/` and starts the platform |
| `app.pack` | the entire platform (33 games, compressed) |
| `.env.example` | environment variable reference |
| `.gitignore` | keeps `app/`, `node_modules/`, runtime data out of git |
| `README.md` | this file |

## Deploy (Render)
1. Upload these files to GitHub (replace the previous files).
2. Render: Build Command `npm install`, Start Command `npm start`. Environment variables are unchanged.
3. The first start prints `[launcher] unpacked N files`, then `[TEAMARENA] Mounted at /teamarena`. Saved settings under `app/data/` are never overwritten.

## What's new in 170: TEAM ARENA

Everything below is inside TEAM ARENA (`/teamarena/`). Nothing else on the platform was changed except the Autopilot format list and the HOME card text.

## Your 15 points
1. **Scoreboard 50% smaller** (RED / BLUE cards, share bar and top-player rows) so every game gets more room.
2. **Memory** starts with ALL tiles face-down (the peek option is gone). Tiles now use the pearl pink / cyan candy design of the MEMORY game, with its 15 picture packs (Kawaii stickers by default, World Flags, Animals, Sweets...). Host picks the pack, or "random pack every game".
3. **Join statement** ("Type RED or BLUE to join a team - only joined players count") is strictly one row. It shrinks its text to fit any phone width. The same applies to the copy in the lobby screen.
4. **Sudoku frozen penalty** is host-controlled: 0-300 s, plus optional "extra seconds for each further mistake" and a "longest freeze" cap. It also appears in Play tab > Quick settings.
5. **Geo Showdown now plays like CITYDLE**: every guess is colour-coded (green found, yellow same country, orange same continent, grey elsewhere; Towndle: yellow same state, orange neighbouring district) with arrow + distance, nearest guesses rise to the top and the newest guess is repeated in a highlighted row. Teams' best guesses and round wins stay in a compact strip. The line under the globe is one short row ("Type any city name", hints replace it).
6. **Rounds for every game.** Each game has a "Rounds" setting (series: the game is played N times in a row, most round wins takes it, scores carry on, short pause between rounds with a NEXT ROUND NOW button). Games that run their own rounds (Geo, Territory, Flagle, Travle, Expandle, Boxdle, Findle, Word Shuffle, Duel) have their own "rounds" setting. Tug of War also has a question limit.
7. **Tug of War** has 14 question types instead of 3 and thousands of questions (see below). All quiz formats (Territory, Relay, Boss) get the same types.
8. **Joining time.** Every game has "Seconds to wait for viewers to join" (0-900, default 45) set per game. Lobby keeps waiting (up to 3 extensions) until every team has the minimum players (Flow settings). New **START NOW** button (⏩) in the top bar, also inside the lobby and between rounds; it also ends the join window of Last Letter Standing and Knockout Bracket.
9. **Top bar is one single row** on every screen size (down to 320 px).
10. **Capture the Word**: the "colours" tag and green square are removed (the "numbers" tag stays only for letter-count teams, it is the only way to tell those boards apart).
11. **New word games** (team vs team, same style as Capture the Word, own board per team, rivals' progress visible): Blindle Duel, Oracle Duel, Forbackle Duel, Rangedle Duel, Shiftle / Twistle Duel, Numberblindle Duel, Fixle Duel, Betweendle Duel, plus Expandle Race, Boxdle Word Hunt, Findle Word Search and Word Shuffle Showdown.
12. **Other platform games added**: Flagle Showdown (blurred flag), Travle Race (link two countries by land borders). Geo Showdown (Citydle/Towndle), Memory, Sudoku and Blossom were already there. 26 formats in total, grouped Team vs team / Word duels / Word hunts / Geography / Duels / Battle royale.
13. **Floating guess window** is one single row (name, guess, result and note side by side).
14. **Join words per game and per team**: new "Join words" tab. For each game you can type different join words for each team (and a join word for games without teams, e.g. Last Letter Standing, or the automatic split modes). Empty = the normal team words.
15. Complete deploy folder (this one).

## Tug of War / quiz question types (all quiz formats)
Mixed, Trivia, Flags (198 countries, picture), Capital cities, Geography (6,300 cities, ~2,500 Malaysian towns, continents), Unscramble with Word Shuffle categories (68,000+ answers), Name one (anything in a category), Maths, Number patterns / Roman numerals / percentages, Word play, Plain-word unscramble, Chemical elements, Emoji picture quiz, True or False, Multiple choice (A/B/C/D). Questions are generated from the platform's own data, so the pool is in the tens of thousands instead of ~370.

## Not ported (and why)
Contexto (needs the large word-vector file / online ranking), Colorblindle, Colordle, Structle, Textle, Codedle, Shapedle, Comparable, Minedle, Linedle, Crossdle, Twistle (merged into Shiftle). They need per-letter keyboards, graphs or image puzzles that do not suit a shared chat board; Wordle itself = Capture the Word.

## Tested
Every one of the 26 formats was simulated end to end with bots (single games and 2-round series), and the real page was driven in headless Chromium at 320 / 360 / 390 / 420 / 1100 px: one-row top bar, join line and guess window, lobby + START NOW, series badge and between-round screen, join-words tab, quick settings.

No new environment variables or npm packages. Saved settings under `app/data/` are kept; the new per-game options simply start at their defaults.
