# Cursor Prompt: TSE User Flow Diagram in FigJam

Paste everything below this line into Cursor.

---

## Task

Create a user flow diagram in FigJam for the **Traveler Supply Exchange (TSE)** prototype. The diagram should cover three flows: the borrower hero flow, the create-and-list flow, and the relist flow.

## Step 1 — Orient yourself

Read `index.html`. It is a single-file static prototype with inline CSS and JS. There is no framework, no build step. The entire UI lives in five `<section class="screen">` elements that show/hide via a `go(id)` function. Understand the screen IDs, their content, and the navigation connections before touching any other tool.

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
Forward hook: "When you return this tent to the exchange, it'll be circulated 5× — and you'll earn the Keep It Moving badge."
CTA: "Done" → back to Home
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
"When are you leaving?" — date picker (today / tomorrow / pick date)
"Preferred meetup area" — neighborhood or landmark text field
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

This flow is **now implemented** in the prototype as a prefilled relist. It is the "close the loop" behavior: when a borrower is done with an item, they pass it on to the next traveler rather than keeping or discarding it. Entry is the "Borrowed Here" card on Home → "Pass it on" sheet → a prefilled relist that reuses the listing screens → a Trail Keeper achievement modal. Map it as it exists in `index.html`.

```
[Entry — multiple paths]
  A: Notification — "Your exchange with Maya ends soon. Returning the tent? Keep it moving."
  B: Home → "My borrows" tab/section → active borrow card → "Return to exchange"
  (Show both entry paths converging)
  ↓

[Active borrow detail]
Item name, image, original lender (Maya R.), borrowed date, days held
CTA: "Return to exchange"
  ↓

[Condition check]
"How is it holding up?"
Options (single select):
  ✅ Great — same as when I got it
  👍 Good — minor wear, fully usable
  ⚠️ Worn — works but showing use (add note)
  ❌ Damaged — doesn't work properly (add note, flag for review)
  ↓

[Confirm relist]
Shows preview of relisted item card
Circulation count increments: "This will be circulated 5×"
Meetup availability: "When can you hand it off?" — today / tomorrow / pick date
CTA: "Put it back in the exchange"
  ↓

[Success — Keep It Moving]
"✓ Tent is back in the exchange"
Badge awarded: 🏅 "Keep It Moving" — first-time badge for closing the loop
"This tent has now passed through 5 travelers. You made that happen."
CTA: "Done" → Home
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
