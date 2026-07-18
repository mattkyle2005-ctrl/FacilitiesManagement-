# Neil Arendse Toolkit — Hosted Tools

Standalone, single-file, browser-based tools for the **Public Transportation Facilities Management and Enforcement** unit, City of Cape Town. Each tool is one self-contained HTML file — no login, no install, no build step, no server. Data lives only in the browser's local storage; AI features are optional and call the Anthropic API directly from the browser with a key entered in Settings.

| Tool | File | What it's for |
|---|---|---|
| **115 Facilities Monitoring Dashboard** | [`index.html`](./index.html) | Day-to-day operational tracking: inspections, work orders, preventative maintenance, contractor performance, QR deep-links. |
| **Complaint Manager & AI Response Drafter** | [`complaints.html`](./complaints.html) | Logging and responding to politician/public complaints, with an AI drafter that adapts to Neil's own writing voice. |
| **Totem Pole Refurbishment Tracker** | [`totem-poles.html`](./totem-poles.html) | Project dashboard for the City's totem pole refurbishment initiative: asset register, phase roadmap, priority tiers, funding model, and AI executive summary generator. |

Once hosted (see "Enable GitHub Pages" below), all three are live at:
- `https://<your-username>.github.io/<repo-name>/` (Dashboard)
- `https://<your-username>.github.io/<repo-name>/complaints.html` (Complaint Manager)
- `https://<your-username>.github.io/<repo-name>/totem-poles.html` (Totem Pole Tracker)

---

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

---

# Complaint Manager & AI Response Drafter

A single-file, browser-based tool for logging and responding to politician and public complaints — Neil's #1 daily pain point per the Toolkit's project notes. Deliberately separate from the Dashboard (different job: complaint correspondence, not facility operations), sharing the same design system and hosted alongside it.

## What it does

- **Dashboard (Response Backlog)** — unresolved/overdue-for-response/drafted-but-not-sent counts, politician complaints flagged first regardless of age, an on-demand "Generate Backlog Summary," and workload by official.
- **Complaints** — full status pipeline (Open → Acknowledged → Investigating → Response Drafted → Responded → Closed), source (Politician/Public/Internal), priority, an activity timeline, and search/filter.
- **AI-Assisted Intake** — paste a raw complaint (email/WhatsApp/call notes) and Claude extracts category, priority, and facility, pre-filling the form for review before anything is saved.
- **AI Response Drafter with a Voice Profile** — drafts adapt tone by complaint source (politician vs public vs internal), and — the key feature — can be grounded in **real examples of how Neil actually writes**, pasted into Settings. When Neil edits a draft before marking it Responded, the tool offers to save the edited version as a new example, so drafts keep sounding more like him the more the tool is used.
- **Import / Export** — CSV template download/upload/paste, JSON backup/restore, and a one-way import of officials from the Dashboard's own JSON backup (no retyping the same team twice).

## Why the Voice Profile, not just a tone switch

An earlier draft of this tool's design used a fixed "formal for politicians, plain for the public" persona switch. That's generic personalization, not real personalization. The Voice Profile replaces/extends it: Neil's own past responses become few-shot examples in the drafting prompt, with the source-based register still applied underneath for structure. No examples yet? Drafts fall back cleanly to the source-based tone alone — the feature is optional and improves gradually from normal use, not something that has to be set up perfectly on day one.

## Categories are a starting guess, not a fixed answer

The default category list (Service Delivery, Staff Conduct, Safety & Security, etc.) is a reasonable guess, **not confirmed with Neil**. It's an editable list in Settings — same add/remove pattern as officials — specifically so it can be corrected once real usage shows how complaints actually get classified in practice.

---

## Updating the hosted version

Replace `index.html` (Dashboard) or `complaints.html` (Complaint Manager) with a newer build and push. GitHub Pages redeploys automatically within a minute or two. Existing users keep their data — it's in their browser, not in the file.

## Verifying a change before publishing

Any change to either tool should be render-verified (not just syntax-checked) before it goes live — each app mounts entirely into `<div id="root">`, so a mount error is a blank page with no visible message. The project keeps a jsdom harness (and, for the Complaint Manager, a standalone unit test of its AI-prompt-building logic) that executes the transformed code against a DOM under first-open, returning-user, and empty states. See the Neil Arendse Toolkit project notes for details.

<!-- Deployment fix Sun Jul  5 17:08:24 SAST 2026 -->
<!-- Force fresh deploy 2026-07-09T08:12:01Z -->
