# Traveler Supply Exchange (TSE) — Claude Context

> **Claude must read this file before every task and update it after every task.**
> Add a dated entry to the [Change log](#change-log) section whenever something meaningful changes.

---

## What this project is

TSE is a concept app: a trusted way for travelers to borrow the gear a trip needs and pass on the gear it leaves behind, instead of over-buying or throwing it away.

- **Root problem:** usable gear stranded near travelers who need it, with no trusted way to hand it off. It's a circulation problem, not a buying problem.
- **Riskiest assumption the MVP tests:** a traveler can find and safely get gear nearby, right now.
- **Purpose of this repo:** a portfolio/interview demo piece showing product thinking, tool fluency, and a shippable MVP.

---

## Stack and architecture

**Plain static site. No framework, no build step, no dependencies.**

- `index.html` at the repo root is the entire app: a single self-contained file with inline CSS and JS.
- Screens are `<section class="screen">` elements. The `go(id)` function switches between them by toggling an `active` class.
- `detectCategory(name)` and `detectBorrowCategory()` handle keyword-based category auto-detection for both flows.
- Mobile-first. Phone frame is ~390px wide.

**Do not** split into multiple files, introduce a framework, bundler, package.json, or npm dependencies unless Barbara explicitly asks.

---

## Current prototype state

### Screens in index.html (11 total)

**Borrow flow (fully built):**
| ID | Screen |
|----|--------|
| `s-home` | Home / search |
| `s-results` | Results list |
| `s-detail` | Item detail |
| `s-exchange` | Safe exchange ground rules |
| `s-done` | Request sent confirmation |

**List/offload flow (fully built):**
| ID | Screen |
|----|--------|
| `s-list-category` | Category selection |
| `s-list-details` | Item name, condition, description |
| `s-list-photo` | Add a photo |
| `s-list-logistics` | Departure date + meetup area |
| `s-list-preview` | Preview listing card |
| `s-list-done` | Listing live confirmation |

### Not built (intentionally cut from MVP)
- Relist / return flow ("Keep It Moving" — the loop-closing behavior, teased on `s-done`)
- Item world-journey map
- Achievements / gamification beyond the badge mention
- Real supply matching
- Any backend

Do not add these unless Barbara asks.

---

## Brand palette

Defined as CSS variables in `:root` inside `index.html`. Do not use hardcoded hex values; reference the variables.

| Variable | Hex | Use |
|----------|-----|-----|
| `--navy` | `#163A5F` | Primary ink / text / logo top quadrant |
| `--blue` | `#3B52C4` | Interactive elements, buttons, badges / logo right quadrant |
| `--blue-light` | `#D4E3FB` | Chip backgrounds |
| `--forest` | `#2F6B04` | "Free" badges, circulation chips / logo bottom quadrant |
| `--sage` | `#6D885A` | Muted / secondary text / logo left quadrant |
| `--teal` | `#75C7C0` | Accent highlights |
| `--bg` | `#FAF8F3` | Page / screen background, warm off-white |
| `--card` | `#ffffff` | Card surfaces |
| `--warn` | `#E2403E` | Error / warning |
| `--gold` | `#F2B733` | Gold / badge highlights |

Logo is an inline SVG 4-quadrant diamond mark followed by the stacked TRAVELERS / --SUPPLY-- / EXCHANGE wordmark. "Supply" is rendered in `--forest`.

---

## Deploy flow

- **Repo:** github.com/bbrdnx/TravelersSupplyExchange
- **Live site:** https://travelers-supply-exchange.vercel.app
- **Vercel project:** `travelers-supply-exchange` — auto-deploys on push to `main`
- `prep/` is version-controlled but excluded from the live site via `.vercelignore`

**Git commands are run by Barbara, not by Claude.** When a change is ready to ship, provide commands one line at a time (zsh parse errors occur with multi-line blocks):

```
git add -A
```
```
git commit -m "describe the change"
```
```
git push
```

---

## Copy and voice conventions

- **No em-dashes.** Use a comma, period, or rewrite. This applies to UI copy and all docs.
- Concise, direct, active voice.
- Card and list descriptions are one line.
- Safety language is plain and reassuring, never legalistic.
- Sentence case for all labels and headings (not ALL CAPS).

---

## How to work with Barbara

- Make changes in small, reviewable steps. Say what you are about to change before changing it.
- Prefer editing `index.html` directly over describing changes.
- When something is ambiguous, ask rather than guess.
- Give terminal commands one line at a time.
- When working in Cursor and Claude together: Cursor handles code edits; Claude handles design thinking, Figma work, and planning. Both tools use the same `.cursor/rules/project.mdc` and this file for context.

---

## Related files

| File | Purpose |
|------|---------|
| `.cursor/rules/project.mdc` | Cursor auto-loaded context (mirrors key sections of this file) |
| `prep/cursor-kickoff.md` | Opening message for starting a Cursor build session |
| `prep/live-build-prompt-sequence.md` | Staged prompt sequence for the live-build interview demo |
| `cursor-figjam-prompt.md` | Prompt for generating the TSE user flow diagram in FigJam |
| `prep/idea-one-pager.html` | Original product concept one-pager |
| `branding/` | Logo, branding guide, logo lockups |
| `assets/tent-hero.png` | Hero image asset |

---

## Figma design

A Figma file exists with iOS-spec screens for the prototype. It includes:
- Home screen with "Popular right now" gear listings (photorealistic images), "Leaving soon?" borrowed-item card, and "List gear you can't take home" chip
- Full Flow 2 listing screens in sentence case
- Screens use the TSE brand palette

Use the Figma MCP (`mcp__f238cea6...`) when doing design work.

---

## Change log

*Add a dated entry here after every meaningful task.*

| Date | Change |
|------|--------|
| 2026-06-24 | Welcome sheet + quick-add suggestions. (1) Added `#welcome-sheet`, a fun intro bottom sheet (diamond mark, "👋 Welcome, you're early", explains it's an MVP demo, nudges to borrow any item) that opens right after the splash hands off to home (`setTimeout` now also calls `openSheet('welcome-sheet')`); reappears on each restart. 5 sheet overlays total. (2) On the pickup logistics screen (`s-list-logistics`), added tap-to-fill suggestions so viewers can click through without typing: a "Quick add" row of time chips (`#time-suggestions`, `addSuggestedTime(day,from,to)` pushes a range, de-dupes) and a "Popular safe spots nearby" row of location chips (`#meetup-suggestions`, `pickMeetup(el)` fills `#list-meetup` from `data-place`). New `.suggest-label` style. `syncMeetupChips()` keeps the location chip highlight in sync with the input (cleared on custom typing); called from `updateListing`, `resetListFlow`, `startRelist`. Verified with jsdom (12 checks pass). |
| 2026-06-24 | Playable borrow loop. The borrow flow no longer dead-ends at `s-done`: its CTA ("Continue") opens a new `#receive-sheet` ("Did you get the item?") showing the requested item plus a tappable 5-star review (`.stars`/`.star`, `setStars()`); Confirm is gated on a rating. `confirmReceived()` sets the dynamic `borrowedItem`, removes it from the home feed (`renderHome()` now filters it out), and shows it via `renderBorrowed()` in both the home "Borrowed Here" section (re-added, `#home-borrowed`, hidden until borrow) and the Profile "Currently Borrowing" section (`#profile-borrowed` + `#profile-borrow-empty` empty state). Teaser/circulation copy is generated from the item's real `circ`. Pass/keep sheets, `startRelist()`, and `openAchievement()` are now keyed off `passItemId` (set by `openPassSheet(id)`/`openKeepSheet(id)`) instead of hardcoded tent2, so any borrowed item flows correctly (relist prefilled from item; achievement shows circ+1). Loop closes by restarting the prototype: `closeAchievement()` and the thank-you sheet's Done now call `location.reload()`. New state vars: `currentDetailId`, `borrowedItem`, `passItemId`, `reviewStars`. Verified with jsdom harness (21 checks pass; reload confirmed firing). Sheets now total 4 overlays. |
| 2026-06-24 | Borrowed-card relocation + thank-you sheet + prototype reset. (1) Removed the "Borrowed Here" section from the home feed; the borrowed card (with its Trail Keeper teaser and Pass it on / Not passing on buttons) now lives in the Profile "Currently Borrowing" section on `s-profile-own` (the old `pi-row` there was replaced by the full `.borrowed-card`; the `bc-row` keeps the openDetail tap). Relist caption links updated from `s-home` to `s-profile-own`. (2) Submitting a not-passing reason now calls `submitKeepReason()` which closes `#keep-sheet` and opens a new `#thanks-sheet` (green check + "Thanks for letting us know"). New `.sheet-check` style. (3) Added a "↻ Reset prototype" button at the bottom of the side caption (`.reset-proto`) that calls `location.reload()` to return the demo to its original state. Verified: braces balanced (469/469), 16 screens, 3 sheet overlays, all onclick handlers defined. |
| 2026-06-24 | Button hierarchy + flow separation on the borrowed card. "List gear you can't take home" and "Pass it on" restyled to secondary (forest outline on card bg); "Not passing on" restyled to tertiary (text only, transparent border to keep row height). Hover states updated to match. Separated the two flows: the single `#return-sheet` was split into `#pass-sheet` (item summary + primary "Pass it on to the next traveler" CTA + "Not now" ghost) and `#keep-sheet` (the not-passing reason checklist + Submit). Sheet JS generalized to `openSheet/closeSheet/closeSheetOutside(id)` with `openPassSheet`, `openKeepSheet`, `closeKeepSheet`; `startRelist()` and the relist caption step-link updated to the pass sheet. Verified: braces balanced (464/464), no orphaned `return-sheet` refs, 2 sheet overlays. |
| 2026-06-24 | App-wide UI states and micro-interactions added in a dedicated CSS block at the end of `<style>`: press (scale) and hover feedback on all buttons, chips, cards, back/icon buttons, gallery thumbs, tab-bar icons, chat send, and time-range remove; visible disabled-button styling (opacity, not-allowed cursor); card hover lift; search and form-field focus polish; success-ring pop animation on confirmation screens; `prefers-reduced-motion` fallback. Also made the Profile tab SVG icon use `currentColor` so it turns blue when active like the PNG icons (invert filter scoped to `img.tab-ic-img`). Verified: braces balanced (461/461), 16 screens intact, no leftover hardcoded icon fills. |
| 2026-06-24 | Home header logo mark shrunk from 52px to 26px (half size). |
| 2026-06-24 | Detail screen: owner stats (exchanges, rating, items listed) moved inside the owner card under an "Owner's track record" label and rendered with the same `.chip-meta` green badges as the item stats, so they clearly read as the owner's, not the item's. Removed the old 3-column `.trust` block. Then lightened `--bg` from `#F0EDE6` to `#FAF8F3` (warmer, near-white) for all screens. |
| 2026-06-24 | Side caption rewritten into three tabbed flows (1 Borrow / 2 List / 3 Pass it on). Every step now has a green value point (`.cap-value`) explaining why it matters, plus a clickable `step-link` that jumps to the live screen (search link auto-runs a tent search; relist link calls `startRelist()`; achievement link previews the badge). `showCaption()` handles the new `relist` tab. Verified with jsdom (10 checks, 0 errors). |
| 2026-06-24 | Navigable prototype pass. (1) Item listings now data-driven: `ITEMS` array of all 12 home items drives the home feed, search results, and a per-item detail screen (`openDetail(id, from)` fills photo gallery, name, description, owner, origin, trust; back target is dynamic). Search (`runSearch()`) filters by detected category. (2) Relist flow: "Pass it on" on the borrowed card calls `startRelist()`, which prefills name/description/condition/category/photo from the borrowed tent and shows a relist banner, then reuses the listing screens. (3) Achievement modal: completing a pass-on calls `finishListing()` → `openAchievement()`, a centered Trail Keeper badge card that animates in over a dimmed background with confetti, then auto-resets to home after ~4.5s (or on tap). New listings still end on `s-list-done`. (4) Messages: all DMs except the most recent (Maya R.) are shown but disabled (`.dm-disabled` + lock glyph). Verified with a jsdom harness (30 checks, 0 errors). |
| 2026-06-24 | Created CLAUDE.md from session history. Documented both flows, brand palette, stack rules, deploy flow, and conventions. |
| 2026-06-24 | Prototype expansion: splash screen, home feed (12 Waikiki items), borrowed-item return card, bottom tab bar, messages list (5 DMs), DM conversation, own + other's profile, item origin on detail screen, return/pass-on bottom sheet. Total screens: 17. |
| 2026-06-24 | Nav redesign: 4-tab bottom nav (Explore/Post/Messages/Profile). SF Pro PNG icons: binoculars=Explore, plus=Post, bubble=Messages, inline SVG person=Profile. Profile moved from header to nav. Logo-mark centered in home header, tagline removed. |
| 2026-06-24 | Home feed polish: "Leaving Soon?" chip moved above item feed; "You borrowed this" label removed from borrowed card; section headers now title case, muted sage color (font-weight 500, no uppercase) — applied across home, profile, and all section labels app-wide. Search icon 24px; icon-to-input gap 8px. |
| 2026-06-24 | "Leaving Soon?" section replaced with a card (recycling icon, value prop, CTA button). Trail Keeper achievement callout (gold-tinted row, medal emoji) moved into the "Borrowed Here" card above the Pass it on / Not passing on buttons, with copy specific to the borrowed item and location. Fixed broken image src for 10-person Instant Cabin Tent in results and home feed (correct filename: `10 person instant back packing tent.jpeg`). |
| 2026-06-XX | Branding integration: CSS variables updated to official TSE palette; inline SVG logo added. |
| 2026-06-XX | Listing flow added: 6 screens (s-list-category through s-list-done). |
| 2026-06-XX | Category detection: both borrow and list flows now use keyword auto-detect instead of static chips. |
| 2026-06-XX | Circular navigation bug fixed: startList/showCaption loop resolved; listing flow lands on details screen. |
