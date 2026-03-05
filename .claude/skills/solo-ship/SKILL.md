---
name: solo-ship
description: "Autonomous project engine -- from idea to deployed test environment. User provides the idea, Claude runs the entire lifecycle: research, PRD, tech selection, development, testing, deployment. Minimal human intervention required."
metadata:
  author: bruce
  version: "1.0"
  last-updated: "2026-03-05"
  origin: "Distilled from Caliber project (PM assessment tool) full lifecycle with Claude Code"
---

# Solo Ship -- Autonomous Project Engine

> One idea in, deployed product out.
> User's only job: describe the idea. Claude handles everything else.

## Activation

When the user says any of the following, activate this skill and BEGIN AUTONOMOUS EXECUTION:

- "I want to build..." / "I have an idea for..." / "Help me make..."
- "New project: [description]"
- "solo-ship: [description]"
- Any description of a product idea with the intent to build it

## Core Principles

1. **Act, don't ask.** Make decisions and move forward. Document decisions in CLAUDE.md so the user can review asynchronously. Never block on "which color do you prefer" type questions.

2. **Opinionated defaults.** When multiple valid options exist, pick one and go. The user can override later. Shipping beats deliberating.

3. **Self-validating.** After each phase, run automated checks (type check, build, lint). Fix issues yourself. Only surface blockers that genuinely require user input (API keys, paid service credentials, business decisions with revenue impact).

4. **Progressive documentation.** Create and maintain a CLAUDE.md in the project root that evolves with the project. This is the single source of truth -- tech stack, architecture, conventions, version history.

5. **Ship the smallest thing that works, then iterate.** Don't build the full vision in one pass. Get to a working deployed URL first, then layer features.

## Execution Pipeline

Once activated, run through these phases sequentially. Do NOT pause between phases unless you hit a genuine blocker.

---

### Phase 0: Understand (5 min)

**Input:** User's idea description (can be as short as one sentence)

**Claude does:**
- Parse the idea into: core problem, target user, key differentiator
- If the idea is too vague to act on (e.g., "make something cool"), ask ONE clarifying question: "Who is this for and what problem does it solve?"
- Otherwise, proceed immediately

**Output:** Mental model (no document needed yet -- save time, start building)

---

### Phase 1: Research & Requirements (autonomous)

**Claude does:**
- Web search for 3-5 closest competitors/alternatives
- Identify what they do well and what gaps exist
- Define MVP scope: 3-5 core features max (ruthlessly cut everything else)
- Write a lightweight PRD in `docs/PRD.md`:
  - Problem statement (2-3 sentences)
  - Target user (1 paragraph)
  - Core features (bulleted, P0 only)
  - Success criteria (how do we know it works)
  - What we are NOT building (explicit exclusions)

**Decision framework for MVP scope:**
- If a feature doesn't directly serve the core use case, cut it
- Auth: skip unless the product requires user-specific data persistence
- Payments: skip in v1, add placeholder pricing page if relevant
- i18n: English only for v1 unless user specifies otherwise
- Admin panel: skip unless core to the product

**Quality gate:** PRD exists and is internally consistent

---

### Phase 2: Technical Architecture (autonomous)

**Claude does:**
- Select tech stack based on product requirements (not personal preference)
- Default stack (override only when requirements demand it):
  - **Web app:** Next.js (App Router) + TypeScript + Tailwind CSS + shadcn/ui
  - **Database:** Supabase (auth + DB + storage in one)
  - **AI features:** OpenAI API or Claude API (pick based on task fit)
  - **Deployment:** Vercel (zero-config for Next.js)
  - **Payments (when needed):** Stripe or LemonSqueezy
- Initialize the project: `npx create-next-app@latest`
- Set up the foundational structure
- Create CLAUDE.md in project root with:
  - Project overview
  - Tech stack with rationale
  - Project structure
  - Key conventions
- Commit: "Initial project setup"

**When to deviate from defaults:**
- Mobile app needed -> React Native / Expo
- Heavy real-time -> add Socket.io or Supabase Realtime
- ML/AI model serving -> add Python backend or use hosted inference
- Static site / blog -> skip Next.js, use Astro
- CLI tool -> Node.js + Commander

**Quality gate:** `npm run build` passes, CLAUDE.md exists

---

### Phase 3: Core Development (autonomous, iterative)

**Claude does:**
- Build features in priority order (P0 first, always)
- Each feature follows this micro-cycle:
  1. Implement the feature
  2. Self-review: read the code back, check for bugs, security issues, edge cases
  3. Test: verify it works (run the dev server, check build)
  4. Commit with descriptive message
- Keep CLAUDE.md updated as architecture evolves

**Development principles:**
- Start with data model and API routes, then build UI on top
- Use real API calls from the start (no mock data in production paths)
- Mobile-responsive from the beginning (not retrofitted)
- Handle loading and error states for every async operation
- Every user-facing string should be easy to find and change

**Design principles (learned from Caliber):**
- Warm, not cold. If the product evaluates/judges the user, lead with positive framing
- Show the product's value immediately (demo/preview before signup)
- One clear CTA per screen. Don't split user attention
- Micro-animations for state changes (fade-in, count-up, slide). Not decorative -- functional
- Typography hierarchy: one font family, 3-4 sizes max, clear visual weight

**Quality gate after each feature:** `npx tsc --noEmit && npm run build` passes

---

### Phase 4: Integration & Polish (autonomous)

**Claude does:**
- End-to-end walkthrough of the entire user flow
- Fix any broken transitions, missing states, or dead ends
- Add:
  - OG meta tags (title, description, og:image) for social sharing
  - Favicon and basic branding
  - Error boundaries / fallback UI for crashes
  - Loading states for all async operations
- Mobile viewport testing (check layout at 390px width)
- Run full build and fix any warnings

**Quality gate:** Complete user journey works end-to-end, build is clean

**Post-polish audit (recommended):**
- Run the `product-review` skill for a comprehensive product audit (brand, features, UI, logic bugs, competitive positioning)
- If the product contains a scoring/evaluation/ranking algorithm, also run the `algorithm-audit` skill to validate the model's theoretical grounding, behavioral anchoring, and weight calibration

---

### Phase 5: Deploy (autonomous)

**Claude does:**
- Initialize git repo if not already done
- Create `.env.example` with all required environment variables (no real values)
- Ensure `.gitignore` covers `.env.local`, `node_modules`, `.next`, etc.
- Deploy to Vercel:
  ```
  npx vercel --yes
  ```
- If Vercel CLI is not installed, install it first
- Verify deployment URL loads correctly
- Report the live URL to the user

**If deployment requires environment variables (API keys, DB URLs):**
- Tell the user exactly which env vars are needed and where to get them
- Provide the Vercel dashboard link for setting env vars
- This is the ONE place where user action is required

**Quality gate:** Live URL is accessible and functional

---

### Phase 6: Handoff Report

**Claude outputs a brief summary:**

```
## Ship Report

**Product:** [name]
**Live URL:** [vercel URL]
**Repo:** [local path]

### What was built
- [Feature 1]
- [Feature 2]
- [Feature 3]

### Tech stack
[stack summary]

### What's NOT built yet (future iterations)
- [Cut feature 1]
- [Cut feature 2]

### Environment variables needed
- `API_KEY_X` -- get from [where]

### Next steps (if you want to keep going)
1. [Most impactful next feature]
2. [Second priority]
3. [Third priority]
```

---

## Blocker Handling

Things that REQUIRE user input (pause and ask):
- API keys / credentials / paid service setup
- Domain name decisions
- Business model decisions (pricing, target market) that affect architecture
- Legal/compliance requirements

Things that DO NOT require user input (just decide):
- Tech stack choices
- UI layout and design
- Color schemes and typography
- File structure and naming
- Library selection
- Database schema
- API design
- Feature prioritization within the defined MVP scope
- Copy/text content (write sensible defaults, user can edit later)

## Recovery

If a phase fails:
1. Diagnose the root cause
2. Try an alternative approach
3. If truly stuck, explain the blocker in one sentence and propose 2 options
4. Never just report an error without a proposed solution

## Project Location

Default: create project in `~/workspace/[project-name]/`
If user specifies a different location, use that instead.
