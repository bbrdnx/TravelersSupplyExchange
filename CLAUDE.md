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
| `--bg` | `#F0EDE6` | Page background / cream |
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
