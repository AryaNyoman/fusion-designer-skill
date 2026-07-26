---
name: fusion-designer-skill
description: Use when the user wants a complete, maximum-quality design or redesign of a web interface (landing page, portfolio, marketing site, product UI) and wants the installed design skills combined — requests like "make it truly beautiful", "high-craft design", "impeccable design", "use my design skills together", "fusion design", or /fusion-designer-skill. Combines ui-ux-pro-max, taste-skill, impeccable, emil-design-eng, apple-design, review-animations, find-animation-opportunities into one pipeline.
---

# Fusion Designer

One deterministic pipeline that fuses four skill families into a single high-craft design workflow:

| Family | Role in the fusion |
|---|---|
| **ui-ux-pro-max** | INTELLIGENCE — what direction to take (style, palette, font pairing, stack). A menu, never a mandate. |
| **taste-skill** | GENERATION LAW — how to build without AI slop (brief inference, dials, banned patterns, layout discipline, pre-flight gate). |
| **emil-design-eng** + **apple-design** | MOTION CRAFT — how it feels (frequency test, easing, duration, springs, gestures). |
| **impeccable** | CRAFT ENGINE & FINAL ARBITER — production-grade code, audit, polish, verified in a real browser. |

Support skills, invoked only at their phase: **find-animation-opportunities**, **review-animations**, **pick-ui-library**, **brandkit** / **imagegen-frontend-web** (image assets).

**Core rule: phases run in order, and every gate in Phase 4 must pass before shipping. No phase skipping, no gate skipping, no substituting skills that are not part of this pipeline.**

## When to Use

- Building or redesigning a landing page, portfolio, marketing site, or product UI where visual quality is the point.
- The user asks for "beautiful", "premium", "high-craft", "anti-generic", or explicitly for this skill.

**When NOT to use:** backend-only work, quick one-line CSS fixes, or when the user asks for a single specific sub-skill (then invoke that sub-skill alone).

**Surface adaptation:** taste-skill's generation law is scoped to landing pages / portfolios / marketing / redesigns. For dashboards and dense product UI, Phase 2 swaps its law source: use impeccable's product register + ui-ux-pro-max patterns instead of taste-skill layout rules. Gates B and C still run in full; Gate A runs only its universal checks (contrast, theme lock, shape lock, em-dash ban, copy audit).

## The Pipeline

```
Phase 0 INTAKE → Phase 1 DIRECTION → Phase 2 STRUCTURE → Phase 3 MOTION
   → Phase 4 GATES (A → B → C, all must pass) → Phase 5 VERIFY & SHIP
```

### Phase 0 — INTAKE (lead: taste-skill, Section 0)

1. Read the brief. Classify: page kind, audience, vibe words, references, existing brand assets, quiet constraints (a11y-first, regulated, trust-first).
2. Output the one-line **Design Read**: "Reading this as: \<page kind> for \<audience>, with a \<vibe> language, leaning toward \<aesthetic family or design system>."
3. Set the three dials with reasons: `DESIGN_VARIANCE / MOTION_INTENSITY / VISUAL_DENSITY`.
4. If (and only if) the design read genuinely diverges, ask exactly ONE clarifying question. Otherwise proceed.

Deliverable: Design Read + dial values. Mandatory. A build with silent default dials is a Phase-0 failure.

### Phase 1 — DIRECTION (lead: ui-ux-pro-max)

1. Query ui-ux-pro-max's databases for the design read: shortlist styles, palettes, font pairings, stack guidance.
2. Pick exactly **1 style + 1 palette + 1 font pairing + 1 stack**. No mixing two styles, no second accent.
3. **Filter every pick through taste-skill's bans before locking it.** ui-ux-pro-max proposes; taste-skill vetoes. Banned as defaults: Inter (unless neutral/Linear-style or public-sector brief), Fraunces / Instrument Serif, AI-purple glow palettes, beige+brass+espresso for premium-consumer briefs, lucide-react icons, hand-rolled SVG icons.
4. Lock the **Design Contract**: color tokens (light AND dark), type scale, spacing scale, ONE corner-radius system, ONE accent, ONE icon family (Phosphor / HugeIcons / Radix / Tabler), motion budget derived from `MOTION_INTENSITY`.

Deliverable: Design Contract. Every later phase obeys it; changing it later requires re-stating it, not silent drift.

### Phase 2 — STRUCTURE (law: taste-skill · craft: impeccable)

1. Section map first, code second. Layout families per taste-skill law: ≥4 distinct families per 8 sections, zigzag cap (max 2 consecutive image+text splits), eyebrow ration (≤ ceil(sections/3)), no split-header default, bento cells = content count.
2. Hero discipline: fits viewport, headline ≤2 lines, subtext ≤20 words, ≤4 text elements, real visual (image-gen tool first, then seeded placeholders — never div-based fake screenshots).
3. Build production-grade per impeccable's standards: real loading / empty / error states, responsive collapse declared per section, semantic HTML, `min-h-[100dvh]` never `h-screen`.
4. Image assets: if an image-generation tool exists, generate section-specific assets (brandkit / imagegen-frontend-web guide the prompts). Otherwise seeded placeholders + a labeled asset list for the user.

Deliverable: complete structured page obeying the Design Contract.

### Phase 3 — MOTION (lead: emil-design-eng · gestures: apple-design)

Run Emil's decision framework for every animation, in order:
1. **Frequency test** — seen 100+ times/day → no animation. Keyboard-initiated → never animate.
2. **Purpose** — must name one: feedback / state / spatial consistency / explanation / preventing jarring change. "Looks cool" fails for frequent UI.
3. **Easing** — enter/exit → `ease-out` (custom curve, e.g. `cubic-bezier(0.23, 1, 0.32, 1)`); on-screen movement → `ease-in-out`; never `ease-in` for UI.
4. **Duration** — UI ≤300ms (press 100–160ms, dropdowns 150–250ms, modals 200–500ms). Marketing moments may be longer.

Component motion (buttons `scale(0.97)` on `:active`, origin-aware popovers, `@starting-style` entries, springs for gestures/drag per apple-design) follows Emil. Page-level scrolltelling (sticky-stack, horizontal pan, scroll reveals) follows taste-skill's canonical GSAP/Motion skeletons — `start: "top top"`, `pin: true`, cleanup, transform/opacity only, `prefers-reduced-motion` collapse for everything above dial 3.

If the page feels static and `MOTION_INTENSITY > 4`, invoke find-animation-opportunities and implement only proposals that pass the frequency test.

Deliverable: motion layer where every animation can be justified in one sentence.

### Phase 4 — GATES (all three, in order; any FAIL → fix → re-run that gate)

- **Gate A — Anti-Slop:** run taste-skill's **Final Pre-Flight Check** as a checklist against the actual code (theme lock, color/shape locks, contrast checks, hero discipline, eyebrow count, layout-family variety, zero em-dashes, no AI tells, copy self-audit). The pre-flight is a SHIP GATE. Running it as an upfront brainstorm and never re-running it against the finished code is a violation.
- **Gate B — Motion Review:** invoke review-animations (flag-by-default posture) on all animation code. Fix every flagged item or state explicitly why it stands.
- **Gate C — Craft Audit:** invoke impeccable's audit on the full result: hierarchy, information architecture, WCAG AA contrast, keyboard navigation, responsive behavior, states coverage, performance (LCP < 2.5s, INP < 200ms, CLS < 0.1).

Nothing ships with a failing gate. "Mostly passes" is a FAIL.

### Phase 5 — VERIFY & SHIP (lead: impeccable + browser)

1. Render and screenshot: desktop AND mobile, light AND dark theme. Look at the screenshots; fix what looks wrong, not just what lints wrong.
2. Final impeccable polish pass on anything the screenshots exposed.
3. Deliver with a short report: Design Read, Design Contract summary, gate results.

## Motion Engine (Phase 3 reference)

The pipeline's official animation engine is **Motion** ([motiondivision/motion](https://github.com/motiondivision/motion), formerly Framer Motion). This is not a new rule — taste-skill mandates it as the default library and emil-design-eng's spring/gesture guidance assumes it. Binding facts:

- **Import from `motion/react`** (`import { motion } from "motion/react"`); `framer-motion` is a legacy alias — do not use it in new code.
- **Division of labor:** Motion for component-level UI motion (enter/exit, gestures, layout, springs); GSAP ScrollTrigger only for page-level scrolltelling per taste-skill's canonical skeletons. **Never both in the same component tree.**
- **Continuous input values** (mouse position, scroll progress, drag) → `useMotionValue` / `useTransform` / `useScroll`. Never `useState` — it re-renders the tree every frame.
- **Springs:** prefer Apple-style config `{ type: "spring", duration, bounce }`, bounce 0.1–0.3 when used at all; springs earn their keep on gestures and interruptible motion (they keep velocity; CSS keyframes restart from zero).
- **Performance caveat (from emil-design-eng):** Motion's shorthand props (`x`, `y`, `scale`) run on the main thread via `requestAnimationFrame`. For animations that must survive a busy main thread, use the full `transform` string or plain CSS animations. Animate transform/opacity only, always.
- **Reduced motion:** gate everything above `MOTION_INTENSITY 3` with `useReducedMotion()`.
- **Official agent-readable docs:** https://motion.dev/llms.txt (index of the full Motion docs). Consult it for API specifics instead of guessing from training data.

## Precedence (deterministic — never renegotiate per conflict)

1. **The user's explicit brief** overrides everything below.
2. **Accessibility & performance floors** — WCAG AA, `prefers-reduced-motion`, transform/opacity-only animation, Core Web Vitals. Non-negotiable, even against aesthetics.
3. **taste-skill bans** override ui-ux-pro-max suggestions (data proposes, law disposes).
4. **Motion:** emil-design-eng wins for component-level UI motion; taste-skill wins for page-level scrolltelling mechanics.
5. **ui-ux-pro-max** fills every remaining open choice with its top-ranked recommendation.
6. **impeccable** arbitrates remaining aesthetic ties during Phases 4–5, but may never reintroduce a banned pattern.

## Quick Reference

| Phase | Lead | Support | Output | Exit condition |
|---|---|---|---|---|
| 0 Intake | taste-skill §0 | — | Design Read + dials | Read stated, dials reasoned |
| 1 Direction | ui-ux-pro-max | taste-skill bans, pick-ui-library | Design Contract | 1 style, 1 palette, 1 pairing, 1 stack locked |
| 2 Structure | taste-skill law | impeccable, brandkit/imagegen | Full page structure | Contract obeyed, real states, real images |
| 3 Motion | emil-design-eng | apple-design, find-animation-opportunities | Motion layer | Every animation justified |
| 4 Gates | taste pre-flight → review-animations → impeccable audit | — | Pass/fail per gate | ALL gates pass |
| 5 Verify | impeccable | Browser screenshots | Shipped page + report | Screenshots checked in both themes & viewports |

## Common Mistakes

| Mistake | Correction |
|---|---|
| Running taste-skill's pre-flight checklist upfront as planning | It is Gate A, run against finished code in Phase 4 |
| Substituting skills not in this pipeline (e.g. a brainstorm skill) uninvited | Use only the listed skills unless the user asks |
| Adopting ui-ux-pro-max's suggestion that hits a taste-skill ban | Precedence rule 3: the ban wins; pick the next-ranked option |
| Skipping Phase 0 dials and "just designing" | Dials gate layout, motion, and density decisions downstream |
| Inventing ad-hoc conflict resolution mid-build | The precedence list is fixed; apply it mechanically |
| Animating everything because motion skills are loaded | Frequency test first; frequent/keyboard UI gets zero animation |
| Declaring done without screenshots | Phase 5 requires looking at rendered output in both themes and viewports |
| Treating a gate FAIL as "minor, ship anyway" | Fix and re-run the gate; no exceptions |

## Red Flags — STOP if you catch yourself thinking

- "The pre-flight can double as my planning checklist" → it's a ship gate.
- "ui-ux-pro-max ranked Inter first, so Inter it is" → filter through bans first.
- "The gates are redundant, my code is clean" → run all three anyway.
- "No time for screenshots" → then the work is not done.
- "These two skills disagree, I'll pick per vibe" → apply the precedence list.
