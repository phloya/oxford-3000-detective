# Как устроена колода

[English](./how-it-works.en.md)

Колода — обычный пакет Anki (`.apkg`): один тип записи, один шаблон карточки и медиафайлы с рисунками. Всё, что описано ниже, можно открыть в Anki на компьютере: **Инструменты → Управление типами записей** (Tools → Manage Note Types).

## Тип записи

«Do Not Give It Back (Oxford 3000)», одна карточка на запись (шаблон «EN → RU»).

| Поле | Что внутри |
|---|---|
| `Word` | английское слово |
| `POS` | часть речи |
| `Level` | уровень CEFR: A1, A2, B1 или B2 |
| `Translation` | перевод слова |
| `Example` | фрагмент истории в HTML: ярлык документа, текст, сцена, рисунок |
| `ExampleRU` | перевод фрагмента и номер серии |

## Разметка фрагмента

Поле `Example` у карточки «button»:

```html
<div class="strip strip-log">
  <img class="wpic" src="tw_1790933808210_….svg" alt="">          <!-- рисунок слова -->
  <div class="panel art-panel scene-office">…</div>             <!-- сцена места -->
  <div class="panel text-panel doc doc-log">
    <div class="story-label"><span class="lbl" data-label="Ida's log, day 1"></span></div>  <!-- ярлык документа -->
    <div class="ex ex-story">Also in the box: one brown <b>button</b>. …</div>
  </div>
</div>
```

- `strip-<вид>` и `doc-<вид>` — вид документа: `scene`, `log`, `card`, `box`, `receipt`, `report`, `news`, `radio`, `announce`, `letter`, `chat`, `voice`, `poster`, `sticky`, `hand`, `overheard`. От вида зависят значок на ярлыке и оформление текста.
- `scene-<место>` — одна из 15 сцен: `office`, `city`, `desk`, `typewriter`, `bus`, `box`, `receipt`, `island`, `harbor`, `radio`, `cafe`, `fridge`, `station`, `street`, `phone`.
- `<b>` — слово колоды внутри фрагмента. Оно всегда выделено ровно один раз и подчёркнуто жёлтым.
- Текст ярлыка лежит в атрибуте `data-label`, а на карточку его выводит правило `.story-label .lbl::before { content: attr(data-label) }`. Озвучка читает поле без тегов и атрибутов, поэтому начинает сразу с текста фрагмента, а не с «Box 1681, lamp card».
- `strip-finale` — последняя карточка каждой части.
- Внутри `art-panel` есть пустые `<i>` и `<u>` от прошлых версий оформления, CSS их скрывает.

`ExampleRU` устроен так же, но без рисунка и сцены. В конце — `<div class="story-meta">Серия N · i/n</div>`.

## Шаблоны и стиль

Файлы лежат в [`docs/template/`](./template/):

- [`front.html`](./template/front.html) — лицевая сторона: слово и поле `Example`. Сцену и рисунок на лицевой стороне прячет CSS.
- [`back.html`](./template/back.html) — оборот: слово, перевод, `Example` и свёрнутый `<details>` с `ExampleRU`. Метка `<hr id=answer>` стоит в начале: к ней AnkiWeb прокручивает страницу после «Show Answer», поэтому слово и перевод остаются на экране.
- [`style.css`](./template/style.css) — дневная и ночная тема (класс `.nightMode` и `prefers-color-scheme`), шрифты Literata и PT Mono из Google Fonts, раскладка для телефона и компьютера.

Чего нет в `style.css`:

- **Сцены.** В стиле колоды добавлены 15 правил `.scene-<место> { background-image: url("data:image/svg+xml,…") }`: SVG сцен встроены прямо в CSS. В файле из `docs` их нет, чтобы его можно было читать.
- **Рисунки слов.** Это медиафайлы `tw_<id записи>_<хэш>.svg`, их 900.

**Озвучка.** На лицевой стороне `{{tts en_US:Word}}`, на обороте `{{tts en_US:Example}}`, голос берётся из системы. Ярлык документа в озвучку не попадает (см. выше про `data-label`). AnkiWeb озвучку не поддерживает и печатает содержимое тега текстом, поэтому этот текст скрыт правилом `.tts > :not(.replay-button):not(a)`.

## Порядок карточек

Новые карточки стоят по позиции в порядке серий: серия 0 — первые 33 карточки, дальше почти везде по 17. Пресет колоды «Do Not Give It Back»: 15 новых и 200 повторений в день. Он подключается, если при импорте включить импорт пресетов.
