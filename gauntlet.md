# The Gauntlet

Run the gates **in order**. Record each result in `qa/gauntlet.md` as `round N | gate | PASS/FAIL | evidence`.
A round only counts if **every gate passes in that same round**. Any FAIL → fix → start a new round at gate 1.
Fixes for a later gate often break an earlier one (mobile CSS shifts desktop, motion changes the final frame), which is why the gauntlet restarts.
Cap: 8 rounds. If it still fails, stop and report the remaining failures honestly with evidence.

For gates 2, 5 and 7 use a **fresh-eyes critic**: dispatch a subagent. Give it the file paths only (reference, `-side.png`, screenshots, URL) and ask for a numbered list of concrete defects with location. Don't include your own opinion. A critic that finds nothing must say so explicitly.

| # | Gate | PASS when |
|---|---|---|
| 1 | **Fidelity** | `diff.py` at the reference viewport: match ≥ 97%, height drift ≤ 8px, no worst cell > 10% (excluding regions listed as excluded in spec.md) |
| 2 | **Pixel details** | Critic compares 2x crops (`palette.py --crop`) of reference vs build for each region: font weight, size, tracking, line-height, radii, borders (1px vs 2px), shadow blur/offset, icon stroke/size, alignment to the same x. Zero listed defects. |
| 3 | **Responsive** | `shoot.py --viewports desktop,laptop,tablet,mobile,small --full` exits 0. Also check: no text clipped or overlapping, images keep their crop intent, sticky and fixed elements don't cover content, landscape phone usable. Apps: safe areas, bottom nav reachable, `100dvh`, no hover-only actions. |
| 4 | **Motion** | `review-animations` passes on the motion code, and the motion budget matches `ph-design-skill` (expressive on hero and marketing, fast and subtle on frequent UI). Every animation has a job (guide the eye, show hierarchy, give feedback). Entrances ≤ 900ms and staggered, easing custom (no linear/default), transform and opacity only, no layout shift, zero console errors, `prefers-reduced-motion` gives a calm static page, and the final frame still passes gate 1. |
| 5 | **Human design** | Critic (use impeccable's critique lens) finds no AI-template tells: default purple/blue gradients, generic card grids, everything centered, identical rounded boxes, emoji as icons, Inter/Roboto defaults unless the reference uses them, meaningless decoration. It must feel designed by a person for this brand. |
| 6 | **Human copy** | humanizer pass done on all written or adapted text. No stock AI phrases, no forced triads, no filler, and CTAs are specific. Same language as the reference or user. |
| 7 | **Quality** | Critic applies web-design-guidelines: text contrast AA, visible focus states, semantic landmarks and headings order, alt text, labels on inputs, keyboard navigation works, no horizontal scroll, Lighthouse-style basics (lazy images, font-display swap). |

After a clean round: publish (SKILL.md → Deliver) and include the round number and final gate evidence in the report to the user.
