# General Service FAQ — R. H. Foster Energy

An internal CSR triage reference for plumbing, heating, fuel, heat pump, and furnace service calls. It's a single, self-contained
`index.html` file (HTML + CSS + JavaScript) with no build step and no dependencies — open it,
edit it, push it.

**Internal use only. Not for customer distribution.**

## Live site

Published via GitHub Pages: https://downeasternman.github.io/plumbingfaq/

## What it does

- Searchable, filterable list of common plumbing, heating, cooling, ductwork, fuel, heat pump, furnace, and thermostat call scenarios
- Each entry shows **Questions to Ask** and **What to Tell the Customer**
- Urgency flags and high-visibility **STOP** banners for life-safety situations
- Live search with typo/synonym handling (e.g. `fawcet` → `faucet`, `lp` → `propane`)
- Category filter pills
- Print-friendly layout for a physical desk reference

## Editing the FAQ

All content lives in a single `FAQ` array near the top of the `<script>` block in
`index.html`. You never need to touch the layout or app logic to add or change entries.

To **add** an entry, copy an existing object in the array and edit the fields:

```js
{
  id: "unique-string-no-spaces",   // must be unique
  category: "Drains",              // becomes a filter pill
  title: "Short displayed name",
  desc: "One-line description shown when collapsed.",
  urgency: null,                   // null | "urgent" | "emergency"
  urgencyLabel: null,              // text shown in the flag when urgency is set
  stopCondition: "",               // optional: imperative STOP banner text (life-safety)
  stopUntil: "",                   // optional: what the CSR must confirm before proceeding
  questions: [
    "First question to ask the customer?",
    "Second question?",
  ],
  script: "What to tell the customer while they wait for a callback.",
  email: "",                       // Phase 2 — dispatch email (not rendered yet)
  phone: "",                       // Phase 2 — branch line (not rendered yet)
},
```

- To **reorder**, move the object up or down in the array.
- To **remove**, delete the object.
- Categories are generated automatically from the `category` values, so a new category
  name creates a new filter pill.

### STOP banners

Set `stopCondition` (and optionally `stopUntil`) on any entry to render a red STOP banner
at the top of the expanded card. Use these for life-safety holds (gas/CO, active flooding,
cracked toilet, etc.).

### Phase 2: dispatch routing

The `email` and `phone` fields are already in every entry but are not displayed yet. When
branch routing is ready, fill them in and wire up the render code.

## Deploying to GitHub Pages

1. Push changes to the `main` branch of this repository.
2. In the repo on GitHub: **Settings → Pages**.
3. Under **Build and deployment**, set **Source** to *Deploy from a branch*.
4. Select branch **`main`** and folder **`/ (root)`**, then **Save**.
5. GitHub builds the site and serves it at the URL shown on that page.

After the initial setup, every push to `main` redeploys automatically (usually within a
minute or two).

## Local preview

Just open `index.html` in any browser — no server required.
