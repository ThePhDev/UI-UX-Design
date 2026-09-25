# The Gauntlet

Based on the [Gauntlet Loop](https://github.com/duolahypercho/gauntlet-loop): build against a named reference, keep construction separate from criticism, and repair until the critic has nothing left. Taste §15 in [taste-reference.md](taste-reference.md) has the full rationale.

## Before round 1: the acceptance contract
Write it at the top of `qa/gauntlet.md` and don't change it mid-loop, except when the user changes the brief (record why):
- **Scope:** pages or screens, the main user journey, and what must be preserved in a redesign.
- **Reference:** the image or site (Path A) or `direction.md` (Path B), plus the specific qualities to match: hierarchy, spacing, asset treatment, motion timing.
- **Acceptance:** visible or testable outcomes per gate. Replace "premium" or "perfect" with observable requirements. For sites, the cinematic directive (taste §5.E–5.G) is required.
Never lower a dial, drop requested behavior, weaken a check or mark something `N/A` just to pass.

## Roles
- **Builder (you):** builds, captures real evidence and repairs. The builder never approves its own work.
- **Critic (fresh subagent):** gets the brief, the reference, the contract and the raw evidence (paths to screenshots, `-side.png`, the URL). It does not get your self-assessment. It demands specifics and doesn't edit files. When possible, show it the reference and the build as **anonymized A/B in random order**, and ask for a preference per criterion with visible reasons. If subagents are unavailable, do separate critic passes yourself and label them **self-review**.
- **The user is the brake:** a stop message ends the loop immediately.

## Rounds
Run the gates **in order** and log each as `round N | gate | PASS/FAIL/UNVERIFIED | evidence`.
A round only counts if **every gate passes in that same round**. Any FAIL → repair → new round from gate 1, because fixes for a later gate often break an earlier one. Gates 2, 5 and 7 always use the critic. Dispatch those critics in parallel.

| # | Gate | PASS when |
|---|---|---|
| 1 | **Fidelity** | Path A: `diff.py` at the reference viewport gives match ≥ 97%, height drift ≤ 8px, and no worst cell > 10% (excluded regions listed in spec.md). Path B: the result matches `direction.md` and the dials. |
| 2 | **Pixel details** | The critic compares 2x crops (`palette.py --crop`) of each region: font weight, size, tracking, line-height, radii, borders (1px vs 2px), shadow blur and offset, icon stroke and size, and alignment. Zero listed defects. |
| 3 | **Responsive** | `shoot.py --viewports desktop,laptop,tablet,mobile,small --full` exits 0. No text is clipped or overlapping, images keep their crop intent, sticky and fixed elements don't cover content, and a landscape phone is usable. Apps also need safe areas, a reachable bottom nav, `100dvh` and no hover-only actions. |
| 4 | **Motion** | `review-animations` passes, and the motion budget holds: cinematic on hero and marketing, fast and subtle on frequent UI. For sites: GSAP-led choreography, a custom animated SVG cursor on fine-pointer desktops, and every visible SVG animated. Check this in real playback, not from imports or screenshots. A generic entrance repeated everywhere fails. Also: transform and opacity only, no layout shift, zero console errors, a calm page under `prefers-reduced-motion`, and the final frame still passes gate 1. |
| 5 | **Human design** | The critic (impeccable lens + taste §9) finds no AI tells: default gradients, generic card grids, everything centered, identical boxes, emoji icons, default fonts, "Jane Doe" content or meaningless decoration. It must feel designed by a person for this brand. |
| 6 | **Human copy** | humanizer pass on all written or adapted text: no stock phrases, forced triads or filler, **no em-dashes** (taste §9.G), and specific CTAs. Same language as the reference or user. |
| 7 | **Quality** | The critic applies web-design-guidelines and taste §14 pre-flight: contrast AA, visible focus, semantic landmarks, heading order, alt text, input labels, keyboard navigation, theme lock and dark mode, no horizontal scroll, performance basics. |

## Findings
Log every finding as `ID | gate | location/state | severity | evidence | required outcome | retest`. Keep IDs stable and close them only with new evidence.
- **Blocker:** the journey breaks, the build fails, or content becomes inaccessible.
- **Major:** a brief mismatch, broken responsive layout, missing cinematic direction, or a visible gap from the reference.
- **Minor:** a local refinement.
Repair in order: blockers, then majors, then minors. Reject vague criticism ("make it more premium") until the critic names an observable problem.

## Stop
- **PASS:** a full round is clean. Publish (SKILL.md → Deliver) and report the round number and the evidence.
- **UNVERIFIED:** no known failures, but a tool, asset or access is missing. Deliver and name what wasn't verified.
- **NEEDS WORK:** after 8 rounds, or two rounds in a row with no measurable improvement, stop. Keep the best version and report the open findings and the next step. Never claim "perfect" without evidence.
