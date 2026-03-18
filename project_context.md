# Project Context: LOOM Moderation Demo (`mod cues`)

The `mod cues` project (also known as the LOOM Moderation Demo) is a standalone frontend web demonstration designed to showcase experimental moderation cues in an interactive community space. Built with a retro, terminal/PS2-inspired aesthetic involving CSS CRT scanlines and monospaced typography, the demo features two main interfaces—a Forum and a Chatbox. It implements real-time, visual consequences for hostile behavior using three primary cues: a reactive "Eye Tracker" that monitors chat toxicity, a "Gravity Sink" that visually buries flagged forum posts, and an "Account Integrity" building that slowly collapses after repeated violations until the user is suspended.

---

## Chronological Development Log

Below is the logical and chronological progression of the project's features, from foundational additions to the most recent integrations.

### 1. Base Design & Identity
- **What was added:** Global CSS variables for a dark, retro-tech color palette (deep purples, neon oranges, terminal greens). Implemented a CSS-only `::after` overlay to simulate CRT monitor scanlines.
- **Why it was added:** To establish a cohesive "PS2/retro-forum" aesthetic requested for the demonstration, giving the environment an old-school, system-level feel.
- **Dependencies:** Relies on the external Google Font *Share Tech Mono*.

### 2. Core Navigation & Layout
- **What was added:** A flexbox-driven mobile-width container (`.app`), a global header with the "LOOM" logo, and a tabbed navigation system switching between "FORUM" and "CHATBOX".
- **Why it was added:** To provide distinct testing grounds for different types of moderation cues (long-form threaded posts vs. rapid ephemeral chat).

### 3. Moderation Logic & Profanity Engine
- **What was added:** A hardcoded JavaScript array (`BAD_WORDS`) containing aggressive, toxic, and meta-hostile phrases (e.g., "architecture is pathetic", "hate", "worthless"). A helper function `isBad(text)` evaluates input.
- **Why it was added:** To serve as the simulated "AI" backend for the demo, instantly flagging text without needing a real server connection.
- **Dependencies:** This engine powers all three visual moderation cues.

### 4. Moderation Cue 1: Gravity Sink (Forum)
- **What was added:** Forum post cards with a "going-bad" and "bad" CSS state. When a flagged post is submitted, it animates downward, blurs heavily (`filter: blur(3.5px)`), drops in opacity, and is relegated to the bottom of the feed. Tagged with "⬇ GRAVITY SINK".
- **Why it was added:** To demonstrate a passive moderation strategy where toxic content isn't necessarily deleted immediately, but socially down-weighted and made difficult to read, reducing its impact.

### 5. Moderation Cue 2: Eye Tracker (Chat)
- **What was added:** An interactive SVG eye embedded above the chat input accompanied by a "Watch Count" and a toxicity progress bar.
- **Why it was added:** As the user types toxic words, the toxicity score spikes. The eye turns red and vibrates (`animation: eyeshake`), the progress bar fills, and the observer count jumps artificially (e.g., "76 PEOPLE -> 106 PEOPLE"). This creates an immediate psychological cue that the community is watching and judging hostile behavior.

### 6. Moderation Cue 3: Account Integrity (Header)
- **What was added:** A miniature 4-story CSS building (`.mini-bld`) positioned next to the user's avatar. Also introduced a global `strikes` variable.
- **Why it was added:** To represent account health. Every time a bad message is posted in the chat or forum, a strike is issued. At 2 strikes, cracks appear. At 3 strikes, rubble animations trigger. At 5 strikes, the building entirely flattens. It provides long-term consequence tracking.

### 7. Suspension System & Modal
- **What was added:** A stark red "ACCOUNT SUSPENDED" modal blocking the UI and a suspended banner in the header. Posts and chats are disabled while this is active.
- **Why it was added:** The ultimate consequence of zero Account Integrity. Demonstrates the final fail-state of the moderation loop, requiring the user to "submit an appeal" (which resets the demo state).
- **Dependencies:** Triggered by Moderation Cue 3 reaching 5 strikes.

### 8. Demonstration Controls
- **What was added:** `<div class="demo-bar">` sections at the bottom of both tabs containing buttons like "+ Good Post", "⚠ Bad Post", "⬇ Strike", and "⬆ Restore".
- **Why it was added:** To allow presenters to instantly showcase the cues (injecting pre-written toxic or positive posts) without manually typing out scenarios every time.

### 9. Alternative/Exploratory Code (`code.html`)
- **What was added:** A separate HTML file using TailwindCSS, featuring a "Console Social" layout, glitch vibration animations, and different font choices (Public Sans / Press Start 2P).
- **Why it was added:** Likely an exploratory styling iteration or structural mockup tested before settling on the vanilla CSS approach used in the final `index.html`.

---

## Current State

The project stands as a fully realized, interactive, static front-end prototype. It relies purely on vanilla HTML, CSS, and JavaScript with zero backend dependencies, utilizing a simulated local profanity filter to trigger state changes. 

All three moderation cues—**Gravity Sink**, **Eye Tracker**, and **Account Integrity**—are fully functional and interconnected via a global strike system. The inclusion of live presentation controls makes the site ready for immediate live demonstration. The repository has been initialized with Git, capturing the codebase and associated graphic assets (`blur cue.png`, `eye cue.png`, `rubble cue.png`) in a single deployable environment.
