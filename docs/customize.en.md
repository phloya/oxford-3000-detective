# Customize it

[Русский](./customize.md)

Style changes are made in Anki desktop: **Tools → Manage Note Types** → "Do Not Give It Back (Oxford 3000)" → **Cards…** → the **Styling** tab. Paste a rule at the very end; it reaches all your devices after a sync.

Both recipes below were tested on a real card of the deck.

## Word only on the front

By default the front shows the word and its story fragment. To recall the word without help from the context, hide the fragment:

```css
.front .ex-story { display: none; }
```

The document label stays, because it does not reveal the meaning. The fragment still appears on the back.

## No pictures and scenes

```css
.wpic, .back .art-panel { display: none !important; }
.back:has(.wpic) .word, .back:has(.wpic) .ru { margin-right: 0; min-height: 0; }
```

The second line removes the space kept for the picture.

## New cards per day

Deck gear → **Options** → **Daily Limits** → **New cards/day**. One episode is 17 cards. To read more on a given day, raise the limit for today.

Do not randomize new cards: their order is the order of the story.

## What cannot be changed

- **Translations are Russian only.**
- **Fonts load from Google Fonts.** Offline, Anki falls back to Georgia, PT Serif and Consolas. The cards still work but look plainer.
