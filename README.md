# Task Catcher

A single-file, browser-only, domain-agnostic personal organizer. Where
[Project Manager](https://github.com/laustenfaund/ProjectManager) tracks one
kind of thing (construction projects) with a fixed set of tabs, Task Catcher
is built for whatever a person actually needs organized — appointments,
doctors, medications, tasks, notes, or anything else — through user-named
modules instead of a fixed structure.

See [`DESIGN.md`](DESIGN.md) for the full reasoning behind every decision
below, including why this is its own app rather than a Project Manager
feature.

## Status: working prototype (Phases 1–4 of 5)

## What's built

- **Modules** — pick a pre-made template from the **Library** (a few generic
  starters, plus a first Medical pack: Doctors, Appointments, Referrals,
  Medications, Notes to Bring), describe what you need and let **AI propose
  one** (fields, and links to what you already have — reviewed and editable
  before anything is created), or build one yourself field by field
  ("Advanced," tucked below the AI option). Name it yourself; it joins the
  sidebar.
- **Records** — add, edit, delete records in any module, rendered
  appropriately for that module's shape (table, checklist, notes, or dated
  event). Every record gets a built-in Notes field automatically.
- **Cross-module links** — a field can link to one or many records in
  another module, always chosen manually. Any record's page shows what it
  links to *and* what links back to it (backlinks), each clickable. Deleting
  something with live backlinks warns first, naming the count; a link that
  goes stale another way shows as "no longer exists" rather than vanishing
  silently.
- **Sync** — per module, a shape-aware choice of Google Sheets / Docs /
  Calendar, reusing Project Manager's existing OAuth pattern (bring your own
  Google Cloud project). A combination that would silently lose meaning is
  refused outright with a reason; one that's just a lossy fit is offered
  with a disclosed warning first. One-way push only, same as the rest of
  the family — nothing is ever read back from Google.
- **AI capture** — Quick Capture on the home page takes typed text and/or a
  photo, and an "AI clean up" pass turns it into one organized note for you
  to review before saving. Uses your own Anthropic key (Connections), same
  BYOK pattern as U/I and Archive Mole.
- **Home page** — four collapsed cards (Quick capture, Coming up, Next
  steps, Unanswered questions), each expanding to a full list on click.
- **Schema editing** — editing a module's fields after records already
  exist in it follows a confirm-then-refuse pattern: a field deletion or
  type change that would lose or corrupt data asks for confirmation or is
  refused outright with an error naming which records are the problem —
  never silently applied partway.
- **Connections** — one place (gear icon, sidebar) to store your Anthropic
  key and Google Client ID / API key. Stored only in this browser; the
  Google sign-in itself doesn't persist across a reload, same as Project
  Manager.

**Not yet built:** Drive file/photo-reference modules — the last open piece
of Phase 5.

## Storage & privacy model

Same pattern as the rest of the family: everything lives in this browser's
`localStorage` on this device. No account, no server. The only network
calls are the direct ones you trigger yourself — an Anthropic API call for
AI capture/module setup, or a Google API call when you click Sync — using
keys you supply under Connections. Nothing routes through a server of ours.

## Usage

Download `index.html` (or clone this repo) and open it directly in a
browser. No build step, no install.

## Installing on your phone

`manifest.json`, `sw.js`, and `icons/` make this app installable as a PWA
once hosted somewhere over `https://` (e.g. GitHub Pages) — a real app
icon (the watercolor stripe motif), a name, and a minimal offline shell
cache instead of just a bookmark.

1. Make sure this repo is public (Settings → Danger Zone → Change
   visibility), then enable GitHub Pages (Settings → Pages → Deploy from
   branch → `main` → `/` root).
2. Once it's live, open `https://<your-username>.github.io/Task_Catcher/`
   on your phone — not the repo's `github.com` page.
3. Use your browser's "Add to Home Screen" / "Install app" option.

## License

All rights reserved — see [`LICENSE`](LICENSE). Shared for personal
reference; reuse requires asking first.
