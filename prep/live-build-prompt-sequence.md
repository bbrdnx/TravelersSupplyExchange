# TSE — Live Build Prompt Sequence

A staged set of small prompts to drive an AI build (Claude cowork or Cursor) for the "I need it tonight" hero flow. The point is not the prompts, it's that you **prompt in small steps, read the output critically, and make the design calls out loud.** Talk between every step.

**Before you start, say this:** "I'm going to build one flow, not the whole app. The flow that proves the riskiest assumption, that a traveler can find and safely get gear they need nearby. I'll build it in small steps and steer as I go."

---

## Step 0 — Set up the canvas (10 sec, say it aloud)
> Create a single self-contained HTML file with inline CSS and JS, no build step, no dependencies. It renders a mobile phone frame (about 390px wide) centered on the page, with simple screen-switching via a `go(id)` function that toggles an `active` class. Mobile-first, clean, lots of white space.

*Say:* "I want zero setup friction so I can iterate fast in front of you."

---

## Step 1 — Home / state the job
> Build screen 1: the home screen. App name "Traveler Supply Exchange" with a one-line tagline "Borrow what your trip needs. Pass on what it leaves behind." A search bar that says "What you need?", and a row of tappable category chips: Tent, Sleeping bag, Camp stove, Beach chair, Cooler. Tapping the search or any chip goes to the results screen.

*Say:* "I'm leading with the user's job in their words, not a logo splash. One primary action."

---

## Step 2 — Results / let the data do the trust work
> Build screen 2: results for "Tents near you." A header "4 available within 2 miles." Then 4 item cards, each with a thumbnail, title, distance (e.g. 0.3 mi), owner first name, a green "Free" badge, and a "circulated N times" badge. Tapping a card opens the detail screen.

*Say:* "Two signals are carrying the whole concept here, distance and how many times this item has been re-circulated. That re-circulation count is doing trust and sustainability work at once."

---

## Step 3 — Item detail / make trust explicit
> Build screen 3: item detail. Large image area, title, "Free" pill, a short description, then a clear **"Not for sale"** notice explaining TSE is exchange-only and to report anyone asking for money. Below that, an owner card with avatar, name, an "ID verified" mark, and an exchange count. Then three small trust stats: re-circulated count, distance, and exchange rating. A primary "Request this item" button pinned to the bottom.

*Say:* "The risk in any stranger exchange is trust and safety, so I'm making it loud, not burying it. The 'not for sale' stance is a product decision, I'm showing it as a first-class element."

---

## Step 4 — Safe exchange / safety as a screen, not fine print
> Build screen 4: "Arrange a safe exchange." Before confirming, show 3 ground-rule rows with icons: meet in a well-lit public place (never your room or Airbnb); no money changes hands (report anyone who asks); bring a friend and share your location. Then a highlighted legal reminder: if an item is illegal to possess in this country, it's illegal to exchange on TSE. Primary button: "Send request & suggest a meeting spot."

*Say:* "This is the screen I care most about. Safety isn't a checkbox in settings, it's a moment in the flow, right before they commit."

---

## Step 5 — Confirmation / reward the loop
> Build screen 5: a success state. Big checkmark, "Request sent." A line that you'll be notified when they confirm a public meeting spot. Then a line that returning the item later circulates it again and earns a "Keep It Moving" badge. A "Done" button returns home.

*Say:* "I'm closing on the behavior the whole system depends on, returning the item. The reward points at re-circulation, not just taking."

---

## Step 6 — One polish pass (only if time)
> Tighten spacing and typography for a clean, modern, trustworthy feel. Add a subtle slide transition between screens. Don't add new screens or features.

*Say:* "Time check, I'd rather have one flow that feels real than five rough ones. Polishing the flow I have."

---

## If you have extra time, pick ONE (say why you chose it)
- **Offload flow:** the "list gear you can't take home" side. *Why:* it's the supply half of the loop.
- **Empty state:** what the user sees when nothing's nearby. *Why:* it's the honest answer to the cold-start problem.
- **Item journey:** a little map of where this item has traveled. *Why:* it's the emotional hook and the sustainability story.

---

## Closing line (don't skip this)
> "If this were real, the first thing I'd test isn't the UI, it's supply, whether travelers actually list gear when they leave. I'd measure exchange completion rate and supply density per destination. The flow I built is the part I was most sure I could make feel safe and simple, so I built that first."

---

### Steering reminders (keep visible)
- Prompt **small**. One screen or one decision per prompt.
- Before you run a prompt, **say what you expect.** After, **react to what you got.**
- When the AI overreaches, **cut it back** out loud: "That's more than I asked for, I'll keep it to the one flow."
- Never go silent while it generates, narrate what you're watching for.
- You are the editor. The tool is the intern.
