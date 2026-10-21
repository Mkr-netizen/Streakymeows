# Streaky Habit Tracker — implementation and design

## Approved product direction

Build a responsive, account-free habit tracker as a static React web app. A person can create, edit, and delete habits with a name, emoji, and color; check or uncheck each one for the current local calendar day; view current and best streaks; inspect a GitHub-style year grid for an individual habit; and see a weekly consistency summary. Persist both habits and completion history in browser `localStorage`; do not add login, a server, or a database. Favor touch-sized controls and a portrait-first mobile layout while adapting the workspace for wide screens.

## Design

Three candidate directions: Joyful editorial stationery (0.07), soft garden minimalism (0.05), candy arcade dashboard (0.03). Choose **joyful editorial stationery**, carrying forward the approved playful and satisfying spirit.

- **Design Movement:** contemporary editorial stationery with tactile, paper-like surfaces and playful ink marks.
- **Core Principles:** make progress legible at a glance; celebrate small actions without pressure; keep controls welcoming and thumb-friendly; use color to identify habits as well as to decorate.
- **Color Philosophy:** warm paper and dark plum ink keep the interface calm and readable; coral is the brand's energetic accent, supported by mint, lilac, lemon, and sky-blue habit colors. Keep contrast high and never make color the only progress signal.
- **Layout Paradigm:** a clear top-of-page daily agenda flows into a weekly recap, then a scrollable year-in-pixels archive. On wide screens, align these into a spacious asymmetric content column rather than a dense dashboard grid; on mobile, stack sections and keep the main check-off action near the top.
- **Signature Elements:** a small four-petal/spark mark for Streaky; color-rimmed emoji tiles; rounded contribution cells with subtle day labels and celebratory check marks.
- **Interaction Philosophy:** checking is one clear tap, immediately reflected in the checkmark, daily count, weekly chart, streaks, and heatmap. Editing and deleting remain discoverable but secondary. Respect reduced-motion preferences.
- **Animation:** brief spring-like check pop, gentle row entrance/reorder, and a few restrained sparkle flecks after a check; use short opacity/transform transitions and disable nonessential motion with `prefers-reduced-motion`.
- **Typography System:** use a friendly rounded display face for headings and a highly legible system sans for controls and data, with tabular numerals for streaks. Use a restrained scale: compact eyebrow, bold page title, clear section headings, readable 14–16px body text.
- **Brand Essence:** a cheerful private habit companion that makes steady effort easy to see; **bright, kind, encouraging**.
- **Brand Voice:** brief, warm encouragement without guilt. Examples: “A little progress adds up.” and “Nice one — today is in the books.”
- **Wordmark & Logo:** “Streaky” paired with a simple hand-drawn four-petal spark made from rounded teardrops; render as lightweight inline vector/CSS artwork so it remains crisp and needs no external image.
- **Signature Brand Color:** vivid coral `#F27767`, used for primary action and small celebratory accents.

## Implementation and project structure

Use the initialized Vite + React + TypeScript static starter with its existing dependencies and `pnpm dev:static`; keep both configured server and database disabled. No account, network persistence, or external API is involved.

- `client/src/pages/Home.tsx`: compose the daily agenda, weekly summary, year section, empty state, and habit editor.
- `client/src/features/habits/model.ts`: habit and completion types, storage key/version, and safe local-storage read/write helpers.
- `client/src/features/habits/dates.ts`: local date-key, week/year generation, completion, and streak calculations.
- `client/src/features/habits/useHabits.ts`: state lifecycle and create/edit/delete/check actions synchronized to local storage.
- `client/src/components/habits/HabitCard.tsx`: color/emoji habit row, completion action, streaks, and edit/delete controls.
- `client/src/components/habits/HabitEditor.tsx`: accessible create/edit dialog with name, emoji, and color selection.
- `client/src/components/habits/YearHeatmap.tsx`: accessible, horizontally scrollable GitHub-style calendar cells for the selected habit and year.
- `client/src/components/habits/WeeklySummary.tsx`: current-week totals, completion ratio, and daily activity bars.
- `client/src/index.css`: responsive editorial-stationery visual system, focus states, and reduced-motion rules.
- `client/public/manus-routes.json`: route manifest for the single-page `/` route.

Use browser-local dates (not UTC date slicing) so midnight and streak calculations follow the person's calendar. Make storage parsing defensive and tolerate unavailable storage without losing the in-session app. Start with an empty state and quick-add suggestions rather than silently inventing or preloading user habits. Keep the static project shell, and do not alter unused server/database starter code.
