# Wireframes: Persona Reframing (v2)

**Product:** Helix (SeekOut.ai)
**Date:** 2026-04-01
**Related:** [Proposal v2](./proposal-memo-v2.md)

---

## 1. Side Navigation — Two Surfaces

```
┌──────────────┐
│  ■ Hiring    │
│  ○ Applying  │
│ ──────────── │
│  ⚙ Settings  │
└──────────────┘
```

No persona switcher. Two surfaces only.

---

## 2. Onboarding — Persona Selection

### Option A: Two-step selection

Surface choice first, then role within Hiring.

**Step 1 — Choose your surface:**

```
┌──────────────────────────────────────────────────────────────────────────────┐
│  seekout>                                                                    │
│                                                                              │
│                        What brings you to SeekOut?                           │
│                                                                              │
│        ┌─────────────────────────────┐  ┌─────────────────────────────┐     │
│        │                             │  │                             │     │
│        │        I'm Hiring           │  │     I'm Looking for        │     │
│        │                             │  │        a Job               │     │
│        │  Find and evaluate          │  │                             │     │
│        │  qualified candidates       │  │  Build your portfolio      │     │
│        │  with AI                    │  │  and apply with AI         │     │
│        │                             │  │  coaching                  │     │
│        │                             │  │                             │     │
│        └─────────────────────────────┘  └─────────────────────────────┘     │
│                                                                              │
└──────────────────────────────────────────────────────────────────────────────┘
```

**Step 2 — (Hiring only) Choose your role:**

```
┌──────────────────────────────────────────────────────────────────────────────┐
│  seekout>                                                                    │
│                                                                              │
│                     What's your role in hiring?                              │
│                                                                              │
│        ┌─────────────────────────────┐  ┌─────────────────────────────┐     │
│        │                             │  │                             │     │
│        │     Hiring Manager          │  │       Recruiter             │     │
│        │                             │  │                             │     │
│        │  I'm hiring for my team.    │  │  I recruit for my           │     │
│        │  Create AI-powered job      │  │  company. Import jobs       │     │
│        │  postings and find          │  │  from your ATS, run AI     │     │
│        │  qualified candidates.      │  │  evaluations, and curate   │     │
│        │                             │  │  top talent for hiring     │     │
│        │                             │  │  managers.                  │     │
│        │                             │  │                             │     │
│        └─────────────────────────────┘  └─────────────────────────────┘     │
│                                                                              │
│              You can always change this later in Settings.                   │
│                                                                              │
└──────────────────────────────────────────────────────────────────────────────┘
```

### Option B: Nested cards

One screen. Hiring is a larger card with two sub-options; Applying is a standalone card.

```
┌──────────────────────────────────────────────────────────────────────────────┐
│  seekout>                                                                    │
│                                                                              │
│                        What brings you to SeekOut?                           │
│                                                                              │
│   ┌──────────────────────────────────────────────┐  ┌────────────────────┐  │
│   │                                              │  │                    │  │
│   │   I'm Hiring                                 │  │  I'm Looking for  │  │
│   │                                              │  │     a Job         │  │
│   │   ┌───────────────────┐ ┌──────────────────┐ │  │                    │  │
│   │   │                   │ │                  │ │  │  Build your        │  │
│   │   │  Hiring Manager   │ │   Recruiter      │ │  │  portfolio and    │  │
│   │   │                   │ │                  │ │  │  apply with AI    │  │
│   │   │  I'm hiring for   │ │  I recruit for   │ │  │  coaching         │  │
│   │   │  my team.         │ │  my company.     │ │  │                    │  │
│   │   │                   │ │                  │ │  │                    │  │
│   │   │  Create job       │ │  Import from     │ │  │                    │  │
│   │   │  postings and     │ │  ATS, run AI     │ │  │                    │  │
│   │   │  find candidates  │ │  evaluations,    │ │  │                    │  │
│   │   │                   │ │  curate talent   │ │  │                    │  │
│   │   │                   │ │                  │ │  │                    │  │
│   │   └───────────────────┘ └──────────────────┘ │  │                    │  │
│   │                                              │  │                    │  │
│   └──────────────────────────────────────────────┘  └────────────────────┘  │
│                                                                              │
│              You can always change this later in Settings.                   │
│                                                                              │
└──────────────────────────────────────────────────────────────────────────────┘
```

---

## 3. Hiring Surface — Hiring Manager Experience

```
┌──────────────┬───────────────────────────────────────────────────────────────┐
│              │                                                               │
│  ■ Hiring    │  My Jobs                                        [+ New Job]  │
│              │                                                               │
│  ○ Applying  │  ┌───────────────────────────────────────────────────────┐   │
│              │  │  Senior Product Designer                              │   │
│ ──────────── │  │  Bellevue, WA · Hybrid                               │   │
│              │  │  12 candidates · 3 unreviewed                        │   │
│  ⚙ Settings  │  ├───────────────────────────────────────────────────────┤   │
│              │  │  Staff Engineer — AI/ML                               │   │
│              │  │  Seattle, WA · Remote                                 │   │
│              │  │  8 candidates · 5 unreviewed                         │   │
│              │  └───────────────────────────────────────────────────────┘   │
│              │                                                               │
└──────────────┴───────────────────────────────────────────────────────────────┘

- Jobs created via job wizard + Sam voice conversation
- Scoped to jobs the HM owns
- Actions: share, review candidates, invite collaborators
```

---

## 4. Hiring Surface — Recruiter Experience

```
┌──────────────┬───────────────────────────────────────────────────────────────┐
│              │                                                               │
│  ■ Hiring    │  Jobs                                    [+ Import from ATS] │
│              │                                                               │
│  ○ Applying  │  ┌───────────────────────────────────────────────────────┐   │
│              │  │  Recruiting Coordinator          ATS: Greenhouse      │   │
│ ──────────── │  │  San Francisco, CA · Onsite                           │   │
│              │  │  34 candidates · 12 unreviewed                       │   │
│  ⚙ Settings  │  ├───────────────────────────────────────────────────────┤   │
│              │  │  Data Analyst                    ATS: Greenhouse      │   │
│              │  │  New York, NY · Hybrid                                │   │
│              │  │  21 candidates · 8 unreviewed                        │   │
│              │  ├───────────────────────────────────────────────────────┤   │
│              │  │  Frontend Developer              ATS: Greenhouse      │   │
│              │  │  Bellevue, WA · Hybrid                               │   │
│              │  │  47 candidates · 19 unreviewed                       │   │
│              │  └───────────────────────────────────────────────────────┘   │
│              │                                                               │
└──────────────┴───────────────────────────────────────────────────────────────┘

- Jobs imported from ATS
- Org-wide scope (all connected ATS jobs)
- Actions: run AI evaluation, curate shortlists, send to HM for review
```

---

## 5. Settings — Role Switcher

```
┌─────────────────────────────────────────────────────────────┐
│  Settings > Account                                         │
│                                                             │
│  Hiring Role                                                │
│  ┌─────────────────────────────────────────────────────┐   │
│  │  ○ Hiring Manager                                    │   │
│  │    See and manage jobs you create                    │   │
│  │                                                      │   │
│  │  ● Recruiter                                         │   │
│  │    Access ATS-imported jobs across your organization │   │
│  └─────────────────────────────────────────────────────┘   │
│                                                             │
│  [Save]                                                     │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```
