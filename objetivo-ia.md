# AI Objective #1 — Morning Dashboard App

## Target
A phone-first morning dashboard that feels like a native app:
- Header: day label, greeting ("What's good, Valentino?"), full date, refresh button
- Weather card: city, current temp, condition, high/low, "updated" time
- "Today" card: my Todoist plan (private, encrypted)
- Top Stories carousel (World) with ‹ Today › day navigation
- Tech carousel and "Around Honduras" carousel with colored category chips and "Read" links
- Sports card: this week's matches (Chelsea, Real Madrid, Marathón)
- Daily lesson card + ▶ audio button
- Installable on the home screen, works offline, dark mode
- Built AND maintained by the daily routine (the loop)

## Rules for every step
- One step ≈ 10 minutes, one visible result.
- Work in a Claude Code session on repo `resumen-diario`, branch `claude/resumen`.
- Every Claude Code prompt starts with: "Work directly on branch claude/resumen. Do not create another branch or a pull request."
- A step is done when its "Done when" check passes.

## Phase 1 — Separate data from design
1. **Daily data file.** Routine also writes `data/YYYY-MM-DD.json` and `data/latest.json` (sections: world, tech, honduras, sports, lesson; each item: title, summary, source, url, category, date). Requires a routine prompt update. Done when: today's JSON exists in the repo and is valid.
2. **Day index.** Routine maintains `data/index.json` listing available dates (newest first). Done when: index lists today.
3. **Page reads JSON.** New `app.html` that fetches `data/latest.json` and renders plain sections. Done when: app.html shows today's news without the routine writing any HTML.
4. **Switch over.** `index.html` becomes the app; routine stops copying `plantilla.html` (routine prompt update). Done when: the home URL shows the JSON-driven page.

## Phase 2 — App-style design
5. **Design system.** Warm light background, rounded white cards, soft shadows, bold sans headings, category colors (World red, Tech blue, Honduras orange, Sports purple). Done when: tokens defined as CSS variables.
6. **Header.** Day label, greeting, full date, refresh button that reloads `latest.json`. Done when: header matches the target.
7. **Weather card.** Browser fetches Open-Meteo (no key) for my city; gradient card with temp, condition, H/L, "updated". Done when: live temperature shows.
8. **Top Stories carousel.** Horizontal swipe cards: source chip, headline, 2-line summary, date, "Read". Done when: swiping works on the phone.
9. **Day navigation.** ‹ Today › arrows load other days from `data/index.json`. Done when: yesterday's stories open.
10. **Tech + Around Honduras.** Two more carousels with colored category chips and "See all". Done when: both render from JSON.
11. **Sports card.** One row per match: team, vs/at rival, day, time (Honduras), competition. Done when: this week's matches show.
12. **Lesson card.** Collapsible card with today's step. Done when: it expands/collapses.
13. **Audio.** ▶ button in the header reads the news sections (EN/ES voices). Done when: audio plays on the phone.
14. **Dark mode.** Follows system setting. Done when: it switches with the phone's theme.

## Phase 3 — Make it feel like an app
15. **Installable (PWA).** Manifest, app icon, theme color. Done when: "Add to Home Screen" opens full-screen without browser bars.
16. **Offline.** Service worker caches the shell and last `latest.json`. Done when: opens in airplane mode.
17. **Polish.** Loading skeletons, smooth transitions, "updated X min ago". Done when: no layout jumps on load.

## Phase 4 — Private data, done right
18. **Encrypted "Today" card.** Routine encrypts my Todoist plan (AES-GCM, passphrase from an environment variable) into `data/private.enc`; the page asks the passphrase once and decrypts in the browser. Done when: tasks show on my phone and the repo only holds ciphertext.
19. **Calendar (optional).** Add Google Calendar to the routine and show the next 48 hours in the private card. Done when: today's events appear.

## Phase 5 — Maintain (the loop)
20. **Self-check.** Before pushing, the routine validates every JSON file and fixes errors. Done when: a bad file is caught and repaired in the run log.
21. **Weekly improvement.** On Mondays the lesson proposes one small upgrade based on what broke or felt slow. Done when: the first proposal ships.

## Progress
(The routine appends one line per day: `YYYY-MM-DD · Step N · presented | repeated`.)
2026-10-01 · Step 1 · presented
2026-10-05 · Step 1 · repeated
