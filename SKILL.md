---
name: ph-design-skill
description: Use when creating, redesigning, styling, cloning or reviewing ANY user-facing interface, with or without a reference image. Covers websites, landing pages, portfolios, web apps, mobile app screens, PWAs, dashboards, study apps, HTML artifacts, single components, small visual tweaks to one element ("make this button prettier", "deixa mais bonito"), and reference images or screenshots to rebuild ("copy this", "clone this design", "pixel perfect", "idêntico", "transforma essa imagem em site/app"). Load it first, before impeccable or frontend-design, and before writing the first line of UI code.
---

# PH_Design_Skill

## Overview
This is the user's house style for anything with a UI, with or without a reference image. Every project gets a deliberate design (or a measured pixel-perfect copy of the reference), equal care on desktop and mobile, motion that feels crafted (Emil Kowalski's bar), human copy, a quality **gauntlet**, and a preview link. It doesn't matter if the project is small.

**Done = one full gauntlet round with zero failures + a working public preview link.** Not "looks close".

## Tools (`python ~/.claude/skills/ph-design-skill/scripts/<script>`)
| Script | Use |
|---|---|
| `palette.py IMG [--at X,Y] [--crop X0,Y0,X1,Y1 out.png [--scale 1]]` | size, dominant hex colors, exact pixel colors, 2x zoom crops, asset extraction |
| `shoot.py URL OUTDIR --viewports desktop,laptop,tablet,mobile,small,1920x1080 [--full] [--no-scroll]` | settled screenshots + responsive audit (`report.json`, exit 1 on issues). Named: desktop 1440, laptop 1280, tablet 768, mobile 390, small 360; any `WxH` works |
| `diff.py REF SHOT OUT [--exclude X0,Y0,X1,Y1 ...]` | match %, height drift, worst grid cells, heatmap + side-by-side |
| `publish.py DIST_DIR_or_PORT` / `publish.py stop` | Cloudflare quick tunnel, prints verified public URL |

Work in `C:\Users\amigi\ClaudeTelegram\sites\<name>\` (Vite + TS; GSAP for motion). Keep `ref/` (reference, if any) and `qa/` (spec, shots, diffs, gauntlet log).

## Route
- **Reference image or screenshot** → Path A.
- **No reference** → Path B.
Both paths then share Mobile, Motion, Copy, Gauntlet and Deliver.

## Path A — rebuild a reference, pixel by pixel
Eyeballing gets you ~85%. The last 15% only comes from measuring.
1. **Read the reference like a spec.** Run `palette.py`, then crop and zoom every region (nav, hero, cards, footer). Write `qa/spec.md` with: canvas width, grid/columns, spacing scale, colors (hex), type (sizes, weights, line-heights, letter-spacing), radii, shadows, icons and images. Use the real text from the image, and only invent text where the image has none. Fonts: see Type.
   **Photos, illustrations and logos:** use the user's own asset if they have one. Otherwise extract it from the reference (`palette.py REF --crop BOX assets/x.png --scale 1`) and tell the user it's a low-res placeholder to swap. Never grab random web images.
2. **Decide the target.** For a desktop reference, build that width first and design the mobile version (see Mobile). A phone-screen reference is an **app**: 390px, `100dvh`, safe areas, bottom nav, 44px touch targets. Give it its own desktop layout, don't stretch the phone screen. If the user sends phone mockups, follow them screen by screen.
3. **Static clone first, no motion.** Use semantic HTML, CSS variables from the spec, `clamp()` type and a real grid.
4. **Measure loop.** `shoot.py --viewports <refW>x<refH-or-900> --no-scroll` (or `--full` for a full-page reference) at the **reference's exact width**. Never diff a 1440 shot against a 1920 reference. Then `diff.py` → open `-side.png` → fix the **worst cell** first. Canvas, WebGL, video and swapped photos go in `--exclude`. Repeat until **match ≥ 97%**, height drift ≤ 8px, and no worst cell > 10%.
5. Continue with Mobile → Motion (the final frame must re-pass step 4) → Copy (text copied verbatim from the reference stays as-is) → Gauntlet → Deliver.

## Path B — design from scratch
1. **Direction.** Before coding, write 5 lines in `qa/direction.md`: audience, mood (3 adjectives), palette (hex), type pairing, and one signature idea (the thing people remember). Use `frontend-design` and `impeccable` to pick a direction that isn't templated. Offer 2-3 directions only when the user asks to compare; `prototype` renders them side by side.
2. Build desktop and mobile together (see Mobile). Then Motion → Copy → Gauntlet (gate 1 = "matches direction.md"; gate 2 = a critic zooming on spacing rhythm, alignment, radii, shadows and icon weight) → Deliver.

## Type (both paths)
**Don't start with Google Fonts.** Identify the real typeface: use WhatTheFont or the Font Squirrel/Fontspring Matcherator on a crop. Search **https://www.dafont.com/pt/** first (the user's favorite source), then the foundry's own site, Fontshare, Font Squirrel or the designer's site. Google Fonts is only a fallback. Many dafont fonts are personal-use only: check the license and tell the user. Self-host the files as woff2 in `assets/fonts` with `@font-face`. With a reference, render 2-3 candidates with the same heading text, diff them against the crop, and keep the lowest delta. Check glyph coverage for everything the content needs: accents, Ω/Δ/Σ, math symbols. Use one family per role (display, body, labels/data), the same everywhere.

## Mobile (both paths, always)
**Mobile gets full care every time, even when the reference only shows a desktop.** Plan the 390px version in `qa/spec.md` or `direction.md` before coding: header, navigation, hero, grids, cards, forms and footer. Keep the same identity, illustrations, type hierarchy and spacing rhythm, and never just shrink or stack. Everything must look regular and tidy: consistent gutters, aligned edges, even spacing, centered where it makes sense, otherwise clearly on a grid. For apps and PWAs apply `mobile-native`: safe areas, `100dvh`, no tap flash or sticky hover, inputs ≥16px. Verify with `shoot.py --viewports tablet,mobile,small --full`: fix every report issue and look at each screenshot.

## Motion (both paths)
The user likes a lot of motion: GSAP, scroll-driven sections, custom cursors, 3D. Emil's rule decides **where** it goes:
| Surface | Motion budget |
|---|---|
| Hero, section reveals, marketing moments, first load | Expressive: choreography, stagger, scroll scenes, WebGL, cursor effects |
| Frequently used UI (buttons, menus, tabs, forms, lists) | Fast and subtle: 150–250ms, ease-out, interruptible, never blocks input |
| Keyboard/repeated actions | None or instant |
- Build with `animate`. Apply `emil-design-eng` polish, and use `apple-design` for springs, drag, sheets and gestures. Name effects with `animation-vocabulary` before building.
- **React Bits** (217 animated components: text effects, backgrounds, cursors, galleries, micro-interactions) → [react-bits-catalog.md](react-bits-catalog.md). Check it before hand-building an effect. React projects: `npx shadcn@latest add @react-bits/<Name>-TS-TW`. Vanilla/Vite projects: port from the local source. Customize colors and timing, and never ship demo defaults.
- Only transform, opacity and filter. Respect `prefers-reduced-motion`. Afterwards run `review-animations`; on an existing project, `find-animation-opportunities` shows what's missing.
- Libraries (charts, OTP, drag and drop, toasts) → `pick-ui-library`.

## Copy, Gauntlet, Deliver (both paths)
- **Copy:** real, specific text in the user's language, passed through `humanizer`.
- **Gauntlet:** run [gauntlet.md](gauntlet.md). Any failure → fix → restart from gate 1.
- **Deliver:** `npm run build` → `publish.py dist` → send the URL plus desktop and mobile screenshots (`shoot.py`). With a reference, also report the final match % and anything excluded.

## Common Mistakes
| Mistake | Fix |
|---|---|
| UI code before `spec.md` / `direction.md` exists | Write it first |
| Declaring "pixel perfect" from memory of the image | Only `diff.py` numbers count |
| Fixing random spots | Always fix the worst cell first; re-diff after each batch |
| Diffing mid-animation | Shots come from `shoot.py` (it settles and finishes animations) |
| Mobile left for the end, or desktop squeezed | Plan it before coding, with the same care; review phone screenshots screen by screen |
| First Google Font that looks close | Identify the real face; Google Fonts is the fallback |
| Font lacks glyphs and silently falls back | Check coverage for all content before choosing |
| Same entrance animation on every element; motion on high-frequency UI | Follow the motion budget table |
| Library component shipped with demo defaults | Retune colors, timing and scale to the design |
| User in a hurry, so critics get skipped | Never skip gates. Dispatch the critics for gates 2, 5 and 7 in parallel and send progress updates |
| Autoplay carousel breaks diffs | Start on slide 1, pause on hover/focus, stop under reduced motion |
| Vite preview returns 403 on the link | `preview/server.allowedHosts: [".trycloudflare.com"]` |
| Raw HTML through the tunnel is blank on phones | Doctype, `<meta charset="utf-8">`, viewport meta; keep non-ASCII out of JS regexes; test the public URL in Playwright |
