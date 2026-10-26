# LocaLive

A Next.js dashboard that shows live location updates for an active session on a Leaflet map. The home page (`app/page.tsx`) subscribes to Supabase realtime changes on the `sessions` and `locations` tables: when a session is active, the map follows its latest position (latitude, longitude, accuracy and heading) and draws the travelled path. A dashboard header, an intelligence panel (`components/osint/OsintIntelPanel`) and a system status bar show the session state (idle, searching, activating, tracking, terminating).

## What it does

- **Live map dashboard (`/`)** — follows the active session's location in realtime, with a marker, accuracy circle, heading and path history.
- **Session handling** — picks up the latest active session from the `sessions` table, reacts to new sessions and to session termination (which clears the map and resets the view).
- **Share pages (`/share/[sessionId]`)** — per-session share pages.
- **OSINT pages (`/osint`)** — the app's OSINT section, backed by `components/osint/`.
- **API routes (`app/api/`)** — backend endpoints for the app.

## Tech stack

- Next.js 14 (App Router) + React 18 + TypeScript
- Supabase (`@supabase/supabase-js`) for sessions/locations storage and realtime subscriptions — schema in `supabase_schema.sql` and `supabase_update.sql`
- Leaflet via `react-leaflet` for the map
- Tailwind CSS 3 + Lucide icons, `zod` for validation

## How to run

```bash
npm install
npm run dev
```

Open http://localhost:3000 with your browser to see the result. Other scripts from `package.json`:

```bash
npm run build   # next build
npm run start   # next start
npm run lint    # next lint
```

## Project structure

```
app/
  page.tsx            # Live map dashboard (home page)
  layout.tsx          # App layout
  api/                # API routes
  osint/              # OSINT pages
  share/[sessionId]/  # Per-session share pages
  fonts/              # Font files
components/
  Map.tsx             # Leaflet map component (dynamically loaded, client-only)
  DashboardHeader.tsx # Dashboard header
  SystemProgressBar.tsx
  osint/              # OsintIntelPanel and related components
lib/
  supabase.ts         # Supabase client
supabase_schema.sql   # Database schema
supabase_update.sql   # Database update script
next.config.mjs       # Next.js configuration
```
