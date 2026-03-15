# EN/NL Language Toggle — Design

## Approach

`data-i18n` attribute + JS translations object (approach A). Self-contained, no dependencies.

## Toggle UI

Pill-shaped `EN · NL` control appended to the nav after `.nav-links`. Active language gets `--accent` gold background; inactive is dimmed. Stays visible on mobile even when nav links are hidden.

```html
<div class="lang-toggle" role="group" aria-label="Language">
  <button class="lang-btn" data-lang="en">EN</button>
  <button class="lang-btn" data-lang="nl">NL</button>
</div>
```

## Translations

`const TRANSLATIONS = { en: {...}, nl: {...} }` in the existing `<script>` block. Every translatable element gets `data-i18n="key"`. Elements with inner HTML use `innerHTML` swap.

### What gets translated
- Nav links
- Hero description, buttons, scroll hint
- About paragraphs
- Fact labels
- Education bullets
- Experience bullets
- Project description
- Skill group headings, level labels, skill names where they differ in Dutch
- Competency tags
- Contact subtitle
- Section `<h2>` headings

### What stays in English
Proper nouns, dates, institution names, tech stack tags, email/links, footer URL.

## Behaviour

- On load: read `localStorage.getItem('lang')`, default `'en'`
- On toggle click: update all `data-i18n` elements via innerHTML, save to `localStorage`, toggle `.active` on buttons
