<p align="center">
  <img src="./assets/readme/cover-en.svg" width="100%" alt="Do Not Give It Back — an Anki deck: learn 3,060 English words by reading one mystery. Background: the night harbour from the deck">
</p>

<p align="center"><a href="./README.md">Русский</a> · <b>English</b></p>

**An Anki deck in which all 3,060 Oxford 3000 words (A1–B2) form one mystery novel.** Learn 17 words a day and you read one episode.

> **Translations are in Russian.** The deck is made for Russian speakers.

> Tidewell is a rainy port city where people forget their own lives. So everybody writes cards. A grey box, Item 1681, arrives at Lost Property with someone's life inside and a note: "Do not give this back to me. Even if I ask."

<p align="center">
  <a href="#how-to-install"><b>Download the deck</b></a> · <a href="#whats-inside">What's inside</a> · <a href="#the-book">The book</a> · <a href="#how-it-is-built">For developers</a> · <a href="#faq">FAQ</a>
</p>

## What it looks like

<p align="center">
  <img src="./assets/readme/proof.png" width="100%" alt="The back of the real card waiter: on a desktop in the day theme and on a phone in the night theme with the fragment translation opened">
</p>

A screenshot from Anki: a card from episode 3 on a desktop (day) and on a phone (night). More screenshots are in [`assets/readme/cards`](./assets/readme/cards).

## What's inside

### Every card is a fragment of one story

3,060 cards form 179 episodes of 17 new words each. A fragment is one or two sentences with the word, styled as a document of the city: a Lost Property log, a card from the box, a police report, a receipt, a night radio show, an overheard line. You remember the word together with a scene, and the next episode is a reason to come back tomorrow.

<p align="center">
  <img src="./assets/readme/anatomy.png" width="100%" alt="Front and back of the card waiter with marks 1 to 6">
</p>

1. The word in its fragment — try to understand it first.
2. The document label.
3. The translation, right under the word.
4. A picture of the word.
5. A scene of the place where it happens.
6. The fragment translation — on tap.

### The story brings words back

Each episode reuses words from the episodes 1, 2, 4, 8, 16, 32, 64 and 128 days back — more than 1,100 returns in total. Anki reviews the card; the story brings back the word itself, in a new scene and next to new words (spaced repetition).

<p align="center">
  <img src="./assets/readme/returns-en.svg" width="100%" alt="Diagram: today's episode reuses words from the episodes 1, 2, 4, 8, 16, 32, 64 and 128 days back">
</p>

### The level grows with the story

The first 30 episodes use only A1 and A2 words, so you can start from zero. Then B1 joins, and by the end of Part 1 (episode 143) only B1 is left. Part 2, episodes 144–178, is B2.

<p align="center">
  <img src="./assets/readme/levels-en.svg" width="100%" alt="Chart: share of A1, A2, B1 and B2 words across the episodes; in Part 1 A1 falls and B1 rises, Part 2 is all B2">
</p>

Words per level: A1 775, A2 876, B1 813, B2 596.

### Understand first, then check

The fragment translation is folded: you work through the English yourself, then check. That makes memory stronger (the testing effect).

<p align="center">
  <img src="./assets/readme/translation.png" width="100%" alt="Two phone screens: the back of a card with the fragment translation folded and opened">
</p>

### Pictures for memory

900 word pictures and 15 place scenes in one style, with day and night themes. A word with a picture is easier to remember (dual coding).

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

## How to install

1. Install Anki: [desktop](https://apps.ankiweb.net) and [Android](https://play.google.com/store/apps/details?id=com.ichi2.anki) are free, [iPhone and iPad](https://apps.apple.com/app/ankimobile-flashcards/id373493387) is paid.
2. Download [`Do-Not-Give-It-Back-Oxford-3000.apkg`](https://github.com/phloya/oxford-3000-detective/releases/latest/download/Do-Not-Give-It-Back-Oxford-3000.apkg) from [Releases](../../releases/latest).
3. Open the file in Anki:
   - **Desktop:** double-click the file or choose File → Import. Enable *Import deck presets* to get 17 new cards a day.
   - **Android:** open the file and choose AnkiDroid.
   - **iPhone and iPad:** open the file in the Files app, tap Share and choose AnkiMobile.
4. Study in order: new cards follow the story, do not shuffle them.

## The book

[The book](https://phloya.github.io/oxford-3000-detective/book/) is a website with the deck's episodes as continuous text, for rereading what you have passed like a novel. You do not need it to study.

- It opens in the browser, nothing to install. The interface is in Russian.
- Only the prologue is open at first. When you pass the next episode in Anki, press "Открыть: Серия N" (Open: Episode N) at the bottom. The other episodes stay closed, so there are no spoilers.
- "перевод" under a card shows its translation; "Весь перевод" shows the translation of the whole episode.
- Opened episodes are remembered in this browser only. The book is not connected to Anki: on another device you open the episodes again.

## How it is built

- Note type "Do Not Give It Back (Oxford 3000)" with the fields `Word`, `POS`, `Level`, `Translation`, `Example`, `ExampleRU`.
- `Example` holds the fragment as HTML: the document label, the text with the word in `<b>`, the scene and the picture. `ExampleRU` holds the translation and the episode number.
- Templates and style are in [`docs/template`](./docs/template). Scenes are embedded in the deck's CSS; pictures are `tw_*.svg` media files.
- Details: [how the deck is built](./docs/how-it-works.en.md) and [customize it](./docs/customize.en.md). For example, keep only the word on the front:

```css
.front .ex-story { display: none; }
```

## FAQ

**Does it work offline?** Yes. Without a connection the Google Fonts do not load and the cards fall back to system fonts.

**Can I study on AnkiWeb?** Yes, but you cannot import the deck there: import it on a computer or phone, then sync. AnkiWeb has no text-to-speech; the ▶ button works in Anki desktop and AnkiDroid.

## License and links

- Texts, translations, pictures and design: [CC BY-NC-SA 4.0](./LICENSE.md) — share and adapt non-commercially, with attribution, under the same license.
- Oxford 3000™ is a word list © Oxford University Press. This project is not affiliated with OUP and uses only the words; all texts are original.
- Found a mistake in a text or translation? Open an [issue](../../issues).
- Author: [phloya](https://github.com/phloya).
