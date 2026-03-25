# Helix Notifications — Wireframes

**Date:** 2026-03-25
**Source:** [PRD](./prd.md)

---

## Screens

### 1. Settings — Notification Preferences (HM-only User)

Notification preferences section in Settings, below Slack integration.

```
┌──────────────────────────────────────────────────────┐
│  seekout>                           [Sarah C.] [⚙]  │
├──────────────┬───────────────────────────────────────┤
│              │                                       │
│  Job postings│  Settings                             │
│              │                                       │
│  ■ Sr. Prod  │  Slack Integration                    │
│    Designer  │  ┌─────────────────────────────────┐  │
│              │  │ ✓ Connected to Acme Workspace   │  │
│ ──────────── │  │ [Test] [Disconnect]             │  │
│              │  └─────────────────────────────────┘  │
│  ⚙ Settings  │                                       │
│              │  ─────────────────────────────────── │
│              │                                       │
│              │  Email Notifications                  │
│              │                                       │
│              │  Choose which events send you an      │
│              │  email. In-app notifications are      │
│              │  always on.                           │
│              │                                       │
│              │  As a hiring manager                  │
│              │                                       │
│              │  ┌─────────────────────────────────┐  │
│              │  │                        Email    │  │
│              │  │ New candidates         [■ ON]   │  │
│              │  │ ─────────────────────────────── │  │
│              │  │ AI screening results   [■ ON]   │  │
│              │  │ ─────────────────────────────── │  │
│              │  │ Updates from teammates [■ ON]   │  │
│              │  │ ─────────────────────────────── │  │
│              │  │ Collaboration invites  Always   │  │
│              │  │ ─────────────────────────────── │  │
│              │  │ Weekly digest          [■ ON]   │  │
│              │  └─────────────────────────────────┘  │
│              │                                       │
└──────────────┴───────────────────────────────────────┘
```

**Key Elements:**

| Region | Contents |
|--------|----------|
| **Slack section** | Existing Slack integration (unchanged) |
| **Section header** | "Email Notifications" with helper text |
| **Role label** | "As a hiring manager" |
| **Toggleable rows** | New candidates, AI screening results, Updates from teammates, Weekly digest — all default ON |
| **Mandatory row** | Collaboration invites shows "Always" (no toggle) |
| **Save feedback** | Toggles show brief inline "Saved" confirmation (no save button) |

**States:**

| State | Description |
|-------|-------------|
| **Default** | All toggles ON (smart defaults) |
| **Partially configured** | Mix of ON/OFF toggles |
| **Slack disconnected** | Slack section shows [Connect Slack] button instead |

---

### 2. Settings — Notification Preferences (Dual-Persona User)

Both role sections visible. Mandatory events show "Always". Digest toggle appears once in General section.

```
┌──────────────────────────────────────────────────────┐
│  seekout>                           [Sarah C.] [⚙]  │
├──────────────┬───────────────────────────────────────┤
│              │                                       │
│  Job postings│  Settings                             │
│              │                                       │
│  ■ Sr. Prod  │  Slack Integration                    │
│    Designer  │  ┌─────────────────────────────────┐  │
│ ──────────── │  │ ✓ Connected to Acme Workspace   │  │
│              │  └─────────────────────────────────┘  │
│  Jobseekers  │                                       │
│  ■ Portfolio │  ─────────────────────────────────── │
│  ■ Apps      │                                       │
│ ──────────── │  Email Notifications                  │
│              │                                       │
│  ⚙ Settings  │  Choose which events send you an      │
│              │  email. In-app notifications are      │
│              │  always on.                           │
│              │                                       │
│              │  As a hiring manager                  │
│              │                                       │
│              │  ┌─────────────────────────────────┐  │
│              │  │                        Email    │  │
│              │  │ New candidates         [■ ON]   │  │
│              │  │ ─────────────────────────────── │  │
│              │  │ AI screening results   [■ ON]   │  │
│              │  │ ─────────────────────────────── │  │
│              │  │ Updates from teammates [■ ON]   │  │
│              │  │ ─────────────────────────────── │  │
│              │  │ Collaboration invites  Always   │  │
│              │  └─────────────────────────────────┘  │
│              │                                       │
│              │  As a job seeker                      │
│              │                                       │
│              │  ┌─────────────────────────────────┐  │
│              │  │                        Email    │  │
│              │  │ Portfolio viewed        Always   │  │
│              │  │ ─────────────────────────────── │  │
│              │  │ Application advancing  Always   │  │
│              │  │ ─────────────────────────────── │  │
│              │  │ Not selected            Always   │  │
│              │  ├─────────────────────────────────┤  │
│              │  │ ℹ These are always on to keep   │  │
│              │  │   you in the loop on your       │  │
│              │  │   applications.                 │  │
│              │  └─────────────────────────────────┘  │
│              │                                       │
│              │  ─────────────────────────────────── │
│              │                                       │
│              │  General                              │
│              │                                       │
│              │  ┌─────────────────────────────────┐  │
│              │  │ Weekly digest          [■ ON]   │  │
│              │  └─────────────────────────────────┘  │
│              │                                       │
└──────────────┴───────────────────────────────────────┘
```

**Key Elements:**

| Region | Contents |
|--------|----------|
| **Sidebar** | Both HM nav (Job postings) and Prospect nav (Portfolio, Apps) |
| **HM section** | 3 toggleable + 1 mandatory event |
| **Prospect section** | 3 mandatory events with "Always" label + info note |
| **General section** | Weekly digest toggle (one toggle, controls combined digest) |

**States:**

| State | Description |
|-------|-------------|
| **HM-only** | HM section + General section only (Screen 1) |
| **Prospect-only** | Prospect section + General section only |
| **Dual-persona** | All three sections (this screen) |

---

### 3. Settings — Notification Preferences (Empty State)

User has no jobs and no applications.

```
┌──────────────────────────────────────────────────────┐
│  seekout>                           [Sarah C.] [⚙]  │
├──────────────┬───────────────────────────────────────┤
│              │                                       │
│  Job postings│  Settings                             │
│              │                                       │
│ ──────────── │  Slack Integration                    │
│              │  ┌─────────────────────────────────┐  │
│  ⚙ Settings  │  │ [Connect Slack]                 │  │
│              │  └─────────────────────────────────┘  │
│              │                                       │
│              │  ─────────────────────────────────── │
│              │                                       │
│              │  Email Notifications                  │
│              │                                       │
│              │  ┌─────────────────────────────────┐  │
│              │  │                                 │  │
│              │  │  Notification preferences will   │  │
│              │  │  appear here once you start      │  │
│              │  │  using SeekOut.                   │  │
│              │  │                                 │  │
│              │  │  [Create a job →]               │  │
│              │  │                                 │  │
│              │  └─────────────────────────────────┘  │
│              │                                       │
└──────────────┴───────────────────────────────────────┘
```

---

### 4. Notification Panel (Unified Feed)

Single notification panel for all users. Dual-persona users see HM and prospect events interleaved chronologically with role indicators. Single-persona users see only their role's events without indicators.

```
┌──────────────────────────────────────────────────────┐
│  seekout>                           [Sarah C.] [⚙]  │
├──────────────┬───────────────────────────────────────┤
│              │                                       │
│  Job postings│  ← Job postings                       │
│              │  Senior Product Designer              │
│  ■ Sr. Prod  │                                       │
│    Designer  │  ...                                  │
│ ──────────── │                                       │
│  Jobseekers  │                                       │
│  ■ Portfolio │                                       │
│  ■ Apps      │                                       │
│ ──────────── │                                       │
│  ⚙ Settings  │                                       │
│              │                                       │
│  🔔 5        │                                       │
│  ┌───────────┴───────────────────────────────────┐   │
│  │ Notifications              [Mark all read]    │   │
│  │                                               │   │
│  │ ● Your portfolio was viewed 3 times in        │   │
│  │   the last hour                               │   │
│  │   Job seeking · 25 min ago                    │   │
│  │ ─────────────────────────────────────────     │   │
│  │ ● 5 new candidates for Sr. Product            │   │
│  │   Designer                                    │   │
│  │   Hiring · 30 min ago                         │   │
│  │ ─────────────────────────────────────────     │   │
│  │ ● Jordan Lee invited you to collaborate       │   │
│  │   on ML Engineer                              │   │
│  │   Hiring · 1 hr ago                           │   │
│  │ ─────────────────────────────────────────     │   │
│  │ ● Your application is progressing             │   │
│  │   Senior Designer at Acme Corp                │   │
│  │   Job seeking · Yesterday                     │   │
│  │ ─────────────────────────────────────────     │   │
│  │ ○ Alex reviewed 4 candidates in               │   │
│  │   Sr. Product Designer                        │   │
│  │   Hiring · Yesterday                          │   │
│  │                                               │   │
│  │            [Notification preferences]         │   │
│  └───────────────────────────────────────────────┘   │
│              │                                       │
└──────────────┴───────────────────────────────────────┘
```

**Key Elements:**

| Region | Contents |
|--------|----------|
| **Sidebar** | Dual-persona nav. Single-persona users see only their role's nav. |
| **Bell badge** | Combined unread count across all roles (red badge, "99+" if >99) |
| **Role indicator** | "Hiring" or "Job seeking" tag on metadata line. Hidden for single-persona users. |
| **Unread indicator** | ● = unread, ○ = read |
| **Preferences link** | Footer link to Settings |

**States:**

| State | Description |
|-------|-------------|
| **Empty** | "No notifications yet" with illustration |
| **All read** | All items show ○, badge hidden |
| **Overflow** | Scrollable, paginated (20 per load) |
| **Single-persona** | Only that role's events; role indicators hidden |

---

### 5. Email — Collaborator Invited

Mandatory email when a HM invites an existing user to collaborate on a job.

```
┌──────────────────────────────────────────────────┐
│ ▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓ │
│ ▓  seekout>                              Helix ▓ │
│ ▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓ │
│                                                  │
│  Hi Jordan,                                      │
│                                                  │
│  Sarah Chen invited you to collaborate on         │
│  the Senior Product Designer role.                │
│                                                  │
│  ┌──────────────────────────────────────────┐    │
│  │  Senior Product Designer                 │    │
│  │  Bellevue, WA · Hybrid                   │    │
│  └──────────────────────────────────────────┘    │
│                                                  │
│          [  View Job  ]                           │
│                                                  │
│  ──────────────────────────────────────────────  │
│  © Helix — AI-powered professional networking    │
│                                                  │
└──────────────────────────────────────────────────┘
```

**Key Elements:**

| Region | Contents |
|--------|----------|
| **Header** | Purple (#7c3aed) branded bar with Helix wordmark |
| **Body** | Who invited, which job, job location card |
| **CTA** | "View Job" deep-links to the job dashboard |
| **Footer** | No preferences link (mandatory event) |

---

### 6. Email — Weekly Digest

Combined weekly summary. Sections only appear if there's activity. Each persona gets an action-first lead-in.

```
┌──────────────────────────────────────────────────┐
│ ▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓ │
│ ▓  seekout>                              Helix ▓ │
│ ▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓ │
│                                                  │
│  Hi Sarah, here's your week in review.           │
│  Mar 17 – Mar 23, 2026                           │
│                                                  │
│  ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━  │
│  Your jobs                                       │
│  ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━  │
│                                                  │
│  ⚡ 3 candidates need your review                │
│  [Review candidates →]                           │
│                                                  │
│  Senior Product Designer                         │
│  ┌──────────────────────────────────────────┐    │
│  │  5 new candidates                        │    │
│  │  3 evaluations completed                 │    │
│  │  2 advanced, 1 rejected                  │    │
│  └──────────────────────────────────────────┘    │
│  [Review candidates →]                           │
│                                                  │
│  ML Engineer                                     │
│  ┌──────────────────────────────────────────┐    │
│  │  2 new candidates                        │    │
│  │  1 evaluation completed                  │    │
│  └──────────────────────────────────────────┘    │
│  [Review candidates →]                           │
│                                                  │
│  ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━  │
│  Your applications                               │
│  ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━  │
│                                                  │
│  ⚡ 2 applications had activity this week        │
│                                                  │
│  ┌──────────────────────────────────────────┐    │
│  │  Google — Sr. PM                         │    │
│  │  ✓ Portfolio viewed 4 times              │    │
│  │  ✓ Application advancing                │    │
│  ├──────────────────────────────────────────┤    │
│  │  Meta — Product Designer                 │    │
│  │  ⏳ Still under review (10 days)         │    │
│  ├──────────────────────────────────────────┤    │
│  │  Acme — ML Engineer                      │    │
│  │  ✗ Not selected                          │    │
│  └──────────────────────────────────────────┘    │
│  [View applications →]                           │
│                                                  │
│  ──────────────────────────────────────────────  │
│  © Helix — AI-powered professional networking    │
│  Manage notification preferences                 │
│                                                  │
└──────────────────────────────────────────────────┘
```

**Key Elements:**

| Region | Contents |
|--------|----------|
| **Header** | Greeting + date range |
| **Your jobs** | Action-first lead: "N candidates need your review." Per-job summary cards. |
| **Your applications** | Action-first lead: "N applications had activity." Per-application status including "Still under review (N days)" |
| **CTAs** | Deep-links to job dashboard or applications page |
| **Footer** | "Manage notification preferences" link |

**States:**

| State | Description |
|-------|-------------|
| **HM-only** | Only "Your jobs" section |
| **Prospect-only** | Only "Your applications" section |
| **Dual-persona** | Both sections |
| **No activity** | Email not sent |

---

## User Flows

### Preferences Discovery & Configuration

```
User receives notification
        │
        ▼
Notification Panel (Screen 4)
        │
        ├──→ Clicks [Notification preferences]
        │           │
        │           ▼
        │    Settings — Preferences (Screen 1/2)
        │           │
        │           ├──→ Toggles email OFF for an event
        │           │    (inline "Saved" confirmation)
        │           │
        │           └──→ Leaves defaults (all ON)
        │
        └──→ Clicks notification → deep-link
```

### New Candidates

```
Candidate applies / sync finds new candidates
        │
        ▼
emit("new_candidates") → 30 min debounce
        │
        ▼
Window expires → aggregate count
        │
        ├──→ IN_APP → SSE → bell badge + toast
        ├──→ EMAIL (if ON in prefs) → deep-link
        └──→ SLACK (if connected) → DM
```

### Portfolio Viewed

```
Someone views prospect's portfolio
        │
        ├──→ Inside seekout.ai
        └──→ Via application tracking link
                    │
                    ▼
              emit("portfolio_viewed") → 1 hr debounce
                    │
                    ▼
              Aggregate count → "Viewed 3 times"
                    │
                    ├──→ IN_APP: always
                    └──→ EMAIL: always (mandatory)
```

### Weekly Digest

```
Monday 9 AM (user-local time)
        │
        ▼
Query activity since last digest
        │
        ├──→ No activity → skip
        └──→ Activity found → build by role
                    │
                    ├──→ Has jobs → "Your jobs" section
                    ├──→ Has apps → "Your applications"
                    └──→ Send email (Screen 6)
```

---

## Edge Cases

- **Slack connect after prefs set:** Slack auto-appends to all events. No per-event Slack config.
- **New event type added post-launch:** Defaults to email ON.
- **Collaborator invite for non-user:** Handled by existing invite email system, not notification module.
- **Digest for new user:** First digest covers activity since account creation.
- **Feature flag OFF:** Candidate emails redirect to mailinator. In-app still created.
- **Applications stuck >7 days:** Surfaced in weekly digest as "Still under review (N days)."
