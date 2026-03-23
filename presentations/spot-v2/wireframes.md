# SPOT — Engage & Settings: ASCII Diagrams, User Flows & UX Specification

> **Scope:** Engage (per-requisition artifact) and Settings (per-requisition)
> **Status:** UX-reviewed, refined from PM prototype + Engage PRD + Settings PRD
> **Date:** 2026-03-23
> **Sources:** PM ASCII prototype, SCREENS_AND_FLOWS.md, Engage PRD, Settings PRD, UX Q&A (25 questions)

---

## Table of Contents

1. [Design Decisions Log](#1-design-decisions-log)
2. [Mental Model & How It Fits](#2-mental-model)
3. [Success Metrics](#3-success-metrics)
4. [Settings Prerequisites (Hard Block)](#4-settings-prerequisites)
5. [Pipeline Stages](#5-pipeline-stages)
6. [Engage — Information Architecture](#6-engage-information-architecture)
7. [Engage — Screen Diagrams](#7-engage-screen-diagrams)
8. [Engage — User Flows](#8-engage-user-flows)
9. [Settings — Information Architecture](#9-settings-information-architecture)
10. [Settings — Screen Diagrams](#10-settings-screen-diagrams)
11. [Settings — User Flows](#11-settings-user-flows)
12. [Cross-Cutting Concerns](#12-cross-cutting-concerns)
13. [Navigation Architecture](#13-navigation-architecture)

---

## 1. Design Decisions Log

Key decisions captured from UX Q&A review + PRD alignment:

| # | Decision | Source |
|---|----------|--------|
| D1 | **List tab is the default landing** within Engage | UX Q&A — recruiters review candidates first, then engage |
| D2 | **Engage is a per-requisition artifact** acting as the recruiter's command center | PRD §1 |
| D3 | **Conversations grouped by requisition** in global view | UX Q&A — prevents confusion across reqs |
| D4 | **7-stage pipeline**: Sourced → Contacted → Responded → Screening → Interview → Offer → Hired | PRD §1 |
| D5 | **Stage transitions are automatic** based on email/system events | UX Q&A + PRD |
| D6 | **Settings are hard prerequisites** — email ops blocked until Sender Identity + Email Sequences + Email Preferences are configured | PRD §3 |
| D7 | **Calendar integrates with Outlook** + has candidate self-booking pages | PRD §4.3 |
| D8 | **Notifications via bell icon** with filter dropdown (Replied, Bounced, Sent, Calendar, Meeting) | UX Q&A |
| D9 | **One active sequence per candidate** at a time | UX Q&A |
| D10 | **Sequence performance stats** per template (open%, reply%, bounce%) | UX Q&A + PRD |
| D11 | **Sequences saveable to library** and reusable across requisitions | UX Q&A |
| D12 | **Metrics: Sankey + Line chart**, view-only, stacked vertically | PRD §4.4 + UX Q&A |
| D13 | **AI Chat available on every page** with approval-card pattern for all mutations | PRD §4 + UX Q&A |
| D14 | **Stage movement via AI Chat + Candidate Detail panel** — both paths | UX Q&A |
| D15 | **Email view has custom labels** with colors, AND-logic filtering | PRD §4.2.1 |
| D16 | **"Draft with AI" split button** with preset templates in email reply | PRD §4.2.3 |
| D17 | **Match score is 1–5** (not percentage) | PRD §4.1 |
| D18 | **AI never acts unprompted** — all mutations require recruiter request + approval card | PRD §4 |

---

## 2. Mental Model

```
┌─────────────────────────────────────────────────────────────────────────┐
│                                                                         │
│  ENGAGE = Recruiter's Command Center                                    │
│                                                                         │
│  Think of it like a CRM dashboard.                                      │
│                                                                         │
│  ┌─────────┐  ┌─────────┐  ┌──────────┐  ┌─────────┐                  │
│  │  LIST   │  │  EMAIL  │  │ CALENDAR │  │ METRICS │                  │
│  │         │  │         │  │          │  │         │                  │
│  │Candidate│  │  Email  │  │  Your    │  │ Perf.   │                  │
│  │ Roster  │  │  Client │  │ Schedule │  │ Report  │                  │
│  └─────────┘  └─────────┘  └──────────┘  └─────────┘                  │
│                                                                         │
│  Same data — four lenses.                                               │
│                                                                         │
│  Candidates flow in from SOURCING STRATEGY ──►                         │
│  Engage manages them through the FULL LIFECYCLE:                        │
│                                                                         │
│  Sourced → Contacted → Responded → Screening →                         │
│  Interview → Offer → Hired                                              │
│                                                                         │
└─────────────────────────────────────────────────────────────────────────┘
```

---

## 3. Success Metrics

| Area | Priority | Metric |
|------|----------|--------|
| **Outreach** | P0 | Reply rate ≥ 20% |
| **Outreach** | P0 | TA agreement on follow-up reply copy > 70% |
| **Outreach** | P1 | # of emails edited before sending |
| **Screening** | P0 | Adoption rate > 30% |
| **Screening** | P1 | # of candidates sent, drop-off funnel |
| **Scheduling** | P0 | % of screenings booked via booking page vs. manual |
| **Scheduling** | P1 | Avg time from "Responded" to "Screening scheduled" |

---

## 4. Settings Prerequisites (Hard Block)

Before ANY email can be composed or sent, three settings MUST be configured:

```
┌─────────────────────────────────────────────────────────────────────────┐
│                      SETTINGS PREREQUISITE CHECK                        │
│                                                                         │
│  Required before any email operation:                                   │
│                                                                         │
│  1. ☐ Sender Identity                                                  │
│     └─ full_name, email_address, signature must be non-empty            │
│                                                                         │
│  2. ☐ Email Sequences                                                  │
│     └─ At least one active sequence with stages + linked templates      │
│                                                                         │
│  3. ☐ Email Preferences                                             │
│     └─ send_window (start, end, timezone) + daily_send_limit            │
│                                                                         │
│  ─────────────────────────────────────────────────────────────────      │
│                                                                         │
│  IF INCOMPLETE:                                                         │
│                                                                         │
│  ┌─────────────────────────────────────────────────────────────────┐   │
│  │ ⚠ Set up your sender identity, email sequences, and outreach   │   │
│  │   preferences before sending emails.                            │   │
│  │                                                                 │   │
│  │                              [Go to Settings →]                 │   │
│  └─────────────────────────────────────────────────────────────────┘   │
│                                                                         │
│  Blocked operations:                                                    │
│  • Compose email (manual or AI)                                         │
│  • Send email                                                           │
│  • Bulk send                                                            │
│  • "Engage" batch action in List view                                   │
│                                                                         │
│  AI behavior when settings incomplete:                                  │
│  → Does NOT attempt to compose                                          │
│  → Informs recruiter which settings are missing                         │
│  → Offers to navigate to Settings or help configure via edit_settings   │
│                                                                         │
└─────────────────────────────────────────────────────────────────────────┘
```

---

## 5. Pipeline Stages

```
┌────────┐   ┌───────────┐   ┌───────────┐   ┌───────────┐   ┌───────────┐   ┌───────┐   ┌───────┐
│Sourced │──►│ Contacted │──►│ Responded │──►│ Screening │──►│ Interview │──►│ Offer │──►│ Hired │
│        │   │           │   │           │   │           │   │           │   │       │   │       │
│Added to│   │ Email     │   │ Candidate │   │ Screen    │   │ Interview │   │ Offer │   │ Offer │
│pipeline│   │ sent      │   │ replied   │   │ scheduled │   │ completed │   │ made  │   │accept.│
└────────┘   └───────────┘   └───────────┘   └───────────┘   └───────────┘   └───────┘   └───────┘
                                    │                │
                                    ▼                ▼
                              ┌───────────┐   ┌───────────┐
                              │  Dropped   │   │ Rejected  │
                              │ (no reply/ │   │ (declined/│
                              │  bounced)  │   │  no fit)  │
                              └───────────┘   └───────────┘

Auto-transition triggers:
  Sourced → Contacted:     "Engage" action or email sent
  Contacted → Responded:   Candidate replies to any email
  Responded → Screening:   Screening booked (via booking page or manual)
  Screening → Interview:   Screening completed + advanced
  Interview → Offer:       Recruiter extends offer
  Offer → Hired:           Candidate accepts offer

Manual override:
  • Via Candidate Detail panel: Stage dropdown
  • Via AI Chat: "Move [candidate] to [stage]" → approval card
```

---

## 6. Engage — Information Architecture

```
Engage (Per-Requisition Artifact)
│
├── Segmented Control: [List] | Email | Calendar | Kanban | Metrics
│                        ↑ default
│   Active view persists across navigations within artifact
│   All views share same underlying pipeline + email data
│
├── List View ───────────────── Candidate roster (§4.1)
│   ├── Table: Name, Title, Company, Exp, Stage, Email Status,
│   │         Screening Status, Match Score (1-5)
│   ├── Search bar + Stage filter dropdown
│   ├── Multi-select checkboxes → Bulk actions
│   │   ├── "Engage" → Move to Contacted + generate emails
│   │   └── (Subject to settings prerequisites)
│   ├── Click row → Candidate detail drawer
│   └── AI: add/move/update/remove candidates (approval cards)
│
├── Email View ──────────────── Outreach inbox (§4.2)
│   ├── Inbox Layout (§4.2.1)
│   │   ├── Threads sorted by most recent activity
│   │   ├── Search by candidate name
│   │   ├── Filters: status + stage + labels (combinable, AND logic)
│   │   ├── Custom label creation (name + color)
│   │   └── AI: compose, edit, bulk outreach (approval cards)
│   ├── Individual Email View (§4.2.2)
│   │   ├── Full thread in right-side drawer
│   │   ├── Engagement data: opens, last opened, reply status
│   │   └── Label management popover
│   └── Drafting Replies (§4.2.3)
│       ├── Compose textarea at bottom of thread
│       ├── "Draft with AI" split button:
│       │   ├── "Send screening link"
│       │   ├── "Answer questions"
│       │   └── "Ask to schedule interview"
│       └── Send button
│
├── Calendar View ───────────── Scheduling hub (§4.3)
│   ├── Calendar Display (§4.3.1)
│   │   ├── Month grid with nav (prev/next + Today)
│   │   ├── Events color-coded: purple=intake, gray=screening, blue=Outlook
│   │   └── Click screening → candidate detail drawer
│   ├── Outlook Calendar Sync (§4.3.2)
│   │   ├── Connect/disconnect via settings
│   │   ├── Outlook events as blocked time (muted/gray)
│   │   └── Spot events sync TO Outlook
│   ├── Candidate Booking Page (§4.3.3)
│   │   ├── Auto-generated unique link (per candidate or per req)
│   │   ├── Config: duration (15/30/45/60), date range, custom message
│   │   ├── Shows available slots (working hours - calendar events)
│   │   └── On book: creates event, syncs Outlook, updates stage, sends confirmation
│   └── Manual Invite Creation (§4.3.4)
│       ├── Click date → create invite modal
│       ├── Select candidate, duration, type, location, notes
│       └── Sends invite email + syncs Outlook + updates screening status
│
├── Kanban View ─────────────── Visual pipeline board
│   ├── Fixed columns (7 stages): Sourced → Contacted → Responded →
│   │     Screening → Interview → Offer → Hired
│   ├── Cards auto-move based on email/system events
│   ├── Each card: candidate name, title, requisition badge
│   ├── Click card → Candidate detail drawer
│   └── Empty column: "No candidates" placeholder
│
└── Metrics View ────────────── Pipeline analytics (§4.4, view-only)
    ├── Pipeline Progression (Sankey Diagram)
    │   ├── Stage-to-stage flow, bars proportional to population
    │   ├── Drop-off paths in RED with count + reason labels
    │   └── Node labels: stage name + count
    ├── Stage Activity Over Time (Line Chart)
    │   ├── One line per stage (distinct colors)
    │   ├── X: date timeline, Y: candidate count
    │   └── Legend + grid lines
    └── Empty: "No pipeline data yet. Add candidates to see metrics."
```

---

## 7. Engage — Screen Diagrams

> **AI Chat Panel behavior:** Hidden by default. Toggled via [💬] button in the
> top nav. When opened, it **pushes/shrinks** the main content area (~65vw content,
> ~35vw chat). Chat is NOT persistent — it must be explicitly opened. All screen
> diagrams below show the **default state (chat closed, full-width content)**.
> See §12.1 for the chat-open layout example.

### 7.1 Engage — List View (Default Landing)

```
┌──────────────────────────────────────────────────────────────────────────┐
│ ← SeekOut — Senior Frontend Engineer @ SeekOut  Mock [toggle] [💬][🔔][👤]│
├──────────┬───────────────────────────────────────────────────────────────┤
│          │                                                               │
│[⊙]Intake │  [List]  Email  Calendar  Kanban  Metrics    [🔍 Search] [≡] │
│          │                                                               │
│[🔍]Source│  [🔍 Search candidates...]  [Stage ▼]                         │
│          │                                                               │
│[▶•]Engage│  ┌──────────────────────────────────────────────────────────┐ │
│          │  │☐ NAME         TITLE       CO      EXP  STAGE     EMAIL  │ │
│[⊞]Views  │  │                                        SCRN     MATCH   │ │
│          │  ├──────────────────────────────────────────────────────────┤ │
│[⚙]Settngs│  │☐ Maya Rod.    Sr FE Eng   Figma   6yr  [Screening]     │ │
│          │  │                                         Replied Sched ★★★★☆│
│          │  ├──────────────────────────────────────────────────────────┤ │
│          │  │☐ Kevin Tran   Sr SWE      Vercel  7yr  [Screening]     │ │
│          │  │                                         Replied Sched ★★★★│
│          │  ├──────────────────────────────────────────────────────────┤ │
│          │  │☐ Alex Chen    Sr SWE      Meta    8yr  [Contacted]     │ │
│          │  │                                         Sent    Not   ★★★★│
│          │  ├──────────────────────────────────────────────────────────┤ │
│          │  │☐ Priya S.     Staff Eng   Google 12yr  [Contacted]     │ │
│          │  │                                         Opened  Not  ★★★★★│
│          │  ├──────────────────────────────────────────────────────────┤ │
│          │  │☐ David Kim    Princ. Eng  Amazon 15yr  [Responded]     │ │
│          │  │                                         Replied Sched ★★★│
│          │  └──────────────────────────────────────────────────────────┘ │
│          │                                                               │
│          │  ┌──────────────────────────────────────────────────────────┐ │
│          │  │ ☑ 2 selected                    [Clear]  [Engage ▼]    │ │
│          │  └──────────────────────────────────────────────────────────┘ │
└──────────┴───────────────────────────────────────────────────────────────┘

Columns:
  NAME        — Candidate full name
  TITLE       — Current job title
  CO          — Current company
  EXP         — Years of experience
  STAGE       — Pipeline stage badge (color-coded)
  EMAIL       — Sent / Opened / Replied / No response
  SCRN        — Scheduled / Completed / Not scheduled
  MATCH       — 1-5 stars

"Engage" bulk action:
  → Checks settings prerequisites first (§4)
  → If settings OK: moves selected to "Contacted" + generates personalized emails
  → If settings incomplete: shows blocking message with link to Settings

Empty state:
  "No candidates in pipeline. Run a search to find candidates."

AI approval card pattern:
  ┌────────────────────────────────────────┐
  │ Move Maya Rodriguez                    │
  │ From: Responded → To: Screening        │
  │                                        │
  │              [Approve] [Reject]        │
  └────────────────────────────────────────┘
```

### 7.2 Engage — Candidate Detail Drawer (from List)

**Trigger:** Click any candidate row

```
┌──────────────────────────────────────────────────────────────────────────┐
│ ← SeekOut — Senior FE @ SeekOut             Mock [toggle] [💬][🔔][👤]  │
├──────────┬──────────────────────────────┬────────────────────────────────┤
│          │ (dimmed list)                │ CANDIDATE DETAIL            ✕  │
│[⊙]Intake │                              │                                │
│          │ ☐ Maya Rod. ← selected       │ [Profile] [Notes] [Activity]   │
│[🔍]Source│ ☐ Kevin Tran                │                                │
│          │ ☐ Alex Chen                  │ ┌──┐  Maya Rodriguez           │
│[▶•]Engage│ ☐ Priya S.                  │ │MR│  Senior FE Engineer        │
│          │ ☐ David Kim                  │ └──┘  Figma                    │
│[⊞]Views  │                              │       📍 Seattle, WA           │
│          │                              │       🗓 6 years               │
│[⚙]Settngs│                             │                                │
│          │                              │ [🔗 View LinkedIn Profile]     │
│          │                              │                                │
│          │                              │ PIPELINE STAGE                 │
│          │                              │ [Screening ▼]                  │
│          │                              │                                │
│          │                              │ MATCH SCORE                    │
│          │                              │ ★★★★☆ (4/5)                   │
│          │                              │                                │
│          │                              │ WHY SPOT PICKED                │
│          │                              │ ┌──────────────────────────┐  │
│          │                              │ │ Near-perfect match. Figma│  │
│          │                              │ │ component library with   │  │
│          │                              │ │ Radix + Tailwind.        │  │
│          │                              │ │ Accessibility audit exp. │  │
│          │                              │ │                          │  │
│          │                              │ │ [React][TS][Radix][TW]   │  │
│          │                              │ └──────────────────────────┘  │
│          │                              │                                │
│          │                              │ EMAIL STATUS                   │
│          │                              │ ✓ Replied · 3 opens · Feb 26  │
│          │                              │                                │
│          │                              │ SCREENING                      │
│          │                              │ 📅 Scheduled — Mar 28, 2pm     │
│          │                              │ [Copy booking link]            │
│          │                              │                                │
│          │                              │ NOTES                          │
│          │                              │ ┌──────────────────────────┐  │
│          │                              │ │ + Add note                │  │
│          │                              │ └──────────────────────────┘  │
└──────────┴──────────────────────────────┴────────────────────────────────┘
```

### 7.3 Engage — Email View: Inbox Layout

**Path:** Engage > Email

```
┌──────────────────────────────────────────────────────────────────────────┐
│ ← SeekOut — Senior FE @ SeekOut             Mock [toggle] [💬][🔔][👤]  │
├──────────┬───────────────────────────────────────────────────────────────┤
│          │                                                               │
│[⊙]Intake │  List  [Email]  Calendar  Kanban  Metrics                     │
│          │                                                               │
│[🔍]Source│  [🔍 Search]  [Status ▼]  [Stage ▼]  [Labels ▼]              │
│          │                                                               │
│[▶•]Engage│  ┌──────────────────────────────────────────────────────────┐ │
│          │  │ Maya Rodriguez   [Screening]                             │ │
│[⊞]Views  │  │ Re: Your work on Figma's canvas —                       │ │
│          │  │ ↩ Thanks for reaching out! I'm open to exploring...     │ │
│[⚙]Settngs│  │ 🏷 [Hot lead] [FE]                          Feb 27      │ │
│          │  ├──────────────────────────────────────────────────────────┤ │
│          │  │ Kevin Tran       [Screening]                             │ │
│          │  │ Following up — SeekOut FE role                           │ │
│          │  │ ↩ Interested, let's talk...                              │ │
│          │  │ 🏷 [FE]                                       Mar 1      │ │
│          │  ├──────────────────────────────────────────────────────────┤ │
│          │  │ Alex Chen        [Contacted]                             │ │
│          │  │ Hi Alex — I'm reaching out about an exciting role...     │ │
│          │  │ 📧 Sent · 0 opens                              Mar 4     │ │
│          │  ├──────────────────────────────────────────────────────────┤ │
│          │  │ Priya Sharma     [Contacted]                             │ │
│          │  │ Hi Priya — I'm recruiting for a position that...        │ │
│          │  │ 📧 Opened · 1 open                             Mar 3     │ │
│          │  ├──────────────────────────────────────────────────────────┤ │
│          │  │ David Kim        [Responded]                             │ │
│          │  │ Re: SeekOut engineering role                              │ │
│          │  │ ↩ When works for a call?                                 │ │
│          │  │ 🏷 [Hot lead]                                  Mar 5     │ │
│          │  └──────────────────────────────────────────────────────────┘ │
│          │                                                               │
└──────────┴───────────────────────────────────────────────────────────────┘

Each row shows:
  • Candidate name + pipeline stage badge
  • Email preview / subject line
  • ↩ = candidate reply snippet (if replied)
  • 🏷 = custom label badges
  • Timestamp (sent date)
  • Status indicator (color-coded: sent/opened/replied/draft)

Filter controls:
  [Status ▼]  — Sent / Opened / Replied / Draft / No response
  [Stage ▼]   — Multi-select across all 7 pipeline stages
  [Labels ▼]  — Multi-select, AND logic (must have ALL selected)
                + "Create label" inline (name + color picker)
  [🔍 Search] — By candidate name

All filters are combinable.

Label creation (inline from filter dropdown):
  ┌─────────────────────────────┐
  │ Labels                      │
  │ ☑ Hot lead  🔴              │
  │ ☑ FE        🔵              │
  │ ☐ Backend   🟢              │
  │ ────────────────────────    │
  │ + Create label              │
  │   Name: [_________]         │
  │   Color: 🔴🟠🟡🟢🔵🟣      │
  │          [Create]           │
  └─────────────────────────────┘

Empty state:
  "No emails yet. Move candidates to Contacted to start outreach."
```

### 7.4 Engage — Email View: Thread Drawer

**Trigger:** Click email row → right-side drawer

```
┌──────────────────────────────────────────────────────────────────────────┐
│ ← SeekOut — Senior FE @ SeekOut             Mock [toggle] [💬][🔔][👤]  │
├──────────┬──────────────────────┬────────────────────────────────────────┤
│          │ (dimmed inbox)       │ THREAD                              ✕  │
│[⊙]Intake │                      │                                        │
│          │ Maya R. ← selected  │ Maya Rodriguez · Sr FE Eng · Figma     │
│[🔍]Source│ Kevin T.            │ [Screening]  📧 3 opens · Last: Feb 26 │
│          │ Alex C.             │ 🏷 [Hot lead] [FE] [+]                 │
│[▶•]Engage│ Priya S.            │                                        │
│          │ David K.            │ ── Feb 24, 9:02am ─────────────────── │
│[⊞]Views  │                      │ ┌─ TC ──────────────────────────────┐ │
│          │                      │ │ Subject: Your work on Figma's     │ │
│[⚙]Settngs│                     │ │ canvas —                           │ │
│          │                      │ │                                    │ │
│          │                      │ │ Hi Maya, I came across your work   │ │
│          │                      │ │ at Figma and was impressed by...   │ │
│          │                      │ └────────────────────────────────────┘ │
│          │                      │                                        │
│          │                      │ ── Feb 27, 2:15pm ─────────────────── │
│          │                      │ ┌─ MR ──────────────────────────────┐ │
│          │                      │ │ Thanks for reaching out! I'm open │ │
│          │                      │ │ to exploring new opportunities.   │ │
│          │                      │ │ When would be good to chat?       │ │
│          │                      │ └────────────────────────────────────┘ │
│          │                      │                                        │
│          │                      │ ✓ Candidate has replied                │
│          │                      │                                        │
│          │                      │ ┌────────────────────────────────────┐ │
│          │                      │ │ Type reply...                      │ │
│          │                      │ └────────────────────────────────────┘ │
│          │                      │                                        │
│          │                      │ [Draft with AI ▼]              [Send] │
│          │                      │  ├─ Send screening link               │
│          │                      │  ├─ Answer questions                   │
│          │                      │  └─ Ask to schedule interview          │
└──────────┴──────────────────────┴────────────────────────────────────────┘

"Draft with AI" split button:
  Main: "Draft with AI" → opens generic AI compose
  Dropdown presets:
    • "Send screening link" → pre-fills with booking template
    • "Answer questions" → pre-fills with Q&A response
    • "Ask to schedule interview" → pre-fills with calendar template
  All presets auto-populate candidate {first_name}
  Recruiter can edit before sending
```

### 7.5 Engage — Calendar View

**Path:** Engage > Calendar

```
┌──────────────────────────────────────────────────────────────────────────┐
│ ← SeekOut — Senior FE @ SeekOut             Mock [toggle] [💬][🔔][👤]  │
├──────────┬───────────────────────────────────────────────────────────────┤
│          │                                                               │
│[⊙]Intake │  List  Email  [Calendar]  Kanban  Metrics                     │
│          │                                                               │
│[🔍]Source│  ◄ March 2026 ►  [Today]    [Connect Outlook] [Booking Link] │
│          │                                                               │
│[▶•]Engage│  ┌──────┬──────┬──────┬──────┬──────┬──────┬──────┐          │
│          │  │ Sun  │ Mon  │ Tue  │ Wed  │ Thu  │ Fri  │ Sat  │          │
│[⊞]Views  │  ├──────┼──────┼──────┼──────┼──────┼──────┼──────┤          │
│          │  │  22  │  23  │  24  │  25  │  26  │  27  │  28  │          │
│[⚙]Settngs│  │      │      │      │      │┌────┐│      │┌────┐│          │
│          │  │      │      │      │      ││🟣  ││      ││⚫  ││          │
│          │  │      │      │      │      ││Intk ││      ││Scrn ││         │
│          │  │      │      │      │      │└────┘│      │└────┘│          │
│          │  │      │      │      │      │┌────┐│      │      │          │
│          │  │      │      │      │      ││⚫  ││      │      │          │
│          │  │      │      │      │      ││Scrn ││      │      │          │
│          │  │      │      │      │      │└────┘│      │      │          │
│          │  │      │      │      │      │┌────┐│      │      │          │
│          │  │      │      │      │      ││🔵  ││      │      │          │
│          │  │      │      │      │      ││Outlk││      │      │          │
│          │  │      │      │      │      │└────┘│      │      │          │
│          │  └──────┴──────┴──────┴──────┴──────┴──────┴──────┘          │
│          │                                                               │
│          │  Legend: 🟣 Intake meeting  ⚫ Screening  🔵 Outlook (blocked)│
│          │                                                               │
│          │  Upcoming                                                     │
│          │  📅 Mar 26, 10am — Priya S. · Screening                       │
│          │  📅 Mar 26, 3pm  — Kevin T. · Interview                       │
│          │  📅 Mar 28, 2pm  — Maya R. · Screening                        │
└──────────┴───────────────────────────────────────────────────────────────┘

Event types (color-coded):
  🟣 Purple  = Intake meeting
  ⚫ Gray    = Candidate screening
  🔵 Blue   = Outlook calendar event (blocked time)

Calendar actions:
  [Connect Outlook]        — OAuth flow → syncs recruiter's calendar
  [Generate Booking Link]  — Creates shareable self-scheduling link
  Click date cell          — Opens manual invite creation modal (§7.5a)
  Click screening event    — Opens candidate detail drawer

Availability derivation:
  Available slots = Working hours (from Settings) MINUS Outlook events
  Booking pages and AI use this availability
```

### 7.5a Calendar — Manual Invite Creation Modal

**Trigger:** Click a date cell on the calendar

```
         ┌──────────────────────────────────────────────┐
         │  New Screening Invite                         │
         │                                               │
         │  Candidate                                    │
         │  ┌──────────────────────────────────────┐    │
         │  │ [Search candidates...            ▼]  │    │
         │  └──────────────────────────────────────┘    │
         │                                               │
         │  Date              Time                       │
         │  ┌──────────┐    ┌──────────┐                │
         │  │ Mar 26   │    │ 2:00 PM  │                │
         │  └──────────┘    └──────────┘                │
         │                                               │
         │  Duration          Meeting Type               │
         │  ┌──────────┐    ┌──────────────────┐        │
         │  │ 30 min ▼ │    │ Screening      ▼ │        │
         │  └──────────┘    └──────────────────┘        │
         │                                               │
         │  Location / Video Link                        │
         │  ┌──────────────────────────────────────┐    │
         │  │ https://zoom.us/j/...                │    │
         │  └──────────────────────────────────────┘    │
         │                                               │
         │  Notes (optional)                             │
         │  ┌──────────────────────────────────────┐    │
         │  │                                      │    │
         │  └──────────────────────────────────────┘    │
         │                                               │
         │  [Cancel]               [Send Invite]        │
         └──────────────────────────────────────────────┘

On creation:
  • Invite email sent to candidate
  • Event appears on Spot calendar
  • Event syncs to Outlook (if connected)
  • Candidate screening_status → "Scheduled"
  • Candidate moves to "Screening" stage (if not already)
```

### 7.5b Calendar — Booking Page Configuration Modal

**Trigger:** Click [Generate Booking Link]

```
         ┌──────────────────────────────────────────────┐
         │  Generate Booking Page                        │
         │                                               │
         │  Screening Duration                           │
         │  ┌──────────────────────────────────────┐    │
         │  │ [15 min] [30 min] [45 min] [60 min]  │    │
         │  │                   ●                   │    │
         │  └──────────────────────────────────────┘    │
         │                                               │
         │  Available Date Range                         │
         │  ┌──────────────────────────────────────┐    │
         │  │ Next [7 ▼] days                      │    │
         │  └──────────────────────────────────────┘    │
         │                                               │
         │  Custom Message (optional)                    │
         │  ┌──────────────────────────────────────┐    │
         │  │ Looking forward to connecting!        │    │
         │  └──────────────────────────────────────┘    │
         │                                               │
         │  [Cancel]            [Generate Link]         │
         └──────────────────────────────────────────────┘
                 │
                 ▼
         ┌──────────────────────────────────────────────┐
         │  ✓ Booking page created                       │
         │                                               │
         │  https://spot.seekout.com/book/abc123         │
         │                          [Copy link]         │
         │                                               │
         │  Share with candidates to let them self-book  │
         │  within your available time.                  │
         └──────────────────────────────────────────────┘
```

### 7.5c Calendar — Candidate Booking Page (Candidate-Facing)

```
┌──────────────────────────────────────────────────────────────────────────┐
│                                                                          │
│                        ┌──────┐                                          │
│                        │ SPOT │                                          │
│                        └──────┘                                          │
│                                                                          │
│            Book a Screening with Taylor Chen                             │
│            Senior Technical Recruiter, SeekOut                           │
│                                                                          │
│            Looking forward to connecting!                                │
│                                                                          │
│            Duration: 30 minutes                                          │
│                                                                          │
│            Select a time:                                                │
│                                                                          │
│            ◄ Week of Mar 23 ►                                           │
│                                                                          │
│            Mon, Mar 23                                                   │
│            ┌─────────────────┐                                           │
│            │ 10:00 AM        │                                           │
│            ├─────────────────┤                                           │
│            │ 11:00 AM        │                                           │
│            ├─────────────────┤                                           │
│            │  2:00 PM        │                                           │
│            └─────────────────┘                                           │
│                                                                          │
│            Tue, Mar 24                                                   │
│            ┌─────────────────┐                                           │
│            │  9:00 AM        │                                           │
│            ├─────────────────┤                                           │
│            │  3:00 PM        │  ← slots reflect real-time availability  │
│            └─────────────────┘                                           │
│                                                                          │
└──────────────────────────────────────────────────────────────────────────┘
                 │
         Candidate clicks slot
                 │
                 ▼
┌──────────────────────────────────────────────────────────────────────────┐
│                                                                          │
│            ✓ You're booked!                                              │
│                                                                          │
│            Monday, March 23 at 10:00 AM                                 │
│            with Taylor Chen                                              │
│                                                                          │
│            A confirmation has been sent to your email.                   │
│                                                                          │
└──────────────────────────────────────────────────────────────────────────┘

On booking:
  • Event created on Spot calendar
  • Event syncs to recruiter's Outlook (if connected)
  • Candidate screening_status → "Scheduled"
  • Candidate stage → "Screening" (if not already)
  • Confirmation emails sent to both parties
  • Slot removed from availability for other candidates
```

### 7.6 Engage — Kanban View

**Path:** Engage > Kanban

```
┌──────────────────────────────────────────────────────────────────────────┐
│ ← SeekOut — Senior FE @ SeekOut             Mock [toggle] [💬][🔔][👤]  │
├──────────┬───────────────────────────────────────────────────────────────┤
│          │                                                               │
│[⊙]Intake │  List  Email  Calendar  [Kanban]  Metrics        [🔍] [≡]    │
│          │                                                               │
│[🔍]Source│ ┌────────┐┌────────┐┌────────┐┌────────┐┌────────┐┌──────┐┌──────┐│
│          │ │Sourced ││Contact.││Respond.││Screen. ││Intervw.││Offer ││Hired ││
│[▶•]Engage│ │   5    ││  12    ││   4    ││   5    ││   3    ││  1   ││  1   ││
│          │ ├────────┤├────────┤├────────┤├────────┤├────────┤├──────┤├──────┤│
│[⊞]Views  │ │┌──────┐││┌──────┐││┌──────┐││┌──────┐││┌──────┐││┌────┐││┌────┐││
│          │ ││Rachel │││Alex C.│││Lucia T│││Maya R.│││James L│││Priya│││Dana ││
│[⚙]Settngs│ ││SWE    │││Sr SWE │││Sr FE  │││Sr FE  │││Sr Eng │││Staff│││Jr   ││
│          │ │└──────┘││└──────┘││└──────┘││└──────┘││└──────┘││└────┘││└────┘││
│          │ │┌──────┐││┌──────┐││┌──────┐││┌──────┐││┌──────┐││      ││      ││
│          │ ││Michae.│││Priya S│││James W│││Kevin T│││Sarah J│││      ││      ││
│          │ ││SWE    │││Staff  │││Sr FE  │││Sr SWE │││Lead   │││      ││      ││
│          │ │└──────┘││└──────┘││└──────┘││└──────┘││└──────┘││      ││      ││
│          │ │        ││┌──────┐││┌──────┐││┌──────┐││┌──────┐││      ││      ││
│          │ │        │││Sarah J│││James O│││Sarah P│││David K│││      ││      ││
│          │ │        │││FE Lead│││Sr SWE │││Sr UI  │││Princ. │││      ││      ││
│          │ │        ││└──────┘││└──────┘││└──────┘││└──────┘││      ││      ││
│          │ └────────┘└────────┘└────────┘└────────┘└────────┘└──────┘└──────┘│
│          │                                                               │
└──────────┴───────────────────────────────────────────────────────────────┘

Columns (FIXED — 7 stages, not configurable):
  1. Sourced      — Added to pipeline, not yet emailed
  2. Contacted    — Outreach sent, no reply yet
  3. Responded    — Candidate replied to outreach
  4. Screening    — In screening process
  5. Interview    — Interview stage
  6. Offer        — Offer extended
  7. Hired        — Offer accepted

Auto-transition triggers:
  • Sourced → Contacted:      "Engage" action or first email sent
  • Contacted → Responded:    Candidate replies to any email
  • Responded → Screening:    Screening booked (booking page or manual)
  • Screening → Interview:    Screening completed + advanced
  • Interview → Offer:        Recruiter extends offer
  • Offer → Hired:            Candidate accepts

Card design:
  • Candidate name (bold)
  • Current title (truncated)
  • Click card → Candidate detail slide-over

Empty column state:
┌────────┐
│Hired   │
│   0    │
├────────┤
│  No    │
│candida.│
└────────┘
```

### 7.7 Engage — Metrics View

```
┌──────────────────────────────────────────────────────────────────────────┐
│ ← SeekOut — Senior FE @ SeekOut             Mock [toggle] [💬][🔔][👤]  │
├──────────┬───────────────────────────────────────────────────────────────┤
│          │                                                               │
│[⊙]Intake │  List  Email  Calendar  Kanban  [Metrics]                     │
│          │                                                               │
│[🔍]Source│  Pipeline Progression                                        │
│          │  ┌──────────────────────────────────────────────────────────┐ │
│[▶•]Engage│  │                                                          │ │
│          │  │ Sourced    Contacted   Responded   Screening              │ │
│[⊞]Views  │  │  (24)  ───── (12) ────── (8) ────── (5)                  │ │
│          │  │          \           \            \                       │ │
│[⚙]Settngs│  │           \── ⬤8     \── ⬤2       \── ⬤3                 │ │
│          │  │            No reply    Bounced      Declined              │ │
│          │  │                                                          │ │
│          │  │ Interview   Offer   Hired                                │ │
│          │  │  (3) ─────── (1) ──── (1)                                │ │
│          │  │        \          \                                       │ │
│          │  │         \── ⬤1     \── ⬤0                                │ │
│          │  │          Withdrew    —                                    │ │
│          │  │                                                          │ │
│          │  │ ════════════════════════════════════════════════          │ │
│          │  │  ══════════════════════════════════                       │ │
│          │  │   ═══════════════════════════                             │ │
│          │  │    ══════════════════                                     │ │
│          │  │     ══════════════                                        │ │
│          │  │      ═══════                                              │ │
│          │  │       ═════                                               │ │
│          │  │                                                          │ │
│          │  │ ⬤ Red = drop-off with count + reason                     │ │
│          │  └──────────────────────────────────────────────────────────┘ │
│          │                                                               │
│          │  Stage Activity Over Time                                     │
│          │  ┌──────────────────────────────────────────────────────────┐ │
│          │  │ 25│                                                      │ │
│          │  │   │ ── Sourced      ··· Contacted                        │ │
│          │  │ 20│/                                                      │ │
│          │  │   │  ····           --- Responded                        │ │
│          │  │ 15│ ····                                                  │ │
│          │  │   │      ────       ─·─ Screening                        │ │
│          │  │ 10│         ----    ═══ Interview                         │ │
│          │  │  5│             ─·─·                                      │ │
│          │  │  0├────────┬────────┬────────┬────────                    │ │
│          │  │   Feb 1    Mar 1    Mar 15   Mar 22                      │ │
│          │  └──────────────────────────────────────────────────────────┘ │
│          │                                                               │
└──────────┴───────────────────────────────────────────────────────────────┘

Sankey details:
  • Bars proportional to stage population
  • Drop-off paths in RED with count + reason labels
  • Node labels: stage name + count
  • 7-stage flow: Sourced → Contacted → Responded → Screening →
                  Interview → Offer → Hired

Line chart details:
  • One line per stage with distinct colors
  • X-axis: date timeline
  • Y-axis: candidate count
  • Legend + grid lines

Empty state:
  ┌─────────────────────────────────────────┐
  │         📊                              │
  │  No pipeline data yet.                  │
  │  Add candidates to see metrics.         │
  └─────────────────────────────────────────┘
```

---

## 8. Engage — User Flows

### 8.1 Primary Engage Flow

```
START
  │
  ▼
Click [▶ Engage] in requisition sub-nav
  │
  ▼
┌─────────────────────────────────────────┐
│  SETTINGS PREREQUISITE CHECK            │
│                                         │
│  Sender Identity configured?  ☑/☐      │
│  Email Sequence configured?   ☑/☐      │
│  Email Preferences configured?   ☑/☐      │
└────────────────┬────────────────────────┘
                 │
         ┌───────┴────────┐
         │ All configured?│
         └───────┬────────┘
            Yes  │  No
         ┌───────┼────────┐
         ▼       │        ▼
  ┌──────────┐   │  ┌──────────────────────┐
  │ Engage   │   │  │ ⚠ Settings required  │
  │ Landing  │   │  │ [Go to Settings →]   │
  │ (List)   │   │  └──────────────────────┘
  └────┬─────┘   │
       │         │
  ┌────┴──────┬──┴───────┬──────────┬───────────┐
  ▼           ▼          ▼          ▼           ▼
[List]     [Email]   [Calendar] [Kanban]   [Metrics]
DEFAULT
```

### 8.2 Outreach Flow (Engage Batch Action)

```
Engage > List View
       │
       ▼
Select candidates via checkboxes
       │
       ▼
Click [Engage ▼]
       │
       ▼
┌──────────────────────────────────────────┐
│ Settings prerequisite check              │
└──────────────────┬───────────────────────┘
                   │
              ┌────┴────┐
              │ Pass?   │
              └────┬────┘
           Yes     │     No
          ┌────────┼────────┐
          ▼        │        ▼
  ┌──────────────┐ │  ┌──────────────────────┐
  │ Move to      │ │  │ ⚠ Configure settings │
  │ "Contacted"  │ │  │ before sending emails │
  │              │ │  └──────────────────────┘
  │ Generate     │ │
  │ personalized │ │
  │ emails per   │ │
  │ candidate    │ │
  └──────┬───────┘ │
         │         │
         ▼         │
  Emails queued    │
  for auto-send    │
  per sequence     │
  schedule         │
```

### 8.3 Email Compose Flow (AI-Driven)

```
AI Chat: "Write an outreach email for Sarah Chen"
       │
       ▼
┌───────────────────────────────────────────────────┐
│ AI checks:                                         │
│ 1. Settings prerequisites met?                     │
│ 2. Candidate profile available?                    │
│ 3. Email sequence/templates configured?            │
└──────────────────────┬────────────────────────────┘
                       │
                  ┌────┴────┐
                  │All OK?  │
                  └────┬────┘
               Yes     │     No
              ┌────────┼────────┐
              ▼        │        ▼
   AI drafts email     │  AI explains what's missing
   (subject + body)    │  Offers to help configure
   grounded in:        │
   • Candidate profile │
   • Job details       │
   • Sequence templates│
              │        │
              ▼        │
   ┌──────────────────────────────────────┐
   │ APPROVAL CARD                        │
   │                                      │
   │ To: Sarah Chen                       │
   │ Subject: Your work at Google...      │
   │ Body: Hi Sarah, I came across...     │
   │                                      │
   │              [Approve] [Reject]      │
   └──────────────────────────────────────┘
              │
       ┌──────┴──────┐
   Approve        Reject
       │              │
       ▼              ▼
  Email queued    Discarded
  for sending     (no action)
```

### 8.4 Bulk Outreach Flow (AI-Driven)

```
AI Chat: "Send emails to all sourced candidates"
       │
       ▼
AI generates personalized emails for each candidate
       │
       ▼
┌──────────────────────────────────────────────────┐
│ BATCH APPROVAL CARD                               │
│                                                   │
│ Generated emails for 12 candidates                │
│                                                   │
│ Preview:                                          │
│ • Sarah Chen — "Your work at Google..."           │
│ • John Park — "Your experience with..."           │
│ • ... (10 more)                                   │
│                                                   │
│           [Approve All] [Reject All]             │
└──────────────────────────────────────────────────┘
       │
       ├── Recruiter can say "cancel" during generation
       │   → Immediate stop, partial emails discarded
       │
       ├── [Approve All] → All emails queued for auto-send
       │
       └── [Reject All] → All discarded

IMPORTANT: AI never suggests bulk send proactively.
           Only generates when recruiter explicitly asks.
```

### 8.5 Calendar Booking Flow

```
Two paths to schedule screenings:

PATH A — Candidate Self-Booking
──────────────────────────────

Recruiter generates booking link
  │
  ├── From Calendar: [Generate Booking Link]
  ├── From Candidate Drawer: [Generate Booking Link]
  └── From AI Chat: "Create a booking page for this req"
       │
       ▼
Configure: duration, date range, custom message
       │
       ▼
Link generated (unique per candidate or per req)
       │
       ▼
Recruiter shares link (via outreach email or manually)
       │
       ▼
Candidate visits booking page
  │
  ▼
Sees available slots (working hours - Outlook events)
  │
  ▼
Candidate selects a slot
  │
  ▼
┌───────────────────────────────────────────────┐
│ On booking:                                    │
│ • Event created on Spot calendar               │
│ • Event syncs to Outlook (if connected)        │
│ • candidate.screening_status → "Scheduled"     │
│ • candidate.stage → "Screening"                │
│ • Confirmation emails to both parties          │
│ • Slot removed from other candidates' view     │
└───────────────────────────────────────────────┘


PATH B — Manual Invite
──────────────────────

Click date cell on calendar → OR → AI: "schedule screening with John Thu 2pm"
       │                               │
       ▼                               ▼
  Invite Modal opens              AI checks availability
  (date pre-filled)                    │
       │                          ┌────┴────┐
       ▼                          │Conflict?│
  Fill: candidate, time,          └────┬────┘
  duration, type, link,         No     │    Yes
  notes                        ┌───────┼───────┐
       │                       ▼       │       ▼
       ▼                  Approval     │  "Slot conflicts with
  [Send Invite]           Card         │   [event]. How about
       │                       │       │   10am or 3pm instead?"
       ▼                       ▼       │
  Same effects as         On approve:  │
  booking flow above      same effects │
```

### 8.6 Email Sequence Creation Flow

```
(Same 4-step wizard as in PM prototype, preserved here)

Engage > List > Select candidates > [Send outreach] > [+ Create new sequence]
       │
       ▼
┌─ STEP 1: Context ────────────────────────────────────────┐
│ Pre-filled from role context:                             │
│ • Job title + company (from Intake)                       │
│ • Candidate profile (from Source strategy)                │
│ • Tone: [Direct ▼] / Warm / Technical        [editable] │
│ • Number of touches: [3 ▼]                    [editable] │
│                                [Generate sequence →]     │
└──────────────────────────────────────────────────────────┘
       │
       ▼ AI generates draft
┌─ STEP 2: Review & Edit Steps ────────────────────────────┐
│ Step 1: Day 0 · Email · Auto-send                         │
│   Subject: [editable]  Body: [editable]   [Edit][Delete] │
│       │ Wait 4 days                                       │
│ Step 2: Day 4 · Email · Auto-send                         │
│   Subject: [editable]  Body: [editable]   [Edit][Delete] │
│       │ Wait 7 days                                       │
│ Step 3: Day 11 · Email · Auto-send                        │
│   Subject: [editable]  Body: [editable]   [Edit][Delete] │
│ [+ Add step]                          [← Back][Continue →]│
└──────────────────────────────────────────────────────────┘
       │
       ▼
┌─ STEP 3: Settings ───────────────────────────────────────┐
│ Sequence name: [auto-suggested, editable]                 │
│ Stop conditions:                                          │
│   ☑ Replies to any email (default ON)                     │
│   ☑ Books a meeting (default ON)                          │
│   ☐ Opens without replying after step 2                   │
│ Sending window: Weekdays · 9am-6pm (America/Los_Angeles)  │
│ Include scheduler link: ☑ Yes                             │
│                                       [← Back][Continue →]│
└──────────────────────────────────────────────────────────┘
       │
       ▼
┌─ STEP 4: Save ───────────────────────────────────────────┐
│ ✓ Sequence ready                                          │
│ "Senior FE — 3-touch" · 3 steps · Auto-send              │
│                                                           │
│ [Save to library]           [Use this time only]         │
│                                                           │
│ → Returns to sequence picker, new sequence pre-selected   │
│   [Start outreach →]                                      │
└──────────────────────────────────────────────────────────┘
```

### 8.7 Notification Flow

```
┌─────────────────────────┐
│ Bell Icon [🔔●]          │
│ ● = new unread activity  │
│ Click → dropdown opens   │
└────────────┬────────────┘
             │
             ▼
┌──────────────────────────────────────────────────────┐
│ NOTIFICATIONS                          [Mark all read]│
│                                                       │
│ [All] [Replied] [Bounced] [Sent] [Calendar] [Meeting]│
│ ──────────────────────────────────────────────────── │
│                                                       │
│ 🟢 Maya Rodriguez replied to your outreach   2m ago  │
│    Sr FE @ SeekOut                                    │
│                                                       │
│ 📅 Kevin Tran booked a screening            1h ago   │
│    Mar 26, 3pm · Sr FE @ SeekOut                      │
│                                                       │
│ 📧 Step 2 sent to David Kim                3h ago    │
│    SWE-Platform @ Meridian                            │
│                                                       │
│ 🔴 Email to sarah.j@old.co bounced         1d ago    │
│    SWE-Platform @ Meridian                            │
│                                                       │
│ 📅 Priya Sharma — interview in 30 min     Upcoming   │
│    SWE-Platform @ Meridian                            │
│                                                       │
└──────────────────────────────────────────────────────┘

Click notification → navigates to relevant screen
```

---

## 9. Settings — Information Architecture

**Mental model:** Like the "Preferences" pane in an email client. You set your
signature, send windows, templates — and every email the AI drafts reflects
those choices.

**Success metric:** Email reply rate > 20% (P0), # emails needed per response (P1).

```
Settings (Per-Requisition — /requisition/:id/settings)
│
│  "The recruiter's control panel for how the AI behaves on their behalf."
│
├── Tab Bar: [Sender Identity] | Email Sequences | Screening Settings | Email Preferences
│                  ↑ default
│
├── Sender Identity ──────────── PREREQUISITE · The "from" line
│   │
│   │  Data model:
│   ├── email_address (text, required) — sender on all outreach
│   ├── full_name (text, required) — recruiter display name
│   ├── title (text) — e.g. "Senior Technical Recruiter"
│   ├── company (text)
│   ├── linkedin_url (URL) — included in signatures and outreach
│   ├── phone (text, optional) — for callbacks or signature
│   ├── signature (long-form text, required) — HTML-safe, supports
│   │     line breaks, links, basic formatting; appended to every email
│   ├── working_hours.start (HH:MM)
│   ├── working_hours.end (HH:MM)
│   ├── working_hours.days (list of weekdays)
│   └── timezone (IANA string, e.g. "America/New_York")
│
│   Key behavior:
│   • Auto-copied from personal settings of workspace owner
│   • If owner changes → auto-update these fields
│   • AI reads all fields to personalize every outreach email
│   • AI respects working hours/timezone for send scheduling
│
├── Email Sequences ─────────── PREREQUISITE · Multi-step outreach cadences
│   │
│   │  Sequence data model:
│   ├── id (string, unique)
│   ├── name (text) — e.g. "Standard 3-Touch Outreach"
│   ├── total_stages (number, 1–4)
│   └── last_modified (timestamp)
│   │
│   │  Stage data model (within sequence):
│   ├── stage (label: first | second | third | fourth)
│   ├── delay_days (number, min 1) — days after previous stage
│   └── template_id (string) — links to email template
│   │
│   │  Email Template data model:
│   ├── id (string, unique)
│   ├── subject (text) — supports {{variables}}
│   │     e.g. {{candidate_name}}, {{company_name}}
│   └── body (text) — supports {{variables}}
│
│   Key behavior:
│   • AI can proactively RECOMMEND sequence changes based on perf data
│     (e.g. "2nd follow-up has 2% reply rate — consider different strategy")
│   • AI never MODIFIES sequences without explicit approval
│
├── Screening Settings ──────── Redirects to SAM landing page
│   └── (Not a form — navigates to external SAM product)
│
└── Email Preferences ───────── PREREQUISITE · Send rules & defaults
    ├── send_window.start (HH:MM, required)
    ├── send_window.end (HH:MM, required)
    ├── send_window.timezone (IANA string, required)
    ├── daily_send_limit (number, required)
    ├── Default stop conditions
    ├── Scheduler link configuration
    └── Email tracking preferences
```

---

## 10. Settings — Screen Diagrams

### 10.1 Settings — Sender Identity (Default Tab)

**The "from" line on every candidate touchpoint.**
Auto-copied from personal settings of workspace owner. If owner changes → auto-update.

```
┌──────────────────────────────────────────────────────────────────────────┐
│ ← SeekOut — Senior FE @ SeekOut                  Mock [toggle] [🔔][👤] │
├──────────┬───────────────────────────────────────┬───────────────────────┤
│          │                                       │                       │
│[⊙]Intake │  ← Settings                           │  [AI Chat Panel]      │
│          │                                       │                       │
│[🔍]Source│  [Sender Identity] Email Sequences    │  "Update my email     │
│          │  Screening Settings  Email Preferences │   signature to        │
│[▶]Engage │                                       │   include VP of       │
│          │  ┌─ 2-column form grid ─────────────┐ │   Talent"             │
│[⊞]Views  │  │                                   │ │                       │
│          │  │  Full Name *         Email *       │ │  Approval card:      │
│[⚙•]Settngs│ │  ┌────────────┐  ┌─────────────┐ │ │  ┌────────────────┐ │
│          │  │  │Taylor Chen │  │taylor@seekout│ │ │  │signature:      │ │
│          │  │  └────────────┘  └─────────────┘ │ │  │old → new       │ │
│          │  │                                   │ │  │[Approve][Reject]│ │
│          │  │  Title               Company      │ │  └────────────────┘ │
│          │  │  ┌────────────┐  ┌─────────────┐ │ │                       │
│          │  │  │Sr Tech Recr│  │ SeekOut     │ │ │                       │
│          │  │  └────────────┘  └─────────────┘ │ │                       │
│          │  │                                   │ │                       │
│          │  │  LinkedIn URL       Phone (opt)   │ │                       │
│          │  │  ┌────────────┐  ┌─────────────┐ │ │                       │
│          │  │  │linkedin.com│  │+1-425-555-01│ │ │                       │
│          │  │  └────────────┘  └─────────────┘ │ │                       │
│          │  │                                   │ │                       │
│          │  │  Email Signature *                 │ │                       │
│          │  │  ┌────────────────────────────┐   │ │                       │
│          │  │  │ Taylor Chen               │   │ │                       │
│          │  │  │ Senior Technical Recruiter │   │ │                       │
│          │  │  │ SeekOut                    │   │ │                       │
│          │  │  │ taylor@seekout.com         │   │ │                       │
│          │  │  │ 📅 calendly.com/taylor     │   │ │                       │
│          │  │  │                            │   │ │                       │
│          │  │  │ (HTML-safe · line breaks · │   │ │                       │
│          │  │  │  links · basic formatting) │   │ │                       │
│          │  │  └────────────────────────────┘   │ │                       │
│          │  │                                   │ │                       │
│          │  │  Working Hours                     │ │                       │
│          │  │  ┌────────────────────────────┐   │ │                       │
│          │  │  │ Start: [09:00]  End:[18:00]│   │ │                       │
│          │  │  │ Timezone: [America/NY   ▼] │   │ │                       │
│          │  │  │ ☑M ☑T ☑W ☑Th ☑F ☐Sa ☐Su  │   │ │                       │
│          │  │  └────────────────────────────┘   │ │                       │
│          │  │                                   │ │                       │
│          │  │  * = Required for email ops       │ │                       │
│          │  │           [Save Changes]           │ │                       │
│          │  └───────────────────────────────────┘ │                       │
└──────────┴───────────────────────────────────────┴───────────────────────┘

All fields are inline-editable.
AI reads these to personalize every outreach email automatically.
AI never asks recruiter to re-confirm these details once configured.
AI respects working hours/timezone — won't propose sends outside window.
```

### 10.2 Settings — Email Sequences

**Pre-defined multi-step outreach cadences (1–4 stages per sequence).**

```
┌──────────────────────────────────────────────────────────────────────────┐
│ ← SeekOut — Senior FE @ SeekOut                  Mock [toggle] [🔔][👤] │
├──────────┬───────────────────────────────────────┬───────────────────────┤
│          │                                       │                       │
│[⊙]Intake │  ← Settings                           │  [AI Chat Panel]      │
│          │                                       │                       │
│[🔍]Source│  Sender Identity [Email Sequences]    │  "Create a 3-touch   │
│          │  Screening Settings  Email Preferences │   sequence for       │
│[▶]Engage │                                       │   passive senior     │
│          │  Email Sequences              [+ New] │   engineers"         │
│[⊞]Views  │                                       │                       │
│          │  ┌────────────────────────────────────┐│  AI approval card:   │
│[⚙•]Settngs│ │ ▸ Senior FE — 3-touch              ││  ┌────────────────┐ │
│          │  │   3 stages · Last modified Mar 18  ││  │Full sequence:   │ │
│          │  │   📊 62% open · 18% reply           ││  │Stage 1: Day 0  │ │
│          │  │                                 [⋮]││  │Stage 2: Day 3  │ │
│          │  └────────────────────────────────────┘│  │Stage 3: Day 10 │ │
│          │                                       │  │[Approve][Reject]│ │
│          │  ┌────────────────────────────────────┐│  └────────────────┘ │
│          │  │ ▸ Platform SWE — 3-touch            ││                     │
│          │  │   3 stages · Last modified Mar 10  ││  AI can proactively │
│          │  │   📊 55% open · 12% reply           ││  RECOMMEND changes: │
│          │  │                                 [⋮]││  "2nd follow-up has │
│          │  └────────────────────────────────────┘│   2% reply rate —   │
│          │                                       │   consider different │
│          │  ┌────────────────────────────────────┐│   subject strategy" │
│          │  │ ▸ Passive candidate — warm           ││                    │
│          │  │   2 stages · Last modified Feb 28  ││  (never modifies    │
│          │  │   📊 71% open · 24% reply           ││   without approval) │
│          │  │                                 [⋮]││                      │
│          │  └────────────────────────────────────┘│                       │
│          │                                       │                       │
│          │  [⋮] → Edit | Duplicate | Delete      │                       │
│          │                                       │                       │
│          │  ⚡ At least one sequence required     │                       │
│          │    for email operations                │                       │
└──────────┴───────────────────────────────────────┴───────────────────────┘
```

### 10.2a Settings — Email Sequence: Expanded Detail

**Trigger:** Click ▸ to expand a sequence card

```
┌──────────────────────────────────────────────────────────────────────────┐
│  ▾ Senior FE — 3-touch                               [Edit] [⋮]        │
│    3 stages · Last modified Mar 18                                       │
│    📊 62% open · 18% reply · 0% bounce                                  │
│                                                                          │
│    ┌─ Stage 1: First Touch ─────────────────────────────────────────┐   │
│    │ Delay: Day 0 (immediate)                                        │   │
│    │ Template: "Initial Outreach — Personalized"                     │   │
│    │                                                                  │   │
│    │ Subject: Your work on {{company_name}}'s {{recent_project}} —   │   │
│    │ Body:    Hi {{candidate_name}}, I came across your work at      │   │
│    │          {{company_name}} and was impressed by...               │   │
│    │                                                   [Preview]     │   │
│    └─────────────────────────────────────────────────────────────────┘   │
│                │ Wait 3 days                                             │
│    ┌─ Stage 2: Second Touch ────────────────────────────────────────┐   │
│    │ Delay: 3 days after Stage 1                                     │   │
│    │ Template: "Follow-up — Value Add"                               │   │
│    │                                                                  │   │
│    │ Subject: Following up — {{job_title}} at {{company_name}}       │   │
│    │ Body:    Just wanted to resurface this — {{company_name}} is    │   │
│    │          building something exciting in...                      │   │
│    │                                                   [Preview]     │   │
│    └─────────────────────────────────────────────────────────────────┘   │
│                │ Wait 7 days                                             │
│    ┌─ Stage 3: Third Touch ─────────────────────────────────────────┐   │
│    │ Delay: 7 days after Stage 2                                     │   │
│    │ Template: "Final Touch — Soft Close"                            │   │
│    │                                                                  │   │
│    │ Subject: Last note — no worries if not a fit                    │   │
│    │ Body:    I'll keep this brief, {{candidate_name}}...            │   │
│    │                                                   [Preview]     │   │
│    └─────────────────────────────────────────────────────────────────┘   │
│                                                                          │
└──────────────────────────────────────────────────────────────────────────┘

[Preview] button: Shows template with sample variable substitution
  e.g. {{candidate_name}} → "Maya Rodriguez"
       {{company_name}} → "SeekOut"

Supported {{variables}}:
  {{candidate_name}}    {{candidate_first_name}}   {{candidate_title}}
  {{candidate_company}} {{company_name}}           {{job_title}}
  {{recruiter_name}}    {{recruiter_title}}        {{linkedin_url}}
```

### 10.3 Settings — Screening Settings

**This tab navigates to the SAM landing page — it is NOT a form within Settings.**

```
┌──────────────────────────────────────────────────────────────────────────┐
│ ← SeekOut — Senior FE @ SeekOut                  Mock [toggle] [🔔][👤] │
├──────────┬───────────────────────────────────────┬───────────────────────┤
│          │                                       │                       │
│[⊙]Intake │  ← Settings                           │  [AI Chat Panel]      │
│          │                                       │                       │
│[🔍]Source│  Sender Identity  Email Sequences     │                       │
│          │  [Screening Settings]  Email Prefs    │                       │
│[▶]Engage │                                       │                       │
│          │  ┌────────────────────────────────────┐│                       │
│[⊞]Views  │  │                                    ││                       │
│          │  │  Screening configuration is        ││                       │
│[⚙•]Settngs│ │  managed in SAM.                    ││                      │
│          │  │                                    ││                       │
│          │  │  [Open SAM →]                      ││                       │
│          │  │                                    ││                       │
│          │  │  (Navigates to SAM landing page)   ││                       │
│          │  │                                    ││                       │
│          │  └────────────────────────────────────┘│                       │
│          │                                       │                       │
└──────────┴───────────────────────────────────────┴───────────────────────┘
```

### 10.4 Settings — Email Preferences

```
┌──────────────────────────────────────────────────────────────────────────┐
│ ← SeekOut — Senior FE @ SeekOut                  Mock [toggle] [🔔][👤] │
├──────────┬───────────────────────────────────────┬───────────────────────┤
│          │                                       │                       │
│[⊙]Intake │  ← Settings                           │  [AI Chat Panel]      │
│          │                                       │                       │
│[🔍]Source│  Sender Identity  Email Sequences     │                       │
│          │  Screening Settings  [Email Prefs]    │                       │
│[▶]Engage │                                       │                       │
│          │  Email Preferences                    │                       │
│[⊞]Views  │                                       │                       │
│          │  Sending Window *                     │                       │
│[⚙•]Settngs│ ┌────────────────────────────────────┐│                      │
│          │  │ Start: [09:00 ▼]  End: [18:00 ▼]   ││                      │
│          │  │ Timezone: [America/New_York    ▼]   ││                      │
│          │  │ Days: ☑M ☑T ☑W ☑Th ☑F ☐Sa ☐Su     ││                      │
│          │  └────────────────────────────────────┘│                       │
│          │                                       │                       │
│          │  Daily Send Limit *                   │                       │
│          │  ┌────────────────────────────────────┐│                       │
│          │  │ Max emails per day: [50 ▼]         ││                       │
│          │  └────────────────────────────────────┘│                       │
│          │                                       │                       │
│          │  Default Stop Conditions              │                       │
│          │  ┌────────────────────────────────────┐│                       │
│          │  │ ☑ Stop when candidate replies       ││                      │
│          │  │ ☑ Stop when candidate books meeting ││                      │
│          │  │ ☐ Stop after X opens without reply  ││                      │
│          │  └────────────────────────────────────┘│                       │
│          │                                       │                       │
│          │  Scheduler Configuration              │                       │
│          │  ┌────────────────────────────────────┐│                       │
│          │  │ Scheduler link:                     ││                      │
│          │  │ ┌──────────────────────────────┐   ││                      │
│          │  │ │ https://calendly.com/taylor  │   ││                      │
│          │  │ └──────────────────────────────┘   ││                      │
│          │  │ ☑ Auto-include in outreach emails  ││                      │
│          │  │ ☑ Show real-time availability       ││                      │
│          │  └────────────────────────────────────┘│                       │
│          │                                       │                       │
│          │  Email Tracking                       │                       │
│          │  ┌────────────────────────────────────┐│                       │
│          │  │ ☑ Track email opens                 ││                      │
│          │  │ ☑ Track link clicks                 ││                      │
│          │  │ ☑ Notify on candidate reply         ││                      │
│          │  │ ☑ Notify on email bounce            ││                      │
│          │  └────────────────────────────────────┘│                       │
│          │                                       │                       │
│          │  * = Required for email operations    │                       │
│          │                                       │                       │
│          │           [Save Preferences]          │                       │
└──────────┴───────────────────────────────────────┴───────────────────────┘
```

---

## 11. Settings — User Flows

### 11.1 Settings Navigation

```
Requisition Detail
       │
       ▼
Click [⚙ Settings] in sub-nav
       │
       ▼
Settings (default: Sender Identity tab)
       │
       ├── [Sender Identity] ── 2-column form grid, all inline-editable
       │   │                     Name*, email*, signature* + extras
       │   │                     Working hours, timezone, active days
       │   │                     Auto-copied from workspace owner
       │   │                     → Save validates required fields
       │   │
       │   └── AI: "update my email signature to include VP of Talent"
       │        → Approval card: field name, old → new value
       │
       ├── [Email Sequences] ── Summary list with expand to see stages
       │   ├── View: summary cards (name, stage count, success rate)
       │   ├── Expand: numbered stages with delay, strategy, template preview
       │   ├── [+ New] → Creates new sequence (or via AI chat)
       │   ├── [⋮] Edit → Edit stages, delays, templates
       │   ├── [⋮] Duplicate → Copy with "(copy)" suffix
       │   ├── [⋮] Delete → "Delete 'name'? Won't affect active candidates."
       │   │
       │   └── AI: "create a 3-touch sequence for passive senior engineers"
       │        → Approval card: full sequence (stages, delays, templates)
       │        AI can also RECOMMEND changes based on perf data
       │
       ├── [Screening Settings] ── Redirects to SAM landing page
       │   └── Not a form — navigates to external SAM product
       │
       └── [Email Preferences] ── Window*, daily limit* + defaults
           │                       Stop conditions, scheduler, tracking
           │
           └── AI: "change my daily send limit to 30"
                → Approval card: field, old → new
```

### 11.2 First-Time Setup Flow

```
New Requisition → First visit to Engage
       │
       ▼
┌──────────────────────────────────────────────────┐
│ ⚠ Set up your sender identity, email sequences,  │
│   and email preferences before sending emails.    │
│                                                   │
│                    [Go to Settings →]             │
└──────────────────────────────────────────────────┘
       │
       ▼
Settings > Sender Identity
  (Auto-copied from workspace owner's personal settings)
  Verify/edit: name, email, signature
  [Save]
       │
       ▼
Settings > Email Sequences
  [+ New] → Create sequence (1-4 stages with templates)
  OR via AI Chat: "create a 3-touch outreach sequence"
       │
       ▼
Settings > Email Preferences
  Fill: send window (start, end, timezone), daily send limit
  [Save]
       │
       ▼
All prerequisites met ✓
       │
       ▼
Navigate to Engage → All email operations unblocked
```

### 11.3 Sequence Creation Flow (from Settings)

```
Settings > Email Sequences > [+ New]
       │
       ▼
┌──────────────────────────────────────────────────────────┐
│  New Sequence                                             │
│                                                           │
│  Sequence Name                                            │
│  ┌──────────────────────────────────────────────────┐    │
│  │ e.g. Standard 3-Touch Outreach                    │    │
│  └──────────────────────────────────────────────────┘    │
│                                                           │
│  Number of Stages: [3 ▼] (1-4)                           │
│                                                           │
│  ┌─ Stage 1 (First) ────────────────────────────────┐    │
│  │ Delay: Day 0 (immediate)                          │    │
│  │ Template: [Select or create ▼]                    │    │
│  │           [+ Create new template]                 │    │
│  └───────────────────────────────────────────────────┘    │
│            │ Delay: [3 ▼] days                            │
│  ┌─ Stage 2 (Second) ───────────────────────────────┐    │
│  │ Template: [Select or create ▼]                    │    │
│  └───────────────────────────────────────────────────┘    │
│            │ Delay: [7 ▼] days                            │
│  ┌─ Stage 3 (Third) ────────────────────────────────┐    │
│  │ Template: [Select or create ▼]                    │    │
│  └───────────────────────────────────────────────────┘    │
│                                                           │
│  [Cancel]                             [Save Sequence]    │
└──────────────────────────────────────────────────────────┘


Template creation (inline or from [+ Create new]):
┌──────────────────────────────────────────────────────────┐
│  New Email Template                                       │
│                                                           │
│  Subject                                                  │
│  ┌──────────────────────────────────────────────────┐    │
│  │ Your work on {{company_name}}'s platform —        │    │
│  └──────────────────────────────────────────────────┘    │
│                                                           │
│  Body                                                     │
│  ┌──────────────────────────────────────────────────┐    │
│  │ Hi {{candidate_first_name}},                      │    │
│  │                                                    │    │
│  │ I came across your work at {{candidate_company}}  │    │
│  │ and was impressed by your experience with...      │    │
│  │                                                    │    │
│  │ {{recruiter_name}}                                │    │
│  │ {{recruiter_title}}, {{company_name}}             │    │
│  └──────────────────────────────────────────────────┘    │
│                                                           │
│  [Preview with sample data]         [Save Template]      │
└──────────────────────────────────────────────────────────┘
```

### 11.4 Owner Change Auto-Update Flow

```
Workspace owner changes (e.g. Taylor → Sarah)
       │
       ▼
System auto-copies Sarah's personal settings:
  • email_address
  • full_name
  • title, company
  • linkedin_url, phone
  • signature
  • working_hours, timezone
       │
       ▼
Settings > Sender Identity reflects new owner
(No manual action needed — seamless handoff)
```

---

## 12. Cross-Cutting Concerns

### 12.1 AI Chat Panel (Persistent, Context-Aware)

```
┌───────────────────────────┐
│  AI Chat Panel (right)    │
│  Width: ~35vw             │
│  Toggle: 💬 in navbar     │
│  Available on ALL pages   │
│                           │
│  RULES:                   │
│  • Never acts unprompted  │
│  • All mutations require  │
│    approval cards         │
│  • Checks prerequisites  │
│    before email ops       │
│                           │
│  CAPABILITIES BY PAGE:    │
│                           │
│  List:                    │
│  "Add Sarah to pipeline"  │
│  "Move Maya to Screening" │
│  "Engage top 5 candidates"│
│                           │
│  Email:                   │
│  "Compose email for Sarah"│
│  "Make subject more casual"│
│  "Send to all sourced"    │
│  "Cancel that" (bulk stop)│
│                           │
│  Calendar:                │
│  "Schedule screening with │
│   John for Thu 2pm"       │
│  "Send booking page to    │
│   Sarah for screening"    │
│  "Create booking page     │
│   for this req"           │
│                           │
│  Settings:                │
│  "Update my email to..."  │
│  "Create a warm sequence" │
│  "Change daily limit to   │
│   30"                     │
│                           │
│  Metrics:                 │
│  "What's our reply rate?" │
│  "Show drop-off analysis" │
│                           │
│  APPROVAL CARD PATTERN:   │
│  ┌─────────────────────┐  │
│  │ [Action description]│  │
│  │ [Details/preview]   │  │
│  │ [Approve] [Reject]  │  │
│  └─────────────────────┘  │
└───────────────────────────┘
```

### 12.2 Notification System

```
Types:
  🟢 Replied   — Candidate responded     → Email tab, thread
  🔴 Bounced   — Email delivery failed   → Email tab, bounce indicator
  📧 Sent      — Sequence step sent      → Email tab, thread
  📅 Calendar  — Candidate booked slot   → Calendar tab, event
  📅 Meeting   — Upcoming reminder       → Calendar tab, event

Bell icon: [🔔] normal, [🔔●] new unread (red dot)
Dropdown filters: [All] [Replied] [Bounced] [Sent] [Calendar] [Meeting]
```

---

## 13. Navigation Architecture

```
SPOT App
│
├── [📋] Requisitions (global)
│        └── Requisition Detail
│              ├── AI Chat (default view)
│              ├── ⊙ Intake
│              ├── 🔍 Source
│              ├── ▶ Engage ──────────────────────────────────────────────
│              │     │
│              │     ├── [List] ← DEFAULT
│              │     │     ├── Table: Name/Title/Co/Exp/Stage/Email/Scrn/Match
│              │     │     ├── Search + Stage filter
│              │     │     ├── Multi-select → [Engage] (batch → Contacted + emails)
│              │     │     ├── Click row → Candidate detail drawer
│              │     │     │     ├── Profile / Notes tabs
│              │     │     │     ├── Stage dropdown (manual override)
│              │     │     │     ├── Match score (1-5)
│              │     │     │     ├── Email status + screening status
│              │     │     │     └── Generate booking link
│              │     │     └── AI: add/move/update/remove (approval cards)
│              │     │
│              │     ├── [Email]
│              │     │     ├── Inbox: threads sorted by recency
│              │     │     ├── Filters: status + stage + labels (AND, combinable)
│              │     │     ├── Custom labels (name + color)
│              │     │     ├── Click thread → Drawer
│              │     │     │     ├── Full thread (chronological)
│              │     │     │     ├── Open count + last opened
│              │     │     │     ├── Label management
│              │     │     │     ├── Reply compose
│              │     │     │     └── "Draft with AI" split button
│              │     │     │           ├── Send screening link
│              │     │     │           ├── Answer questions
│              │     │     │           └── Ask to schedule
│              │     │     └── AI: compose, edit, bulk outreach (approval cards)
│              │     │
│              │     ├── [Calendar]
│              │     │     ├── Month grid (prev/next/Today)
│              │     │     ├── Color-coded: 🟣 intake, ⚫ screening, 🔵 Outlook
│              │     │     ├── [Connect Outlook] (OAuth sync)
│              │     │     ├── [Generate Booking Link] → config modal → shareable
│              │     │     ├── Click date → Manual invite modal
│              │     │     ├── Click event → Candidate drawer
│              │     │     ├── Upcoming events list
│              │     │     └── AI: schedule, send booking page, check availability
│              │     │
│              │     ├── [Kanban]
│              │     │     ├── Fixed 7 columns (pipeline stages)
│              │     │     ├── Cards auto-move on email/system events
│              │     │     ├── Click card → Candidate detail drawer
│              │     │     └── Empty column: "No candidates" placeholder
│              │     │
│              │     └── [Metrics]
│              │           ├── Pipeline Progression (Sankey, 7 stages)
│              │           ├── Stage Activity Over Time (Line chart)
│              │           └── View-only + empty state
│              │
│              ├── ⊞ Views
│              └── ⚙ Settings ────────────────────────────────────────────
│                    │
│                    ├── [Sender Identity] ← DEFAULT
│                    │     ├── email_address * | full_name *
│                    │     ├── title | company
│                    │     ├── linkedin_url | phone (opt)
│                    │     ├── signature * (HTML-safe, rich text)
│                    │     ├── working_hours (start/end/days)
│                    │     ├── timezone (IANA)
│                    │     └── Auto-copied from workspace owner
│                    │
│                    ├── [Email Sequences]
│                    │     ├── Summary list with expand for stage detail
│                    │     ├── Sequence: name, total_stages (1-4), last_modified
│                    │     ├── Stage: label (first-fourth), delay_days, template_id
│                    │     ├── Template: subject + body with {{variables}}
│                    │     ├── [+ New] | [⋮] Edit | Duplicate | Delete
│                    │     └── AI recommends changes, never modifies without approval
│                    │
│                    ├── [Screening Settings]
│                    │     └── Redirects to SAM landing page (external)
│                    │
│                    └── [Email Preferences]
│                          ├── send_window * (start/end/tz)
│                          ├── daily_send_limit *
│                          ├── Default stop conditions
│                          ├── Scheduler link config
│                          └── Email tracking toggles
│
├── [▶] Engage (global — cross-requisition)
│        └── Same 5 views but shows ALL candidates with Req column
│
└── [🔔] Notifications (top nav)
         ├── Filters: Replied / Bounced / Sent / Calendar / Meeting
         └── Click → Navigate to relevant screen

* = Required field (prerequisite for email operations)
```

---

*UX specification for Engage & Settings — March 2026*
*Sources: PM ASCII prototype, Engage PRD, Settings PRD, UX Q&A (25 questions), SCREENS_AND_FLOWS.md*
*Note: Screening Settings redirects to SAM (external). Confluence docs require auth for additional context.*
