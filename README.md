# Traveler Supply Exchange (TSE)

A concept for a trusted, members-free way for travelers to **borrow the gear a trip needs and pass on the gear a trip leaves behind**, instead of over-buying or throwing it away.

Built as a live-prototyping exercise to show product thinking, tool use, and a shippable MVP.

## The idea in one line
Usable travel gear gets stranded near other travelers who need it, with no trusted way to hand it off. TSE closes that loop.

- **Root cause:** it's a circulation problem, not a buying problem.
- **Riskiest assumption (the MVP tests this):** a traveler can find and *safely* get gear they need, nearby, right now.

## Project structure
```
TravelersSupplyExchange/
├── index.html          # Clickable 5-screen MVP of the "I need it tonight" hero flow (served at /)
├── prep/               # Interview-prep docs (excluded from the deployed site via .vercelignore)
│   ├── idea-one-pager.html
│   └── live-build-prompt-sequence.md
├── .gitignore
├── .vercelignore
└── README.md
```

## Deploy
Static site, no build step. Hosted on Vercel (project `travelers-supply-exchange`),
auto-deploys on push to `main`:

```
git add -A
git commit -m "your message"
git push
```

Vercel builds and publishes within a minute or so. The `prep/` folder is kept in the
repo but excluded from the live site by `.vercelignore`.

## The MVP hero flow
Search a need → matched items nearby (distance + re-circulation count) → item detail with trust signals and a "not for sale" stance → safe-exchange ground rules → confirmation that rewards returning the item.

Open `prototype/index.html` in a browser to click through it.

## What's intentionally *not* built
Offload/listing flow, item world-journey, achievements, and real supply matching. Named aloud as the vision, cut from the MVP so one flow ships honest and complete. Inventory is seeded to sidestep the cold-start problem for the demo.
