<p align="center">
  <img src="./assets/readme/cover-en.svg" width="100%" alt="Do Not Give It Back — an Anki deck: learn 3,060 English words by reading one mystery. Background: the night harbour from the deck">
</p>

<p align="center"><a href="./README.md">Русский</a> · <b>English</b></p>

**An Anki deck in which all 3,060 Oxford 3000 words (A1–B2) form one mystery novel.** Learn 17 words a day and you read one episode.

> **Translations are Russian.** The deck is made for Russian speakers: every word and every fragment has a Russian translation.

> Tidewell is a rainy port city where people forget their own lives. So everybody writes cards. A grey box, Item 1681, arrives at Lost Property with someone's life inside and a note: "Do not give this back to me. Even if I ask."

<p align="center">
  <a href="#quick-start"><b>Download the deck</b></a> · <a href="#whats-inside">What's inside</a> · <a href="#how-it-is-built">For developers</a> · <a href="#faq">FAQ</a>
</p>

## The problem

A typical deck is a list: "word — translation" and a random dictionary example. The examples have nothing to do with each other, so a new word has nothing to hold on to, and reviews quickly turn into a chore that is easy to skip.

## What it looks like

<p align="center">
  <img src="./assets/readme/proof.png" width="100%" alt="The back of the real card waiter: on a desktop in the day theme and on a phone in the night theme with the fragment translation opened">
</p>

A real card from episode 3, rendered by Anki's own engine: the back on a desktop in the day theme and on a phone at night, with the fragment translation opened. More screenshots are in [`assets/readme/cards`](./assets/readme/cards).

## What's inside

### Every card is a fragment of one story

**What it does.** 3,060 cards form 179 episodes of 17 new words each. A fragment is one or two sentences built around the word, styled as a document of the city: a Lost Property log, a card from the box, a police report, a receipt, a night radio show, an overheard line.

**Why it matters.** You remember the word together with a scene, and the next episode is a reason to come back tomorrow.

**The idea behind it.** Connected meaning is easier to remember than isolated facts: a new word gets something to attach to.

<p align="center">
  <img src="./assets/readme/anatomy.png" width="100%" alt="Front and back of the card waiter with marks 1 to 6">
</p>

1. The word in its fragment — try to understand it first.
2. The document label.
3. The translation, right under the word.
4. A picture of the word.
5. A scene of the place where it happens.
6. The fragment translation — on tap.

### The book brings words back

**What it does.** Each episode reuses words from the episodes 1, 2, 4, 8, 16, 32, 64 and 128 days back — more than 1,100 such returns in the text.

**Why it matters.** Anki reviews the card; the story shows you the word again, in a new situation and next to new words.

**The idea behind it.** Spaced repetition: memory holds better when encounters are spread out with growing gaps. Anki itself is built on the same principle.

<p align="center">
  <img src="./assets/readme/returns-en.svg" width="100%" alt="Diagram: today's episode reuses words from the episodes 1, 2, 4, 8, 16, 32, 64 and 128 days back">
</p>

### The level grows with the book

**What it does.** The first 30 episodes use only A1 and A2 words. Then B1 joins, and by the end of Part 1 (episode 143) only B1 is left. Part 2, episodes 144–178, is B2.

**Why it matters.** You can start from zero; the difficulty grows gradually.

<p align="center">
  <img src="./assets/readme/levels-en.svg" width="100%" alt="Chart: share of A1, A2, B1 and B2 words across the episodes; in Part 1 A1 falls and B1 rises, Part 2 is all B2">
</p>

Words per level: A1 775, A2 876, B1 813, B2 596.

### Understand first, then check

**What it does.** The word's translation sits right under the word. The translation of the whole fragment is folded away until you tap it.

**Why it matters.** You work through the English text yourself, and the translation becomes a check.

**The idea behind it.** Trying to understand or recall on your own makes memory stronger than reading a ready answer — the testing effect.

<p align="center">
  <img src="./assets/readme/translation.png" width="100%" alt="Two phone screens: the back of a card with the fragment translation folded and opened">
</p>

### Pictures for memory

**What it does.** 900 word pictures and 15 place scenes in one style, with day and night themes.

**Why it matters.** An image is one more hook: the word and the picture come back together.

**The idea behind it.** A word plus an image leaves two traces in memory instead of one (dual coding).

<p align="center">
  <img src="./assets/readme/pictures.png" width="100%" alt="20 word pictures: umbrella, lemon, bicycle, listen, ticket, wait and more">
</p>

<details>
<summary>All 15 scenes</summary>
<br>
<p align="center">
  <img src="./assets/readme/scenes.png" width="100%" alt="15 scenes of the city: Lost Property, a stairwell window, a card shop, a typewriter, a bus, Box 1681, receipts, an island, the harbour, a radio studio, a café, a kitchen, a station, a street, a bus stop">
</p>
</details>

## Quick start

1. Download the deck (4 MB, pictures included): [`Do-Not-Give-It-Back-Oxford-3000.apkg`](./deck/Do-Not-Give-It-Back-Oxford-3000.apkg). Direct link:
   ```text
   https://github.com/phloya/oxford-3000-detective/raw/main/deck/Do-Not-Give-It-Back-Oxford-3000.apkg
   ```
2. Import it:
   - **Anki desktop:** File → Import. Enable *Import deck presets* to get 17 new cards a day.
   - **AnkiDroid:** ⋮ → Import, or open the file on the phone.
   - **iPhone/iPad (AnkiMobile):** open the file and share it to AnkiMobile.
   - **AnkiWeb** cannot import `.apkg` files: import on a computer or phone, then sync.
3. Study in order. New cards follow the story — **do not randomize them**.

You can reread the episodes you have passed as a book, with scenes and translation on tap: **[open the book](https://phloya.github.io/oxford-3000-detective/book/)** (Russian interface). The next episode opens only when you press the button, so there are no spoilers.

## How it is built

- Note type "Do Not Give It Back (Oxford 3000)" with the fields `Word`, `POS`, `Level`, `Translation`, `Example`, `ExampleRU`.
- `Example` holds the fragment as HTML: the document label, the text with the word in `<b>`, the scene and the picture. `ExampleRU` holds the translation and the episode number.
- Templates and style are in [`docs/template`](./docs/template). Scenes are embedded in the deck's CSS; pictures are `tw_*.svg` media files.
- Details: [how the deck is built](./docs/how-it-works.en.md) and [customize it](./docs/customize.en.md). For example, keep only the word on the front:

```css
.front .ex-story { display: none; }
```

## FAQ

**What level do I need?** A1 is fine: the first 30 episodes use only A1 and A2 words.

**Can I shuffle the cards?** No. The order of new cards is the order of the story.

**Are there spoilers here?** No. This README and the screenshots show only the beginning: the prologue and the first episodes.

**Does it work offline?** Yes. Without a connection the Google Fonts do not load and the cards fall back to system fonts.

**Can I study on AnkiWeb?** Yes, after a sync. AnkiWeb has no text-to-speech; the ▶ button works in Anki desktop and AnkiDroid.

## License and links

- Texts, translations, pictures and design: [CC BY-NC-SA 4.0](./LICENSE.md) — share and adapt non-commercially, with attribution, under the same license.
- Oxford 3000™ is a word list © Oxford University Press. This project is not affiliated with OUP and uses only the words; all texts are original.
- Found a mistake in a text or translation? Open an [issue](../../issues).
- Author: [phloya](https://github.com/phloya).
