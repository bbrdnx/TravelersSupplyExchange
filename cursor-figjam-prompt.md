# Cursor Prompt: TSE User Flow Diagram in FigJam

Paste everything below this line into Cursor.

---

## Task

Create a user flow diagram in FigJam for the **Traveler Supply Exchange (TSE)** prototype. The diagram should cover three flows: the borrower hero flow, the create-and-list flow, and the relist flow.

## Step 1 — Orient yourself

Read `index.html`. It is a single-file static prototype with inline CSS and JS. There is no framework, no build step. The UI lives in sixteen `<section class="screen">` elements (borrow, list/pass-on, and supporting screens) that show/hide via a `go(id)` function, plus several bottom-sheet overlays (welcome, receive/review, pass, keep, thank-you) and an achievement modal. Understand the screen IDs, the overlays, their content, and the navigation connections before touching any other tool.

## Step 2 — Create the FigJam diagram

Use the Figma MCP (`generate_diagram` or the FigJam tools) to create a new FigJam file. Title it **"TSE — User Flows"**.

Map out three flows as described below. Lay them out as three horizontal swim lanes, one per flow, reading left to right.

---

## Flow 1 — "I need it today" (the borrow hero flow)

This flow is fully implemented in the prototype. Map it exactly as it exists.

**Entry:** User opens the app.

```
[Home]
Brand header + tagline
Search bar: "What do you need?"
Quick chips: Tent / Sleeping bag / Camp stove / Beach chair / Trekking poles / Cooler
Leaving soon chip: "List gear you can't take home" → branches to Flow 2
  ↓ tap any chip or search bar

[Results]
"Tents near you" — 4 results
Each card: item name, distance, owner name, Free badge, circulation count (e.g. ↻ 4×)
  ↓ tap a card

[Item Detail]
Hero image, title, Free pill
Description
"Not for sale" notice (TSE is exchange-only, report anyone who asks for money)
Owner card: name, ID verified badge, exchange count, rating
Trust stats: re-circulated ×N, distance, star rating
CTA: "Request this item"
  ↓

[Safe Exchange]
Ground rules (three rows):
  • Meet in a well-lit public place
  • No money changes hands
  • Bring a friend if you can
Legal note: items illegal to possess are illegal to exchange on TSE
CTA: "Send request & suggest a meeting spot"
  ↓

[Success — Request Sent]
"Request sent to Maya"
"You'll get a notification when she confirms a public meeting spot near you."
Forward hook points at returning the item to circulate it and earn the Keep It Moving badge.
CTA: "Continue"
  ↓

[Receive + review sheet]
"Did you get the item?" — item summary plus a tappable star rating
Confirm is disabled until a rating is chosen
  ↓ confirm

[Home — Borrowed Here]
The borrowed item now appears in a "Borrowed Here" section on Home (and in the profile's Currently Borrowing), with a Trail Keeper teaser → branches to Flow 3
```

---

## Flow 2 — Create & list an item

This flow is **now implemented** in the prototype (screens `s-list-category` through `s-list-done`). Map it as it exists, reading `index.html` for the exact screens; the outline below matches the build. Entry is the "List gear you can't take home" card on Home.

```
[Home] — entry via "List gear you can't take home" chip
  ↓

[What are you listing?]
Category chips: ⛺ Tent / 🛌 Sleeping bag / 🔥 Camp stove / 🪑 Chair / 🥾 Poles / 🧊 Cooler / Other
  ↓ select category

[Item details]
Fields: Item name (pre-filled from category, editable), Condition (Great / Good / Worn but works), Short description (140 chars)
  ↓

[Add a photo]
Camera or library — single photo minimum
Skip option (not recommended — trust signal note shown)
  ↓

[Pickup logistics]
"When can you meet?" availability windows (add a day + time range, or tap a quick-add suggestion chip)
"Preferred meetup area" text field, with tap-to-fill location suggestion chips
  ↓

[Preview your listing]
Shows a card that matches how it appears in Results
  — item image, name, Free badge, "circulated 0×", user's name + verified status
Reminder: "No money, ever. Exchange only."
CTA: "List it"
  ↓

[Listed — Success]
"Your [item name] is live"
"Travelers near you can see it now. You'll get a notification when someone requests it."
Forward hook: "Once someone borrows it and passes it on, it earns its first ↻ circulation."
CTA: "Done" → Home
```

---

## Flow 3 — Relist a borrowed item

This flow is **now implemented** in the prototype. It is the "close the loop" behavior: when a borrower is done with an item, they pass it on to the next traveler rather than keeping or discarding it. Entry is the "Borrowed Here" card (on Home after a borrow, and in the profile's Currently Borrowing). It branches into two paths, both of which restart the prototype at the end. Map it as it exists in `index.html` (the pass and keep sheets, then the relist screens or the thank-you sheet).

```
[Entry — Borrowed Here card]
Item thumb, original lender, borrowed date, circulation count, Trail Keeper teaser
Two buttons: "Pass it on" (secondary) and "Not passing on" (tertiary)
  ↓ branches

— Path A: Pass it on —
[Pass-it-on sheet]
Item summary + "Pass it on to the next traveler"
  ↓
[Relist (prefilled)]
Reuses the listing screens (details / photo / logistics / preview), every field prefilled from the borrowed item
  ↓ "List it"
[Trail Keeper achievement modal]
Badge animates in with confetti; circulation shows N+1
  ↓ (tap or auto) restarts the prototype

— Path B: Not passing on —
[Not-passing sheet]
Reason checklist (keeping it / consumed / no longer usable / passed off app / other)
  ↓ Submit
[Thank-you sheet]
"Thanks for letting us know"
  ↓ Done restarts the prototype
```

---

## Diagram conventions

- **Screen node:** rounded rectangle, label = screen name in bold, sub-label = 1–2 key elements shown on screen
- **Action / CTA:** pill-shaped connector label on the arrow (e.g., "Tap 'Request this item'")
- **Decision point:** diamond node (e.g., condition check branching on "Damaged")
- **Entry point:** filled circle
- **Terminal / Home return:** double-bordered rounded rectangle
- **Trust / safety callout:** sticky note in gold (#F7B32B) pinned next to any screen that has a safety or trust signal
- All three flows are implemented; render them with the same solid style (no dashed "not built" treatment)
- Use TSE's brand color `#127475` (teal) for flow swimlane headers

## Notes

- Keep all three flows in a single FigJam file, three swim lanes
- The diagram is for design communication, not engineering spec — favor clarity over exhaustiveness
- If `generate_diagram` accepts a Mermaid or structured description, pass the flow text above; if it needs a different format, adapt accordingly
- After creating the diagram, share the FigJam URL
