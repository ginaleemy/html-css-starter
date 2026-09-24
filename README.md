# HTML & CSS Design Standards

## URL : https://ginaleemy.github.io/html-css-starter/
## 1. Purpose

This document is the design reference for all future HTML and CSS pages. It keeps typography, colours, spacing, shadows, border radii, page structure, reusable components, and responsive behaviour consistent.

Use the approved values in this guide instead of choosing arbitrary sizes for each page.

## 2. Measurement convention

Use `rem` for font sizes, spacing, widths, heights, border radii, and similar measurements.

Set the root font size once:

```css
html {
  /* 10px / 16px = 62.5%; therefore 1rem = 10px at the default browser size. */
  font-size: 62.5%;
}
```

With this convention:

```text
1px = 0.1rem
10px = 1rem
16px = 1.6rem
```

Use unitless values for `line-height` and `font-weight`. Use `em` for media-query breakpoints because media queries use the browser font size, normally `1em = 16px`.

## 3. Recommended project structure

```text
project/
├── index.html
├── css/
│   ├── general.css
│   ├── style.css
│   └── queries.css
├── js/
│   └── script.js
└── img/
    ├── logos/
    ├── icons/
    └── content/
```

### File responsibilities

| File          | Purpose                                                                                  |
| ------------- | ---------------------------------------------------------------------------------------- |
| `index.html`  | Semantic page structure and content                                                      |
| `general.css` | Design tokens, reset, typography, reusable layout classes and shared components          |
| `style.css`   | Styles for page-specific sections such as the header, hero, features, pricing and footer |
| `queries.css` | Responsive adjustments, ordered from the largest breakpoint to the smallest              |
| `script.js`   | Navigation, interactions and other behaviour                                             |

Load CSS files in this order so that page and responsive rules can override the base styles:

```html
<link rel="stylesheet" href="css/general.css" />
<link rel="stylesheet" href="css/style.css" />
<link rel="stylesheet" href="css/queries.css" />
```

## 4. Design tokens

Place the following variables near the top of `general.css`.

```css
:root {
  /* Colours */
  --color-primary: #e67e22;
  --color-primary-tint-1: #fdf2e9;
  --color-primary-tint-2: #fae5d3;
  --color-primary-tint-3: #eb984e;
  --color-primary-shade-1: #cf711f;
  --color-primary-shade-2: #45260a;

  --color-white: #fff;
  --color-grey-1: #888;
  --color-grey-2: #767676;
  --color-grey-3: #6f6f6f;
  --color-grey-4: #555;
  --color-grey-5: #333;

  /* Font weights */
  --font-weight-default: 400;
  --font-weight-medium: 500;
  --font-weight-semibold: 600;
  --font-weight-bold: 700;

  /* Line heights */
  --line-height-default: 1;
  --line-height-small: 1.05;
  --line-height-medium: 1.2;
  --line-height-paragraph: 1.6;
  --line-height-large: 1.8;

  /* Letter spacing */
  --letter-spacing-tight: -0.05rem;
  --letter-spacing-wide: 0.075rem;

  /* Border radii */
  --radius-default: 0.9rem;
  --radius-medium: 1.1rem;

  /* Shadows */
  --shadow-default: 0 2.4rem 4.8rem rgba(0, 0, 0, 0.075);

  /* Layout */
  --container-max-width: 120rem;
}
```

## 5. Typography system

### Font-size scale

| Pixels |      rem | Suggested use                      |
| -----: | -------: | ---------------------------------- |
|   10px |   `1rem` | Very small labels; use sparingly   |
|   12px | `1.2rem` | Captions and metadata              |
|   14px | `1.4rem` | Small labels and helper text       |
|   16px | `1.6rem` | Standard body text and subheadings |
|   18px | `1.8rem` | Large body text and navigation     |
|   20px |   `2rem` | Lead paragraphs and buttons        |
|   24px | `2.4rem` | Small heading                      |
|   30px |   `3rem` | Tertiary heading                   |
|   36px | `3.6rem` | Responsive secondary heading       |
|   44px | `4.4rem` | Secondary heading                  |
|   52px | `5.2rem` | Primary heading                    |
|   62px | `6.2rem` | Display heading                    |
|   74px | `7.4rem` | Large display number               |
|   86px | `8.6rem` | Step number or visual statistic    |
|   98px | `9.8rem` | Extra-large display text           |

Do not introduce an in-between font size unless a project requirement makes it necessary.

### Font weights

| Name      | Value | Typical use                        |
| --------- | ----: | ---------------------------------- |
| Default   | `400` | Paragraphs and general text        |
| Medium    | `500` | Navigation, labels and subheadings |
| Semi-bold | `600` | Buttons, statistics and emphasis   |
| Bold      | `700` | Main headings and strong emphasis  |

### Line heights

| Name              |  Value | Typical use                                     |
| ----------------- | -----: | ----------------------------------------------- |
| Default           |    `1` | Short display text                              |
| Small             | `1.05` | Large primary headings                          |
| Medium            |  `1.2` | Secondary and tertiary headings                 |
| Paragraph default |  `1.6` | General paragraphs                              |
| Large             |  `1.8` | Long descriptions requiring more breathing room |

### Letter spacing

| Pixels |        rem | Typical use                      |
| -----: | ---------: | -------------------------------- |
| -0.5px | `-0.05rem` | Large headings                   |
| 0.75px | `0.075rem` | Uppercase labels and subheadings |

### Standard heading classes

```css
.heading-primary,
.heading-secondary,
.heading-tertiary {
  color: var(--color-grey-5);
  font-weight: var(--font-weight-bold);
  letter-spacing: var(--letter-spacing-tight);
}

.heading-primary {
  margin-bottom: 3.2rem;
  font-size: 5.2rem;
  line-height: var(--line-height-small);
}

.heading-secondary {
  margin-bottom: 9.6rem;
  font-size: 4.4rem;
  line-height: var(--line-height-medium);
}

.heading-tertiary {
  margin-bottom: 3.2rem;
  font-size: 3rem;
  line-height: var(--line-height-medium);
}

.subheading {
  display: block;
  margin-bottom: 1.6rem;
  color: var(--color-primary-shade-1);
  font-size: 1.6rem;
  font-weight: var(--font-weight-medium);
  letter-spacing: var(--letter-spacing-wide);
  text-transform: uppercase;
}
```

## 6. Colour system

### Brand colours

| Role    | Value     | Typical use                               |
| ------- | --------- | ----------------------------------------- |
| Primary | `#e67e22` | Main buttons, links, highlights and icons |
| Tint 1  | `#fdf2e9` | Light section backgrounds                 |
| Tint 2  | `#fae5d3` | Decorative backgrounds and hover states   |
| Tint 3  | `#eb984e` | Lighter primary accents                   |
| Shade 1 | `#cf711f` | Primary hover and active states           |
| Shade 2 | `#45260a` | Dark brand contrast and form buttons      |

### Neutral colours

| Value     | Typical use                              |
| --------- | ---------------------------------------- |
| `#888`    | Muted labels and secondary information   |
| `#767676` | Lightest approved grey text on `#fff`    |
| `#6f6f6f` | Lightest approved grey text on `#fdf2e9` |
| `#555`    | Default body text                        |
| `#333`    | Headings and strong text                 |

When text is placed on a new background colour, verify that the contrast remains readable. The two lightest-grey limits above apply only to the specified backgrounds.

## 7. Spacing system

Use spacing values from this scale for padding, margin, gap and layout measurements.

| Pixels |       rem | Token example |
| -----: | --------: | ------------- |
|    2px |  `0.2rem` | `--space-2`   |
|    4px |  `0.4rem` | `--space-4`   |
|    8px |  `0.8rem` | `--space-8`   |
|   12px |  `1.2rem` | `--space-12`  |
|   16px |  `1.6rem` | `--space-16`  |
|   24px |  `2.4rem` | `--space-24`  |
|   32px |  `3.2rem` | `--space-32`  |
|   48px |  `4.8rem` | `--space-48`  |
|   64px |  `6.4rem` | `--space-64`  |
|   80px |    `8rem` | `--space-80`  |
|   96px |  `9.6rem` | `--space-96`  |
|  128px | `12.8rem` | `--space-128` |

Optional variables:

```css
:root {
  --space-2: 0.2rem;
  --space-4: 0.4rem;
  --space-8: 0.8rem;
  --space-12: 1.2rem;
  --space-16: 1.6rem;
  --space-24: 2.4rem;
  --space-32: 3.2rem;
  --space-48: 4.8rem;
  --space-64: 6.4rem;
  --space-80: 8rem;
  --space-96: 9.6rem;
  --space-128: 12.8rem;
}
```

## 8. Shadows and border radii

Use the standard card shadow:

```css
box-shadow: var(--shadow-default);
```

Use the default radius for buttons and controls, and the medium radius for cards and large panels:

```css
.button {
  border-radius: var(--radius-default);
}

.card {
  border-radius: var(--radius-medium);
  box-shadow: var(--shadow-default);
}
```

## 9. Base CSS and reusable layout

Keep these general rules in `general.css`:

```css
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

html {
  font-size: 62.5%;
  overflow-x: hidden;
}

body {
  overflow-x: hidden;
  color: var(--color-grey-4);
  font-family: "Rubik", sans-serif;
  font-size: 1.6rem;
  font-weight: var(--font-weight-default);
  line-height: var(--line-height-default);
}

img {
  display: block;
  max-width: 100%;
}

.container {
  max-width: var(--container-max-width);
  margin: 0 auto;
  padding: 0 3.2rem;
}

.grid {
  display: grid;
  column-gap: 6.4rem;
  row-gap: 9.6rem;
}

.grid--2-cols {
  grid-template-columns: repeat(2, minmax(0, 1fr));
}

.grid--3-cols {
  grid-template-columns: repeat(3, minmax(0, 1fr));
}

.grid--4-cols {
  grid-template-columns: repeat(4, minmax(0, 1fr));
}

.grid--center-v {
  align-items: center;
}
```

## 10. Button standard

```css
.btn,
.btn:link,
.btn:visited {
  display: inline-block;
  padding: 1.6rem 3.2rem;
  border: 0;
  border-radius: var(--radius-default);
  font: inherit;
  font-size: 2rem;
  font-weight: var(--font-weight-semibold);
  text-decoration: none;
  cursor: pointer;
  transition:
    background-color 0.3s,
    color 0.3s,
    box-shadow 0.3s,
    transform 0.3s;
}

.btn--primary:link,
.btn--primary:visited,
.btn--primary {
  background-color: var(--color-primary);
  color: var(--color-white);
}

.btn--primary:hover,
.btn--primary:active {
  background-color: var(--color-primary-shade-1);
}
```

Interactive controls must also have a visible keyboard focus style:

```css
a:focus-visible,
button:focus-visible,
input:focus-visible,
select:focus-visible,
textarea:focus-visible {
  outline: 0.3rem solid var(--color-primary-tint-3);
  outline-offset: 0.3rem;
}
```

## 11. CSS organization order

Organize `style.css` in the same order as the HTML page:

```css
/**************************/
/* HEADER */
/**************************/

/**************************/
/* NAVIGATION */
/**************************/

/**************************/
/* HERO */
/**************************/

/**************************/
/* FEATURES */
/**************************/

/**************************/
/* CONTENT / HOW IT WORKS */
/**************************/

/**************************/
/* TESTIMONIALS */
/**************************/

/**************************/
/* PRICING */
/**************************/

/**************************/
/* CALL TO ACTION */
/**************************/

/**************************/
/* FOOTER */
/**************************/
```

Inside each section, prefer this property order:

1. Positioning: `position`, `top`, `right`, `bottom`, `left`, `z-index`.
2. Layout: `display`, grid/flex properties, alignment and gaps.
3. Box model: `width`, `height`, `margin`, `padding`, `border`.
4. Typography: `font`, `line-height`, `letter-spacing`, `text-align`.
5. Appearance: colours, background, shadow and radius.
6. Behaviour: cursor, overflow, transform, transition and animation.

## 12. Naming convention

Use clear, reusable class names:

```text
.component
.component__element
.component--modifier
```

Examples:

```html
<article class="card card--featured">
  <h3 class="card__title">Website Package</h3>
  <p class="card__description">A responsive business website.</p>
</article>
```

Avoid styling by HTML IDs. Reserve IDs for page anchors, JavaScript hooks where necessary, and unique accessibility relationships.

## 13. Responsive breakpoints

Place all breakpoints in `queries.css`, ordered from large to small.

| Maximum width | `em` value | Typical target    |
| ------------: | ---------: | ----------------- |
|        1344px |     `84em` | Smaller desktops  |
|        1200px |     `75em` | Landscape tablets |
|         944px |     `59em` | Tablets           |
|         704px |     `44em` | Smaller tablets   |
|         544px |     `34em` | Phones            |

Example:

```css
/* Below 1200px: landscape tablets */
@media (max-width: 75em) {
  .grid {
    column-gap: 4.8rem;
    row-gap: 6.4rem;
  }
}

/* Below 704px: smaller tablets */
@media (max-width: 44em) {
  .grid--3-cols,
  .grid--4-cols {
    grid-template-columns: repeat(2, minmax(0, 1fr));
  }
}

/* Below 544px: phones */
@media (max-width: 34em) {
  .grid--2-cols,
  .grid--3-cols,
  .grid--4-cols {
    grid-template-columns: 1fr;
  }
}
```

Add a new breakpoint only when the content or layout visibly breaks. Do not create a breakpoint for a specific device model.

## 14. HTML page structure

Use semantic elements and keep the section order easy to understand:

```html
<!doctype html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta name="description" content="A concise description of the page." />

    <link rel="preconnect" href="https://fonts.googleapis.com" />
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
    <link rel="stylesheet" href="css/general.css" />
    <link rel="stylesheet" href="css/style.css" />
    <link rel="stylesheet" href="css/queries.css" />

    <script defer src="js/script.js"></script>
    <title>Page title</title>
  </head>
  <body>
    <header class="header">
      <nav class="main-nav" aria-label="Main navigation"></nav>
    </header>

    <main>
      <section class="section-hero"></section>
      <section class="section-features"></section>
      <section class="section-cta"></section>
    </main>

    <footer class="footer"></footer>
  </body>
</html>
```

## 15. HTML and CSS checklist

Before considering a page complete, confirm the following:

- The page has one clear `h1`, followed by correctly ordered `h2` and `h3` headings.
- Every meaningful image has descriptive `alt` text; decorative images use `alt=""`.
- Every form field has an associated label.
- Buttons perform actions; links navigate to another page or location.
- Interactive elements work with a keyboard and have a visible focus style.
- Colours come from the approved palette.
- Font sizes and spacing come from the approved scales.
- Measurements use `rem`; media-query breakpoints use `em`.
- Reusable rules are in `general.css`.
- Page-section rules are in `style.css`.
- Responsive overrides are in `queries.css`.
- The layout is checked at desktop, tablet and phone widths.
- No horizontal scrolling appears on a phone-sized viewport.
- The browser console has no missing-file or JavaScript errors.

## 16. Working rule for future pages

When creating or redesigning a page:

1. Start with semantic HTML and the standard file structure.
2. Reuse existing tokens, utilities and components from `general.css`.
3. Add page-specific section styles to `style.css`.
4. Add responsive corrections to `queries.css` only after the base layout is working.
5. Use the closest approved typography or spacing value instead of inventing a new value.
6. Test the final page at the five standard breakpoints.

## 17. Choose a website personality first

Before selecting fonts, colours, images, icons, shadows or border radii, define the visual personality of the website. The personality should match the business, audience and message.

| Personality         | Design direction                                                                                        |
| ------------------- | ------------------------------------------------------------------------------------------------------- |
| Serious / Elegant   | Thin serif typefaces, restrained layouts, gold or pastel colours and large, high-quality photography    |
| Minimalist / Simple | Essential content, small or medium sans-serif text, strong alignment, few images and limited decoration |
| Plain / Neutral     | Neutral typography, predictable components and a highly structured corporate layout                     |
| Bold / Confident    | Large, heavy typography, bright colour blocks, strong contrast and decisive calls to action             |
| Calm / Peaceful     | Soft serif headings, gentle pastel colours, generous whitespace and harmonious imagery                  |
| Startup / Upbeat    | Medium sans-serif typography, light-grey surfaces, rounded components and friendly illustrations        |
| Playful / Fun       | Bright colours, rounded shapes, expressive illustrations, purposeful animation and informal language    |

Record the chosen personality at the beginning of a project:

```text
Website personality: Calm / Peaceful
Primary audience: Families looking for a relaxing homestay
Design choices: Natural images, soft green palette, rounded cards, generous spacing
```

Do not mix several personalities without a clear reason. A consistent direction produces a more professional result.

## 18. Typography decision rules

The approved type scale in Section 5 remains the source of truth. Apply it using these rules:

- Use a proven, readable typeface. One typeface is often enough; use no more than two font families on one page.
- Match the typeface to the selected website personality.
- Use at least `1.6rem` for normal body text. Sizes from `1.6rem` to `3.2rem` are suitable for general content, depending on context.
- For long-form reading, consider `2rem` or larger with a comfortable line height.
- Large headlines may use `5.2rem` or more and a weight of `600` or `700` when the design calls for strong impact.
- Do not use a font weight below `400` for ordinary text.
- Keep long text lines below approximately 75 characters. Use `max-width` to control line length.
- Use a line height from `1.5` to `2` for normal text. Large headings should normally stay below `1.5`.
- Tighten letter spacing slightly when a large heading looks too loose.
- Uppercase is suitable for short labels. Pair it with a smaller size, stronger weight and wider letter spacing.
- Keep paragraphs left-aligned in most layouts. Avoid justified text and avoid centring long paragraphs.

Example for readable long-form content:

```css
.article-copy {
  max-width: 70ch;
  font-size: 2rem;
  line-height: var(--line-height-large);
}
```

## 19. Colour decision rules

The palette in Section 6 is the default palette for this design system. When a project requires different branding, build the replacement palette with the same roles: primary, tints, shades, neutral greys and optional accent colours.

- Choose a primary colour that fits the website personality and business message.
- Use intentional colour values from a defined palette rather than random CSS named colours.
- Every palette needs at least one primary colour and a neutral-grey scale.
- Add an accent colour only when it has a specific role that the primary colour cannot serve.
- Create lighter tints and darker shades from the primary colour to support backgrounds, borders, hover states and emphasis.
- Reserve the strongest colour for the most important elements, such as the primary call to action.
- Use colour to distinguish key sections, selected states, important icons and useful status messages.
- Where appropriate, repeat brand colours within photography or illustrations for a more unified composition.
- On a dark surface, use a light tint related to that surface instead of pure white when it creates a softer result.
- Prefer dark grey over pure black for body text when black feels visually harsh.
- Validate text and background contrast before approving a colour combination.

## 20. Images and illustrations

Images must support the message of the page. They should explain the product, show an experience, build trust or strengthen the desired emotion.

### Selection rules

- Choose the appropriate image type: product photography, storytelling photography, illustration or decorative pattern.
- Prefer original photography. When stock photography is necessary, select images that feel natural and specific to the business.
- Real people can create a stronger emotional connection when their presence is relevant.
- Crop images around the intended subject and message rather than accepting the original composition by default.
- Photos, illustrations and patterns may be combined when they share a coherent visual style.
- Images displayed side by side should use the same aspect ratio and rendered dimensions.

### Text placed over images

Use one of these approaches to keep the text readable:

1. Apply a dark or light overlay, optionally using a gradient.
2. Place the text in an uncluttered part of the image.
3. Place the text inside a solid or translucent content box.

Example overlay:

```css
.hero-media {
  background-image: linear-gradient(rgba(0, 0, 0, 0.55), rgba(0, 0, 0, 0.25)), url("../img/hero.webp");
  background-position: center;
  background-size: cover;
}
```

### Image performance

- Provide source images at roughly twice their displayed dimensions for high-density screens.
- Compress images before publishing.
- Prefer modern formats such as WebP or AVIF, with a fallback where the audience requires it.
- Set `width` and `height` attributes in HTML when known to reduce layout movement while the image loads.
- Use responsive images with `srcset` and `sizes` when the same image is displayed at substantially different widths.
- Lazy-load images below the first screen with `loading="lazy"`.

```html
<img src="img/villa-800.webp" srcset="img/villa-800.webp 800w, img/villa-1600.webp 1600w" sizes="(max-width: 44em) 100vw, 50vw" width="800" height="600" loading="lazy" alt="Living room overlooking the garden" />
```

## 21. Icon rules

- Select one high-quality icon family for the entire website. Do not mix unrelated icon styles.
- Prefer SVG icons because they scale cleanly and allow colour control. Avoid JPG icons and use PNG only when SVG is unavailable.
- Match icon roundness, stroke weight and filled or outlined style to the typography and website personality.
- Use icons to support labels, features, actions, list items and status information.
- Label action icons unless the meaning is universally clear and the available space is limited.
- Use the text colour for neutral icons and the primary or accent colour when the icon needs emphasis.
- Every icon must match its label or action. Decorative icons should not create false affordances.
- Do not enlarge an icon beyond the size for which its detail was designed. Place a small icon inside a larger background shape when more visual weight is needed.
- Hide decorative SVG icons from assistive technology with `aria-hidden="true"`. Give standalone icon buttons an accessible name.

```html
<button class="icon-button" type="button" aria-label="Open navigation">
  <svg aria-hidden="true" focusable="false"><!-- icon paths --></svg>
</button>
```

## 22. Shadow and border-radius decisions

### Shadows

- Use shadows only when they suit the website personality or clarify elevation.
- Apply them selectively. A shadow on every component weakens the hierarchy.
- Keep shadows soft and light; avoid opaque black shadows.
- Use a small shadow for compact controls, a medium shadow for cards and a large shadow only for floating elements such as dialogs.
- Hover and pressed states may adjust the shadow when the movement communicates interaction.
- A coloured glow can be used sparingly for focus or a special highlighted state.

The standard shadow remains:

```css
box-shadow: var(--shadow-default);
```

### Border radii

- More rounded corners make a design feel friendlier and more playful; smaller radii feel more formal.
- Match the roundness of cards and buttons to the character of the selected typeface.
- Use radii consistently on buttons, images, icon containers, cards and highlighted sections.
- Use the existing `--radius-default` and `--radius-medium` tokens before adding another radius.

## 23. Whitespace and grouping

Whitespace is part of the visual structure. It separates unrelated content and connects related content.

- Use generous space between major page sections.
- Use clear spacing between content groups and smaller spacing between elements inside a group.
- Prefer whitespace over separator lines when spacing alone can communicate the grouping.
- Place strongly related elements closer together than loosely related elements.
- Begin a layout with generous spacing and reduce it only where the page feels disconnected.
- Increase spacing when the design uses large typography, icons or images.
- Choose every margin, padding and gap from the spacing scale in Section 7.

A useful relationship is:

```text
Space inside a component < space between components < space between sections
```

## 24. Visual hierarchy

The page should make the order of attention obvious without requiring the visitor to study it.

- Place the main message and primary action near the top of the page.
- Treat large images as high-attention elements and use them only where that attention is useful.
- Use whitespace to isolate and emphasize important content.
- Express text importance through size, weight, colour and surrounding space.
- Give clear emphasis to headings, subheadings, links, buttons, important figures and meaningful icons.
- Highlight a key component with a background, border, shadow or a carefully chosen combination.
- When two components compete, reduce the visual weight of the secondary component.
- Common emphasis targets include testimonials, calls to action, featured cards, forms, pricing plans and important table rows or columns.

For each page, define these three levels before styling:

```text
Primary: Main headline and primary call to action
Secondary: Section headings and featured content
Supporting: Descriptions, metadata and secondary actions
```

## 25. User-experience rules

- Use familiar navigation, form and content patterns so users can predict how the page works.
- Make the primary call to action visually prominent and write a specific action label such as “Book a consultation”.
- Reserve blue underlined text for links. Do not make ordinary text look clickable.
- Keep interface animations purposeful and fast, normally between `200ms` and `500ms`.
- Respect visitors who prefer reduced motion.
- Align form labels and fields in a single vertical flow when possible so the form is easy to scan.
- Give clear feedback after every action, including loading, success, validation and error states.
- Place an action control close to the content it affects.
- Use a descriptive, keyword-focused main headline that explains the offer.
- Remove irrelevant content and keep instructions direct.
- Use common words and explain unavoidable technical terms.
- Break long content into sections with headings, lists, images, quotations or other meaningful structures.

```css
@media (prefers-reduced-motion: reduce) {
  *,
  *::before,
  *::after {
    scroll-behavior: auto !important;
    transition-duration: 0.01ms !important;
    animation-duration: 0.01ms !important;
    animation-iteration-count: 1 !important;
  }
}
```

## 26. Components and layout assembly

Build pages from reusable components instead of styling every page element independently.

### Common components

- Header and navigation
- Hero section
- Buttons and text links
- Feature card
- Image-and-text block
- Testimonial
- Pricing card
- Form and validation message
- Call-to-action section
- Footer

### Common layout patterns

- Single-column reading layout
- Two-column image-and-text layout
- Repeating card grid
- Alternating feature rows
- Split-screen hero
- Sidebar with main content
- Full-width call-to-action band

Assemble the page in three levels:

1. Elements: headings, paragraphs, images, icons, links and buttons.
2. Components: cards, navigation, forms, testimonials and calls to action.
3. Layout areas: header, hero, content sections and footer.

Create a reusable component when the same visual pattern appears more than once or will be used on another page. Keep its shared styling in `general.css`; keep content-specific positioning in `style.css`.
