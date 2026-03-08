# WRIT — A Kindle Vocab Game

> *Win Rounds, Improve Thinking*

A single-file browser game that turns your Kindle lookup history into a vocabulary drill. No server, no install, no account — open `index.html` and play.

Built in one Sunday evening using [Claude](https://claude.ai).

---

## Quick start

```
1. Open index.html in any modern browser
2. Click "Use Bundled Vocabulary" — 464 words load automatically
3. Pick a game mode and hit Begin Round →
```

Or drag your own `.xlsx` / `.json` vocabulary file onto the upload zone.

---

## Getting your words off your Kindle

Your Kindle silently saves every word you look up into a file called `vocab.db`. Here's how to turn it into something WRIT can load:

1. **Connect your Kindle via USB** — it appears as a drive in your file explorer
2. **Find `vocab.db`** — it lives at `system › vocabulary › vocab.db` (hidden folder; search for it)
   - Windows: search in File Explorer
   - Mac: Finder → select Kindle drive → ⌘F → search `vocab.db`
3. **Copy it to your Desktop** — don't move the original
4. **Go to [kindle-vocab-export.vercel.app](https://kindle-vocab-export.vercel.app/)** — upload the file, everything runs in your browser
5. **Download the Excel file** it produces
6. **Drag the `.xlsx` onto WRIT's upload zone** — done

> **Tip:** Words you only looked up once are probably not worth drilling. The export tool shows lookup counts — delete low-frequency rows before loading to keep your set tight.

---

## Game modes

| Mode | How it works |
|------|-------------|
| 📖 **Word → Define** | See the word, pick the correct definition |
| 🔍 **Define → Word** | See the definition, identify the word |
| ✍️ **Spell It** | See the definition, type the word (1 typo forgiven) |

Double-click any mode card to select it and start immediately. Keyboard shortcuts: `A` `B` `C` `D` to answer, `Enter` / `Space` to advance.

---

## Scoring

| Event | Points |
|-------|--------|
| Correct answer | +100 pts |
| Streak of 3+ | +50 bonus |
| Wrong answer | −1 life (3 lives per round) |

---

## After a round

- **Results screen** — definition cards for every word you missed, right there on the page
- **📋 Review All Words** — full glossary of every word played, with Wiktionary and Wikipedia links, and live pronunciation via the Merriam-Webster API (if you add a key in Settings)
- **🔁 Study Missed** — starts a new round using only the words you got wrong (requires ≥ 4 missed words)

---

## Vocabulary file format

WRIT reads `.xlsx` and `.json` files. The Excel file must have these column headers on the first sheet:

| Column | Required | Description |
|--------|----------|-------------|
| `Word` | ✅ | The vocabulary word |
| `Definition` | ✅ | Used as answer text and shown on review cards |
| `Part of Speech` | optional | Shown as a badge on the game card |
| `Origin / Etymology` | optional | Shown on review cards |
| `Book` | optional | Source book title, shown for context |
| `Lookups` | optional | How many times looked up on Kindle; higher = appears more often (capped at 3×) |

Column order doesn't matter — the game reads by name. Extra columns are ignored. You need at least 4 rows to start a game.

---

## Merriam-Webster pronunciation

WRIT can play audio pronunciations on review cards using the free [Merriam-Webster Collegiate Dictionary API](https://dictionaryapi.com/register/index).

1. Register at dictionaryapi.com and create a **Collegiate Dictionary** key
2. Open ⚙ Settings in WRIT and paste the key
3. A 🔊 button appears on every review card — click to hear the word

The key is stored only in your browser's `localStorage` and is never sent anywhere except `api.dictionaryapi.com`.

---

## Keyboard shortcuts

Press `?` anywhere in the game to show or hide the shortcut panel.

| Context | Key | Action |
|---------|-----|--------|
| Anywhere | `?` | Toggle shortcut panel |
| Anywhere | `Esc` | Close overlay / settings |
| Title screen | `← →` | Navigate game modes |
| Title screen | `Enter` | Start game (on selected mode) |
| Game — multiple choice | `A` `B` `C` `D` | Select answer |
| Game — any mode | `Enter` / `Space` | Next question |
| Game — Spell It | `Enter` | Submit typed answer |

---

## Files

```
index.html                  The entire game — this is all you need to play
vocab_data.json             Auto-loaded vocabulary (464 words, Kindle-sourced)
vocabenriched20260308.xlsx  Editable word list with definitions and origins
README.md                   This file
LICENSE                     MIT
```

---

## Built with

- Vanilla HTML, CSS, JavaScript — zero dependencies, zero build step
- [SheetJS](https://sheetjs.com/) for `.xlsx` parsing (CDN)
- [Merriam-Webster API](https://dictionaryapi.com/) for pronunciation (optional, key required)
- [Claude](https://claude.ai) for everything else

---

## License

MIT — see [LICENSE](LICENSE)
