# SadNest — Project Brief (v2, consolidated)

A mental health companion app built around a personal safety plan — always at hand, warm in feeling, action-oriented in a crisis. A soft, safe nest for hard moments.

**Platform decision (updated): mobile-first, React Native via Expo** — not web-first as originally scoped. Reasoning: a crisis tool needs a home-screen icon and instant launch; a browser tab loses precious seconds. One Expo codebase ships to iOS and Android, works offline, and can be tested on a real phone in minutes via Expo Go.

---

## The Red Button Flow (MVP core loop)

1. Big red button on the home screen — one tap, no navigation.
2. App asks how the person is feeling — mood options (Anxious / Sad / Numb / Scared, etc.)
3. For Anxious specifically: a **1–10 intensity scale**, each level mapped to its own strategy (e.g. low levels → grounding/breathing; high levels → simpler, more physical interventions — the higher the number, the less cognitive load the suggestion should require).
4. For Scared: a **physical-action response** — e.g. prompted to go for a walk, change location, move the body. Fear responses lean toward *doing* something physical rather than reflecting.
5. Based on mood + intensity + the saved safety plan, the app surfaces the most fitting response:
   - A distraction from the person's list (pets, outside, YouTube)
   - A coping strategy (music, journaling, breathing, sleep)
   - Or opens Spotify/YouTube directly with something comforting
6. **Feedback loop:** after every suggestion, ask "did this help?" (yes / no / somewhat) and log it. This is what lets the app get more accurate over time.
7. Feels like someone wrapping a blanket around you — warm, not clinical.

## Learning / Personalization — build in stages, not all at once

- **v1 — rule-based, no ML.** Mood → intensity → matching strategy via a simple decision tree. Feedback logged locally but not yet used to change suggestions. Ship this first — predictable, explainable behavior matters more than cleverness in a crisis tool.
- **v2 — feedback-weighted suggestions.** No model needed yet — just track "this strategy worked X/Y times for this mood+level combo" and surface the best-performing one first. This is already meaningful personalization.
- **v3+ — smarter model** only once the rule-based version is validated with real usage and the weighting approach hits its limits.

## Safety Plan Setup

Based on the Stanley-Brown / mysafetyplan.org format:

- ⚠️ My Warning Signs
- 🧘 My Coping Strategies
- 🎯 My Distractions
- 👥 My Supports (friends, family)
- 🏥 My Professional Supports
- 🏠 My Safer Environment
- 📞 Emergency contacts (pre-filled: 988, local equivalents)

Filled in during calm moments. The red button draws from it during hard ones.

## Integrations

- **Spotify** — open a comfort playlist directly from the app
- **YouTube** — deep link to a calming video or channel
- Both should feel like the app is *doing something for you*, not just listing links

---

## Explicitly out of scope: peer/nearby-helper matching

The original brief floated a "nearby helper" / "emotional Uber" phase-2 idea (matching someone low with a nearby volunteer). **Decision: shelve this indefinitely.** Matching a person in crisis with an unvetted stranger creates a real safety risk — a rating system doesn't fix it, since predatory users can farm good ratings over time, and someone in crisis is the least equipped to vet a stranger in the moment. If this is ever revisited, it needs a completely different trust model (licensed counselors, verified professionals), not casual peer matching.

## Monetization — donation jar, not subscriptions

- No paywalls, no feature-gating, no tiers on the core check-in/suggestion/feedback loop — gating actual coping strategies behind payment could directly harm someone who needs them and can't pay.
- Instead: an optional **donation jar** (Ko-fi or Buy Me a Coffee) — a low-key "support SadNest" link in settings, not a popup.
- Keeps the MVP simpler too: no payment logic, no subscription state to build or test.

## v3 "extras" (post-MVP, once the core loop is solid)

- **Flowers** — "order yourself flowers" as a self-care suggestion in the strategy library; as a business feature, use an affiliate link (e.g. 1-800-Flowers, BloomNation) rather than building fulfillment.
- **Postcards** — fits the app's emotional logic well: a physical, delayed-arrival "someone is thinking of you" object.
  - *Send-to-self, scheduled*: write yourself a postcard during a low moment, have it arrive in 2–4 weeks — the most on-brand version.
  - *Send-to-someone*: same idea sent to a friend/family member.
  - Fulfillment via an existing API (e.g. Postable, Touchnote, Postagram) rather than building printing/shipping in-house.

---

## Tech Stack

- **Frontend:** React Native + TypeScript, via Expo
- **Styling:** NativeWind (Tailwind for React Native) — warm, soft design language
- **Auth:** simple (email or magic link — nothing heavy)
- **Data:** safety plan and feedback logs stored locally first, then synced
- **Integrations:** Spotify Web API, YouTube deep links; Ko-fi/BMC link; affiliate links for flowers/postcards (v3)
- **Repo:** GitHub, built via Claude Code

## Design Principles

- Warm, not clinical
- Fast to reach in a crisis (red button = 1 tap from anywhere)
- Feels like care, not a checklist
- Predictable and explainable before it's clever

---

## Build order

1. **MVP:** safety plan setup form → home screen with red button → mood + intensity check → rule-based suggestion → feedback logging
2. **v2:** feedback-weighted suggestion ranking
3. **v3:** donation link, flowers/postcard affiliate integrations, Spotify/YouTube deep links polish
