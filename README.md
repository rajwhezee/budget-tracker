# Budget Tracker

A single page budget tracker. Log income and expenses, set a monthly budget, and see
where the money actually goes.

**Live demo → [budget-tracker-rajveer.vercel.app](https://budget-tracker-rajveer.vercel.app)**

![Budget Tracker](screenshot.png)

## What it does

- **Transactions** — add income or expenses with a description, amount, category and date
- **Monthly budget** — set a budget and track how much of it is spent, with a bar that turns
  red once you go over
- **Category breakdown** — a donut chart of this month's spending, drawn directly on a
  `<canvas>` with no charting library
- **Custom categories** — add or remove your own
- **Sample data** — loads automatically on a first visit so the page is never empty

Everything persists to `localStorage`, so your data survives a refresh and never leaves
your browser.

## Running it

There is no build step and no dependencies. Open the file:

```bash
open index.html
```

Or serve it locally:

```bash
python3 -m http.server 8000
```

## Notes on the build

The whole app is one `index.html` — markup, styles and logic. For something this size that
keeps it easy to read and trivial to deploy anywhere that serves static files.

A few decisions worth calling out:

- **No accounts.** An earlier version of this project had a login screen that stored
  passwords in `localStorage` in plain text and could be skipped by navigating straight to
  the main page. That is worse than no authentication at all, because it implies a security
  guarantee it cannot keep. It was removed rather than patched. Real accounts need a server,
  hashed passwords and sessions, which is a different project.
- **Reads from storage are defensive.** `localStorage` throws in some private browsing
  modes and can return corrupt JSON, so every read is wrapped and falls back to empty state.
- **The chart is hand drawn.** Arc strokes on a canvas, scaled to `devicePixelRatio` so it
  stays sharp on retina displays. Pulling in a charting library for one donut was not worth
  the weight.

## Origin

This started as my IB Computer Science internal assessment — a finance tracker built for a
university student tracking expenses on paper. That version was a Flask backend that only
stored category names, a table that lost every row on refresh, and the fake login described
above. This is a rewrite that keeps the original idea and makes it actually work.

## License

MIT
