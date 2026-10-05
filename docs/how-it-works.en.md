# How the deck is built

[Русский](./how-it-works.md)

The deck is a plain Anki package (`.apkg`): one note type, one card template and media files with pictures. Everything below can be opened in Anki desktop via **Tools → Manage Note Types**.

## Note type

"Do Not Give It Back (Oxford 3000)", one card per note (template "EN → RU").

| Field | Content |
|---|---|
| `Word` | the English word |
| `POS` | part of speech |
| `Level` | CEFR level: A1, A2, B1 or B2 |
| `Translation` | Russian translation of the word |
| `Example` | the story fragment as HTML: document label, text, scene, picture |
| `ExampleRU` | Russian translation of the fragment and the episode number |

## Fragment markup

The `Example` field of the card "button":

```html
<div class="strip strip-log">
  <img class="wpic" src="tw_1790933808210_….svg" alt="">          <!-- word picture -->
  <div class="panel art-panel scene-office">…</div>             <!-- place scene -->
  <div class="panel text-panel doc doc-log">
    <div class="story-label">Ida's log, day 1</div>             <!-- document label -->
    <div class="ex ex-story">Also in the box: one brown <b>button</b>. …</div>
  </div>
</div>
```

- `strip-<kind>` / `doc-<kind>` — the document kind: `scene`, `log`, `card`, `box`, `receipt`, `report`, `news`, `radio`, `announce`, `letter`, `chat`, `voice`, `poster`, `sticky`, `hand`, `overheard`. It sets the label icon and the text style.
- `scene-<place>` — one of 15 scenes: `office`, `city`, `desk`, `typewriter`, `bus`, `box`, `receipt`, `island`, `harbor`, `radio`, `cafe`, `fridge`, `station`, `street`, `phone`.
- `<b>` — the deck word inside the fragment, always exactly once, with a yellow underline.
- `strip-finale` — the last card of each part.
- The empty `<i>` and `<u>` elements inside `art-panel` are left over from earlier designs and are hidden by the CSS.

`ExampleRU` has the same structure without the picture and the scene, and ends with `<div class="story-meta">Серия N · i/n</div>` (episode N, card i of n).

## Templates and style

The files are in [`docs/template/`](./template/):

- [`front.html`](./template/front.html) — the front: the word and the `Example` field. The CSS hides the scene and the picture on the front.
- [`back.html`](./template/back.html) — the back: the word, the translation, `Example` and a folded `<details>` with `ExampleRU`. The `<hr id=answer>` mark sits at the top: AnkiWeb scrolls to it after "Show Answer", so the word and its translation stay on screen.
- [`style.css`](./template/style.css) — day and night themes (`.nightMode` and `prefers-color-scheme`), the Literata and PT Mono fonts from Google Fonts, the phone and desktop layout.

What `style.css` does not contain:

- **Scenes.** The deck's style also has 15 rules `.scene-<place> { background-image: url("data:image/svg+xml,…") }`, with the scene SVGs embedded in the CSS. They are left out of the file in `docs` so it stays readable.
- **Word pictures.** These are 900 media files named `tw_<note id>_<hash>.svg`.

**Text-to-speech.** The front uses `{{tts en_US:Word}}` and the back `{{tts en_US:Example}}`, with the system voice. AnkiWeb has no TTS and prints the tag's content as text, so that text is hidden by `.tts > :not(.replay-button):not(a)`.

## Card order

New cards are positioned in episode order: episode 0 is the first 33 cards, and almost every episode after it has 17. The deck preset "Do Not Give It Back" sets 17 new cards and 200 reviews a day. It is applied if you enable importing deck presets.
