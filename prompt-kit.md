# Prompt Kit: Figma-shot screens (no-reference projects)

This is the **v2 standard the user approved** (2026-09-25): flat color bands, owned palette and fonts, isometric vector hero with "+" hotspots, labeled image placeholders, minimal surface with content behind interaction. The paper/texture (v1.5.1) and all-typography (v1.5.2) variants were rejected; do not bring them back.

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
9. **Mobile is designed, not squeezed.** The same color bands, typography and illustrations recomposed for 390px, with a thumb-reachable sticky action and the same interaction patterns (accordions, sheets). The mobile image shows the screens **inside realistic iPhone mockups** (front view, not tilted).

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

### 2.3 Screen prompts
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
Canvas: 4 realistic iPhone 16 Pro mockups in a row, front view, straight (not tilted), natural titanium frame, Dynamic Island, thin even bezels, soft contact shadow under each phone, on a flat {BACKDROP} studio background. Each screen shows the {BRAND} site at 390x844, rendered flat and crisp inside the phone (the UI itself stays a clean Figma-style design; only the device is realistic).
Screen 1 hero · Screen 2 signature interaction open (hotspot/accordion) · Screen 3 {content} · Screen 4 booking with sticky action.
Same bands, fonts and illustrations as desktop; 44px tap targets; 20px margins.
{NEGATIVE}
```

## 3. Per-tool notes (creative generators first)
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
