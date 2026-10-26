# Playroom — Playful Retro Game Collection

A starter website built with Astro + Svelte. The homepage is rendered by Astro; the interactive game catalog (search and category filters) is a Svelte component.

## Requirements
- Node.js 20.3+ (recommended current LTS)

## Run locally
```bash
npm install
npm run dev
```

## Build for production
```bash
npm run build
npm run preview
```

## Add your own HTML games
1. Put a game folder under `public/games/`, for example `public/games/space-cat/index.html`.
2. Open `src/components/GameCatalog.svelte`.
3. Add or edit an object in the `games` array. Change its `url` to `/games/space-cat/index.html`.
4. Set the title, category, description, emoji/cover color, and time label.

Example:
```js
{
  title: 'Space Cat',
  category: 'Arcade',
  description: 'Help a tiny cat dodge asteroids.',
  emoji: '🐱',
  color: 'cover-blue',
  badge: 'New',
  time: '5 MIN',
  url: '/games/space-cat/index.html',
  number: '07'
}
```

## Notes
- Sample cards use `url: '#'` as placeholders. Replace them with actual local paths or external URLs.
- For games hosted elsewhere, check that the host permits embedding if you plan to use an iframe on a game detail page.
- Fonts load from Google Fonts when network access is available; the site falls back to system fonts.
# corner-games
