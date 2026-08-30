# AGENTS.md — Goldstein Single-HTML Codex Instructions

These instructions apply to this project directory and every file below it unless a more specific `AGENTS.md` exists deeper in the tree.

## NON-NEGOTIABLE PROJECT FORMAT

This project must stay extremely simple.

The intended working structure is:

```text
project/
├── AGENTS.md
└── goldstein-emergency-plumbing.html   # or the single target .html file named by the user
```

**All webpage implementation must live in ONE HTML file.**

That single HTML file must contain:

- all HTML markup;
- all page CSS inside `<style>` tags;
- all page JavaScript inside `<script>` tags;
- header markup and styling;
- every page section in DOM order;
- footer markup and styling;
- responsive CSS;
- interactions and small page behavior;
- SVG icons inline when practical;
- existing external image/font/CDN URLs when already used by the reference.

Do **not** create separate files such as:

```text
styles.css
style.css
script.js
main.js
app.js
components/
src/
public/
dist/
build/
package.json
vite.config.*
webpack.config.*
```

Do not split the page into components, templates, includes, modules, or partials unless the user explicitly asks for that later.

Do not create new local image/asset files just to reorganize the page. Keep usable existing asset URLs directly in the HTML. If the user later supplies new assets or explicitly requests generated/local assets, follow that request.

## DESIGN SOURCE OF TRUTH

The canonical design reference is the single file:

```text
goldstein-emergency-plumbing.html
```

If the actual filename contains a suffix such as `(10)`, use that exact existing file instead. Do not rename, duplicate, or replace files unless the user asks.

This `AGENTS.md` contains the condensed design system and workflow rules. There is **no separate `style.md` requirement**.

Priority order:

1. User's latest instruction.
2. This `AGENTS.md`.
3. The effective/final styling and structure in `goldstein-emergency-plumbing.html`.
4. Existing target-page code that the user has not asked to change.

The reference HTML contains historical CSS revision blocks and later overrides. CSS cascade order matters. **Later effective rules win.** Never copy an early rule without checking whether a later rule supersedes it.

---

# START-OF-SESSION RULE — ANALYZE ONLY

When the user starts a new Codex session with an analysis request, the first pass must be **READ-ONLY**.

During that first pass:

1. Read this `AGENTS.md` completely.
2. Locate the single requested/reference HTML file.
3. Read and analyze that HTML file.
4. Identify its structure: header, sections in DOM order, footer, CSS blocks, responsive rules, JavaScript, forms, assets, and important shared behavior.
5. Identify the final/effective design rules, especially later CSS overrides.
6. Report a concise section-by-section implementation map.
7. Report any important constraints or fragile behavior.
8. **DO NOT edit, create, delete, rename, format, or move any project file.**
9. **DO NOT run a browser preview.**
10. **DO NOT start a dev server.**
11. **DO NOT run build/test/npm commands.**
12. Stop after the analysis and wait for the user's next instruction.

If the first user prompt says only to scan/analyze, **making even a harmless formatting change is not allowed**.

---

# FAST EDIT MODE

After the user explicitly tells you to implement or edit something, work directly in the single HTML file.

Default workflow:

```text
read the relevant HTML/CSS/JS range
→ edit only the requested section
→ perform lightweight code sanity checks
→ report exactly what changed
```

Unless the user explicitly asks for visual/browser verification, DO NOT:

- launch a browser preview;
- open Chrome/Chromium;
- use Playwright, Puppeteer or Selenium;
- take screenshots;
- run visual-diff tooling;
- start localhost/Vite/Live Server only for preview;
- repeatedly reload a browser;
- run Lighthouse;
- install browser packages;
- browse unrelated websites;
- perform long UI exploration before editing.

Unless explicitly requested or absolutely required, DO NOT run:

```text
npm install
npm ci
npm run dev
npm run build
npm test
npm run test
npm run lint
npx playwright ...
npx vite ...
webpack ...
```

Do not install dependencies for this project just to edit a self-contained HTML page.

Lightweight checks are allowed, for example:

- targeted text search;
- inspect the edited line range;
- basic HTML/CSS/JS syntax sanity checks;
- `git diff -- <single-html-file>` if Git is available;
- `git status --short` when useful.

Do not recursively scan `node_modules`, `.git`, `dist`, `build`, caches, or unrelated project folders.

---

# SECTION-BY-SECTION WORKFLOW

When cloning/building a Goldstein service page, work in this sequence unless the user's target page intentionally differs:

```text
1. Shared header
2. Hero
3. Response / benefits
4. Services
5. Process
6. Trust
7. Service area
8. Reviews
9. FAQ
10. Quote / contact
11. Shared footer
```

When asked for one section:

- change that section only;
- change shared styles only when required for that section;
- keep already-approved sections unchanged;
- do not redesign later sections;
- do not reorder unrelated markup;
- do not perform broad refactors for cleanliness;
- do not convert the file into a framework.

When asked for the whole page, still build it in the sequence above and preserve completed sections while moving forward.

---

# SINGLE-FILE IMPLEMENTATION RULES

## CSS

All owned CSS stays in `<style>` tags in the single HTML file. Prefer organized comment blocks, for example:

```html
<style>
  /* ===== RESET / TOKENS ===== */
  /* ===== HEADER ===== */
  /* ===== HERO ===== */
  /* ===== SERVICES ===== */
  /* ===== PROCESS ===== */
  /* ===== TRUST ===== */
  /* ===== AREA ===== */
  /* ===== REVIEWS ===== */
  /* ===== FAQ ===== */
  /* ===== QUOTE ===== */
  /* ===== FOOTER ===== */
  /* ===== RESPONSIVE ===== */
</style>
```

Do not move these styles into a separate stylesheet.

## JavaScript

All owned page behavior stays in `<script>` tags near the end of the same HTML file unless the existing reference intentionally places a critical script elsewhere.

Do not create a separate JS file.

## Icons

Prefer existing inline SVG patterns from the reference. Do not add an icon library dependency when a simple inline SVG is enough.

## Images

Preserve working reference URLs and existing local paths. Do not download/re-encode every image unless the user asks. Do not invent different photography if the user asks for an exact clone.

## Fonts

The design may load Google Fonts/CDN font resources from `<head>`. External font requests are acceptable because the page implementation itself remains a single HTML file.

---

# CRITICAL BEHAVIOR — DO NOT BREAK

The reference page is deliberately self-contained and its owned header/page/footer behavior must be preserved.

## Lead form

Preserve the lead endpoint when present:

```html
<form action="/api/lead" method="post">
```

Do not add a page-level submit handler that prevents the existing shared lead logic from working. Do not casually remove hidden attribution fields, validation, CTA/page values, or the existing safety-net behavior.

## Sticky header

Do not fix horizontal overflow by putting `overflow-x:hidden` on an ancestor that must allow `position: sticky` to work.

Use the established `overflow-x: clip` approach where applicable.

Preserve the scroll state/class behavior that changes the header background when it becomes stuck.

## Anchor offsets

Preserve the in-page jump behavior that prevents headings from landing underneath the pinned header.

## Existing interactions

Preserve working mobile-menu, FAQ, review, map, quote-form and other existing interactions unless the user explicitly asks to alter them.

---

# DESIGN SYSTEM

## 3. Brand personality

The design should feel:

- Premium but practical.
- High-trust home service, not a SaaS landing page.
- Strong, cinematic and photo-led.
- Clean, highly legible and conversion-focused.
- Dark navy sections alternating with bright off-white sections.
- Gold used as a controlled accent, not as a full background everywhere.
- Bright blue used for plumbing/service cues and secondary emphasis.
- Photography should feel real, local and service-specific: technicians, plumbing work, branded vehicles, tools, pipes, homes and actual repair scenarios.
- Avoid generic abstract illustrations when a real service photo would communicate the job better.

Do not introduce unrelated colors, neon gradients, purple, generic black, glass-heavy crypto styling, or rounded-everything SaaS aesthetics.

---

## 4. Typography

### Display / headings

Primary display family:

```css
font-family: "Barlow Condensed", "Arial Narrow", Impact, sans-serif;
```

Use for:

- H1
- H2
- Major service-card headings
- Process-card headings
- Large phone numbers / strong CTA display text

Typical characteristics:

```css
font-weight: 400; /* page display headings */
letter-spacing: .012em;
text-transform: uppercase;
line-height: .95 - 1.02;
```

For the quote/footer promotional display treatment, use the stronger italic style:

```css
font-family: "Barlow Condensed", Poppins, sans-serif;
font-weight: 800;
font-style: italic;
text-transform: uppercase;
```

### Body / UI

```css
font-family: "Poppins", Arial, sans-serif;
```

Supported weights in the reference:

```text
400 / 500 / 600 / 700 / 800
```

Use Poppins for:

- Body copy
- Eyebrows
- Navigation
- Buttons
- Form fields
- FAQ text
- Trust proof text
- Review copy
- Footer links

### Heading behavior

Headings in dark bands inherit white. Headings in light bands inherit dark ink/navy. Do not allow the WordPress theme to force headings to `#242424`; the reference explicitly restores heading color inheritance.

---

## 5. Core color system

### Main service-page tokens (`.gpe`)

```css
--ink:         #06101F;
--navy:        #011226;
--deep:        #021A33;
--blue:        #086BD8;
--blue-bright: #0596FF;
--gold:        #F9A401;
--gold-light:  #FFBD18;
--paper:       #F1F1F1;
--white:       #FFFFFF;
--muted:       #AEB7C3;
```

### Shared-header tokens (`.gpx`)

```css
--gp-navy: #001327;
--gp-bar:  #004B8E;
--gp-strip:#034E91;
--gp-gold: #E6AF1C;
--gp-ink:  #0B1220;
```

### Footer tokens (`.gpf`)

```css
background: #040B18;
--fgold: #F0B21E;
color: #D8DCE3;
```

### Useful supporting colors

```css
Trust navy:            #0E2A52;
Brand blue:            #004B8E;
Body gray on light:    #4A5768 / #4A5A70;
FAQ navy:              #01152B;
Quote navy:            #04162C;
Process deep field:    #06101F / #081426;
Service-area deep:     #06101F / #08182C;
Focus blue:            #48A9FF;
Focus gold:            #FFC527;
```

### Color usage rule

Use navy as the structural base, gold as the primary accent/CTA, bright blue as a service/technical accent, white/off-white for contrast, and muted blue-gray for supporting text. Never replace the Goldstein navy with near-black unless the reference section specifically uses the footer `#040B18`.

---

## 6. Width system and page gutters

### Main page shell

```css
--shell: 1170px;

.pageShell {
  width: min(1170px, calc(100% - 96px));
  margin-inline: auto;
}
```

Desktop side gutter is therefore approximately `48px` until the max width is reached.

### Tablet / smaller screens

At `<= 900px`:

```css
.pageShell {
  width: min(calc(100% - 40px), 720px);
}
```

At `<= 680px`:

```css
.pageShell {
  width: calc(100% - 36px);
}
```

### Wide components

The quote and footer intentionally use a wider shell than the main content:

```css
.gs-quote__in {
  width: min(94%, 1680px);
}

.gpf__in {
  width: min(94%, 1720px);
}
```

Do not force every section into one identical width. Main editorial sections use the 1170px shell; the quote/footer use the wider 94% presentation shell.

---

## 7. Vertical rhythm

The page is built from substantial full-width bands rather than small isolated blocks.

Use these general desktop spacing ranges:

```text
Large section top/bottom padding: 60–120px
Regular section top/bottom padding: 44–76px
Heading → body gap: ~18–30px
Eyebrow → heading: ~18px plus underline rule
Card grid gap: ~18–24px
Button groups: ~12–14px
```

Use `clamp()` for wide-screen scaling where helpful. Do not add arbitrary 150–250px white gaps between sections.

Section seams are designed to feel continuous. Do not insert decorative horizontal rules between major bands unless the reference specifically has one.

---

## 8. Eyebrows and accent rules

Standard eyebrow:

```css
.eyebrow {
  display: inline-flex;
  align-items: center;
  margin-bottom: 18px;
  padding-bottom: 12px;
  font-size: 15px;
  font-weight: 700;
  letter-spacing: .025em;
  text-transform: uppercase;
}
```

The underline is approximately:

```css
width: 82px;
height: 3px;
border-radius: 10px;
background: currentColor;
```

Dark bands normally use gold eyebrows. Light bands often use brand blue.

---

## 9. Buttons

### Primary pill button

```css
.button {
  display: inline-flex;
  min-height: 46px;
  align-items: center;
  justify-content: center;
  gap: 9px;
  padding: 0 25px;
  border-radius: 999px;
  font-size: 13px;
  font-weight: 700;
  letter-spacing: .015em;
  text-transform: uppercase;
}
```

### Gold CTA

```css
.buttonGold {
  color: #09101A;
  border-color: #F9A401;
  background: linear-gradient(90deg, #FFB208, #FFBD19);
  box-shadow: 0 8px 24px rgba(249,164,1,.16);
}
```

### Outline CTA on dark sections

```css
.buttonOutline {
  color: inherit;
  border: 1px solid rgba(249,164,1,.5);
  background: rgba(1,18,38,.38);
}
```

### Outline CTA on light sections

```css
.lightSection .buttonOutline {
  border-color: #9AA5B2;
  background: rgba(255,255,255,.5);
}
```

### Motion

```css
:hover  -> translateY(-2px), slight brightness/shadow increase
:active -> translateY(0) scale(.985)
```

Buttons on narrow mobile layouts can become full width with minimum touch height around `46–50px`.

---

## 10. Card language

Common Goldstein card characteristics:

- Border radius: typically `13–20px`.
- Fine cool-gray or blue border.
- Shadows are soft, not huge blurred blobs.
- Dark-section cards can use layered navy/blue glass treatment, but keep it restrained.
- Light-section cards should usually be solid or near-solid white.
- Icon accents are either Goldstein gold or plumbing blue.
- Hover lift is small: around `3–6px`.

### Light service cards

Final service-card direction:

```css
border-radius: 18px;
border: 1px solid #C5C9CF;
background: rgba(255,255,255,.68);
box-shadow: 0 8px 24px rgba(9,21,37,.04);
```

The final desktop cards are visually larger than the earliest rules in the file:

```text
minimum height: about 310px
image height: about 205px
icon badge: about 54px
```

Do not copy the smaller historical `252px / 158px` card sizing when cloning the approved visual.

---

## 11. Shared header (`.gpx`)

The shared header is an important part of the visual identity. Reuse it instead of inventing a page-specific navigation.

### Header palette

```css
Top bar:    #004B8E
Main navy:  #001327
Gold:       #E6AF1C
White text: #FFFFFF
```

### Desktop top bar

- Social icons on the left.
- Address/email/phone information aligned across the row.
- Gold icons.
- Maximum inner width about `1660px`.
- Typical inner padding `10px 32px`.

### Desktop nav

- Large Goldstein logo on left.
- Navigation centered.
- Gold rounded “Book Now” CTA on right.
- White nav links.
- Active link uses gold underline.
- Dropdowns are dark navy panels with clean hover/focus behavior.

Normal desktop nav target height is approximately `126px` before sticky compression.

### Header over full-bleed hero

For hero pages using the overlaid header mode:

- Hero is pulled up behind the nav.
- Top bar remains solid.
- Unstuck nav is transparent / uses a dark-to-transparent legibility gradient.
- Do **not** create a solid navy rectangle over the hero before scrolling.

### Sticky / scrolled state — MUST MATCH

The custom header is sticky:

```css
.gpx {
  position: sticky;
  top: -49px;   /* desktop: top bar scrolls away */
  z-index: 60;
}
```

On small mobile:

```css
top: -56px;
```

JavaScript adds `.is-stuck` after the page scrolls past the top-bar height.

When stuck:

```css
.gp-nav {
  height: 100px;
  background: #001327;
}

.gpx.is-stuck {
  box-shadow: 0 8px 26px rgba(0,0,0,.34);
}

.gp-nav__logo img {
  max-height: 76px;
}
```

On small mobile the stuck nav is approximately `74px` high and the logo max-height is approximately `56px`.

### Critical sticky-header rule

Do **not** use this on the page body:

```css
overflow-x: hidden;
```

It can create a scroll container and break `position: sticky`.

Use:

```css
body.gpe-full {
  overflow-x: clip !important;
  overflow-y: visible !important;
}
```

### Mobile header

At about `<=1024px`:

- Hide desktop nav links and desktop CTA.
- Show burger button.
- Burger target approximately `46x46px`.
- Main mobile nav row minimum height approximately `78px` in the final shared header rules.
- Drawer is a fixed full-screen dark navy overlay.
- Drawer closes on link click or Escape.
- Do not let theme button styles collapse the three burger bars; explicitly stretch the burger and give each bar `width:100%` and `height:3px`.

---

## 12. Hero section

### Visual structure

- Full-width deep navy band.
- Cinematic service photo concentrated toward the right.
- Copy column on the left.
- Dark left scrim for readability on desktop.
- H1 uses large condensed uppercase display typography.
- Primary phrase/city/service word can be gold.
- Two CTA buttons.
- Trust proof row below the CTA area.

### Desktop sizing

```css
.hero {
  min-height: max(570px, calc(100svh - 167px));
  background: #001327;
}

.hero h1 {
  font-size: clamp(54px, 5vw, 67px);
}

.heroCopy {
  width: ~520px;
}
```

Body lead is intentionally much smaller than the display heading, around `14px`, with a readable max width.

### Image treatment

The final hero does not simply use `background-size: cover` everywhere. On desktop the composition keeps the service image anchored to the right and layers vertical + horizontal gradients for a clean transition into the next dark band.

Rule of thumb for new hero imagery:

- Leave copy-safe negative space on the left.
- Keep the technician/work subject visible on the right or center-right.
- Avoid putting critical visual detail under the nav.
- Use natural lighting and realistic service activity.

### Mobile hero

On mobile the copy moves above the photo. Because copy is no longer over the photo, do not keep the heavy desktop left scrim over the mobile image. The mobile picture should stay visibly photographic and only feather at its top/bottom edges.

---

## 13. Response / benefits section

Purpose: immediately reassure the user after the hero.

Visual direction:

- Dark `#021A33` band.
- Real plumbing/service photo blended into the band.
- Left copy column.
- Large condensed H2 around `64px` desktop.
- Short explanatory paragraph.
- Feature list with round/outlined service icons.
- Wide CTA panel near the bottom.

Use image masking/gradients to transition smoothly from hero into this section. Avoid obvious hard edges between full-width photos.

---

## 14. Services section

Background: light paper/off-white.

Layout:

```text
Eyebrow + large heading on left
Supporting paragraph on right
3-column service card grid on desktop
CTA rail/card below
```

Desktop service grid:

```css
grid-template-columns: repeat(3, 1fr);
gap: ~22–24px;
```

Cards:

- Large real service photo at top.
- Blue icon badge overlapping photo/content edge.
- Centered condensed uppercase heading.
- Short supporting description.
- White/light-gray card surface.
- Fine border + subtle hover lift.

Responsive:

- `<=900px`: commonly 2 columns.
- `<=680px`: 1 column.

---

## 15. Process / “How it works” section

Final approved process treatment uses a built dark field, not the older full-width background photograph.

Background:

```css
radial-gradient(...blue glow...),
radial-gradient(...gold glow...),
linear-gradient(180deg, #06101F 0%, #081426 55%, #06101F 100%);
```

A subtle 64px grid texture is layered over the field.

### Timeline

Desktop:

- 3 equal steps.
- Horizontal gold rail behind numbered markers.
- Each step contains a photo on top and a card beneath it.

```css
.gpeTl__rail {
  grid-template-columns: repeat(3, minmax(0,1fr));
}
```

Step image:

```css
aspect-ratio: 16 / 10;
border-radius: 16px 16px 0 0;
object-fit: cover;
```

Step card final treatment:

- Deep blue translucent gradient.
- Thin blue border.
- Subtle backdrop blur.
- White heading.
- Cool blue-gray body text.
- Gold icon treatment.

Mobile:

- Rail becomes vertical.
- Steps become one column.
- Number marker aligns to the vertical rail.
- Explicitly set step/card/image widths to 100% to avoid overflow differences between browsers.

---

## 16. Trust section

Final approved trust band is LIGHT, even though older rules in the reference may show a darker iteration.

Background:

```css
linear-gradient(180deg, #FFFFFF 0%, #F6F8FB 55%, #EEF2F7 100%);
```

Layout:

- Copy left.
- Technician/service photo on right.
- Photo fades westward into the light background.
- Large navy heading.
- Plumbing/brand word can use `#004B8E`.
- Gas/accent word can use `#E6AF1C`.
- Trust proof cards are SOLID white, not translucent glass over the photo.

Trust proof cards:

```css
background: #FFFFFF;
border: 1px solid #E3E9F1;
box-shadow: 0 10px 26px rgba(6,19,31,.07);
```

Main trust heading:

```css
font-size: clamp(34px, 4.1vw, 60px);
line-height: 1;
```

---

## 17. Service area section

Final approved treatment uses a real interactive map, not the older full-bleed location illustration.

Background:

```css
radial-gradient(80% 70% at 78% 22%, rgba(0,75,142,.30), transparent 62%),
linear-gradient(180deg, #06101F 0%, #08182C 55%, #06101F 100%);
```

Desktop split:

```css
grid-template-columns: minmax(0,.86fr) minmax(0,1.14fr);
gap: clamp(26px, 3.4vw, 58px);
```

Map:

```css
height: clamp(420px, 46vw, 560px);
border-radius: 20px;
border: 1px solid rgba(120,170,255,.30);
box-shadow: 0 26px 60px rgba(0,0,0,.45);
```

At roughly `<=979px` the area becomes one column and map height is around `440px`.

City links use compact rows with gold map-pin icons. On smaller phones use two columns down to ~340px, then one column only when necessary.

---

## 18. Reviews section

Final approved review treatment:

- Light background: white to very pale gray.
- Centered heading.
- Small gold rule above heading.
- Google/review badge directly under/near heading.
- **One** continuous marquee row in the final design; the second reverse row is intentionally disabled.
- Review cards should be equal height.
- No WordPress/Woodmart blue blockquote border.

Heading:

```css
color: #001327;
font-size: clamp(34px, 4.2vw, 62px); /* final refined range */
line-height: ~1.02;
```

Marquee final speed is approximately `38s` for a full cycle in the reference.

Respect `prefers-reduced-motion`; allow the review strip to pause / become horizontally scrollable instead of forcing animation.

---

## 19. FAQ section

Background:

```css
#01152B
```

Layout:

- Copy/accordion on left.
- Technician photo on right.
- Photo fades into navy with a horizontal scrim.
- Large condensed H2 around `58px` desktop.
- Accordion rows are dark blue cards rather than plain text separators in the final refinement.

Final FAQ item feel:

```css
border: 1px solid rgba(61,126,191,.28);
border-radius: 13px;
background: rgba(2,23,43,.72);
```

Hover/focus:

- Stronger blue border.
- Slightly brighter navy background.
- Fine gold inset edge.
- Small `translateX(3px)` movement.

Summary target should be comfortably tappable; reference refined rows to around `62px` minimum height.

---

## 20. Quote / contact section

Background base:

```css
#04162C
```

This is a wide presentation band with a large service/vehicle image plate and a dark form card.

Desktop inner grid:

```css
.gs-quote__in {
  width: min(94%, 1680px);
  grid-template-columns: 36% 1fr;
  gap: clamp(24px, 4vw, 90px);
}
```

Display heading:

```css
font-family: "Barlow Condensed", Poppins, sans-serif;
font-weight: 800;
font-style: italic;
font-size: clamp(30px, 4.5vw, 80px);
line-height: .95;
text-transform: uppercase;
```

Form card:

```css
background: rgba(6,14,30,.93);
border: 2px solid rgba(240,178,30,.85);
border-radius: clamp(10px,1vw,18px);
box-shadow: 0 24px 60px rgba(0,0,0,.45);
```

The form card uses a subtle clipped-corner shape. Preserve the strong dark-card + gold-rim visual.

### Form contract — do not break

When reusing this form pattern:

```html
<form action="/api/lead" method="post" ...>
```

Expected names include:

```text
page
cta
name
phone
email
service
message
```

Do not add a page-level submit handler that intercepts the form with `preventDefault()` before the shared lead handler can claim it.

---

## 21. Footer (`.gpf`)

Footer background:

```css
#040B18
```

Main footer width:

```css
.gpf__in {
  width: min(94%, 1720px);
}
```

### CTA banner

- Large rounded glassy navy banner.
- Blue edge glow.
- Optional artwork image behind with mask.
- Large italic condensed headline.
- White + gold headline treatment.
- Phone number in gold.
- Gold pill CTA.

Typical banner radius:

```css
clamp(12px, 1.2vw, 24px)
```

### Footer grid

Desktop:

```css
grid-template-columns: 1.4fr repeat(4, 1fr);
```

Contains:

- Brand/logo + NAP information + social icons.
- Service/navigation link columns.
- Gold uppercase column headings.
- Fine divider lines.

Responsive:

- `<=1100px`: 3 columns and brand spans full row.
- `<=768px`: 2 columns.
- Very small mobile keeps two compact link columns where possible, with brand full width.

### Footer social buttons

- 40px circles.
- Gold border/icon.
- Hover: gold fill and dark icon.

---

## 22. Image direction

When new imagery is needed, match these principles:

1. Ultra-realistic service photography.
2. Natural or believable practical lighting.
3. Show actual plumbing/heating work clearly.
4. Avoid generic smiling-stock-model compositions.
5. Technician, tools and repair area should make sense together.
6. Keep text-safe negative space where the layout needs copy.
7. Branded vehicle/logo can appear only where it would naturally exist in the real scene.
8. Do not paste floating Goldstein logos onto random photo backgrounds as decorative overlays.
9. Prefer WebP/JPEG for photographic assets; keep SVG for icons.
10. Use `object-fit: cover` for card imagery and compose the crop deliberately.

---

## 23. Icon direction

Use clean line icons similar to the reference:

```css
fill: none;
stroke: currentColor;
stroke-width: ~1.7–2.2;
stroke-linecap: round;
stroke-linejoin: round;
```

Icons should be simple and recognizable:

- phone
- calendar
- shield/check
- clock
- droplet
- drain/pipe
- flame/gas
- wrench/tools
- map pin
- star/review
- arrow/chevron

Prefer inline SVG so the icon inherits current color and scales with the component.

---

## 24. Motion and interaction

Motion should be subtle and consistent.

### Scroll reveal

Reference reveal pattern:

```css
opacity: 0;
transform: translateY(18px);
transition:
  opacity .58s cubic-bezier(.22,.61,.24,1),
  transform .66s cubic-bezier(.16,.84,.44,1);
```

Visible state:

```css
opacity: 1;
transform: none;
```

### Timeline

- Gold line draws across on desktop.
- Gold line draws downward on mobile.
- Number markers scale/fade in after the rail.

### Cards / links

- Small hover lift only.
- Image zoom around `1.05–1.055` max.
- City links can translate right around `4px`.
- No large bouncing or looping hero animations.

### Accessibility

Always respect:

```css
@media (prefers-reduced-motion: reduce)
```

Disable reveal transforms, timeline animation and forced marquee motion for reduced-motion users.

---

## 25. Responsive breakpoints to preserve

The reference primarily uses these breakpoints:

```text
~1180px  header information reduction
~1100px  footer layout reduction
1024px   desktop header → mobile header/drawer
980px    service-area map stacks
900px    major page layouts become tablet/mobile
768px    header/footer mobile refinements
680px    most page sections become single-column phone layout
560px    compact location/list handling
480px    footer/link grid refinements
340px    very narrow single-column fallback
```

Do not design only for desktop. Preserve mobile touch targets and avoid horizontal overflow.

---

## 26. WordPress/live-site integration rules

These are part of the design implementation and must not be “cleaned up” casually.

### Body overflow for sticky header

Use:

```css
overflow-x: clip;
overflow-y: visible;
```

Do not use `overflow-x:hidden` on an ancestor of the sticky header.

### Theme heading override

Keep direct heading color inheritance so Woodmart does not force dark heading colors into dark sections.

### Full-width reset

The service page intentionally removes theme content padding/max-width around `.gpe` so the page bands are truly full width.

### Native theme footer/header

When the custom Goldstein `.gpx` / `.gpf` components are present, do not duplicate the Woodmart header/footer visually.

### Review blockquotes

Reset theme blockquote borders inside review components.

---

## 27. Section cloning workflow

When a user gives Codex a target screenshot/page and says “clone it using the Goldstein design,” follow this sequence:

```text
A. Shared header
B. Hero
C. Section 2 / response or first content band
D. Services / feature cards
E. Process
F. Trust
G. Service area
H. Reviews
I. FAQ
J. Quote/contact
K. Shared footer
```

For each section:

1. Inspect only that target section and the matching reference section.
2. Preserve the Goldstein typography, colors, button system and container rules.
3. Adapt content and imagery to the new service.
4. Keep the section responsive.
5. Do not disturb completed sections unless a shared token/component genuinely needs adjustment.
6. Continue in DOM order so spacing and seams remain predictable.

---

## 28. What NOT to copy from the reference

Do not blindly copy:

- Old CSS rounds that are later superseded.
- Decorative logo pseudo-elements that later rules remove.
- The older process background-photo treatment; final process uses a built dark field.
- The older service-area illustration; final service area uses a real map.
- The older dark trust treatment; final trust band is light.
- The second reverse review marquee row; final reviews use one row.
- Woodmart/theme header/footer markup.
- Theme-generated utility classes unless the target page actually needs them.
- Duplicate scripts or page-level form interception.

---

## 29. Quality checklist

Before considering a section finished, verify from code:

- [ ] Goldstein navy/blue/gold palette is used.
- [ ] Barlow Condensed is used for display headings.
- [ ] Poppins is used for body/UI.
- [ ] Main shell width follows the 1170px system unless the section is intentionally wide.
- [ ] Buttons match the pill/gold/outline system.
- [ ] Card radius and shadows match the reference.
- [ ] Image crop is service-specific and believable.
- [ ] Desktop and mobile rules exist.
- [ ] No accidental horizontal overflow is introduced.
- [ ] Sticky header contract is preserved.
- [ ] Existing forms and JavaScript behavior are not broken.
- [ ] No duplicate WordPress theme header/footer is introduced.
- [ ] Section order is correct.

---

## 30. Canonical instruction for Codex

When there is a visual disagreement between a new implementation and the reference:

> Prefer the final effective appearance of `goldstein-emergency-plumbing*.html`, interpreted through this `style.md`. Preserve the brand system first; adapt only content, service-specific imagery and section-specific layout requirements.


---

# FINAL CODEX BEHAVIOR CHECKLIST

Before editing, ask yourself:

- Am I editing only the single HTML file the user named?
- Did the user actually ask me to edit, or only to analyze?
- Am I preserving already-approved sections?
- Am I following the final effective reference styles rather than an obsolete earlier override?
- Am I avoiding separate CSS/JS/component files?
- Am I avoiding browser/build/npm work unless explicitly requested?
- Am I preserving sticky header and form behavior?

After an edit, report only:

1. which section was changed;
2. which single HTML file was changed;
3. any important behavior preserved;
4. whether any additional files were created — normally the answer must be **none**.

Do not claim visual verification unless the user explicitly asked for it and it was actually performed.
