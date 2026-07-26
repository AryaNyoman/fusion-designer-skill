# Fusion Designer Skill

**One deterministic pipeline that fuses four design-skill families into a single high-craft workflow for Claude Code.**

Modern agent skills are excellent at one axis each: one knows *what* direction to pick, one knows *how* to generate without AI slop, one knows *how motion should feel*, one knows *how to audit and polish*. Used separately they overlap, disagree, and get invoked in the wrong order. Fusion Designer turns them into one pipeline with fixed phases, deterministic conflict precedence, and hard ship gates.

## The Fusion

| Family | Skill(s) | Role |
|---|---|---|
| Intelligence | ui-ux-pro-max | *What* direction: 67 styles, 161 palettes, 57 font pairings, stack guidance. A menu, never a mandate. |
| Generation law | [taste-skill](https://github.com/leonxlnx/taste-skill) | *How to build* without slop: brief inference, design dials, banned AI-tells, layout discipline, pre-flight ship gate. |
| Motion craft | [emil-design-eng, apple-design, review-animations, find-animation-opportunities](https://github.com/emilkowalski/skills) | *How it feels*: frequency test, easing, duration caps, springs, gestures, strict motion review. |
| Craft engine | impeccable | Production-grade code, full audit (hierarchy, WCAG AA, responsive, states, Core Web Vitals), browser-verified polish. Final arbiter. |

## Prerequisites

The component skills must be installed as Claude Code skills (e.g. under `~/.claude/skills/`):

- `ui-ux-pro-max`
- `impeccable`
- `taste-skill` (from [leonxlnx/taste-skill](https://github.com/leonxlnx/taste-skill))
- `emil-design-eng`, `apple-design`, `review-animations`, `find-animation-opportunities`, `pick-ui-library` (from [emilkowalski/skills](https://github.com/emilkowalski/skills))
- Optional asset support: `brandkit`, `imagegen-frontend-web` (from leonxlnx/taste-skill)

Fusion Designer degrades gracefully if an optional support skill is missing, but the four core families are required.

## Install

```bash
git clone https://github.com/AryaNyoman/fusion-designer-skill.git
cp -r fusion-designer-skill/skills/fusion-designer-skill ~/.claude/skills/
```

Then in Claude Code:

```
/fusion-designer-skill
```

or just ask for a "high-craft" / "truly beautiful" design — the skill triggers on intent.

## The Pipeline

```
Phase 0 INTAKE      taste-skill brief inference → Design Read + 3 dials
Phase 1 DIRECTION   ui-ux-pro-max picks 1 style + 1 palette + 1 pairing + 1 stack,
                    filtered through taste-skill bans → Design Contract
Phase 2 STRUCTURE   taste-skill layout law + impeccable craft → full page structure
Phase 3 MOTION      emil-design-eng decision framework + apple-design gestures
                    + taste-skill scrolltelling skeletons → motion layer
Phase 4 GATES       Gate A taste-skill Final Pre-Flight Check (anti-slop)
                    Gate B review-animations (strict motion review)
                    Gate C impeccable audit (hierarchy, a11y, responsive, CWV)
                    → ALL must pass; FAIL → fix → re-run that gate
Phase 5 VERIFY      screenshots desktop+mobile, light+dark → fix → polish → ship
```

**Core rule: phases run in order, every gate must pass before shipping. No phase skipping, no gate skipping, no substituting skills that are not part of the pipeline.**

### Animation engine

The pipeline's official animation engine is **[Motion](https://github.com/motiondivision/motion)** (formerly Framer Motion) — the library both taste-skill and emil-design-eng already assume. The skill pins the binding facts: import from `motion/react` (never the legacy `framer-motion` alias), Motion for component-level motion vs GSAP ScrollTrigger for page-level scrolltelling (never both in one component tree), `useMotionValue`/`useTransform` for continuous input (never `useState`), Apple-style spring config, the main-thread caveat for shorthand props, and `useReducedMotion()` gating. For API specifics it defers to Motion's official agent-readable docs at [motion.dev/llms.txt](https://motion.dev/llms.txt).

### Deterministic precedence (conflicts are never renegotiated)

1. The user's explicit brief.
2. Accessibility & performance floors (WCAG AA, `prefers-reduced-motion`, transform/opacity-only animation, Core Web Vitals).
3. taste-skill bans override ui-ux-pro-max suggestions (data proposes, law disposes).
4. Motion: emil-design-eng wins for component-level UI motion; taste-skill wins for page-level scrolltelling mechanics.
5. ui-ux-pro-max fills every remaining open choice with its top-ranked recommendation.
6. impeccable arbitrates remaining aesthetic ties in review phases, but may never reintroduce a banned pattern.

Example: ui-ux-pro-max ranks Inter + lucide-react highest for a brief → taste-skill bans both as defaults → rule 3 applies, the next-ranked font pairing and an allowed icon family (Phosphor / HugeIcons / Radix / Tabler) are used instead. No debate, no vibe-based picks.

### Why gates instead of "best effort"

Testing showed that without this pipeline, an agent given all the component skills will: run taste-skill's pre-flight checklist as upfront planning (it is a ship gate), pull in unrelated skills uninvited, skip the design dials, and invent a different conflict-resolution scheme every run. The pipeline exists precisely to make those failures impossible.

## What's in the skill

- `skills/fusion-designer-skill/SKILL.md` — the skill itself: pipeline, per-phase deliverables and exit conditions, precedence table, quick reference, common mistakes, red flags.

## Credits

This skill orchestrates work by others — all credit for the underlying design intelligence goes to them:

- **leonxlnx** — [taste-skill](https://github.com/leonxlnx/taste-skill) (anti-slop generation law)
- **Emil Kowalski** — [skills](https://github.com/emilkowalski/skills) (design-engineering & animation craft)
- **ui-ux-pro-max** and **impeccable** skill authors
- **Motion** — [motiondivision/motion](https://github.com/motiondivision/motion) (the animation library the pipeline standardizes on)

Fusion Designer contains no copied content from those repositories; it references their skills by name and defines the orchestration layer on top.
