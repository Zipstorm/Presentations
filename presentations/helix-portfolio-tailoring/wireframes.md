# Wireframes: Helix Portfolio Tailoring

**Project**: Helix - Portfolio Tailoring
**Date**: 2026-03-24
**Scope**: Full project — onboarding, portfolio editing, share flow, post-share

**Reference**: [Screen Diagrams](../../context/products/helix/screen-diagrams.md) for existing Helix layout patterns
**Note**: Layout is desktop-first. Mobile/narrow viewport behavior deferred to separate scope.

---

## Conventions

| Symbol | Meaning |
|--------|---------|
| `[Button]` | Clickable button or CTA |
| `(● Option)` | Selected radio / active option |
| `(○ Option)` | Unselected radio / inactive option |
| `[x] Item` | Completed checkbox |
| `[ ] Item` | Unchecked checkbox |
| `■` | Active nav item |
| `[✕]` | Close button |
| `← →` | Navigation arrows |
| `┌ ┐ └ ┘ │ ─` | Box-drawing characters |
| `...` | Truncated / repeating content |

---

## Section 1: Onboarding (Screens 1–4)

### Screen 1: Value Prop Screen

Entry point from signup. Introduces the unified portfolio concept.

```
┌──────────────────────────────────────────────────────────────────────┐
│  seekout>                                                            │
│                                                                      │
│                                                                      │
│                    Your career, one portfolio.                        │
│                                                                      │
│           ┌────────────────────────────────────────────┐             │
│           │                                            │             │
│           │         (illustration / graphic)           │             │
│           │    AI-powered resume · GitHub · Links ·    │             │
│           │    Video · Tailored for every job          │             │
│           │                                            │             │
│           └────────────────────────────────────────────┘             │
│                                                                      │
│           ✦ AI resume builder — fix, improve, tailor                 │
│           ✦ One portfolio, tailored for every opportunity            │
│           ✦ Track who views your shared links                        │
│           ✦ Share anywhere — LinkedIn, email, direct                 │
│                                                                      │
│                                                                      │
│                       [Get Started →]                                │
│                                                                      │
│                                                                      │
└──────────────────────────────────────────────────────────────────────┘
```

**Key Elements:**
- Value messaging: AI resume builder, unified portfolio, tracking
- Single CTA: [Get Started →] → navigates to Screen 2

---

### Screen 2: Wizard — Add Details

Single screen combining resume upload, diagnosis, template selection, GitHub, portfolio URL, and links.

#### State 2A: Empty (No Resume Yet)

```
┌──────────────────────────────────────────────────────────────────────────┐
│                                                                          │
│  Create your AI-forward profile                                          │
│                                                                          │
│       (Resume Details)─────(Links & resources)─────(Try an edit)  [✕]   │
│        ● active              ○                      ○                    │
│                                                                          │
│  ┌──────────────────────────────────────────────────────────────────────┐ │
│  │                          📋                                         │ │
│  │          First, let us know the basics of your background           │ │
│  │          We use this to create your modern profile                  │ │
│  └──────────────────────────────────────────────────────────────────────┘ │
│                                                                          │
│  Resume                                                                  │
│  ┌──────────────────────────────────────────────────────────────────────┐ │
│  │                                                                      │ │
│  │              📄 Click to upload or drag your resume                  │ │
│  │                           PDF only                                   │ │
│  │                                                                      │ │
│  └──────────────────────────────────────────────────────────────────────┘ │
│                                                                          │
│  Github Profile                    Add Portfolio                         │
│  ┌────────────────────────────┐    ┌────────────────────────────────┐    │
│  │                            │    │                                │    │
│  └────────────────────────────┘    └────────────────────────────────┘    │
│                                                                          │
│  Additional Links                                                        │
│  ┌──────────────────────────────────────────────────────────────────────┐ │
│  │ You can paste multiple links here                                    │ │
│  └──────────────────────────────────────────────────────────────────────┘ │
│                                                                          │
│  ───────────────────────────────────────────────────────────────────────  │
│                                                         [Next →]         │
│                                                                          │
└──────────────────────────────────────────────────────────────────────────┘
```

#### State 2B: Resume Uploaded, Analyzing

```
┌──────────────────────────────────────────────────────────────────────────┐
│                                                                          │
│  Create your AI-forward profile                                          │
│                                                                          │
│       (Resume Details)─────(Links & resources)─────(Try an edit)  [✕]   │
│        ● active              ○                      ○                    │
│                                                                          │
│  Resume                                                                  │
│  ┌────────────────────────────┐                                          │
│  │ Sarah_Resume.pdf  ✓       │                                          │
│  └────────────────────────────┘                                          │
│                                                                          │
│  ┌──────────────────────────────────────────────────────────────────────┐ │
│  │ ⚡ Analyzing your resume...                             Helix AI    │ │
│  │                                                                      │ │
│  │      ● Extracting content                                ✓          │ │
│  │      ● Checking ATS compatibility                        ◌          │ │
│  │      ● Identifying improvement opportunities             ◌          │ │
│  │                                                                      │ │
│  └──────────────────────────────────────────────────────────────────────┘ │
│                                                                          │
│  Github Profile                    Add Portfolio                         │
│  ┌────────────────────────────┐    ┌────────────────────────────────┐    │
│  │                            │    │                                │    │
│  └────────────────────────────┘    └────────────────────────────────┘    │
│                                                                          │
│  ───────────────────────────────────────────────────────────────────────  │
│                                                         [Next →]         │
│                                                                          │
└──────────────────────────────────────────────────────────────────────────┘
```

**Note**: [Next →] enabled during analysis — prospect can continue without waiting.

#### State 2C: Diagnosis Ready + Template Selection

```
┌──────────────────────────────────────────────────────────────────────────┐
│                                                                          │
│  Create your AI-forward profile                                          │
│                                                                          │
│       (Resume Details)─────(Links & resources)─────(Try an edit)  [✕]   │
│        ● active              ○                      ○                    │
│                                                                          │
│  Resume                                                                  │
│  ┌────────────────────────────┐                                          │
│  │ Sarah_Resume.pdf  ✓       │                                          │
│  └────────────────────────────┘                                          │
│                                                                          │
│  ┌──────────────────────────────────────────────────────────────────────┐ │
│  │ ⚡ Resume Analysis                                      Helix AI    │ │
│  │                                                                      │ │
│  │  Your resume has a few areas we can optimize:                        │ │
│  │                                                                      │ │
│  │  ⚠ ATS compatibility — formatting may cause parsing issues          │ │
│  │  ⚠ Inconsistent date formatting across 3 roles                     │ │
│  │  💡 3 bullet points could be strengthened with measurable impact    │ │
│  │                                                                      │ │
│  │  Choose a template and we'll create an optimized, editable          │ │
│  │  version of your resume:                                             │ │
│  │                                                                      │ │
│  │   ┌────────────┐   ┌────────────┐   ┌────────────┐                  │ │
│  │   │ ┌────────┐ │   │ ┌────────┐ │   │ ┌────────┐ │                  │ │
│  │   │ │ Modern │ │   │ │Classic │ │   │ │Minimal │ │                  │ │
│  │   │ │ ────── │ │   │ │ ────── │ │   │ │        │ │                  │ │
│  │   │ │ ▪ ▪ ▪  │ │   │ │ ▪ ▪ ▪  │ │   │ │ ▪ ▪ ▪  │ │                  │ │
│  │   │ │ ▪ ▪ ▪  │ │   │ │ ▪ ▪ ▪  │ │   │ │ ▪ ▪ ▪  │ │                  │ │
│  │   │ └────────┘ │   │ └────────┘ │   │ └────────┘ │                  │ │
│  │   │  ● Modern  │   │  ○ Classic │   │  ○ Minimal │                  │ │
│  │   └────────────┘   └────────────┘   └────────────┘                  │ │
│  │                                                                      │ │
│  │  ℹ We'll fix formatting issues automatically. Content suggestions   │ │
│  │    will be available for you to review after your profile is ready.  │ │
│  └──────────────────────────────────────────────────────────────────────┘ │
│                                                                          │
│  Github Profile                    Add Portfolio                         │
│  ┌────────────────────────────┐    ┌────────────────────────────────┐    │
│  │ github.com/sarahc          │    │ portfolio.dev/sarahc           │    │
│  └────────────────────────────┘    └────────────────────────────────┘    │
│                                                                          │
│  ───────────────────────────────────────────────────────────────────────  │
│                                                         [Next →]         │
│                                                                          │
└──────────────────────────────────────────────────────────────────────────┘
```

**Key Elements:**
- Diagnosis card: 2-3 specific issues found
- Template selection: 3 templates, Modern pre-selected
- Template thumbnails are clickable (entire card, not just radio)
- Conversion runs in background after [Next →]

**States:**
- 2A: Empty — no resume uploaded
- 2B: Uploaded, analyzing — progress indicators
- 2C: Analysis complete — diagnosis + template selection visible

---

### Screen 3: Wizard — Try an Edit (UPDATED)

Split view: resume preview + NL editor with starter prompts. **Optional step** — both [Skip →] and [Create Portfolio →] visible.

#### State 3A: Loading (Conversion Not Ready)

```
┌──────────────────────────────────────────────────────────────────────────┐
│                                                                          │
│  Create your AI-forward profile                                          │
│                                                                          │
│       (Resume Details)─────(Links & resources)─────(Try an edit)  [✕]   │
│        ✓                    ✓                      ● active              │
│                                                                          │
│  ┌──────────────────────────────┬───────────────────────────────────────┐ │
│  │                              │                                       │ │
│  │                              │  ✨ Try an edit                        │ │
│  │                              │                                       │ │
│  │                              │  Once your resume is ready, you can   │ │
│  │    ⚡ Preparing your         │  try editing it with AI. Here are     │ │
│  │    resume for editing...     │  some suggestions based on your       │ │
│  │                              │  resume analysis:                     │ │
│  │    ● Applying template       │                                       │ │
│  │    ● Fixing ATS formatting   │  ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░     │ │
│  │    ● Typesetting content     │  ░░░░░░░░░░░░░░░░░░░░░░░░           │ │
│  │                              │  ░░░░░░░░░░░░░░░░░░░░░░░░░░░        │ │
│  │    This usually takes a      │                                       │ │
│  │    few seconds.              │                                       │ │
│  │                              │                                       │ │
│  │                              │                                       │ │
│  │                              │  ┌─────────────────────────────────┐  │ │
│  │                              │  │ Type your edit...               │  │ │
│  │                              │  └─────────────────────────────────┘  │ │
│  └──────────────────────────────┴───────────────────────────────────────┘ │
│                                                                          │
│  ───────────────────────────────────────────────────────────────────────  │
│                                     [Skip →]    [Create Portfolio →]     │
│                                                                          │
└──────────────────────────────────────────────────────────────────────────┘
```

#### State 3B: Ready (Conversion Complete)

```
┌──────────────────────────────────────────────────────────────────────────┐
│                                                                          │
│  Create your AI-forward profile                                          │
│                                                                          │
│       (Resume Details)─────(Links & resources)─────(Try an edit)  [✕]   │
│        ✓                    ✓                      ● active              │
│                                                                          │
│  ┌──────────────────────────────┬───────────────────────────────────────┐ │
│  │                              │                                       │ │
│  │                              │  ✨ Try an edit                        │ │
│  │   Sarah Chen                 │                                       │ │
│  │   Product Manager | Seattle  │  We found a few things to improve.    │ │
│  │   sarah@email.com            │  Try one of these edits:              │ │
│  │                              │                                       │ │
│  │   ── Experience ──────────   │  [Make my summary more specific       │ │
│  │                              │   to product management            ]  │ │
│  │   Product Manager            │                                       │ │
│  │   Acme Corp  2022-Present    │  [Add metrics to my role at Google ]  │ │
│  │   • Led product strategy     │                                       │ │
│  │     for enterprise platform  │  [Strengthen my education section  ]  │ │
│  │   • Managed team of 8        │                                       │ │
│  │                              │  Or type your own:                    │ │
│  │   Software Engineer          │                                       │ │
│  │   Google  2019-2022          │  ┌─────────────────────────────────┐  │ │
│  │   • Built data pipeline      │  │ Type your edit...               │  │ │
│  │   • Improved latency by 40%  │  └─────────────────────────────────┘  │ │
│  │                              │                                       │ │
│  │   ── Skills ──────────────   │                                       │ │
│  │   Strategy  SQL  Analytics   │  This step is optional — you can      │ │
│  │                              │  always edit from your portfolio.      │ │
│  └──────────────────────────────┴───────────────────────────────────────┘ │
│                                                                          │
│  ───────────────────────────────────────────────────────────────────────  │
│                                     [Skip →]    [Create Portfolio →]     │
│                                                                          │
└──────────────────────────────────────────────────────────────────────────┘
```

#### State 3C: After Edit

```
┌──────────────────────────────────────────────────────────────────────────┐
│                                                                          │
│  Create your AI-forward profile                                          │
│                                                                          │
│       (Resume Details)─────(Links & resources)─────(Try an edit)  [✕]   │
│        ✓                    ✓                      ● active              │
│                                                                          │
│  ┌──────────────────────────────┬───────────────────────────────────────┐ │
│  │                              │                                       │ │
│  │                              │  ✨ Try an edit                        │ │
│  │   Sarah Chen                 │                                       │ │
│  │   Product Manager | Seattle  │  ┌─────────────────────────────────┐  │ │
│  │   sarah@email.com            │  │ 👤 Make my summary more        │  │ │
│  │                              │  │ specific to product management  │  │ │
│  │ ┌─ UPDATED ───────────────┐  │  └─────────────────────────────────┘  │ │
│  │ │ Product leader with 5+  │  │                                       │ │
│  │ │ years driving strategy  │  │  ┌─────────────────────────────────┐  │ │
│  │ │ and execution across    │  │  │ ✅ Updated your summary to     │  │ │
│  │ │ enterprise B2B...       │  │  │ emphasize product leadership,  │  │ │
│  │ │ └───────────────────────┘  │  │ cross-functional collaboration │  │ │
│  │                              │  │ and measurable impact.         │  │ │
│  │   ── Experience ──────────   │  └─────────────────────────────────┘  │ │
│  │                              │                                       │ │
│  │   Product Manager            │  Try another:                         │ │
│  │   Acme Corp  2022-Present    │  [Add metrics to my role at Google ]  │ │
│  │   • Led product strategy     │                                       │ │
│  │     for enterprise platform  │  ┌─────────────────────────────────┐  │ │
│  │   • Managed team of 8        │  │ Type your edit...               │  │ │
│  │                              │  └─────────────────────────────────┘  │ │
│  └──────────────────────────────┴───────────────────────────────────────┘ │
│                                                                          │
│  ───────────────────────────────────────────────────────────────────────  │
│                                     [Skip →]    [Create Portfolio →]     │
│                                                                          │
└──────────────────────────────────────────────────────────────────────────┘
```

**Key Elements:**
- Split view: left = Typst-rendered resume preview, right = NL editor
- Starter prompts based on diagnosis (clickable suggestion chips)
- **[Skip →]** creates portfolio from conversion only (no edits)
- **[Create Portfolio →]** creates portfolio with edits applied
- Both buttons always visible — step is optional

**States:**
- 3A: Loading — conversion not yet complete
- 3B: Ready — resume preview + starter prompts
- 3C: After edit — updated preview, change summary in chat, more suggestions

---

### Screen 4: Portfolio View (UPDATED — major changes)

The main screen after onboarding. **Always-on AI chat panel** on the right. Content area narrowed to make room.

#### State 4A: Default (Edit Resume Active, Suggestions Shown)

```
┌─────────────┬────────────────────────────────────┬──────────────────────────────┐
│             │                                    │                              │
│ seekout>    │  My Portfolio       [Share][⬇ DL]  │  [Edit Resume] [Career Coach]│
│             │                                    │                              │
│ Jobseekers  │  Overview · Resume · Github ·      │  ✨ Suggestions               │
│             │  Links · Video                     │                              │
│ ■ Portfolio │  ──────────────────────────────     │  Based on your resume:       │
│ ○ Apps      │                                    │                              │
│             │  ┌──────────────────────────────┐   │  [Strengthen your summary    │
│ ─────────── │  │                              │   │   for PM roles            ]  │
│ ⚙ Settings  │  │   Sarah Chen                 │   │                              │
│             │  │   Product Manager | Seattle   │   │  [Add metrics to your       │
│ ─────────── │  │   sarah@email.com             │   │   Google role             ]  │
│             │  │                              │   │                              │
│ Tasks       │  │   ── Summary ────────────    │   │  [Rewrite education section  │
│             │  │   Product leader with 5+     │   │   to highlight relevance  ]  │
│ [ ] Edit    │  │   years driving strategy     │   │                              │
│     resume  │  │   and execution...           │   │                              │
│ [ ] Share   │  │                              │   │                              │
│     portfolio│  │   ── Experience ──────────   │   │                              │
│ [ ] Try AI  │  │                              │   │                              │
│     Career  │  │   Product Manager            │   │                              │
│     Coach   │  │   Acme Corp  2022-Present    │   │                              │
│ [ ] Tailor  │  │   • Led product strategy...  │   │                              │
│     for a   │  │   • Managed team of 8...     │   │                              │
│     job     │  │                              │   │                              │
│             │  │   Software Engineer           │   │                              │
│ ─────────── │  │   Google  2019-2022          │   │                              │
│             │  │   • Built data pipeline...   │   │                              │
│ (avatar)    │  │                              │   │  ┌────────────────────────┐  │
│ Sarah C.    │  └──────────────────────────────┘   │  │ Type a message...      │  │
│             │                                    │  └────────────────────────┘  │
└─────────────┴────────────────────────────────────┴──────────────────────────────┘
```

**Sidebar elements:**
- Portfolio (active), Apps — main nav
- Settings
- Task checklist:
  - [ ] Edit resume
  - [ ] Share portfolio — creates an application (tailored or as-is)
  - [ ] Try AI Career Coach
  - [ ] Tailor for a job — nudge to try the tailored share path specifically

**Chat panel elements:**
- **[Edit Resume]** button (active/default mode)
- **[Career Coach]** button (opens separate Coach UI — separate team's feature)
- Tab-aware contextual suggestions (change based on active tab)
- Chat input at bottom

#### State 4B: Github Tab Active (Tab-Aware Suggestions)

```
                                    │                                    │                              │
                                    │  Overview · Resume · [Github] ·   │  ✨ Suggestions               │
                                    │  Links · Video                    │                              │
                                    │  ──────────────────────────────    │  Based on your GitHub:       │
                                    │                                    │                              │
                                    │  GitHub Profile                    │  [Link your top             │
                                    │  ┌──────────────────────────────┐  │   repositories            ]  │
                                    │  │ github.com/sarahc             │  │                              │
                                    │  │                              │  │  [Add descriptions to       │
                                    │  │ (no repositories linked yet) │  │   pinned repos            ]  │
                                    │  │                              │  │                              │
                                    │  │        [Link Repos]          │  │  [Highlight your open       │
                                    │  │                              │  │   source contributions   ]  │
                                    │  └──────────────────────────────┘  │                              │
```

#### State 4C: Links Tab Active (Tab-Aware Suggestions)

```
                                    │                                    │                              │
                                    │  Overview · Resume · Github ·     │  ✨ Suggestions               │
                                    │  [Links] · Video                  │                              │
                                    │  ──────────────────────────────    │  Based on your links:        │
                                    │                                    │                              │
                                    │  Portfolio Links                   │  [Add your portfolio         │
                                    │  ┌──────────────────────────────┐  │   website                 ]  │
                                    │  │ portfolio.dev/sarahc          │  │                              │
                                    │  │                              │  │  [Include a case study     │
                                    │  │ [+ Add Link]                 │  │   or writing sample      ]  │
                                    │  └──────────────────────────────┘  │                              │
```

#### State 4D: Video Tab Active (Tab-Aware Suggestions)

```
                                    │                                    │                              │
                                    │  Overview · Resume · Github ·     │  ✨ Suggestions               │
                                    │  Links · [Video]                  │                              │
                                    │  ──────────────────────────────    │  Intro videos help you       │
                                    │                                    │  stand out:                   │
                                    │  Intro Video                       │                              │
                                    │  ┌──────────────────────────────┐  │  [Record a 60-second        │
                                    │  │                              │  │   intro video             ]  │
                                    │  │    (no video recorded yet)   │  │                              │
                                    │  │                              │  │  [Get script suggestions   │
                                    │  │   [Record Video] [Upload]   │  │   for your intro          ]  │
                                    │  │                              │  │                              │
                                    │  └──────────────────────────────┘  │                              │
```

#### State 4E: After Edits (Suggestions Updated)

```
┌─────────────┬────────────────────────────────────┬──────────────────────────────┐
│             │                                    │                              │
│ seekout>    │  My Portfolio       [Share][⬇ DL]  │  [Edit Resume] [Career Coach]│
│             │                                    │                              │
│ Jobseekers  │  Overview · [Resume] · Github ·    │  ┌────────────────────────┐  │
│             │  Links · Video                     │  │ 👤 Strengthen my       │  │
│ ■ Portfolio │  ──────────────────────────────     │  │ summary for PM roles   │  │
│ ○ Apps      │                                    │  └────────────────────────┘  │
│             │  ┌──────────────────────────────┐   │                              │
│ ─────────── │  │                              │   │  ┌────────────────────────┐  │
│ ⚙ Settings  │  │   Sarah Chen                 │   │  │ ✅ Updated your       │  │
│             │  │   Product Manager | Seattle   │   │  │ summary to emphasize  │  │
│ ─────────── │  │                              │   │  │ product leadership     │  │
│             │  │ ┌─ UPDATED ───────────────┐  │   │  │ and cross-functional   │  │
│ Tasks       │  │ │ Product leader with 5+  │  │   │  │ collaboration.        │  │
│             │  │ │ years driving strategy  │  │   │  └────────────────────────┘  │
│ [x] Edit    │  │ │ and execution across    │  │   │                              │
│     resume  │  │ │ enterprise B2B...       │  │   │  More suggestions:           │
│ [ ] Share   │  │ └────────────────────────┘  │   │                              │
│     portfolio│  │                              │   │  [Add metrics to your       │
│ [ ] Try AI  │  │   ── Experience ──────────   │   │   Google role             ]  │
│     Career  │  │                              │   │                              │
│     Coach   │  │   Product Manager            │   │  [Highlight leadership      │
│ [ ] Tailor  │  │   Acme Corp  2022-Present    │   │   across your experience ]  │
│     for a   │  │   • Led product strategy...  │   │                              │
│     job     │  │   • Managed team of 8...     │   │                              │
│             │  │                              │   │                              │
│ ─────────── │  │   ...                        │   │  ┌────────────────────────┐  │
│ (avatar)    │  │                              │   │  │ Type a message...      │  │
│ Sarah C.    │  └──────────────────────────────┘   │  └────────────────────────┘  │
└─────────────┴────────────────────────────────────┴──────────────────────────────┘
```

#### State 4F: LLM Asking Clarification

```
                                                    │                              │
                                                    │  ┌────────────────────────┐  │
                                                    │  │ 👤 Add my AWS         │  │
                                                    │  │ certification          │  │
                                                    │  └────────────────────────┘  │
                                                    │                              │
                                                    │  ┌────────────────────────┐  │
                                                    │  │ 🟡 Which AWS          │  │
                                                    │  │ certification do you   │  │
                                                    │  │ have? And when did     │  │
                                                    │  │ you earn it?           │  │
                                                    │  │                        │  │
                                                    │  │ Common ones:           │  │
                                                    │  │ • Solutions Architect  │  │
                                                    │  │ • Developer Associate  │  │
                                                    │  │ • Cloud Practitioner   │  │
                                                    │  └────────────────────────┘  │
                                                    │                              │
                                                    │  ┌────────────────────────┐  │
                                                    │  │ Type a message...      │  │
                                                    │  └────────────────────────┘  │
```

Resume preview unchanged — no edit applied yet. Waiting for prospect response.

#### State 4G: LLM Error (Malformed Typst)

```
                                                    │                              │
                                                    │  ┌────────────────────────┐  │
                                                    │  │ 👤 Reorganize into    │  │
                                                    │  │ two columns            │  │
                                                    │  └────────────────────────┘  │
                                                    │                              │
                                                    │  ┌────────────────────────┐  │
                                                    │  │ ⚠ That change          │  │
                                                    │  │ couldn't be applied.   │  │
                                                    │  │ Your resume has been   │  │
                                                    │  │ restored to the last   │  │
                                                    │  │ working version.       │  │
                                                    │  │                        │  │
                                                    │  │ Try rephrasing your    │  │
                                                    │  │ request, or try a      │  │
                                                    │  │ different change.      │  │
                                                    │  │                        │  │
                                                    │  │         [Retry]        │  │
                                                    │  └────────────────────────┘  │
                                                    │                              │
                                                    │  ┌────────────────────────┐  │
                                                    │  │ Type a message...      │  │
                                                    │  └────────────────────────┘  │
```

Resume reverts to last working version. Error message + [Retry] in chat.

#### State 4H: Chat-Initiated Share Prompt

```
                                                    │                              │
                                                    │  ✅ Updated your summary.    │
                                                    │                              │
                                                    │  ┌────────────────────────┐  │
                                                    │  │ Your portfolio is       │  │
                                                    │  │ looking great! Ready    │  │
                                                    │  │ to share it?            │  │
                                                    │  │                        │  │
                                                    │  │    [Share it →]        │  │
                                                    │  └────────────────────────┘  │
                                                    │                              │
                                                    │  ┌────────────────────────┐  │
                                                    │  │ Type a message...      │  │
                                                    │  └────────────────────────┘  │
```

Clicking [Share it →] opens the Share Decision wizard (Screen 5).

#### State 4I: All Tasks Complete (Kudos State)

```
┌─────────────┬────────────────────────────────────┬──────────────────────────────┐
│             │                                    │                              │
│ seekout>    │  My Portfolio       [Share][⬇ DL]  │  [Edit Resume] [Career Coach]│
│             │                                    │                              │
│ Jobseekers  │  Overview · [Resume] · Github ·    │  You're all set! Keep your   │
│             │  Links · Video                     │  portfolio updated and share  │
│ ■ Portfolio │  ──────────────────────────────     │  it for new opportunities.   │
│ ○ Apps      │                                    │                              │
│             │  ┌──────────────────────────────┐   │  [Improve my summary      ]  │
│ ─────────── │  │                              │   │                              │
│ ⚙ Settings  │  │   Sarah Chen                 │   │  [Tailor for another job  ]  │
│             │  │   Product Manager | Seattle   │   │                              │
│ ─────────── │  │   sarah@email.com             │   │                              │
│             │  │                              │   │                              │
│  🚀 Kudos   │  │   ── Summary ────────────    │   │                              │
│  you are    │  │   Product leader with 5+     │   │                              │
│  all set!   │  │   years driving strategy...  │   │                              │
│             │  │                              │   │                              │
│ [x] Edit    │  │   ── Experience ──────────   │   │                              │
│     resume  │  │   ...                        │   │                              │
│ [x] Share   │  │                              │   │                              │
│     portfolio│  └──────────────────────────────┘   │                              │
│ [x] Try AI  │                                    │                              │
│     Career  │                                    │                              │
│     Coach   │                                    │                              │
│ [x] Tailor  │                                    │  ┌────────────────────────┐  │
│     for a   │  Track your shared links           │  │ Type a message...      │  │
│     job     │  in the dashboard →                │  └────────────────────────┘  │
│             │                                    │                              │
└─────────────┴────────────────────────────────────┴──────────────────────────────┘
```

**Key Elements (Screen 4):**
- Always-on chat panel replaces button-triggered editing
- [Edit Resume] is default mode; [Career Coach] opens separate Coach UI
- Tab-aware suggestions change based on active tab
- Chat can handle portfolio extras ("Add my photo", "Update GitHub link")
- Share prompts surface based on portfolio completeness
- Direct edit affordances (upload buttons, link fields) remain on each tab
- Portfolio content narrowed to make room for chat panel
- No [Edit with AI] button needed — chat panel replaces it

**States:**
- 4A: Default — Edit Resume active, resume tab, suggestions shown
- 4B–4D: Tab-aware — suggestions change per active tab (Github, Links, Video)
- 4E: After edits — updated preview, change summary, new suggestions
- 4F: Clarification — LLM asks question, resume unchanged
- 4G: Error — malformed Typst, revert + error message + [Retry]
- 4H: Share prompt — chat suggests sharing when appropriate
- 4I: All tasks complete — kudos state

---

## Section 2: Share Flow (Screens 5–9)

### Screen 5: Share Decision Modal (UPDATED)

Modal triggered by [Share] button in portfolio header or chat panel suggestion.

```
┌──────────────────────────────────────────────────────────────────────────┐
│                                                                          │
│                        Share Your Portfolio                               │
│                                                                          │
│  ┌──────────────────────────────────────────────────────────────────────┐ │
│  │                                                                      │ │
│  │     Do you have a specific job in mind?                              │ │
│  │                                                                      │ │
│  │     We can tailor your portfolio for the role — this increases       │ │
│  │     your chances by 35%.                                             │ │
│  │                                                                      │ │
│  │  ┌──────────────────────────────────────────────────────────────┐    │ │
│  │  │                                                              │    │ │
│  │  │  ✦ Tailored for a specific job                              │    │ │
│  │  │                                                              │    │ │
│  │  │  We'll adjust your summary, reorder experience, and          │    │ │
│  │  │  highlight matching skills — never fabricate.                │    │ │
│  │  │                                                              │    │ │
│  │  │                    [Yes, tailor for a job]                    │    │ │
│  │  │                                                              │    │ │
│  │  └──────────────────────────────────────────────────────────────┘    │ │
│  │                                                                      │ │
│  │  ┌──────────────────────────────────────────────────────────────┐    │ │
│  │  │                                                              │    │ │
│  │  │  Share as-is                                                 │    │ │
│  │  │                                                              │    │ │
│  │  │  Share your current portfolio without tailoring.             │    │ │
│  │  │                                                              │    │ │
│  │  │                       [No, share as-is]                      │    │ │
│  │  │                                                              │    │ │
│  │  └──────────────────────────────────────────────────────────────┘    │ │
│  │                                                                      │ │
│  └──────────────────────────────────────────────────────────────────────┘ │
│                                                                          │
│                              [✕ Cancel]                                  │
│                                                                          │
└──────────────────────────────────────────────────────────────────────────┘
```

**Key Elements:**
- Updated copy: "increases your chances by 35%"
- Two clear options: [Yes, tailor for a job] / [No, share as-is]
- Brief explanation of what tailoring does (adjust, reorder, highlight — never fabricate)
- **Two entry points**: [Share] button in header, or chat panel suggestion (e.g., "Ready to share?")

---

### Screen 6: JD Input

Shown after choosing "Yes, tailor for a job" from decision modal.

```
┌──────────────────────────────────────────────────────────────────────────┐
│                                                                          │
│                        Tailor for a Job                                   │
│                                                                          │
│  Step 1 of 3: Add the job details                                        │
│                                                                          │
│  ┌──────────────────────────────────────────────────────────────────────┐ │
│  │                                                                      │ │
│  │  Paste the job posting URL                                           │ │
│  │  ┌──────────────────────────────────────────────────────────────┐    │ │
│  │  │ https://                                                     │    │ │
│  │  └──────────────────────────────────────────────────────────────┘    │ │
│  │                                                                      │ │
│  │  ──────────── or ────────────                                        │ │
│  │                                                                      │ │
│  │  Paste the job description                                           │ │
│  │  ┌──────────────────────────────────────────────────────────────┐    │ │
│  │  │                                                              │    │ │
│  │  │  Paste the full job description here...                     │    │ │
│  │  │                                                              │    │ │
│  │  │                                                              │    │ │
│  │  │                                                              │    │ │
│  │  └──────────────────────────────────────────────────────────────┘    │ │
│  │                                                                      │ │
│  └──────────────────────────────────────────────────────────────────────┘ │
│                                                                          │
│                        [← Back]    [Tailor My Portfolio →]               │
│                                                                          │
└──────────────────────────────────────────────────────────────────────────┘
```

**Key Elements:**
- URL field for job posting
- Fallback: text area for pasting full JD (if URL scrape fails or prospect prefers)
- [← Back] returns to decision modal
- [Tailor My Portfolio →] starts tailoring pipeline

---

### Screen 7: Tailoring Progress (UPDATED — absorbs education content)

Shows pipeline steps with **inline tailoring education** during natural wait time.

```
┌──────────────────────────────────────────────────────────────────────────┐
│                                                                          │
│                        Tailoring Your Portfolio                           │
│                                                                          │
│  ┌──────────────────────────────────────────────────────────────────────┐ │
│  │                                                                      │ │
│  │  ✓ Analyzing job description                                        │ │
│  │  ◉ Evaluating fit...                                                │ │
│  │  ○ Tailoring your portfolio                                         │ │
│  │  ○ Preview                                                          │ │
│  │                                                                      │ │
│  ├──────────────────────────────────────────────────────────────────────┤ │
│  │                                                                      │ │
│  │   What happens during tailoring?                                     │ │
│  │                                                                      │ │
│  │   We analyze the job requirements and adjust your portfolio          │ │
│  │   to put your best foot forward:                                     │ │
│  │                                                                      │ │
│  │   ✦ Reorder experience to lead with what matters most               │ │
│  │   ✦ Rewrite bullet points to mirror the job's language              │ │
│  │   ✦ Emphasize matching skills and qualifications                    │ │
│  │   ✦ Adjust your summary for the specific role                       │ │
│  │                                                                      │ │
│  │   We never fabricate — everything comes from your real experience.   │ │
│  │                                                                      │ │
│  │   ┌──────────────────────────────────────────────────────────────┐   │ │
│  │   │  Before               →          After                      │   │ │
│  │   │                                                              │   │ │
│  │   │  "Managed team"       →  "Led cross-functional team of 8    │   │ │
│  │   │                           engineers and designers to ship    │   │ │
│  │   │                           enterprise features quarterly"    │   │ │
│  │   └──────────────────────────────────────────────────────────────┘   │ │
│  │                                                                      │ │
│  │   Tailored portfolios get 35% more interviews.                       │ │
│  │                                                                      │ │
│  └──────────────────────────────────────────────────────────────────────┘ │
│                                                                          │
└──────────────────────────────────────────────────────────────────────────┘
```

**Key Elements:**
- Step indicators: Analyzing JD → Evaluating fit → Tailoring → Preview
- **Education content inline** — fills natural wait time (not a separate blocking screen)
- Explains what changes: reorder, rewrite, emphasize — never fabricate
- Before/after preview snippet showing real improvement
- "35% more interviews" stat reinforces value
- Auto-advances to Screen 8 when tailoring completes

**States:**
- Each step indicator progresses: ✓ (done), ◉ (in progress), ○ (pending)
- Education content visible throughout (not changing per step)

---

### Screen 8: Tailored Preview + Share

Read-only preview of tailored result with change summary and sharing options.

```
┌──────────────────────────────────────────────────────────────────────────┐
│                                                                          │
│                        Tailored Preview                                   │
│                                                                          │
│  Google — Senior Product Manager                                         │
│                                                                          │
│  ┌──────────────────────────┬───────────────────────────────────────────┐ │
│  │                          │                                           │ │
│  │   Sarah Chen             │  Changes made:                            │ │
│  │   Product Manager        │                                           │ │
│  │                          │  ✦ Summary rewritten to emphasize        │ │
│  │ ┌─ TAILORED ──────────┐ │    product strategy and data-driven      │ │
│  │ │ Product strategist   │ │    decision making                       │ │
│  │ │ with 5+ years        │ │                                           │ │
│  │ │ driving data-driven  │ │  ✦ Experience reordered — Google role    │ │
│  │ │ product decisions... │ │    moved to top (most relevant)          │ │
│  │ └────────────────────┘ │ │                                           │ │
│  │                          │  ✦ 4 bullet points rewritten to          │ │
│  │   ── Experience ───────  │    mirror JD language                     │ │
│  │                          │                                           │ │
│  │   Software Engineer      │  ✦ Skills reordered — SQL, Analytics,    │ │
│  │   Google  2019-2022      │    Strategy moved to front               │ │
│  │   • Built data pipeline  │                                           │ │
│  │     serving 10M daily    │                                           │ │
│  │     queries...           │                                           │ │
│  │                          │                                           │ │
│  │   Product Manager        │                                           │ │
│  │   Acme Corp  2022-Pres   │                                           │ │
│  │   • Led product strategy │                                           │ │
│  │     for enterprise...    │                                           │ │
│  │                          │                                           │ │
│  └──────────────────────────┴───────────────────────────────────────────┘ │
│                                                                          │
│  Share via:                                                              │
│  ┌──────────────────────────────────────────────────────────────────────┐ │
│  │  [● LinkedIn]  [○ X]  [○ Facebook]  [○ Reddit]  [○ Copy Link]      │ │
│  │                                                                      │ │
│  │  ┌──────────────────────────────────────────────────────────────┐    │ │
│  │  │ Hi, I'm excited to share my portfolio tailored for the      │    │ │
│  │  │ Senior PM role at Google. I bring 5+ years of product       │    │ │
│  │  │ strategy experience with a data-driven approach...          │    │ │
│  │  └──────────────────────────────────────────────────────────────┘    │ │
│  │                                                                      │ │
│  │              [↻ Regenerate Message]           [Share →]              │ │
│  └──────────────────────────────────────────────────────────────────────┘ │
│                                                                          │
│                        [← Back to Portfolio]                             │
│                                                                          │
└──────────────────────────────────────────────────────────────────────────┘
```

**Key Elements:**
- Read-only tailored resume preview (left)
- Change summary (right) — what was adjusted and why
- Platform selector: LinkedIn (default), X, Facebook, Reddit, Copy Link
- AI-generated sharing message with template variables
- [↻ Regenerate Message] to get a new message
- [Share →] creates application (immutable snapshot) and shares
- Prospect previews but doesn't manually edit tailored output (V1)

---

### Screen 9: As-Is Share Modal

Shown after choosing "No, share as-is" from decision modal.

```
┌──────────────────────────────────────────────────────────────────────────┐
│                                                                          │
│                        Share Your Portfolio                               │
│                                                                          │
│  ┌──────────────────────────────────────────────────────────────────────┐ │
│  │                                                                      │ │
│  │  Name this share (for your tracking)                                 │ │
│  │  ┌──────────────────────────────────────────────────────────────┐    │ │
│  │  │ e.g., "Networking — General" or "Recruiter Outreach"         │    │ │
│  │  └──────────────────────────────────────────────────────────────┘    │ │
│  │                                                                      │ │
│  └──────────────────────────────────────────────────────────────────────┘ │
│                                                                          │
│  Share via:                                                              │
│  ┌──────────────────────────────────────────────────────────────────────┐ │
│  │  [● LinkedIn]  [○ X]  [○ Facebook]  [○ Reddit]  [○ Copy Link]      │ │
│  │                                                                      │ │
│  │  ┌──────────────────────────────────────────────────────────────┐    │ │
│  │  │ Check out my portfolio — I'd love to connect about product  │    │ │
│  │  │ management opportunities. Here's a look at my experience    │    │ │
│  │  │ and projects...                                              │    │ │
│  │  └──────────────────────────────────────────────────────────────┘    │ │
│  │                                                                      │ │
│  │              [↻ Regenerate Message]           [Share →]              │ │
│  └──────────────────────────────────────────────────────────────────────┘ │
│                                                                          │
│                        [← Back to Portfolio]                             │
│                                                                          │
└──────────────────────────────────────────────────────────────────────────┘
```

**Key Elements:**
- Name input for tracking (user-provided)
- Same platform selector and AI message as tailored share
- Creates as-is application (immutable snapshot of current portfolio)

---

## Section 3: Post-Share (Screens 10–11)

### Screen 10: Share Confirmation Modal

Shown immediately after sharing (both tailored and as-is paths).

```
┌──────────────────────────────────────────────────────────────────────────┐
│                                                                          │
│  ┌──────────────────────────────────────────────────────────────────────┐ │
│  │                                                                      │ │
│  │                        🎉                                            │ │
│  │                                                                      │ │
│  │               Congratulations!                                       │ │
│  │                                                                      │ │
│  │        Your portfolio has been shared.                               │ │
│  │                                                                      │ │
│  │   ┌──────────────────────────────────────────────────────────────┐   │ │
│  │   │  Google — Senior Product Manager          Tailored          │   │ │
│  │   │  seekout.ai/p/sarahc/google-sr-pm                           │   │ │
│  │   │                                            [Copy Link]      │   │ │
│  │   └──────────────────────────────────────────────────────────────┘   │ │
│  │                                                                      │ │
│  │   The link will be updated with data upon visitor arrival.           │ │
│  │   Track views, clicks, and engagement in your dashboard.            │ │
│  │                                                                      │ │
│  │                                                                      │ │
│  │              [View in Applications →]    [Back to Portfolio]         │ │
│  │                                                                      │ │
│  └──────────────────────────────────────────────────────────────────────┘ │
│                                                                          │
└──────────────────────────────────────────────────────────────────────────┘
```

**Key Elements:**
- Celebration moment
- Shows application name, tracking link, tailored/as-is badge
- [Copy Link] to copy tracking URL
- Note about live tracking data
- [View in Applications →] navigates to Applications page (Screen 11)
- [Back to Portfolio] returns to Portfolio View (Screen 4)
- Design consideration: auto-redirect to Applications page after a few seconds

---

### Screen 11: Applications Page

List of all shared portfolios with metadata and activity tracking.

```
┌─────────────┬────────────────────────────────────────────────────────────────┐
│             │                                                                │
│ seekout>    │  Applications                                                  │
│             │                                                                │
│ Jobseekers  │  ┌────────────────────────────────────────────────────────────┐ │
│             │  │                                                            │ │
│ ○ Portfolio │  │  Google — Sr. Product Manager                              │ │
│ ■ Apps      │  │  Tailored · Mar 24 · 12 views · Recruiter: Jane D.        │ │
│             │  │  seekout.ai/p/sarahc/google-sr-pm         [Copy] [View]   │ │
│ ─────────── │  │                                                            │ │
│ ⚙ Settings  │  ├────────────────────────────────────────────────────────────┤ │
│             │  │                                                            │ │
│             │  │  Meta — Product Designer                                   │ │
│             │  │  Tailored · Mar 20 · 3 views · Direct share               │ │
│             │  │  seekout.ai/p/sarahc/meta-pd              [Copy] [View]   │ │
│             │  │                                                            │ │
│             │  ├────────────────────────────────────────────────────────────┤ │
│             │  │                                                            │ │
│             │  │  Networking — General                                      │ │
│             │  │  As-is · Mar 18 · 7 views · Direct share                  │ │
│             │  │  seekout.ai/p/sarahc/networking            [Copy] [View]   │ │
│             │  │                                                            │ │
│             │  └────────────────────────────────────────────────────────────┘ │
│             │                                                                │
│ (avatar)    │                                                                │
│ Sarah C.    │                                                                │
└─────────────┴────────────────────────────────────────────────────────────────┘
```

#### Expanded Application Detail (Activity Feed)

```
│  ┌────────────────────────────────────────────────────────────────────────┐ │
│  │                                                                        │ │
│  │  Google — Sr. Product Manager                              [Collapse] │ │
│  │  Tailored · Mar 24 · 12 views · Recruiter: Jane D.                   │ │
│  │  seekout.ai/p/sarahc/google-sr-pm                    [Copy] [View]   │ │
│  │                                                                        │ │
│  │  Activity                                                              │ │
│  │  ──────────────────────────────────────────────────────                │ │
│  │  Mar 24  3:42pm  👁 Viewed portfolio          San Francisco, CA       │ │
│  │  Mar 24  3:44pm  📄 Downloaded resume         San Francisco, CA       │ │
│  │  Mar 24  3:45pm  🎬 Played intro video (45s)  San Francisco, CA       │ │
│  │  Mar 25  9:15am  👁 Viewed portfolio          New York, NY            │ │
│  │  Mar 25  9:17am  🔗 Clicked GitHub link       New York, NY            │ │
│  │  ...                                                                   │ │
│  │                                                                        │ │
│  └────────────────────────────────────────────────────────────────────────┘ │
```

**Key Elements:**
- List of application cards: name, tailored/as-is badge, date, view count, recruiter link
- Each card has [Copy] (tracking link) and [View] (preview frozen portfolio)
- Expandable to show chronological activity feed (views, downloads, video plays, clicks)
- Activity includes timestamps and locations
- Sidebar: Portfolio, Apps (active), Settings

---

## User Flows

### Flow 1: Happy Path (Onboarding → First Tailored Share)

```
Website → Signup
    │
    ▼
(1) Value Prop Screen
    │
    ▼ [Get Started →]
(2) Wizard — Add Details
    │  Upload resume → Diagnosis + Template selection
    │
    ▼ [Next →]
(3) Wizard — Try an Edit [optional]
    │
    ├── Prospect makes an edit → [Create Portfolio →]
    │
    ▼
(4) Portfolio View (chat panel shows suggestions)
    │
    ▼ [Share]
(5) Share Decision Modal → [Yes, tailor for a job]
    │
    ▼
(6) JD Input → [Tailor My Portfolio →]
    │
    ▼
(7) Tailoring Progress (with inline education content)
    │
    ▼ (auto-advances)
(8) Tailored Preview + Share → [Share →]
    │
    ▼
(10) Share Confirmation → [View in Applications →]
    │
    ▼
(11) Applications Page
```

### Flow 2: Skip Edit Path

```
(2) Wizard — Add Details → [Next →]
    │
    ▼
(3) Wizard — Try an Edit
    │
    ▼ [Skip →]
(4) Portfolio View
    (chat panel shows diagnosis-based suggestions immediately)
```

### Flow 3: As-Is Share

```
(4) Portfolio View → [Share]
    │
    ▼
(5) Share Decision Modal → [No, share as-is]
    │
    ▼
(9) As-Is Share Modal → [Share →]
    │
    ▼
(10) Share Confirmation → [View in Applications →]
    │
    ▼
(11) Applications Page
```

### Flow 4: Post-Onboarding Edit Loop

```
(4) Portfolio View
    │
    ├── Click suggestion chip or type edit in chat panel
    │
    ▼
LLM decides:
    │
    ├── update_resume → Typst recompiles → portfolio updates
    │   → new tab-aware suggestions appear
    │   → State 4E
    │
    ├── ask_clarification → question shown in chat
    │   → prospect responds → loop back to LLM
    │   → State 4F
    │
    └── On error:
        → malformed Typst → revert to last working version
        → error message + [Retry] in chat
        → State 4G
```

### Flow 5: AI Career Coach Entry

```
(4) Portfolio View → click [Career Coach] in chat panel header
    │
    ▼
Career Coach UI opens (separate team's feature)
```

### Flow 6: Chat-Initiated Share

```
(4) Portfolio View
    │
    ├── Chat panel suggests "Your portfolio is looking great! [Share it →]"
    │   (based on portfolio completeness / checklist state)
    │
    ▼ [Share it →]
(5) Share Decision Modal
    │
    ├── [Yes, tailor for a job] → Flow 1 from step 6
    └── [No, share as-is] → Flow 3 from step 9
```

---

## Screen Inventory

| # | Screen | Section | States | Key Changes |
|---|--------|---------|--------|-------------|
| 1 | Value Prop | Onboarding | 1 | New screen |
| 2 | Wizard — Add Details | Onboarding | 3 (empty, analyzing, diagnosis) | From screen-diagrams §3 |
| 3 | Wizard — Try an Edit | Onboarding | 3 (loading, ready, after-edit) | **UPDATED**: optional with [Skip →] |
| 4 | Portfolio View | Onboarding/Editing | 9 (default, 3 tabs, edits, clarification, error, share prompt, kudos) | **UPDATED**: always-on chat panel, tab-aware |
| 5 | Share Decision Modal | Share Flow | 1 | **UPDATED**: "35%" copy, two entry points |
| 6 | JD Input | Share Flow | 1 | From screen-diagrams §4 |
| 7 | Tailoring Progress | Share Flow | 1 (steps animate) | **UPDATED**: inline education content |
| 8 | Tailored Preview + Share | Share Flow | 1 | From screen-diagrams §4 |
| 9 | As-Is Share Modal | Share Flow | 1 | From screen-diagrams §4 |
| 10 | Share Confirmation | Post-Share | 1 | New screen |
| 11 | Applications Page | Post-Share | 2 (list, expanded detail) | From solution design §4 |
