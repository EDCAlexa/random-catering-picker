# Weekly Catering Picker

A little web page for picking the team's catering order. Upload your menu, say how many
people you're feeding, and hit the button — it picks a restaurant and a combo for you.
Don't love it? Reroll until you do.

## Using it

1. **Upload your menu.** Click **⬆️ Upload menu CSV** and choose the file you exported from
   your spreadsheet (in Google Sheets: *File → Download → Comma-separated values*). It's read
   right there in your browser. New to this? Hit **⬇️ CSV template** to grab a
   filled-in example you can copy. We decided to upload it into an editable Google Sheet.
2. **Set your options.** Number of people, an optional budget cap, the kind of combo you want
   (one entrée + one appetizer, two entrées, two appetizers, or "Any"), and the dietary
   checkboxes.
3. **Hit 🎲 Pick / Reroll.** You get a restaurant, the items to order and how many of each, the
   total, and a note about who can eat what. Reroll as much as you want.

There's also a **🔍 Preview how your menu imported** section. Open it and each restaurant
shows up as a dropdown; click one to see exactly how the app read every row — course tags,
proteins, serving size, price, and little labels like "bundle," "has protein," or
"⚠ no protein tag" so you can catch anything that didn't come in the way you expected.

## What your CSV should look like

Eight columns, starting with this header row:

`Restaurant, Meal, Meal Status, Protein, Serving, Price, Delivery, Notes`

- **Meal Status** — `Entree`, `Appetizer`, and/or `Dessert`. Comma-separate them if one item
  covers several courses (like a bundle that's an entrée + appetizer + dessert all in one).
- **Protein** — `Chicken`, `Beef`, `Pork`, `Seafood`, `Turkey`, `Lamb`, `Vegetarian` (an actual
  vegetarian protein, like beans or tofu), or `None` (a side with no protein — fries, mac &
  cheese, and so on). Comma-separate if there's more than one.
- **Serving** — a plain number: how many people one order feeds.
- **Price** — like `$210.00`.
- **Delivery** and **Notes** — free text. They show up with the pick but don't affect anything.

The **CSV template** button downloads a one-row example so you can see the format and build
your own from it.

## How it picks

- A combo is **two items from the same restaurant** — one entrée + one appetizer, two entrées,
  or two appetizers. It only ever pulls from a single place, so it's one order.
- If a single item is tagged as **both an entrée and an appetizer** — one of those all-in-one
  bundle packages — that's already a full combo, so it suggests just the one thing instead of
  doubling up. All of its course tags show as badges.
- **Everybody gets protein.** At least one item in the combo has a real protein (a meat, or
  Vegetarian), so it won't hand you a meal that's two sides. (Checkbox — you can switch it off.)
- **The vegetarian can eat.** At least one item works for them. If it's a build-your-own with
  several proteins, the result reminds you to pick the vegetarian option.
- **The no-pork person can eat.** At least one item isn't pork-only, with the same kind of
  reminder on multi-protein items. (A pork-only dish like "Pork Dumplings" won't count for them.)
- **Quantities are worked out for you.** Feeding 60 people with an item that serves 20? It says
  order 3. Expect a little overlap or leftovers — better than running short.
- **Budget** caps the total of what you'd actually order, quantities included. Leave it blank
  for no limit.
- **Desserts** are listed off to the side for whichever restaurant got picked, with a suggested
  quantity. They're never added to the total or counted against your budget.
