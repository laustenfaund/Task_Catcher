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

## Status: early prototype (Phase 1 of 5)

This is the module engine and local record-keeping only — the part of the
design with no existing code to reuse from the rest of the family. **Not
yet built:** cross-module links & backlinks, sync (Sheets/Docx/Drive/
Calendar), and AI photo capture. See "Build phases" below.

## What's in this prototype

- **Modules** — pick a pre-made template from the **Library** (a few generic
  starters, plus a first Medical pack: Doctors, Appointments, Referrals,
  Medications, Notes to Bring) or build a custom one from scratch. Name it
  yourself; it joins the sidebar.
- **Records** — add, edit, delete records in any module, rendered
  appropriately for that module's shape (table, checklist, notes, or dated
  event). Every record gets a built-in Notes field automatically.
- **Home page** — four collapsed cards (Quick capture, Coming up, Next
  steps, Unanswered questions), each expanding to a full list on click.
- **Schema editing** — editing a module's fields after records already
  exist in it follows a confirm-then-refuse pattern: a field deletion that
  would lose data asks for confirmation first; a field-type change that
  existing values genuinely don't fit is refused outright, with an error
  naming which records are the problem — never silently applied partway.

## Build phases

1. **Module engine + Library + local record CRUD** — this prototype.
2. Cross-module links and the backlink index (the one piece of
   infrastructure with no precedent elsewhere in the family).
3. Sync — porting Project Manager's existing Google OAuth / Sheets / Docx /
   Drive pattern, plus Calendar as a new push target.
4. AI capture — porting the BYOK Claude pattern from U/I and Archive Mole,
   scoped narrowly to "messy photo/text → one clean organized note."
5. The Medical pack's content, home-page polish, PWA installability
   (manifest/service worker/icons, following the same pattern as the other
   three apps).

## Storage & privacy model

Same pattern as the rest of the family: everything lives in this browser's
`localStorage` on this device. No account, no server, nothing sent
anywhere — this prototype phase doesn't call any external service at all.

## Usage

Download `index.html` (or clone this repo) and open it directly in a
browser. No build step, no install.

## License

All rights reserved — see [`LICENSE`](LICENSE). Shared for personal
reference; reuse requires asking first.
