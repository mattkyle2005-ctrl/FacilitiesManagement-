# 115 Facilities Monitoring Dashboard

A single-file, browser-based dashboard for the **Public Transportation Facilities Management** unit, City of Cape Town. It tracks day-to-day operations across 115 public transport facilities: inspection status, work orders (modelled on the real WhatsApp reporting workflow), preventative maintenance, contractor performance, and per-facility QR deep-links.

Part of the **Neil Arendse Toolkit**. This is the operational, "what needs attention today" tool — a companion to the strategic Facilities Rationalisation Planner.

## What it does

- **Dashboard** — at-a-glance counts (facilities tracked, overdue inspections, open work orders, overdue maintenance), an optional AI daily briefing, and workload per monitoring official.
- **Facilities** — add/edit facilities, log inspections, attach a site **photo**, search and filter.
- **Work Orders** — full status pipeline (Reported → Logged → Contractor Assigned → In Progress → Resolved → Closed), severity, contractor, cross-department "waiting on" tags, photo evidence, and a timestamped activity timeline. Includes a **WhatsApp quick-log** paste box and automatic **duplicate detection**.
- **Maintenance** — recurring preventative tasks with computed next-due dates, sorted most-overdue-first.
- **Contractors** — performance stats aggregated automatically from work-order history.
- **QR Codes** — one per facility, encoding a deep-link into this page for on-site phone use (see "Why host it" below).
- **Import / Export** — several ways to load facilities (see below), plus CSV exports and a full JSON backup/restore.

## How Neil can load his facilities

There are several paths, so there's always an easy one:

1. **Download the CSV template** (Import / Export tab), fill it in with Excel or Google Sheets, and **upload the file** back.
2. **Paste CSV rows** directly into the import box.
3. **Add facilities one at a time** with the manual form (including a photo).
4. **Import a Facilities Rationalisation Planner backup** (JSON) to bring names, officials, and notes across without retyping.
5. **Restore a full JSON backup** from a previous session or another computer.

On first open the dashboard shows **example data** so it isn't a blank shell — a banner lets you clear it in one click, and importing real data clears the examples automatically.

## Why host it (and what hosting fixes)

The dashboard runs perfectly by just double-clicking the file — **except the QR-code feature**. A QR code that points at a `file://` path on one computer can't be reached by a phone camera. Hosting this file at a real web address makes the QR codes work: scanning one opens a focused, on-site quick-action screen for that single facility.

### Enable GitHub Pages

1. Create a GitHub repository and push this folder to it (the repo must contain `index.html` at its root — it already does).
2. In the repo, go to **Settings → Pages**.
3. Under **Build and deployment**, set **Source** to *Deploy from a branch*, choose the `main` branch and the `/ (root)` folder, and save.
4. After a minute, the dashboard is live at `https://<your-username>.github.io/<repo-name>/`.
5. Open that URL, go to the **QR Codes** tab, and print the sheet — every code now points at the live address and works from any phone.

The `.nojekyll` file in this folder tells GitHub Pages to serve everything as-is.

## Privacy & data

- **All data lives only in the browser's local storage.** Nothing about facilities, work orders, or photos is ever sent to any server.
- The only outbound network call is the **optional** AI Daily Briefing, which goes **directly** from the browser to Anthropic's API using a key you enter in Settings (stored locally, never routed through a third party).
- Because data is per-browser, use **Download full backup (JSON)** periodically — clearing browser data or switching computers otherwise loses everything.
- Hosting this page publicly exposes only the empty app shell (plus example data), never anyone's real data.

## Updating the hosted version

Replace `index.html` with a newer build of the dashboard and push. GitHub Pages redeploys automatically within a minute or two. Existing users keep their data — it's in their browser, not in the file.

## Verifying a change before publishing

Any change to `index.html` should be render-verified (not just syntax-checked) before it goes live — the app mounts entirely into `<div id="root">`, so a mount error is a blank page with no visible message. The project keeps a jsdom harness that executes the transformed code against a DOM under first-open, returning-user, and empty states. See the Neil Arendse Toolkit project notes for details.
