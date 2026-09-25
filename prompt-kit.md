# Prompt Kit: Creative Minimal (no-reference projects)

When the user asks for a site or app **without a reference image**, deliver a **prompt pack** that generates the reference screens (desktop + mobile) in the user's chosen style. The user then picks one of two options:
- **A) Generate the images** in an image model, send them back, and the build continues on **Path A** (pixel-by-pixel from the generated screens).
- **B) Build without generating.** The prompt pack becomes the spec: its style block, sections and copy are written into `direction.md`, and the build follows Path B.

The style comes from 7 studied references in `references/creative-minimal/`: Wandor, Mugic, ShipSphere, FNJ, Finley, Odella and Oriel. When the image tool accepts image inputs, attach 1–2 of them as **style references** (not content).

## 1. Style DNA ("creative minimalist, human-made")
What makes these read as designed by a person:
1. **Airy light canvas.** White or warm off-white (#FAF8F5, #F7F7F5) sections, generous whitespace, content max ~1200px, and one confident brand hue plus 3–4 soft pastel tints (peach, mint, lavender, pink, sky).
2. **Headline voice.** A large geometric or grotesk sans (Outfit, General Sans, Satoshi or Inter Display character), weight 500–600, tight tracking (-0.02 to -0.03em), deep ink color (navy, forest or near-black) instead of pure black. **One twist per headline**: an italic serif phrase ("finally understood."), a second line in muted gray ("Oriel does the rest."), or one or two words in the brand color.
3. **One signature hero metaphor** that could only belong to this brand. The references do it this way:
   - Wandor: a sticker-collage panorama of world landmarks with a wavy cut-out edge.
   - Mugic: the product as a physical object (a lavender device with a dot-matrix speaker).
   - ShipSphere: an isometric pastel supply-chain loop.
   - FNJ: a pixel-mosaic block holding the input.
   - Finley: a phone in a hand over a green gradient.
   - Oriel: a sky with clouds and floating UI cards around a phone.
4. **Real product fragments.** Small floating UI cards with believable data (exact figures, +8.4% chips, dates, names), mini dashboards inside feature cards, and a product screenshot framed by something ownable (a flower wreath, a soft-tinted stage).
5. **One illustration system per brand.** Same stroke, shading and palette everywhere, from hero to feature icons to footer. Flat pastel isometric, sticker collage, and soft line-plus-fill are the three seen.
6. **Section rhythm.** A centered hero, then sections alternating "title left / short paragraph right" headers, a **bento grid** of soft-tinted panels (1px hairline borders, 12–16px radii, no heavy shadows), a stats row with 3–4 large numbers, a colored testimonial card marquee, 2–3 column pricing with the middle plan filled in the brand color, an FAQ accordion, a final CTA band, and a footer with 3–4 link columns.
7. **Human touches.** Playful physical metaphors (a notebook spiral binding between step cards, an airplane window, a cable hanging from the pricing card), tiny inline illustrations inside sentences, and a **giant brand wordmark** closing the footer (colorful letter-shapes, a fading gradient, or a landmark collage).
8. **Controls.** Small pill buttons: a filled deep-color primary and a ghost or outline secondary. A small announcement pill ("New · …") is allowed only as a clickable link chip, never as a decorative eyebrow label.
9. **Mobile is designed, not squeezed.** The same hero metaphor recomposed vertically, bento panels stacked full-width, a sticky compact nav with a menu sheet, stats as a 2×2 grid, a swipeable testimonial row, and pricing cards stacked with the popular plan first.

## 2. Build the pack
Fill these from the brief before writing prompts, and show them to the user in 5 lines:
`BRAND` (name + one-line product truth) · `MODE` (Persuade/Experience/Read/Operate) · `HUE` (brand color hex + pastel tints) · `METAPHOR` (the ownable hero idea) · `ILLUSTRATION` (one system) · `TYPE` (display + body families) · `SCREENS` (list).
Invent a metaphor that is **specific to the product's world**; never reuse one of the 7 references literally.

### 2.1 Style block (paste into every prompt, unchanged)
```
Style: creative minimalist product website, human-made craft, Dribbble/Behance shot quality.
Light airy canvas (#FAF8F5 / white), generous whitespace, 12-column grid, max content width 1200px.
Brand color {HUE} used sparingly, with soft pastel tints {TINTS} for panels.
Headlines in a geometric sans ({DISPLAY}), weight 500-600, tight tracking, deep ink color {INK};
one headline twist: {TWIST}. Body in {BODY}, small and quiet, muted gray.
Illustration system: {ILLUSTRATION}, identical style everywhere.
Soft-tinted bento panels with 1px hairline borders and 14px radius, no heavy drop shadows.
Small pill buttons (filled {INK or HUE} primary, outline secondary). Crisp realistic UI fragments with believable data.
Pixel-perfect alignment, consistent spacing rhythm (8px scale), readable real English/Portuguese copy, no lorem ipsum.
```

### 2.2 Negative block (append to every prompt)
```
Avoid: generic SaaS template, purple-blue gradient blobs, glassmorphism, neon, dark mode, stock photos of people at laptops,
3D clay characters, emoji icons, random decorative shapes, cluttered layout, tiny unreadable gibberish text, misaligned grids,
heavy shadows, gradient text, eyebrow labels above headings, fake logos with typos, watermark, device mockup tilted at extreme angles.
```

### 2.3 Screen prompts
Write **one prompt per screen**. Every prompt has: `{STYLE}` + canvas + section-by-section content (with the real copy) + `{NEGATIVE}`.

**Desktop, full landing page (presentation shot):**
```
{STYLE}
Canvas: 1440px-wide full-length landing page for {BRAND}, shown as a tall Dribbble presentation:
two long page columns side by side on a light gray (#ECECEC) backdrop, page corners rounded 16px.
Sections top to bottom:
1. Nav: wordmark "{BRAND}" left, 3-4 links center, "{CTA}" pill right.
2. Hero: centered headline "{HEADLINE}" ({TWIST}), one-line subhead, primary + secondary pill; signature visual: {METAPHOR}.
3. Social proof: a row of 5-6 muted monochrome partner logos.
4. Section header left "{SECTION_TITLE}" / short paragraph right; bento grid of {N} soft-tinted panels, each with a small real UI fragment: {FRAGMENTS}.
5. Stats row: {STAT_1}, {STAT_2}, {STAT_3}, {STAT_4} as large numbers with tiny captions on pastel-topped tiles.
6. Testimonials: horizontal row of colored cards (peach, mint, lavender, pink) with quote, name, role.
7. Pricing: {PLANS}; middle plan filled with brand color and a "Popular" pill.
8. FAQ: title left, accordion right with 5 questions, first one open.
9. Final CTA band with {METAPHOR_ECHO}.
10. Footer: 4 link columns, social icons, then a giant "{BRAND}" wordmark {WORDMARK_TREATMENT}.
{NEGATIVE}
```

**Mobile, key screens (one image, 3–4 phones):**
```
{STYLE}
Canvas: 3 to 4 iPhone-size screens (390x844) of the {BRAND} {site|app}, laid flat side by side on a light gray backdrop, no device frames, 32px rounded screen corners.
Screen 1 - Hero: compact nav with wordmark + menu icon, headline "{HEADLINE}" stacked in 3 short lines, subhead, full-width pill CTA, {METAPHOR} recomposed vertically.
Screen 2 - Features: bento panels stacked full-width, each with one real UI fragment.
Screen 3 - Stats 2x2 + swipeable testimonial card row with pagination dots.
Screen 4 - Pricing stacked, popular plan first, FAQ accordion, footer with giant wordmark.
Thumb-friendly 44px tap targets, 20px side margins, same typography and colors as desktop.
{NEGATIVE}
```

**App (Operate mode), one prompt per flow:**
```
{STYLE}
Canvas: {N} mobile app screens (390x844) for {BRAND}, side by side, flat, no device frames.
{SCREEN_1}: {purpose}, top app bar "{title}", {content blocks with real data}, bottom tab bar with {4-5 tabs}.
{SCREEN_2}: ...
Calm, scannable, brand color only on primary actions and active states; illustrations only in empty states and onboarding.
{NEGATIVE}
```
Add a desktop dashboard prompt when the app also has a web version (sidebar + header greeting + 3 metric cards + main chart + activity list + one "suggested next step" card).

## 3. Per-tool notes
- **GPT Image / ChatGPT:** paste the prompt as is, size 1024x1536 (portrait) for full pages. Ask for "legible text"; regenerate only the screens that fail.
- **Nano Banana (Gemini image):** attach 1–2 reference JPGs from `references/creative-minimal/` as style references. It keeps consistency across edits, so generate desktop first, then ask "same brand, now the mobile screens".
- **Midjourney v7:** put the style block last and add `--ar 2:3 --style raw --stylize 150`. Use `--sref` with a reference image URL for style lock. The text will be approximate, so treat the output as layout and mood.
- **Figma Make / Google Stitch / v0:** paste the section list as the brief. They output editable screens, which are ideal for option A.

## 4. Deliver to the user
Send the pack in this order, in one message per prompt so each is easy to copy:
1. The 5-line concept (BRAND, MODE, HUE, METAPHOR, ILLUSTRATION).
2. The desktop landing prompt.
3. The mobile prompt (or the app prompts).
4. One line: "Generate and send the images back (I'll clone them pixel by pixel), or reply 'build' and I'll build straight from this direction."
Record the pack in `qa/prompt-pack.md`.

## 5. Checks before sending
- The metaphor belongs to this product only, and the copy is real, specific and humanized, with no em-dashes.
- The same style block appears in every prompt, and desktop and mobile describe the same brand.
- Every section has concrete content (numbers, names, labels), not "some features".
- The negative block is attached to every prompt.
