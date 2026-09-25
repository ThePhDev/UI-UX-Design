# Prompt Kit: Figma-shot screens (no-reference projects)

When the user asks for a site or app **without a reference image**, deliver a **prompt pack** that generates the reference screens (desktop + mobile) **before any code**. Never skip it, even when the client already has real photos: the user considers these prompts essential. Wait for the user to choose:
- **A) Generate the images** and send them back → the build continues on **Path A** (pixel by pixel from the generated screens).
- **B) "build"** → the pack becomes the spec: its style block, sections and copy go into `direction.md` and the build follows Path B.

The screens must read as **a finished Figma frame or a Dribbble/Behance shot**, a designer's definitive UI print, and never as a photo mockup of the place.

## 1. Style DNA ("creative, designed by a person")
1. **No photorealism of the business.** Every photo slot is an **image placeholder**: a flat tinted block with a thin outline, a small image icon and a caption saying what goes there ("FOTO: pergolado com primavera, horizontal 4:3"). The generator must not invent the place, people, food or products. Real photos come from the client later.
2. **Brave, owned color.** Build a palette from the business's world, not the AI default (no beige + terracotta + sage by habit, no purple-blue gradients). Pick one dominant hue, one surprising accent and a dark anchor. Name each hex and its role (background, surface, text, accent, section band).
3. **Color that travels.** Each section sits on its own color band from the palette. The page is a sequence of color fields, and the prompt describes how one field hands off to the next: a diagonal wipe, a curved edge, an overlapping card that straddles the two colors, or a gradient seam.
4. **Typography with character.** Never the usual AI stack (Inter, Poppins, Montserrat, Playfair, "a geometric sans"). Choose a display face with personality from dafont.com first (check the license), then from foundries like Fontshare, Pangram Pangram, Velvetyne, Collletttivo or ATF. Examples: condensed grotesk, wide expanded sans, stencil, chunky soft serif, variable display with ink traps. Pair it with a quiet text face. Use big scale contrast (display 120–200px desktop), mixed weights inside one headline and tight tracking. Name the fonts in the prompt.
5. **Illustration system with depth.** Instead of photos, the art is **detailed vector illustration**: layered shapes with light direction, soft shadows, highlights and gradients for volume, and a few **3D objects** (isometric or soft 3D render style) that belong to the business. The same light direction and palette appear everywhere. They are drawn to be animated as seamless loops later.
6. **Minimal surface, deep content.** Each screen shows only the essentials: one headline, a short line and one action. Everything else about the business still exists, but it sits behind interaction: expandable cards, "+" hotspots on an illustration, tabs, accordions, a drawer. The shot shows 1–2 of these in the open state so the builder knows the pattern.
7. **Generous space.** Wide vertical rhythm between sections (160–240px on desktop), a clear 12-column grid, and a lot of calm area around each focal element.
8. **Real product fragments.** Buttons, chips, a date picker, a WhatsApp preview bubble and a price or capacity tag, with believable text in the user's language. No lorem ipsum or gibberish.
9. **An art concept, not a template.** Name a concept for the brand (e.g. "Verão de primavera: a tactile editorial poster") and a **material world** it is made of: risograph paper, cut paper, clay, felt, resin, letterpress, gold foil, screen print, ceramic, neon glass, and so on. Sections become physical layers of that world (torn or die-cut edges, real thickness, soft cast shadows), and the texture is visible up close: paper grain, halftone, misregistration, emboss or deboss, foil specular.
10. **Bolder effects, still usable UI.** Pick 3–4 from: halftone sunburst rays, light leaks, caustics, depth-of-field on foreground elements, motion-blurred falling pieces, washi tape, embossed or foil type, type overlapping the art, warped or stacked kinetic type. The controls (buttons, inputs, calendar) stay crisp and legible on top of it.
11. **Mobile is designed, not squeezed.** The same color bands, typography and illustrations recomposed for 390px, with a thumb-reachable sticky action and the same interaction patterns (accordions, sheets).

## 2. Build the pack
Research the business first (site, Instagram, Google, marketplaces) and list the real facts. Then fill these in and show them to the user in 5–7 lines:
`BRAND` (name + one-line truth) · `MODE` · `PALETTE` (hex + role each) · `TYPE` (display + text, with source) · `ILLUSTRATION` (the vector/3D system and its light) · `SIGNATURE` (the one idea only this business could have) · `DISCLOSURE` (what hides behind which interaction) · `SCREENS`.

### 2.1 Style block (paste into every prompt, unchanged)
```
Style: finished Figma UI frame / Dribbble shot of a real website, crisp flat UI, designed by a senior human designer, not a photo mockup.
All photo areas are EMPTY IMAGE PLACEHOLDERS: flat {PLACEHOLDER_TINT} blocks with a 1px outline, a small image icon and a short label describing the photo that will go there. Do not render any photograph.
Palette: {PALETTE with roles}. Each section is a full-width color band; transitions between bands are {TRANSITION}.
Typography: display "{DISPLAY}" huge (120-200px), mixed weights, tight tracking; text "{TEXT}" small and calm. Clear hierarchy, strong scale contrast.
Illustrations: detailed vector art with one light source from {LIGHT}, soft shadows, highlights, gradients for volume and depth, plus a few soft-3D objects: {OBJECTS}. Same style everywhere.
Minimal layout with deep content: only essentials visible, extra info behind "+" hotspots, expandable cards and accordions (show one opened).
Generous spacing (160-240px between sections), 12-column grid, pixel-perfect alignment, readable real {LANGUAGE} copy.
```

### 2.2 Negative block (append to every prompt)
```
Avoid: photorealistic photos of the place, people, food or rooms; stock photography; AI-default fonts (Inter, Poppins, Montserrat, Playfair);
beige + terracotta + sage by default; purple-blue gradients; glassmorphism; generic SaaS template; identical icon cards; emoji icons;
tiny gibberish text; lorem ipsum; misaligned grid; heavy drop shadows; gradient text; eyebrow labels above headings; watermark; tilted device mockups.
```

### 2.3 Default format: GPT Image 2.5 Sunburst (the user's generator)
Sunburst follows labeled sections best. Every prompt has these blocks, in this order, in plain words (no tags soup):
- `DELIVERABLE:` the exact output first: what it is (finished website design, Dribbble/Awwwards presentation), canvas (desktop: two tall columns of a 1440px page on a studio backdrop, portrait; mobile: four 390x844 screens, landscape) and "crisp shipped UI that looks like it already exists".
- `CONCEPT:` the named concept and its material world, in 2–3 sentences.
- `SCENE:` the page top to bottom, one numbered line per section: its paper/color band, the essentials, the one open disclosure state, and how its edge hands off to the next section.
- `TEXT:` every visible string in double quotes, with position and type role, in the user's language; then "No other text anywhere. Check spelling and accents". Spell brand names exactly.
- `DETAILS:` palette hexes with roles, typography described by character (and the real font names as "like X"), materials and textures, one light direction with shadow color and falloff, depth layers, the chosen effects, how image placeholders look, spacing.
- `CONSTRAINTS:` no photos of the place (placeholders only), banned fonts and clichés, legibility of small UI text.
- `PROTECTED ANCHORS:` the 5–7 traits that must survive every edit (palette, material world, hero object, light direction, placeholders, quoted text). Repeat this block in each edit.
Settings line above the prompt: `model gpt-image-2.5-sunburst · quality high (xhigh for the final) · 1024x1536 to iterate, final 2160x3840 (mobile 3840x2160) · opaque background`. Iterate one change at a time, passing the previous output back with the protected anchors.
The style and negative blocks below are the short form for other generators.

### 2.4 Screen prompts (other generators)
One prompt per screen: `{STYLE}` + canvas + section-by-section content with the real copy, the band color of each section and how it transitions to the next + `{NEGATIVE}`.

**Desktop (presentation shot):**
```
{STYLE}
Canvas: 1440px-wide full landing page for {BRAND} shown as a Dribbble presentation: two long page columns side by side on a neutral backdrop.
Sections top to bottom (band color → transition → next):
1. Nav on {COLOR}: wordmark, 4-5 links, one action pill.
2. Hero on {COLOR}: huge headline "{HEADLINE}", one short line, one primary pill; signature illustration {SIGNATURE} (vector + soft 3D, lit from {LIGHT}); one image placeholder labeled "{PHOTO_1}". Transition: {TRANSITION_1}.
3..N. {SECTION}: {essentials only}; {what is behind the interaction, one item shown open}; placeholders labeled {PHOTOS}. Transition: {TRANSITION_N}.
N+1. Booking/contact block with the real controls (date picker, chips, WhatsApp preview bubble).
N+2. Footer on {DARK}: 4 small columns with real contact data, giant wordmark in the display font.
{NEGATIVE}
```

**Mobile (3–4 screens in one image):**
```
{STYLE}
Canvas: 4 iPhone screens (390x844) of the {BRAND} site side by side, flat, no device frames, 32px corners.
Screen 1 hero · Screen 2 signature interaction open (hotspot/accordion) · Screen 3 {content} · Screen 4 booking with sticky action.
Same bands, fonts and illustrations as desktop; 44px tap targets; 20px margins.
{NEGATIVE}
```

## 3. Per-tool notes (creative generators first)
- **GPT Image 2.5 Sunburst (default):** use the §2.3 structure. Sunburst for quality and precise edits; Flare only for fast drafts.
- **Midjourney v7:** best for creative layouts. Put the style block last and add `--ar 2:3 --style raw --stylize 250 --chaos 15`. Use `--sref` with a Dribbble shot you like to lock the style. Text will be approximate, so treat it as layout and mood.
- **Ideogram 3 / Recraft v3:** best for legible UI text and vector-style art. Recraft: use a "vector illustration" or "digital illustration" style for the art.
- **GPT Image / ChatGPT:** paste as is, portrait 1024x1536, ask for "legible text, empty image placeholders".
- **Nano Banana (Gemini):** generate desktop first, then "same brand, now the mobile screens".
- **Figma Make / Google Stitch / v0:** paste the section list as the brief; they output editable frames, good for option A.

## 4. Deliver to the user
One message per item, easy to copy:
1. The 5–7 line concept (with the researched facts that will appear).
2. The desktop prompt (also as a .txt file).
3. The mobile prompt (also as a .txt file).
4. One line: "Generate and send the images back (I'll clone them pixel by pixel, replacing the placeholders with the real photos), or reply 'build'."
Record the pack in `qa/prompt-pack.md`.

## 5. Checks before sending
- No prompt asks for a photo; every photo slot is a labeled placeholder.
- Palette and fonts are named, owned and not the AI default; each section has its band color and transition.
- Content is complete (every real fact has a home) but the visible surface is minimal; the disclosure pattern is described.
- Illustrations specify light direction, depth and the 3D objects; they can loop.
- Same style block and negative block in every prompt; desktop and mobile describe the same brand; copy is real, humanized, no em-dashes.
