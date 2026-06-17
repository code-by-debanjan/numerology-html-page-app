# MyNumerologyApp

A single-page, zero-dependency numerology calculator built with pure HTML, CSS, and JavaScript. No framework, no build step — open `index.html` in any browser and it works.

---

## Features

### Core Calculations

- **Moolank (Birth Number)** — day of birth reduced to a single digit
- **Bhagyank (Destiny Number)** — full date of birth reduced, with Life Path detection (Master Numbers 11, 22, 33 preserved)
- **Naamank (Name Number)** — Chaldean or Pythagorean sum of the full name

### Numerology Systems

- **Chaldean** (default) — ancient system where 9 is unassigned; letters map to 1–8
- **Pythagorean** — sequential A=1…Z=8 mapping; toggled via a segmented selector in the sidebar

### Grids

- **Lo Shu Grid** — 3×3 magic square populated with DOB digits; repeated digits shown as dots
- **Vedic Grid** — alternative 3×3 placement; adjacent number pairs detected as Yutis

### Compound Number · Auspicious Check _(Chaldean only)_

- Each word in the name gets its own compound sum with an **Auspicious / Inauspicious** badge
- Keyword and meaning shown for every number in the 10–52 range (e.g. _Star of the Magi_, _Hidden Dangers_)
- Numbers **above 52** use a chain-reduction algorithm: subtract 9 until ≤ 52, build a chain down to ≥ 10, then majority-vote the verdict — with a visual chip trail showing each step

### Planetary Relationship Tables

- **Moolank & Bhagyank** — planet-to-planet relationship (Friend / Neutral / Enemy)
- **Naamank & Moolank** — compatibility check
- **Naamank & Bhagyank** — compatibility check
- Tables include highlighted rows, full borders, and alternating row stripes

### Vedic Yutis

- All adjacent number pairs in the Vedic Grid are matched against a 36-entry Yuti table
- Each Yuti card shows: planet pair, Positive / Virodhi / Conditional / Neutral badge, effects, and Upaay (remedy)

### Reference Pages

- 📖 **[Compound Numbers Guide](compound-numbers.html)** — full 10–52 reference with keywords, meanings, auspiciousness, and step-by-step explanation of the above-52 algorithm with worked examples
- 🪐 **[Vedic Yutis Reference](yutis.html)** — all 36 planetary conjunctions with filterable cards by type

### UI / UX

- **Dark / Light theme** toggle — dark (default) uses deep navy/purple palette; light uses warm parchment/amber tones
- **Auto-calculate on load** — pre-filled with today's date and "John Smith" as a demonstration default
- Responsive layout with a fixed sidebar and scrollable main content area
- Angel number detection (11, 22, 33, 44 … 99) shown as badges on core number cards

---

## File Structure

```
numerology-html-page-app/
├── index.html               # Main app (single file, fully self-contained)
├── compound-numbers.html    # Reference: compound number meanings & algorithm
├── yutis.html               # Reference: all 36 Vedic Yutis
└── README.md
```

---

## Usage

1. Open `index.html` in any modern browser — no server required.
2. Enter a **Date of Birth** and **Full Name**.
3. Select **Chaldean** or **Pythagorean** numerology system.
4. Click **Generate Grid**.
5. Use the **Dark / Light** toggle to switch themes.
6. Click the reference buttons in the sidebar to open the Compound Numbers or Yutis guide.

---

## Numerology Logic

| Term            | Description                                                                        |
| --------------- | ---------------------------------------------------------------------------------- |
| Moolank         | Day of birth reduced to 1–9 (Master Numbers preserved)                             |
| Bhagyank        | Full DOB (DD+MM+YYYY) reduced to single digit or Master Number                     |
| Naamank         | Sum of letter values (Chaldean or Pythagorean) reduced to single digit             |
| Compound Number | Any name-part sum ≥ 10 before reduction                                            |
| Auspicious Set  | {10,13,17,19,20,21,23,24,25,27,30,31,32,33,34,36,37,39,40,41,42,45,46,48,49,50,51} |
| Yuti            | A planetary conjunction formed by two adjacent numbers in the Vedic Grid           |

---

## License

See [LICENSE.txt](LICENSE.txt).
