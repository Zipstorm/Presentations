# Candidate Presentation — Wireframes

**Date:** 2026-04-15
**Source:** [prd.md](./prd.md), [solution-design.md](./solution-design.md), [pm-notes.md](./pm-notes.md), [Spot Screen Diagrams](../../../context/products/spot/screen-diagrams.md), [Live Spot reference](https://spot.seekout.ai/candidate-presentation/jf0JqHsijUS5Sh0ohRSssA)

Wireframes cover the recruiter-side builder, the HM rich summary email, the HM-side external presentation surface (desktop + mobile), the Job Overview rubric view, and key edge states. HM-side surfaces (Screens 11, 12, 15, 16) follow the live Spot reference linked above.

---

## Screens

### 1. Job Landing Page — Entry Point + Post-Share State

The recruiter's existing Job Landing Page (Recruiter Flow 5), augmented with the new "Present to HM" CTA (top right) and per-candidate HM thumb status pills once a presentation has been sent. Also shows the all-thumbs-down banner state.

```
┌──────────────────────────────────────────────────────────────────────┐
│ Helix · Acme · Senior PM · Active           [bell] [Akshay v]        │
├──────────────────────────────────────────────────────────────────────┤
│ ← All Jobs                                                           │
│                                                                      │
│  Senior Product Manager — Acme              [⇪ Present to HM]        │
│  Sourced + Inbound · 47 candidates · Sam intake updated 3d ago       │
│                                                                      │
│ ⚠ All 5 candidates passed on "Shortlist for Priya" (sent 2d ago).    │
│   [↻ Refresh shortlist with Sam]   [Message Priya]   [Dismiss]       │
│                                                                      │
│ ┌──────────────────────────────────────────────────────────────────┐ │
│ │ Tabs: ■Needs review (12)  ○All (47)  ○Sent  ○Hidden              │ │
│ ├──────────────────────────────────────────────────────────────────┤ │
│ │ Filter: [Score v] [Source v] [HM thumb v]    Sort: [Score v]     │ │
│ ├──────────────────────────────────────────────────────────────────┤ │
│ │ ◉  Maya Chen      ●●●●○  AI ✓  Sourced     👍 Priya  ··· [open] │ │
│ │ ◉  Daniel Ortiz   ●●●●●  AI ✓  Inbound    👍👎 2 HMs ··· [open] │ │
│ │ ◉  Priya Shah     ●●●○○  AI ✓  Sourced       — no resp ··· [op] │ │
│ │ ◉  James Wu       ●●●●○  AI ✓  Inbound      👎 Priya  ··· [open] │ │
│ │ ◉  Lin Park       ●●○○○  AI –  Sourced       — not sent ··· [op] │ │
│ │ ...                                                              │ │
│ └──────────────────────────────────────────────────────────────────┘ │
└──────────────────────────────────────────────────────────────────────┘
```

**Key Elements:**
- **[⇪ Present to HM]** — new top-right CTA; primary entry into the builder
- **All-thumbs-down banner** — appears when every candidate in a sent presentation was thumbed down; primary action re-engages Sam
- **HM thumb column** — per-row status pill showing 👍 / 👎 / — (no response) per recipient. Multi-recipient case shows count + expand affordance
- **Hover on thumb** reveals the optional one-line reason (not shown)
- **"Sent" tab** — quick filter for candidates currently in any presentation

**States:**
- **No presentation sent yet:** banner hidden, HM thumb column shows "— not sent" for all rows
- **Presentation in flight:** rows show pending/received thumbs; "Sent" tab badge counts active presentations
- **Bounced email:** affected row shows ⚠ tooltip with bounce reason next to the recipient name (not shown — design owned)

---

### 2. Presentation Builder — Main

The builder opens as a full-page worksheet (or right-side panel — design call) when "Present to HM" is clicked. Categories, candidates, AI-pre-filled notes, Job Overview, settings.

```
┌──────────────────────────────────────────────────────────────────────┐
│ ← Back to Job          New Presentation · Senior PM — Acme           │
│                                       [Preview]  [Send to HM →]      │
├──────────────────────────────────────────────────────────────────────┤
│ ┌─ Job Overview ─────────────────────────────────────────────────┐  │
│ │ Senior Product Manager  ·  Acme  ·  Remote (US)               │  │
│ │ Priorities: B2B SaaS PM, 0→1 ownership, eng-adjacent fluency  │  │
│ │ Dealbreakers: < 5y PM tenure, agency-only background          │  │
│ │ Nice-to-haves: ML/AI exposure, design partnership             │  │
│ │ [Edit] (re-runs Sam intake summary)                            │  │
│ └────────────────────────────────────────────────────────────────┘  │
│                                                                      │
│ Settings:  [x] Show rubric scores in HM view                         │
│                                                                      │
│ ─── High Potential (2) ──────────────────────── [+ Add candidate] ── │
│                                                                      │
│ ⋮⋮ ┌──────────────────────────────────────────────────────────────┐ │
│    │ [photo] Maya Chen  ·  PM @ Stripe  ·  ●●●●○                  │ │
│    │ Note (AI draft — please edit):                               │ │
│    │ ┌──────────────────────────────────────────────────────────┐ │ │
│    │ │ Strong 0→1 signal — built Stripe Climate from scratch.   │ │ │
│    │ │ In Sam, talked specifically about losing eng trust as    │ │ │
│    │ │ the failure mode she watches for.                        │ │ │
│    │ └──────────────────────────────────────────────────────────┘ │ │
│    │ ✦ AI-drafted · [Regenerate]   ⓘ Add what's not on the CV    │ │
│    │                                              [Remove]        │ │
│    └──────────────────────────────────────────────────────────────┘ │
│                                                                      │
│ ⋮⋮ ┌──────────────────────────────────────────────────────────────┐ │
│    │ [photo] Daniel Ortiz · PM @ Plaid · ●●●●●         [Remove]   │ │
│    │ Note: Strongest rubric match. Has shipped two AI features... │ │
│    │ ✦ Edited · [Regenerate]                                      │ │
│    └──────────────────────────────────────────────────────────────┘ │
│                                                                      │
│ ─── Screened (1) ───────────────────────────── [+ Add candidate] ── │
│                                                                      │
│ ⋮⋮ ┌──────────────────────────────────────────────────────────────┐ │
│    │ [photo] Priya Shah · PM @ Notion · ●●●○○          [Remove]   │ │
│    │ Note: Met the bar but lighter on enterprise. Worth a look... │ │
│    └──────────────────────────────────────────────────────────────┘ │
│                                                                      │
│ [+ Add category]  [Rename] [Delete] (per category, on hover)         │
└──────────────────────────────────────────────────────────────────────┘
```

**Key Elements:**
- **Job Overview** — auto-populated from latest Sam intake summary; reflects re-runs
- **Categories** — "High Potential" and "Screened" defaults (mirrors Spot); rename/add/delete on hover
- **⋮⋮ drag handle** — per candidate, drag-to-reorder within a category
- **Note field** — pre-filled with AI draft; tag shows "AI draft" vs "Edited"; [Regenerate] always available
- **Inline nudge** — "Add what's not on the CV" prompt encourages recruiter customization
- **Settings toggle** — Show rubric scores in HM view (default on)
- **[Preview] / [Send to HM →]** — top-right primary actions

**States:**
- **AI-drafted (untouched):** ✦ AI-drafted tag, nudge visible
- **Edited:** ✦ Edited tag, nudge hidden
- **Regenerate after edit:** confirm modal "Discard your edits and regenerate?" (not shown)
- **Empty category:** "[+ Add candidate]" placeholder with "No candidates yet" text
- **No AI screening on candidate:** note pre-fills with rubric-top-match phrasing only
- **0 candidates total:** [Send to HM] disabled with tooltip "Add at least 1 candidate"

---

### 3. Add Candidates Modal

Triggered by [+ Add candidate]. Multi-select from the Job Landing Page candidate list, scoped by source.

```
┌──────────────────────────────────────────────────────────────────────┐
│  Add candidates to "High Potential"                          [✕]     │
├──────────────────────────────────────────────────────────────────────┤
│  Source: ■All  ○Sourced  ○Inbound       Search: [name or company]   │
│  Sort:   [Score (high → low) v]                                      │
├──────────────────────────────────────────────────────────────────────┤
│  [x] Maya Chen        PM @ Stripe        ●●●●○  Sourced  AI ✓        │
│  [x] Daniel Ortiz     PM @ Plaid         ●●●●●  Inbound  AI ✓        │
│  [ ] Priya Shah       PM @ Notion        ●●●○○  Sourced  AI ✓        │
│  [ ] James Wu         PM @ Linear        ●●●●○  Inbound  AI ✓        │
│  [ ] Lin Park         PM @ Asana         ●●○○○  Sourced  AI –        │
│  [ ] Rosa Diaz        PM @ Figma         ●●●○○  Inbound  AI ✓        │
│  ...                                                                 │
├──────────────────────────────────────────────────────────────────────┤
│  2 selected                                       [Cancel]  [Add 2]  │
└──────────────────────────────────────────────────────────────────────┘
```

**Key Elements:**
- **Source filter** — All / Sourced / Inbound (mixed-mode supported in v1, see PRD Open Question)
- **AI ✓ / AI –** — indicates whether candidate has AI screening data (drives note pre-fill)
- **Already-added candidates** — disabled and tagged "Already in presentation" (not shown for brevity)

**States:**
- **Empty list:** "No candidates match — adjust filters" placeholder
- **Mixed source warning:** if Sourced + Inbound both selected, footer note: "ⓘ Mixed source presentation — make sure your context handles this for the HM"

---

### 4. Preview

What the HM will see — recruiter renders the same external page in a read-only preview frame so they can validate before sending. Right rail offers shortcuts back to the builder.

```
┌──────────────────────────────────────────────────────────────────────┐
│  Preview · how this looks to your HM            [✕]   [← Back]       │
├───────────────────────────────────────────────┬──────────────────────┤
│  ┌─────────────────────────────────────────┐ │  Quick edits         │
│  │ helix.seekout.ai/p/preview              │ │                      │
│  │                                         │ │  Categories:         │
│  │ Senior Product Manager · Acme           │ │   High Potential (2) │
│  │ Curated by Akshay Gupta at Acme         │ │   Screened (1)       │
│  │                                         │ │   [+ Add category]   │
│  │ ── Job Overview ────────────────────    │ │                      │
│  │ Priorities: B2B SaaS PM, 0→1...         │ │  Settings:           │
│  │                                         │ │   [x] Show scores    │
│  │ ── High Potential (2) ──────────────    │ │                      │
│  │  ┌─────────────────────┐ ┌──────────┐  │ │  [Edit builder]      │
│  │  │ [photo]             │ │ [photo]  │  │ │                      │
│  │  │ Maya Chen           │ │ Daniel.. │  │ │  When you're ready:  │
│  │  │ PM @ Stripe         │ │ PM @ ... │  │ │   [Send to HM →]     │
│  │  │ "Strong 0→1 signal..│ │ "Strong..│  │ │                      │
│  │  │ ●●●●○               │ │ ●●●●●    │  │ │                      │
│  │  └─────────────────────┘ └──────────┘  │ │                      │
│  │                                         │ │                      │
│  │ ── Screened (1) ────────────────────    │ │                      │
│  │  ┌─────────────────────┐                │ │                      │
│  │  │ Priya Shah ...      │                │ │                      │
│  │  └─────────────────────┘                │ │                      │
│  └─────────────────────────────────────────┘ │                      │
└───────────────────────────────────────────────┴──────────────────────┘
```

**Key Elements:**
- **Preview frame** — pixel-faithful render of the HM landing page (Screen 11)
- **Right rail** — quick edits to categories, settings; primary [Send to HM] CTA so recruiter doesn't have to back out

**States:**
- Preview reflects "Show rubric scores" toggle live
- Toggling categories or note edits updates preview without page reload

---

### 5. Send Modal

Triggered by [Send to HM →]. Recruiter picks access mode, enters recipients (Email-share) or skips (Public link), sets expiration.

```
┌──────────────────────────────────────────────────────────────────────┐
│  Send presentation                                            [✕]    │
├──────────────────────────────────────────────────────────────────────┤
│  Access mode                                                         │
│  (●) Email-share with OTP                                            │
│      Recipients verify with a one-time code on first open.           │
│      We send a rich summary email automatically.                     │
│  (○) Public link                                                     │
│      Anyone with the link can open. Recipient self-identifies        │
│      (name + email) on first visit. No automated send.               │
│                                                                      │
│  Recipients (Email-share)                                            │
│  ┌────────────────────────────────────────────────────────────────┐ │
│  │ priya@acme.com  ✕                                              │ │
│  │ jordan@acme.com ✕                                              │ │
│  │ [+ Add another]                                                │ │
│  └────────────────────────────────────────────────────────────────┘ │
│                                                                      │
│  Sender:    "Akshay Gupta via Helix"                                 │
│  Reply-to:  akshay@acme.com (your email)                             │
│                                                                      │
│  Link expires:  [30 days v]   (you can extend or revoke later)       │
│                                                                      │
│                                       [Cancel]  [Send & copy link →] │
└──────────────────────────────────────────────────────────────────────┘
```

**Key Elements:**
- **Access mode radio** — Email-share with OTP (default) vs. Public link
- **Recipients field** — only shown for Email-share; chip-style entry, validated email format
- **Sender / Reply-to** — fixed display, confirms HM will know who sent it
- **Expiration** — default 30 days, options 7 / 30 / 90 / never

**States:**
- **Public link selected:** Recipients section hidden; CTA reads [Generate link →]
- **Invalid email:** chip turns red with inline error
- **0 recipients (Email-share):** [Send] disabled with tooltip "Add at least one recipient"
- **Re-send to same recipient:** badge "Already sent" next to chip; allowed

---

### 6. Send Confirmation

Replaces the Send modal after action completes. Surfaces the copyable link in both modes; for Email-share also confirms send + recipient list.

```
┌──────────────────────────────────────────────────────────────────────┐
│  ✓ Sent                                                       [✕]    │
├──────────────────────────────────────────────────────────────────────┤
│                                                                      │
│  Email-share — sent to 2 recipients                                  │
│  • priya@acme.com                                                    │
│  • jordan@acme.com                                                   │
│                                                                      │
│  We'll let you know on the Job Landing Page when they open and       │
│  thumb candidates.                                                   │
│                                                                      │
│  Copyable link (in case you want to send manually)                   │
│  ┌────────────────────────────────────────────────────────────────┐ │
│  │ helix.seekout.ai/p/8f4a-9c2d-bea1-3f7e            [📋 Copy]   │ │
│  └────────────────────────────────────────────────────────────────┘ │
│  Expires May 15, 2026 · [Extend] [Revoke now]                       │
│                                                                      │
│                                              [Back to Job Landing →] │
└──────────────────────────────────────────────────────────────────────┘
```

**Key Elements:**
- **Recipient list** — confirms who got the rich summary email
- **Copyable link** — always shown, both modes; for manual sends through other channels
- **Expiration controls** — quick [Extend] / [Revoke now]

**States:**
- **Public link mode:** Recipient list section hidden; headline reads "Public link generated"
- **Email send failure (any bounce):** ⚠ inline note "1 of 2 emails couldn't be delivered — see Job Landing Page for details"

---

### 7. Rich Summary Email — Standard

What the HM receives. Plain HTML, deliverability-tested. Recruiter judgment lands here even if HM never clicks.

```
┌──────────────────────────────────────────────────────────────────────┐
│ From: Akshay Gupta via Helix <noreply@helix.seekout.ai>              │
│ Reply-To: akshay@acme.com                                            │
│ Subject: Akshay sent you 3 candidates for Senior Product Manager     │
├──────────────────────────────────────────────────────────────────────┤
│                                                                      │
│  Hi Priya,                                                           │
│                                                                      │
│  I've shortlisted 3 candidates for Senior Product Manager at Acme.   │
│  Quick read below — open the full presentation when you're ready.    │
│                                                                      │
│  ── Job Overview ──────────────────────────────────────────────      │
│  Priorities: B2B SaaS PM, 0→1 ownership, eng-adjacent fluency        │
│                                                                      │
│  ── High Potential ────────────────────────────────────────────      │
│                                                                      │
│  ┌────────────────────────────────────────────────────────────────┐ │
│  │ [photo]  Maya Chen                                             │ │
│  │          PM @ Stripe · Climate                                 │ │
│  │                                                                │ │
│  │ "Strong 0→1 signal — built Stripe Climate from scratch.        │ │
│  │  In Sam, talked specifically about losing eng trust as the     │ │
│  │  failure mode she watches for."                                │ │
│  │                                                                │ │
│  │ Top matches: ✓ 0→1 ownership   ✓ B2B SaaS PM                  │ │
│  │                                                                │ │
│  │                                       [View this candidate →]  │ │
│  └────────────────────────────────────────────────────────────────┘ │
│                                                                      │
│  ┌────────────────────────────────────────────────────────────────┐ │
│  │ [photo]  Daniel Ortiz                                          │ │
│  │          PM @ Plaid · Identity                                 │ │
│  │ "Strongest rubric match. Has shipped two AI features at Plaid  │ │
│  │  and ran the eng-product weekly..."                            │ │
│  │ Top matches: ✓ B2B SaaS PM   ✓ ML/AI exposure                  │ │
│  │                                       [View this candidate →]  │ │
│  └────────────────────────────────────────────────────────────────┘ │
│                                                                      │
│  ── Screened ──────────────────────────────────────────────────      │
│                                                                      │
│  ┌────────────────────────────────────────────────────────────────┐ │
│  │ [photo]  Priya Shah · PM @ Notion                              │ │
│  │ "Met the bar but lighter on enterprise. Worth a look..."       │ │
│  │ Top matches: ✓ 0→1 ownership                                   │ │
│  │                                       [View this candidate →]  │ │
│  └────────────────────────────────────────────────────────────────┘ │
│                                                                      │
│  ┌────────────────────────────────────────────────────────────────┐ │
│  │             [⇪ Open full presentation]                         │ │
│  │     Recordings, evaluation grid, full rubric — on the page     │ │
│  └────────────────────────────────────────────────────────────────┘ │
│                                                                      │
│  Hiring for your own role? Post free on Helix → [Learn more]         │
│                                                                      │
│  — Akshay Gupta, Acme                                                │
└──────────────────────────────────────────────────────────────────────┘
```

**Key Elements:**
- **Subject pattern** — "[Recruiter] sent you [N] candidates for [Role]"
- **Per-candidate card** — photo, name, current title + company, **full recruiter note** (the differentiator), top 2 rubric matches, [View this candidate →] deep link
- **Job Overview block** — Sam intake priorities, gives HM context
- **Primary CTA** — [Open full presentation], visually anchored after candidates
- **Signup teaser** — small, tonally light; full pitch lives on the closure screen

**States:**
- Reply-to is recruiter's email — replies route directly to recruiter, not Helix
- "Show rubric scores" toggled off → "Top matches" line hidden in email and page

---

### 8. Rich Summary Email — Condensed (>6 candidates)

For slates >6, top category renders in full; remaining categories collapse to a condensed line list. CTA stays prominent above the fold.

```
┌──────────────────────────────────────────────────────────────────────┐
│ Subject: Akshay sent you 9 candidates for Senior Product Manager     │
├──────────────────────────────────────────────────────────────────────┤
│                                                                      │
│  9 candidates for Senior Product Manager at Acme.                    │
│                                                                      │
│  ┌────────────────────────────────────────────────────────────────┐ │
│  │             [⇪ Open full presentation (9 candidates)]          │ │
│  └────────────────────────────────────────────────────────────────┘ │
│                                                                      │
│  ── High Potential (3 — top category, full detail) ────────────      │
│                                                                      │
│  ┌────────────────────────────────────────────────────────────────┐ │
│  │ [photo] Maya Chen · PM @ Stripe                                │ │
│  │ "Strong 0→1 signal — built Stripe Climate..."                  │ │
│  │ Top matches: ✓ 0→1 ownership   ✓ B2B SaaS PM                  │ │
│  │                                       [View this candidate →]  │ │
│  └────────────────────────────────────────────────────────────────┘ │
│  [... 2 more "High Potential" cards rendered in full ...]            │
│                                                                      │
│  ── Worth Considering (4) — condensed ────────────────────────       │
│  •  James Wu     · PM @ Linear   · "Strong eng instincts..." [→]    │
│  •  Lin Park     · PM @ Asana    · "Background in growth..."  [→]    │
│  •  Rosa Diaz    · PM @ Figma    · "Design fluency, ships..." [→]    │
│  •  Sam Becker   · PM @ Webflow  · "0→1 with ambiguous..."    [→]    │
│                                                                      │
│  ── Screened (2) — condensed ──────────────────────────────────      │
│  •  Priya Shah   · PM @ Notion   · "Lighter on enterprise..." [→]    │
│  •  Tom Hall     · PM @ Slack    · "Solid IC, leadership TBD"  [→]   │
│                                                                      │
│  ┌────────────────────────────────────────────────────────────────┐ │
│  │             [⇪ Open full presentation]                         │ │
│  └────────────────────────────────────────────────────────────────┘ │
│                                                                      │
│  Hiring for your own role? Post free on Helix → [Learn more]         │
└──────────────────────────────────────────────────────────────────────┘
```

**Key Elements:**
- **Top CTA above the fold** — first content block after one-line intro; protects against clipping
- **Top category in full** — recruiter's strongest picks render with full note + matches
- **Remaining categories condensed** — single line per candidate (name, company, truncated note, deep link)
- **Closing CTA** — repeats below the list

**States:**
- **All categories condensed (e.g. very long slates):** top CTA + condensed list only; cap at clipping limit (~25 lines)

---

### 9. Identity Capture (Combined — OTP and Self-Identify)

Shown to the HM on first visit, before any candidate data is rendered. Single screen layout — copy and primary action vary by access mode.

```
┌──────────────────────────────────────────────────────────────────────┐
│  helix.seekout.ai/p/8f4a-9c2d-bea1-3f7e                              │
├──────────────────────────────────────────────────────────────────────┤
│                                                                      │
│                          [Helix logo]                                │
│                                                                      │
│              Senior Product Manager — Acme                           │
│              Curated by Akshay Gupta at Acme                         │
│                                                                      │
│  ┌────────────────────────────────────────────────────────────────┐ │
│  │                                                                │ │
│  │   [STATE: EMAIL-SHARE / OTP]                                   │ │
│  │   Akshay shared this with priya@acme.com.                      │ │
│  │   Enter the 6-digit code we sent to that email to continue.    │ │
│  │                                                                │ │
│  │   Code:  [_][_][_]-[_][_][_]                                   │ │
│  │                                                                │ │
│  │                                                  [Continue →]  │ │
│  │                                                                │ │
│  │   Didn't receive it? [Resend code]                             │ │
│  │                                                                │ │
│  ├─ OR ───────────────────────────────────────────────────────────┤ │
│  │                                                                │ │
│  │   [STATE: PUBLIC LINK / SELF-IDENTIFY]                         │ │
│  │   Tell us who you are so Akshay can follow up on your picks.   │ │
│  │                                                                │ │
│  │   Name      [                                            ]     │ │
│  │   Email     [                                            ]     │ │
│  │                                                                │ │
│  │                                                  [Continue →]  │ │
│  │                                                                │ │
│  └────────────────────────────────────────────────────────────────┘ │
│                                                                      │
│  This page is private and will not appear in search results.         │
└──────────────────────────────────────────────────────────────────────┘
```

**Key Elements:**
- **Hero context** — role + recruiter ID before any auth, so HM knows the link is legit
- **OTP state** — pre-fills the recipient email (token bound), only code entry needed
- **Self-identify state** — name + email; minimum needed to attribute thumbs back to a known recipient
- **Footer reassurance** — page is unindexed (no SEO exposure)

**States:**
- **OTP — wrong code:** inline red error "Code doesn't match. Try again or resend."
- **OTP — expired code:** "Code expired. [Resend code]"
- **Self-identify — invalid email:** inline format error
- **Self-identify — declines / closes:** no candidate data shown; recipient can return any time
- **Already authenticated this session:** screen skipped, jump to Screen 11

---

### 10. (Reserved — see Screen 9)

Identity capture variants are combined into Screen 9 above per design call.

---

### 11. Branded Landing — Hero + Tabbed Candidate List

After identity capture. The HM's main hub: split layout with role context + decision counters on the left, and a recruiter-defined tab strip on the right that always splits Not Reviewed / Reviewed inside. Mirrors Spot Screen 5. Persistent thin signup banner.

```
┌──────────────────────────────────────────────────────────────────────┐
│  Helix  ·  Senior Product Manager — Acme         [Hi, Priya v]       │
├──────────────────────────────────────────────────────────────────────┤
│ ▍ Hiring for your own role? Post free on Helix →           [✕]      │
├────────────────────────────────────┬─────────────────────────────────┤
│                                    │ [#All] [High Pot.] [Screened]   │
│  Candidates for                    │ ─────────────────────────────── │
│                                    │                                 │
│   Senior Product                   │ Not Reviewed (2)                │
│   Manager                          │ ┌─────────────────────────────┐ │
│                                    │ │ (◯) Maya Chen               │ │
│  Acme · Remote (US)                │ ├─────────────────────────────┤ │
│  Curated by Akshay Gupta           │ │ (◯) Daniel Ortiz            │ │
│  Acme · 3 candidates               │ └─────────────────────────────┘ │
│                                    │                                 │
│  ┌─────┐ ┌─────┐ ┌─────────────┐   │ Reviewed (1)                    │
│  │👍 0 │ │👎 1 │ │— 2 to review│   │ ┌─────────────────────────────┐ │
│  └─────┘ └─────┘ └─────────────┘   │ │ (◯) Priya Shah  👎  💬      │ │
│                                    │ └─────────────────────────────┘ │
│  [Review Candidates →]             │                                 │
│  [Job Overview →]                  │                                 │
│                                    │                                 │
└────────────────────────────────────┴─────────────────────────────────┘
```

**Key Elements:**
- **Persistent signup banner** — thin top strip, dismissible per session (returns next session)
- **Left hero** — role, location, curator line ("Curated by [recruiter] · [company] · [N] candidates"); status pill row showing aggregate decisions; primary CTAs `[Review Candidates]` (deep-links to first unreviewed candidate detail) and `[Job Overview]` (opens Screen 16)
- **Status pills** — `👍 N` Interview, `👎 N` Pass, `— N to review` Pending. Working copy; design copy review needed for HM-facing tone (see Notes).
- **Right tab strip** — `[All]` always present + one tab per recruiter category (recruiter-defined in Builder Screen 2). Every tab — including category tabs — renders the same Not Reviewed / Reviewed split inside.
- **Candidate cards** — minimal: avatar `(◯)` + name only. Reviewed cards add a decision pill (`👍` / `👎`) and a `💬` icon if the HM left an optional reason. No title, no note preview, no scores on the card — those live in the detail view.
- **No inline Job Overview block** — moved entirely behind `[Job Overview]` CTA (Screen 16), per Spot pattern.

**States:**
- **First-time visit** — all candidates in Not Reviewed; Reviewed section hidden or shown empty with copy
- **Mid-review** — mix; status pills reflect running count
- **Fully reviewed** — Not Reviewed section shows "All caught up. Good work."; Reviewed section full
- **Per-tab counts** — each tab badge updates as decisions sync (e.g. `[All (3)]`, `[High Pot. (2)]`)
- **Live update** — if recruiter adds/removes candidates post-share, list updates with a small "Updated [date]" note in the Reviewed/Not Reviewed header (not shown — design call)

---

### 12. Candidate Detail — Default State

Tap a card → detail view. Three-region top (identity · recruiter note band · action rail) + two-column body (scorecards left · summary/experience/recordings right) with click-to-highlight evidence. Mirrors Spot Screen 6, with Helix's recruiter note pinned as a horizontal band per the live screenshot reference.

```
┌──────────────────────────────────────────────────────────────────────┐
│  ←  Senior Product Manager   1/3              [<]   [Next cand. >]   │
├──────────────────────────────────────────────────────────────────────┤
│ ┌────┐                                                ┌─────────────┐│
│ │ ◯  │ Maya Chen          ┌─────────────────────────┐ │👍 Interview ││
│ │phot│ PM @ Stripe·Climate│ "Strong 0→1 signal —    │ ├─────────────┤│
│ │    │ SF · 6y experience │  built Stripe Climate   │ │👎 Pass      ││
│ └────┘                    │  from scratch. In Sam,  │ └─────────────┘│
│                           │  talked about losing    │  Why? (opt.)   │
│                           │  eng trust as the       │  [           ] │
│                           │  failure mode..."       │                │
│                           │  — Akshay's note        │                │
│                           └─────────────────────────┘                │
├──────────────────────────────────────┬───────────────────────────────┤
│ Scorecards                           │ ┌───────────────────────────┐ │
│ Click a scorecard to highlight       │ │ Candidate Summary [in] →  │ │
│ the evidence on the right.           │ ├───────────────────────────┤ │
│                                      │ │ Senior PM | B2B SaaS PM | │ │
│ Must-haves                           │ │ 0→1 ownership | Eng       │ │
│ ┌──────────────────────────────────┐ │ │ partnership | 5y+ tenure  │ │
│ │ B2B SaaS PM            Strong ● │ │ └───────────────────────────┘ │
│ │ • Stripe (4y) building Climate  │ │                               │
│ │   from concept through GA       │ │ [#Experience]                 │
│ └──────────────────────────────────┘ │                               │
│ ┌──────────────────────────────────┐ │ ┌───────────────────────────┐ │
│ │ 0→1 Ownership          Strong ● │ │ │ Work Experience           │ │
│ │ • Built Stripe Climate from     │ │ ├───────────────────────────┤ │
│ │   scratch                       │ │ │ PM, Climate               │ │
│ └──────────────────────────────────┘ │ │ Stripe · 2022 – present   │ │
│ ┌──────────────────────────────────┐ │ │ Built Stripe Climate from │ │
│ │ Eng-adjacent fluency  Partial ◐ │ │ │ concept through GA. Ran   │ │
│ │ • Patterns for keeping eng trust│ │ │ eng-product weekly...     │ │
│ └──────────────────────────────────┘ │ │                           │ │
│                                      │ │ PM, Identity              │ │
│ Nice-to-haves                        │ │ Plaid · 2019 – 2022       │ │
│ ┌──────────────────────────────────┐ │ │ Built fraud-detection ML  │ │
│ │ ML/AI exposure         Strong ● │ │ │ pipeline...               │ │
│ │ • Shipped ML for fraud detect.  │ │ └───────────────────────────┘ │
│ └──────────────────────────────────┘ │                               │
│                                      │ ┌───────────────────────────┐ │
│                                      │ │ AI Interview Recordings   │ │
│                                      │ ├───────────────────────────┤ │
│                                      │ │ ▶ "Walk me through Stripe │ │
│                                      │ │   Climate..."  4:12  [📝] │ │
│                                      │ │ ▶ "Tell me about a time   │ │
│                                      │ │   eng trust..."  3:48 [📝]│ │
│                                      │ └───────────────────────────┘ │
├──────────────────────────────────────┴───────────────────────────────┤
│                          [← Previous]   [Next candidate →]           │
└──────────────────────────────────────────────────────────────────────┘
```

**Key Elements:**
- **Top bar** — back arrow, role title, slate position `1/3`, prev/next nav at right
- **Top region (3 parts side-by-side)** — identity block (left: photo + name + title @ company + location/years), **Akshay's note as a horizontal band** in the center (the recruiter's pinned context, per user-supplied screenshot — quoted styling, signed `— Akshay's note`), action rail stacked on the right (`👍 Interview` primary, `👎 Pass`, optional one-line `Why?` text input below)
- **Body left — Scorecards** — heading with click-to-highlight hint; rubric criterion cards grouped Must-haves / Nice-to-haves; each card has criterion title, evidence bullets, and a strength indicator (●/◐/○) when "Show rubric scores" is on
- **Body right — Candidate Summary + Experience + Recordings** — Candidate Summary card with skill / cert chips and `[in] Visit Profile →` LinkedIn link in card header; `[Experience]` tab pill (single tab for v1, future tabs reserved); Work Experience block with per-role title / company / dates / narrative bullets; AI Interview Recordings block (Helix-specific — ungated inline players with transcript indicator)
- **Bottom pager** — Previous / Next candidate; on the last candidate `[Next candidate →]` becomes `[Finish review →]`

**Interaction — click-to-highlight:** Clicking a scorecard card on the left
- Adds a highlight border + filled accent to the selected card
- Highlights matching evidence spans in the right pane (skill chips in Candidate Summary, narrative bullets in Work Experience, transcript snippets if available)
- Auto-scrolls the right pane to the first match if it's below the fold
- Clicking the same card again clears; clicking another swaps the highlight
- See **Screen 12 — Selected State** below for the visual treatment

**States:**
- **Default** — no scorecard selected; evidence un-highlighted (above)
- **Card selected** — see Screen 12 — Selected State
- **Already thumbed** — action rail shows current state + `[Change]` affordance: `👍 Interview · [Change]`
- **"Show rubric scores" OFF** — strength indicator (●/◐/○) hidden on every scorecard; evidence bullets remain
- **No recordings** — AI Interview Recordings block hidden
- **No recruiter note** — center band collapses; top region renders as 2 regions (identity + action rail)
- **Last candidate thumbed** — `[Next candidate →]` becomes `[Finish review →]` and routes to closure (Screen 13)

---

### 12b. Candidate Detail — Selected (Click-to-Highlight) State

Same screen as 12, after the HM clicks the "0→1 Ownership" scorecard. Selected card gains a heavy border + accent fill (rendered as `█...█`); matching evidence in the right pane is wrapped with `✦...✦` to indicate visual emphasis (highlight / underline / accent color — design-owned).

```
┌──────────────────────────────────────────────────────────────────────┐
│  ...top region unchanged...                                          │
├──────────────────────────────────────┬───────────────────────────────┤
│ Scorecards                           │ ┌───────────────────────────┐ │
│ Click a scorecard to highlight       │ │ Candidate Summary [in] →  │ │
│ the evidence on the right.           │ ├───────────────────────────┤ │
│                                      │ │ Senior PM | B2B SaaS PM | │ │
│ Must-haves                           │ │ ✦0→1 ownership✦ | Eng     │ │
│ ┌──────────────────────────────────┐ │ │ partnership | 5y+ tenure  │ │
│ │ B2B SaaS PM            Strong ● │ │ └───────────────────────────┘ │
│ │ • Stripe (4y) building Climate  │ │                               │
│ │   from concept through GA       │ │ [#Experience]                 │
│ └──────────────────────────────────┘ │                               │
│ ████████████████████████████████████ │ ┌───────────────────────────┐ │
│ █ 0→1 Ownership          Strong ● █ │ │ Work Experience           │ │
│ █ • Built Stripe Climate from    █ │ │ ├───────────────────────────┤ │
│ █   scratch                      █ │ │ │ PM, Climate               │ │
│ ████████████████████████████████████ │ │ Stripe · 2022 – present   │ │
│ ┌──────────────────────────────────┐ │ │ ✦Built Stripe Climate     │ │
│ │ Eng-adjacent fluency  Partial ◐ │ │ │  from concept through GA✦.│ │
│ │ • Patterns for keeping eng trust│ │ │ Ran eng-product weekly... │ │
│ └──────────────────────────────────┘ │ │                           │ │
│                                      │ │ PM, Identity              │ │
│ Nice-to-haves                        │ │ Plaid · 2019 – 2022       │ │
│ ┌──────────────────────────────────┐ │ │ Built fraud-detection ML  │ │
│ │ ML/AI exposure         Strong ● │ │ │ pipeline...               │ │
│ │ • Shipped ML for fraud detect.  │ │ └───────────────────────────┘ │
│ └──────────────────────────────────┘ │                               │
│                                      │ ┌───────────────────────────┐ │
│                                      │ │ AI Interview Recordings   │ │
│                                      │ ├───────────────────────────┤ │
│                                      │ │ ✦▶ "Walk me through       │ │
│                                      │ │  Stripe Climate..." 4:12✦ │ │
│                                      │ │ ▶ "Tell me about a time   │ │
│                                      │ │   eng trust..."  3:48 [📝]│ │
│                                      │ └───────────────────────────┘ │
└──────────────────────────────────────┴───────────────────────────────┘
```

**Key behaviors illustrated:**
- Selected scorecard uses heavy border + accent fill (`█`) — design-owned visual treatment
- Matched evidence appears in (1) Candidate Summary chips, (2) Work Experience narrative bullets, and (3) Recordings questions when transcript topics match — wrapped in `✦` for the wireframe
- Right pane auto-scrolls to first match if below the fold
- Other scorecards remain in default state (border + bullets, no fill)
- Clicking the selected card again, or another card, clears/swaps the highlight

---

### 13. Closure Screen

Auto-triggered on the last thumb. Acknowledgment + signup CTA pitching outbound capability.

```
┌──────────────────────────────────────────────────────────────────────┐
│  helix.seekout.ai/p/8f4a-9c2d-bea1-3f7e                              │
├──────────────────────────────────────────────────────────────────────┤
│                                                                      │
│                          ✓                                           │
│                                                                      │
│             Thanks, Priya — that's all 3.                            │
│        Akshay will follow up on your interview picks.                │
│                                                                      │
│       ┌─────┐ ┌─────┐ ┌─────────────┐                                │
│       │👍 2 │ │👎 1 │ │— 0 to review│                                │
│       └─────┘ └─────┘ └─────────────┘                                │
│            [Review your picks again]                                 │
│                                                                      │
│                                                                      │
│  ┌────────────────────────────────────────────────────────────────┐ │
│  │                                                                │ │
│  │   Hiring for your own role?                                    │ │
│  │                                                                │ │
│  │   Get AI-screened candidates from your own network and         │ │
│  │   inbound pipeline. Sam runs the intake, the AI screens,       │ │
│  │   you review the shortlist.                                    │ │
│  │                                                                │ │
│  │              [Post a role free →]                              │ │
│  │                                                                │ │
│  │   Already on Helix? [Sign in]                                  │ │
│  │                                                                │ │
│  └────────────────────────────────────────────────────────────────┘ │
│                                                                      │
│  Need anything? Reply to Akshay at akshay@acme.com                   │
└──────────────────────────────────────────────────────────────────────┘
```

**Key Elements:**
- **Acknowledgment** — names the recruiter; sets the expectation that recruiter follows up
- **Decision summary** — same status pill style as the landing hero (Screen 11), so the count chips read consistently across surfaces; `[Review your picks again]` deep-links back to Screen 15 (Resumed Session)
- **Signup CTA card** — the conversion moment; pitches outbound (network sourcing / post-your-role), NOT recordings
- **Recruiter contact** — reply-to surfaced for the HM's convenience

**States:**
- **All thumbs-down case:** identical screen, no editorialization. ("Thanks — Akshay will follow up..." with `👎 3` shown.) Recruiter sees the all-thumbs-down banner on the Job Landing Page (Screen 1) — not the HM.
- **Signup attribution:** [Post a role free →] carries `?utm_source=presentation&token=<token>`

---

### 14. Expired / Revoked Link

Friendly fallback when the link is no longer active.

```
┌──────────────────────────────────────────────────────────────────────┐
│  helix.seekout.ai/p/8f4a-9c2d-bea1-3f7e                              │
├──────────────────────────────────────────────────────────────────────┤
│                                                                      │
│                                                                      │
│                          ⏱                                           │
│                                                                      │
│              This presentation is no longer available.               │
│                                                                      │
│         Get in touch with Akshay Gupta at akshay@acme.com            │
│                  for an updated link or candidates.                  │
│                                                                      │
│                                                                      │
│  ┌────────────────────────────────────────────────────────────────┐ │
│  │  Hiring for your own role?                                     │ │
│  │  Post free on Helix → [Learn more]                             │ │
│  └────────────────────────────────────────────────────────────────┘ │
│                                                                      │
└──────────────────────────────────────────────────────────────────────┘
```

**Key Elements:**
- **No candidate data shown** — including no candidate names or counts (privacy)
- **Recruiter contact** — surfaced explicitly so the HM has a clear next step
- **Quiet signup teaser** — small, doesn't override the main message

**States:**
- **Expired (time-based):** copy reads "This presentation has expired."
- **Revoked by recruiter:** copy reads "This presentation is no longer available."
- **Token never existed / malformed:** generic 404 styling, same fallback

---

### 15. Resumed Session

Returning recipient is reauthenticated and lands on the same Branded Landing layout (Screen 11), with a "Welcome back" eyebrow and the tab the recipient was last viewing pre-selected. Reviewed and Not Reviewed sections show the recipient's prior decisions; tapping a Reviewed card reopens the Candidate Detail (Screen 12) and the action rail shows the existing pick with `[Change]`.

```
┌──────────────────────────────────────────────────────────────────────┐
│  Helix  ·  Senior Product Manager — Acme         [Hi, Priya v]       │
├──────────────────────────────────────────────────────────────────────┤
│  Welcome back, Priya. Open any candidate to change your pick —       │
│  Akshay sees only your most recent decision.                         │
├────────────────────────────────────┬─────────────────────────────────┤
│                                    │ [#All] [High Pot.] [Screened]   │
│  Candidates for                    │ ─────────────────────────────── │
│                                    │                                 │
│   Senior Product                   │ Not Reviewed (0)                │
│   Manager                          │ All caught up. Good work.       │
│                                    │                                 │
│  Acme · Remote (US)                │ Reviewed (3)                    │
│  Curated by Akshay Gupta           │ ┌─────────────────────────────┐ │
│  Acme · 3 candidates               │ │ (◯) Maya Chen     👍        │ │
│                                    │ ├─────────────────────────────┤ │
│  ┌─────┐ ┌─────┐ ┌─────────────┐   │ │ (◯) Daniel Ortiz  👍  💬    │ │
│  │👍 2 │ │👎 1 │ │— 0 to review│   │ ├─────────────────────────────┤ │
│  └─────┘ └─────┘ └─────────────┘   │ │ (◯) Priya Shah    👎        │ │
│                                    │ └─────────────────────────────┘ │
│  [Review your picks again]         │                                 │
│  [Job Overview →]                  │                                 │
│                                    │                                 │
└────────────────────────────────────┴─────────────────────────────────┘
```

**Key Elements:**
- **Welcome-back banner** — short, single line; reassures the HM that re-decisions are safe and Akshay sees only the latest pick
- **Same Screen 11 structure** — left hero with status pills (now reflecting actual decisions) and `[Review your picks again]` (deep-links into first reviewed card for re-review) plus `[Job Overview →]`
- **Tab strip and Reviewed/Not Reviewed split** — identical pattern to Screen 11; in this all-reviewed example Not Reviewed is empty with friendly copy, Reviewed lists every candidate with their decision pill
- **Editing a pick** — tap a Reviewed card → Screen 12 with the action rail in `[Change]` state; updated decision overwrites prior one and the slate's "changed [date]" indicator shows up on the recruiter's Job Landing Page

**States:**
- **Partial review** — both Not Reviewed and Reviewed sections populated; tab counts reflect current splits
- **All passed** — same UX as any other fully-reviewed slate (no editorialization)
- **New candidate added by recruiter post-share** — appears in Not Reviewed with a small "New" tag (design-owned)

---

### 16. Job Overview — Rubric Evaluation Criteria

Opens from the `[Job Overview]` CTA on Screen 11. Job-level view (no candidate context) showing the rubric criteria the recruiter is using and how the slate distributes against each one (rarity bars). Mirrors Spot Screen 7. v1 has a single tab — Funnel and People Insights are deferred (see Notes); no grayed v2 placeholders in the rail.

```
┌──────────────────────────────────────────────────────────────────────┐
│  ←  Senior Product Manager — Acme                                    │
├─────────────────────────┬────────────────────────────────────────────┤
│                         │  Evaluation criteria                       │
│ Job Overview            │  How the slate distributes against the     │
│                         │  rubric Akshay is using.                   │
│ # Rubric Evaluation     │                                            │
│   Criteria              │  Click a criterion to highlight its        │
│                         │  rarity bar on the right.                  │
│                         │                                            │
│                         │  Rarity legend:  ▓ Strong  ▒ Partial  ░ Low│
│                         │                                            │
│                         │  ── Must-haves ─────────────────────────── │
│                         │  ┌─────────────────────┐ ┌───────────────┐ │
│                         │  │ B2B SaaS PM         │─│ ▓▓▓▓▓▓ 60%    │ │
│                         │  │ Has the candidate   │ │ ▒▒▒▒  30%     │ │
│                         │  │ shipped a B2B SaaS  │ │ ░░    10%     │ │
│                         │  │ PM role in the      │ └───────────────┘ │
│                         │  │ last 4 years?       │                   │
│                         │  └─────────────────────┘                   │
│                         │  ┌─────────────────────┐ ┌───────────────┐ │
│                         │  │ 0→1 Ownership       │─│ ▓▓▓▓ 40%      │ │
│                         │  │ Has the candidate   │ │ ▒▒▒▒▒ 50%     │ │
│                         │  │ owned a product     │ │ ░ 10%         │ │
│                         │  │ from concept to GA? │ └───────────────┘ │
│                         │  └─────────────────────┘                   │
│                         │  ┌─────────────────────┐ ┌───────────────┐ │
│                         │  │ Eng-adjacent fluency│─│ ▓▓ 20%        │ │
│                         │  │ Can the candidate   │ │ ▒▒▒▒▒▒ 60%    │ │
│                         │  │ partner with eng on │ │ ░░ 20%        │ │
│                         │  │ technical tradeoffs?│ └───────────────┘ │
│                         │  └─────────────────────┘                   │
│                         │                                            │
│                         │  ── Nice-to-haves ──────────────────────── │
│                         │  ┌─────────────────────┐ ┌───────────────┐ │
│                         │  │ ML/AI exposure      │─│ ▓▓ 20%        │ │
│                         │  │ Has the candidate   │ │ ▒▒ 20%        │ │
│                         │  │ shipped ML/AI work? │ │ ░░░░░░ 60%    │ │
│                         │  └─────────────────────┘ └───────────────┘ │
│                         │                                            │
└─────────────────────────┴────────────────────────────────────────────┘
```

**Key Elements:**
- **Top bar** — back arrow + role title (no slate pagination — this is a job-level view)
- **Left rail** — `Job Overview` heading + single active tab `# Rubric Evaluation Criteria`. **No grayed placeholders for Funnel / People Insights** (Spot doesn't show grayed tabs; we follow suit).
- **Header** — section title + short blurb explaining rubric + click-to-pair hint
- **Rarity legend** — Strong / Partial / Low bands rendered with `▓`/`▒`/`░` shading (visual treatment is design-owned color choice)
- **Body** — left: criterion cards grouped by Must-haves / Nice-to-haves with title + full evaluation prompt; right: paired horizontal stacked rarity bars showing how the slate distributes against this criterion (Strong / Partial / Low percentages summing to 100%)
- **Click-to-pair interaction** — clicking a criterion card emphasizes its paired rarity bar (and vice versa). Default state shown above; selected state would render the pair with heavier border / accent color (analogous to Screen 12b's `█`/`✦` treatment, design-owned)

**States:**
- **Default** — no criterion selected
- **Selected** — paired card + bar emphasized
- **Insufficient data** — bar shows "insufficient data" placeholder if the slate is too small to compute distribution

**Open dependency (flagged in Notes):** rubric rarity score computation across the slate is a data dependency. Engineering needs to confirm we can compute Low / Partial / Strong distribution at v1 from the existing per-candidate rubric scores; otherwise downgrade to a simpler "X of Y candidates strong" summary.

---

### 11M. Branded Landing — Mobile

Stacked single-column treatment of Screen 11. Tab strip is horizontally scrollable when there are many recruiter categories.

```
┌────────────────────────┐
│ Helix · Senior PM —    │
│ Acme       [Hi, Priya v]│
├────────────────────────┤
│ ▍ Hiring for your      │
│   own role? Post free →│
│   on Helix       [✕]  │
├────────────────────────┤
│ Candidates for         │
│  Senior Product        │
│  Manager               │
│ Acme · Remote (US)     │
│ Curated by Akshay      │
│ Gupta · Acme           │
│ 3 candidates           │
│                        │
│ ┌─────┐┌─────┐┌──────┐ │
│ │👍 0 ││👎 1 ││— 2 to│ │
│ │     ││     ││review│ │
│ └─────┘└─────┘└──────┘ │
│                        │
│ [Review Candidates →]  │
│ [Job Overview →]       │
│                        │
│ [#All][High Pot][Scrnd]│
│ ◂ scroll for more cats │
│                        │
│ Not Reviewed (2)       │
│ ┌────────────────────┐ │
│ │ (◯) Maya Chen      │ │
│ ├────────────────────┤ │
│ │ (◯) Daniel Ortiz   │ │
│ └────────────────────┘ │
│                        │
│ Reviewed (1)           │
│ ┌────────────────────┐ │
│ │ (◯) Priya Shah  👎 │ │
│ │           💬       │ │
│ └────────────────────┘ │
└────────────────────────┘
```

**Mobile-specific behaviors:**
- Tab strip is horizontally scrollable; active tab indicator anchored left
- Status pill row + CTAs are full-width buttons
- Cards span full screen width with 16px gutter
- Sticky page header: role title + recipient menu remain at top on scroll

---

### 12M. Candidate Detail — Mobile

Stacked single-column with sticky bottom decision bar. Click-to-highlight becomes tap-to-reveal evidence inline beneath the scorecard (no left/right pairing on a single column).

```
┌────────────────────────┐
│ ←  Sr PM  1/3   <    > │
├────────────────────────┤
│       ┌──────┐         │
│       │  ◯   │         │
│       │ photo│         │
│       └──────┘         │
│      Maya Chen         │
│   PM @ Stripe·Climate  │
│   SF · 6y experience   │
│                        │
│ ┌────────────────────┐ │
│ │ "Strong 0→1 signal │ │
│ │  — built Stripe    │ │
│ │  Climate from      │ │
│ │  scratch..."       │ │
│ │  — Akshay's note   │ │
│ └────────────────────┘ │
│                        │
│ Scorecards             │
│ Tap a card to see      │
│ matching evidence.     │
│                        │
│ Must-haves             │
│ ┌────────────────────┐ │
│ │ B2B SaaS PM     ●  │ │
│ │ • Stripe (4y)...   │ │
│ └────────────────────┘ │
│ ┌────────────────────┐ │
│ │ 0→1 Ownership   ●  │ │
│ │ • Built Stripe...  │ │
│ │ ▾ Evidence:        │ │
│ │   ✦Built Stripe    │ │
│ │   Climate from     │ │
│ │   concept...✦      │ │
│ └────────────────────┘ │
│                        │
│ Candidate Summary      │
│      [in] Visit Profile│
│ Senior PM | B2B SaaS PM│
│ | 0→1 ownership | ...  │
│                        │
│ Work Experience        │
│ PM, Climate            │
│ Stripe · 2022 - present│
│ Built Stripe Climate.. │
│                        │
│ AI Interview Recordings│
│ ▶ "Walk me through..." │
│   4:12  [📝]            │
│ ▶ "Tell me about..."   │
│   3:48  [📝]            │
├────────────────────────┤  ← sticky bottom bar
│ [👍 Interview][👎 Pass]│
└────────────────────────┘
```

**Mobile-specific behaviors:**
- **Sticky bottom decision bar** — `[👍 Interview]` / `[👎 Pass]` always visible regardless of scroll position
- **Reason field** — opens as a half-sheet keyboard panel on tap of either decision (optional, dismissible)
- **Tap-to-reveal evidence** — tapping a scorecard expands an inline `▾ Evidence:` accordion below the card showing the matching spans wrapped in `✦`. No left/right pairing.
- **Identity block** is centered (photo + name stacked) for visual balance on narrow viewports
- **Recruiter note band** is full-width below identity, before the body

---

### 16M. Job Overview — Rubric Evaluation Criteria — Mobile

Stacked single-column. Each criterion card sits over its rarity bar (no left/right pairing). Tap to emphasize.

```
┌────────────────────────┐
│ ← Senior PM — Acme     │
├────────────────────────┤
│ Evaluation criteria    │
│ How the slate          │
│ distributes against    │
│ the rubric.            │
│                        │
│ Rarity:                │
│ ▓ Strong  ▒ Partial    │
│ ░ Low                  │
│                        │
│ ── Must-haves ──────── │
│ ┌────────────────────┐ │
│ │ B2B SaaS PM        │ │
│ │ Has the candidate  │ │
│ │ shipped B2B SaaS   │ │
│ │ in last 4 years?   │ │
│ └────────────────────┘ │
│ ┌────────────────────┐ │
│ │ ▓▓▓▓▓▓ 60%         │ │
│ │ ▒▒▒▒  30%          │ │
│ │ ░░    10%          │ │
│ └────────────────────┘ │
│                        │
│ ┌────────────────────┐ │
│ │ 0→1 Ownership      │ │
│ │ Has the candidate  │ │
│ │ owned product...   │ │
│ └────────────────────┘ │
│ ┌────────────────────┐ │
│ │ ▓▓▓▓ 40%           │ │
│ │ ▒▒▒▒▒ 50%          │ │
│ │ ░ 10%              │ │
│ └────────────────────┘ │
│                        │
│ ── Nice-to-haves ───── │
│ ┌────────────────────┐ │
│ │ ML/AI exposure     │ │
│ └────────────────────┘ │
│ ┌────────────────────┐ │
│ │ ▓▓ 20% ▒▒ 20%      │ │
│ │ ░░░░░░ 60%         │ │
│ └────────────────────┘ │
└────────────────────────┘
```

**Mobile-specific behaviors:**
- Criterion card stacked DIRECTLY over its rarity bar — they read as a vertical pair
- Tap a card or a bar to emphasize the pair (visual treatment design-owned)
- No persistent left rail; "Job Overview" context lives in the page title only

---

## User Flows

### Happy Path

```
RECRUITER                                         HM
─────────                                         ──
[Job Landing Page] (Screen 1)
       │
       ▼
[Press "Present to HM"]
       │
       ▼
[Builder] (Screen 2)
   ├─→ [Add Candidates modal] (Screen 3) ──┐
   │                                       │
   │←──────────────────────────────────────┘
   │
   ├─→ Edit notes / categories / settings
   │
   ├─→ [Preview] (Screen 4) ───┐
   │←──────────────────────────┘
   │
   ▼
[Send modal] (Screen 5)
       │
       ▼
[Send confirmation] (Screen 6) ─── triggers send ───────┐
                                                        │
                                                        ▼
                                            [Rich summary email arrives]
                                                  (Screen 7 or 8)
                                                        │
                                                        ▼
                                            [Open full presentation]
                                                        │
                                                        ▼
                                            [Identity capture] (Screen 9)
                                                        │
                                                        ▼
                                            [Branded Landing] (Screen 11)
                                              ├─→ [Job Overview] (Screen 16)
                                              │      └─→ back to Screen 11
                                              ▼
                                            [Candidate detail] (Screen 12)
                                                  ↻ thumbs per candidate
                                              ├─→ click scorecard → 12b
                                              │      (highlight evidence)
                                              ▼
                                            [Closure screen] (Screen 13)
                                                        │
       ┌──────── thumb sync (Model A) ──────────────────┘
       ▼
[Job Landing Page — post-share] (Screen 1)
   ├─→ Status pills updated per candidate
   ├─→ "First thumb arrived" notification (Notifications PRD)
   └─→ Recruiter judges + acts
```

### Edge Paths

**Bounced email**

```
[Send confirmation] (Screen 6) → email bounce → recruiter sees ⚠ on
[Job Landing Page] (Screen 1) — affected recipient + reason →
[Recruiter resends or removes recipient]
```

**Public link forwarded to a third party**

```
[Recipient A] (authenticated) ──forwards link──▶ [Recipient B]
                                                       │
                                                       ▼
                                     [Identity capture — self-identify]
                                              (Screen 9)
                                                       │
                                                       ▼
                              [Branded Landing] (Screen 11)
                              (recorded as a separate recipient)
```

**Email-share OTP forwarding (blocked path)**

```
[Recipient A] forwards link to [Recipient B]
                                       │
                                       ▼
                            [Identity capture — OTP] (Screen 9)
                                       │
                                       ▼
                            OTP sent only to A's email →
                            B can't pass OTP → no candidate data shown
```

**Candidate removed by recruiter mid-review**

```
[HM viewing Candidate Detail] (Screen 12)
                │  recruiter removes candidate
                ▼
   "This candidate is no longer in the presentation"
                │
                ▼
   Auto-return to [Branded Landing] (Screen 11)
```

**Link expired or revoked**

```
[HM clicks link] → [Identity capture] (skipped) →
[Expired/revoked fallback] (Screen 14)
```

**All-thumbs-down**

```
[HM closure screen] (Screen 13) — same UX, no editorialization
                                            │
              ┌─── thumb sync ──────────────┘
              ▼
[Job Landing Page] (Screen 1)
   ⚠ Banner: "All candidates passed. Refresh shortlist with Sam?"
   primary action: re-engage Sam (one-click)
```

**Recipient returns to a fully-reviewed slate**

```
[HM clicks link] → [Identity capture — auto-reauth] (Screen 9) →
[Resumed session] (Screen 15) →
   └─→ Tap a Reviewed card → [Candidate detail] (Screen 12)
       in [Change] state → updated thumb syncs;
       recruiter sees "Changed [date]" on Job Landing Page
```

**Mixed source presentation (Sourced + Inbound)**

```
[Add Candidates modal] (Screen 3) — source filter: All
                │
                ▼
   Footer note: "ⓘ Mixed source presentation —
                  make sure your context handles this for the HM"
                │
                ▼
[Builder] (Screen 2) — categories can mix sources
                │
                ▼
   Standard send + HM flow (PRD flags as supported but
   not core happy path; revisit in v2 per Open Question)
```

---

## Notes

### Resolved design questions
- **Resumed session (Design Q1) — RESOLVED 2026-04-15.** Collapsed from A/B variants (in-place edit vs. separate Reviewed section) into a single Screen 15. Decision driver: per-tab Reviewed / Not Reviewed split (user-confirmed for Screen 11) makes the segmented option correct everywhere; in-place `[Edit]` is a card-level affordance that still works inside the Reviewed section by tapping a card → Screen 12 in `[Change]` state. No design context lost — both old options informed the final pattern.

### Design discrepancies / things to watch
- **Per-recipient thumb display on Job Landing Page (Design Q5):** Screen 1 shows a simple count + emoji ("👍👎 2 HMs"). Density treatment for 3+ recipients is design-owned — current treatment will need revisit.
- **All-thumbs-down banner (Design Q2):** Screen 1 shows a banner-style treatment. Modal vs. inline vs. banner is design-owned.
- **Email-share vs. Public link mode UX in Builder (Design Q3):** Screen 5 shows a radio with descriptive copy. Default is Email-share. Confirm hierarchy and copy with design.
- **Identity capture form on Public link (Design Q4):** Screen 9 shows a basic name + email form. PRD flags "what to do if recipient declines" — current treatment is "no candidate data shown, can return any time." Confirm fallback behavior.
- **Regenerate UX (Design Q7):** Screen 2 shows a [Regenerate] button beside the AI tag. Confirm-modal on regenerate-after-edit is mentioned in States but not drawn — design-owned.
- **Hero status pill copy (Screen 11):** `Interview` / `Pass` / `to review` is working placeholder copy. HM-facing tone may want softer terms (e.g. "Selected" / "Passed" / "Yet to review"). Design copy review needed.
- **Click-to-highlight visual treatment (Screen 12b, Screen 16):** wireframe uses `█` borders and `✦` markers as placeholders for the selected/highlighted state. Actual color, weight, and animation are design-owned.

### Open items flagged in wireframes
- **Job Overview v1 = Rubric Evaluation Criteria only.** Funnel and People Insights are deferred to v2 (recruiter telemetry + pool diversity data not yet wired). **No grayed-out v2 placeholders in the UI** — Spot doesn't show grayed tabs and we don't either.
- **Click-to-highlight on Candidate Detail (Screen 12 / 12b) and Job Overview (Screen 16):** in scope for v1 per PRD. Risk: evidence-mapping accuracy. Fallback is the static layout (no highlight) if accuracy is below the QA bar — covered in PRD Risks.
- **Rubric rarity score computation** (Screen 16): data dependency. Engineering needs to confirm we can compute Strong / Partial / Low distribution at v1 from the existing per-candidate rubric scores, or downgrade to a simpler "X of Y candidates strong" summary. Tracked in PRD Open Questions.
- **Mobile variants** (Screens 11M, 12M, 16M) — sticky bottom decision bar (12M) and tap-to-reveal evidence accordion (12M) are the two non-trivial mobile patterns; both are design-owned in detail.
- **Live update indicator** (Screen 11) when recruiter edits a sent presentation — not drawn; design call.
- **Drag-to-reorder mobile behavior** (Screen 2) — Open Question 16 in `open-questions.md`; not drawn.
- **Bounced email UX on Job Landing Page row** (Screen 1) — flagged but not drawn; tooltip approach assumed.

### Suggested next steps
- `/design-review` once Figma exists — compare design output back to these wireframes + PRD for completeness, especially Screen 12's three-region top, Screen 12b's highlight treatment, and Screen 16's rarity bars.
- `/ux-expert` for usability heuristics on the HM flow (identity capture friction, click-to-highlight discoverability, sticky decision bar on mobile, closure CTA).
- `/screen-diagrams` to promote the Helix-side patterns (Builder, Branded Landing, Candidate Detail, Job Overview) into `context/products/helix/screen-diagrams.md` once we ship v1.
