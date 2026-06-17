# Weekly Catering Picker

A single-file web app that picks a random catering combo from one restaurant and lets you
reroll until you like it. No build step, no server, no dependencies — just `index.html`.

## How it works

1. Open the app and click **⬆️ Upload menu CSV** to load your menu (exported from your
   spreadsheet: File → Download → Comma-separated values `.csv`).
2. The menu is **remembered in your browser**, so reroll — and even a page refresh — keep
   using it without re-uploading. Upload again only when the menu changes.
3. Set **People**, an optional **Max $ total**, **Combo type**, **Restaurant**, and the
   dietary toggles, then hit **🎲 Pick / Reroll**.

### Expected CSV columns
`Restaurant, Meal, Meal Status, Protein, Serving, Price, Delivery, Notes`
- **Meal Status** — `Entree` / `Appetizer` / `Dessert` (comma-separated if several).
- **Protein** — `Chicken, Beef, Pork, Seafood, Turkey, Lamb`, `Vegetarian` (a real veg
  protein — beans/tofu), or `None` (a side with no protein). Comma-separated if several.
- **Serving** — a number (how many people one order feeds). **Price** — like `$108.00`.

## Hosting

It's a static page, so host it anywhere:
- **Just open it** — double-click `index.html`. (To make the "remembered" menu survive
  reloads reliably, serve it over http rather than `file://` — e.g. `python -m http.server`.)
- **GitHub Pages** — put `index.html` in a repo, enable Pages, share the link. Add an empty
  file named `.nojekyll` so Pages serves everything as-is. ⚠️ A free Pages site is **public** —
  anyone with the URL can use it (the menu lives only in each person's browser after they
  upload, so it isn't published).
- **Netlify / SharePoint / any intranet** — drop the file in.

## The rules it enforces

- A combo is **two "main" items from one restaurant** — 1 entrée + 1 appetizer, 2 entrées,
  or 2 appetizers (selectable, or "Any").
- **Bundles count as one item.** An item tagged both Entrée *and* Appetizer (e.g. a "Perfect
  Bundle" that includes entrée + appetizer + dessert) is a complete combo on its own, so it's
  shown alone — never paired with a second bundle. All of its course tags are shown as badges.
- **Has a protein** (toggle, on by default): at least one main carries a real protein — any
  meat, or `Vegetarian`. Stops "two sides" combos. A `🍗 Protein:` line names the dish.
- **Vegetarian-friendly:** at least one main is `Vegetarian` or meatless (`None`). A multi-protein
  item counts, with a note that the vegetarian option must be chosen.
- **Pork-free:** at least one main isn't pork-only. A multi-protein item counts, with a note that
  a non-pork option must be chosen. A pork-only item ("Pork Dumplings") doesn't.
- **People** → the app computes **how many of each item to order** to cover the headcount
  (serves 20, for 60 people → order 3); there may be overlap / extra food.
- **Max $ total** → caps the quantity-adjusted order total of the mains (blank = no limit).
- **Desserts** are listed separately (with a suggested quantity) and never counted in the total.
- Any meal with a **blank protein cell** is flagged in the status as a "row warning."

## Files

| File | Purpose |
|------|---------|
| `index.html` | The entire app. |
| `menu.csv` | A sample menu you can upload (your data — not needed for the app to run). |
