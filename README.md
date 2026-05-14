# Lucy's Lantern

> *A quiet place for the words that matter.*

Lucy's Lantern is a reflective quote app designed around calm interaction, lightweight personalization, and simple content management. It allows users to curate personal quotes, pair them with visual backgrounds, and return to a focused reading experience that feels intentional rather than noisy.

Built as a personal portfolio project by a systems-minded developer who cares about user experience, clean organization, and thoughtful app behavior.

---

## Features

- **Quote management** — Add, edit, delete, and favorite personal quotes with optional author and mood tags
- **Visual backgrounds** — Upload custom photos or use curated gradients as dynamic backgrounds
- **Shuffle mode** — Randomly cycle through quotes and backgrounds for a fresh reading experience
- **Auto-refresh** — Configurable timer quietly rotates content on an interval (15s to 10min)
- **Favorites** — Mark quotes as favorites; they surface preferentially during shuffle
- **Light / Dark theme** — Full theme toggle with warm, carefully crafted color palettes for both modes
- **Manage view** — Dedicated page to review, edit, and organize all saved quotes and backgrounds
- **Day-part awareness** — Subtle time-of-day greeting sets a contextual tone (morning, afternoon, evening, night)
- **Mobile-first layout** — Responsive design with safe-area insets and a floating dock navigation
- **Persistent state** — Quotes and backgrounds are stored in a backend API and survive page refreshes

---

## Why I Built This

I wanted a personal app that felt like it was built *for me* rather than for a crowd. Most productivity tools are loud: notifications, metrics, streaks. I wanted something quieter.

Lucy's Lantern is the result of that: a small shell where you can drop in a quote you want to carry with you, set a background that matches your mood, and come back to it later. The name comes from the idea of a lantern as something small, warm, and personal — not a floodlight, just enough to see by.

From a technical standpoint, this project gave me hands-on experience with component-driven UI architecture in React, state management with TanStack Query, custom theming with CSS variables, and building a responsive layout with Tailwind CSS that holds up across device sizes.

---

## Tech Stack

| Layer | Technology |
|---|---|
| Framework | React 18 |
| Build tool | Vite |
| Styling | Tailwind CSS v3 |
| Component library | Radix UI primitives |
| State / data fetching | TanStack Query (React Query) |
| Icons | Lucide React |
| Typography | Plus Jakarta Sans, Source Serif 4, JetBrains Mono |
| Routing | React Router |
| Backend | REST API (quote and background persistence) |

---

## Project Structure

```
lucys-lantern/
├── index.html              # App entry point
├── favicon.svg             # Custom SVG lantern icon
├── .gitignore
├── README.md
└── assets/
    ├── index-[hash].js     # Compiled React app bundle (Vite output)
    └── index-[hash].css    # Compiled Tailwind stylesheet (Vite output)
```

**Key app sections (from the source):**

- `/` — Main quote display view with dock controls (shuffle, add, settings, manage)
- `/manage` — Full management interface with tabs for Quotes and Backgrounds
- Quote editor dialog with text, author, and mood fields
- Background manager with upload support and gradient presets
- Auto-refresh settings via popover with live interval slider

---

## Getting Started

This project is distributed as a pre-built static app. To run it locally:

### Option 1: Serve the static files

```bash
# Clone the repository
git clone https://github.com/Luzija/lucys-lantern.git
cd lucys-lantern

# Serve with any static file server, e.g.:
npx serve .
# or
python -m http.server 8080
```

Then open `http://localhost:8080` (or the port shown) in your browser.

> **Note:** The app connects to a backend API for data persistence. Quote and background data will be fetched from the configured API endpoint. If running fully locally without a backend, the app will display an empty state — you can still explore the UI and add content.

### Option 2: Deploy to a static host

Drop the repository contents into any static hosting platform:
- **GitHub Pages** — enable in repository Settings > Pages
- **Netlify** — drag and drop the folder into the Netlify dashboard
- **Vercel** — import the repo and set output directory to `/`

---

## Design Decisions

- **Warm color palette** — The light theme uses `#f5ebda` (parchment) as the background and muted terracotta/amber as primary accents. The dark theme uses `#171210` (near-black brown), keeping warmth in dark mode rather than defaulting to blue-grays.
- **Glass morphism UI** — Cards, chips, and the dock use frosted glass styling (`backdrop-filter: blur`) to keep content visible behind animated backgrounds.
- **Breathing animation** — Background images use a subtle `breathe` keyframe animation (gentle scale + translate) to make the interface feel alive without being distracting.
- **Readability scrim** — A radial gradient overlay sits between the background and the content layer, ensuring quote text remains legible against any uploaded photo.
- **Serif italic for quotes** — Quote text uses Source Serif 4 in italic to visually distinguish it from UI chrome and evoke the feeling of reading from a notebook.

---

## Future Improvements

- [ ] Source code release with full Vite + React project setup
- [ ] PWA support (offline access, home screen install)
- [ ] Quote import via CSV or plaintext paste
- [ ] Keyboard navigation between quotes (arrow keys)
- [ ] Export quotes as a styled PDF or image card
- [ ] Shared collections — generate a read-only link to your quote set
- [ ] Tag-based filtering and search within the manage view
- [ ] Smooth background crossfade transitions during auto-shuffle

---

## License

This project is personal portfolio work. Feel free to fork and adapt it for your own use.

---

*Built with care in Denver, CO.*
