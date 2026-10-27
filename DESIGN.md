# MAYO Gaming Shop: design system

**Direction:** a black-and-white storefront that looks like the MAYO logo.
The page is a dark, quiet stage. The only color comes from the products
themselves (RGB keyboards and mice on white "photo stages"), from the green
of WhatsApp actions and from the red of sale tags. The site sells on price,
so prices are the boldest text on every card.

The site is dark only. Every value below lives as a CSS variable in
`styles.css` (`:root`). Pages use the variable names, never raw values.

> This direction is based on the existing MAYO logo and brand, not on a
> comparison with real gaming-store websites. UXKIN wasn't reachable from
> this environment.

## Color

| Token | Value | Role |
|---|---|---|
| `--bg` | `#0a0a0b` | Page background |
| `--surface` | `#151517` | Cards, cart drawer, info boxes |
| `--surface-2` | `#1e1e21` | Inputs, quantity stepper, hover fills |
| `--line` | `#2a2a2e` | Dividers and card borders |
| `--line-strong` | `#6b6b74` | Borders of controls: chips, inputs, ghost buttons (3:1 on `--bg`) |
| `--text` | `#f4f4f5` | Body text and headings |
| `--muted` | `#a8a8b0` | Secondary text, categories, old prices (8:1 on `--surface`) |
| `--primary` | `#ffffff` | Primary buttons, active filter chip, cart count, demo bar |
| `--primary-ink` | `#0a0a0b` | Text on `--primary` |
| `--primary-hover` | `#d4d4d8` | Hover state of "add to cart" |
| `--wa` / `--wa-ink` | `#25d366` / `#04210f` | WhatsApp actions only: send order, contact |
| `--sale` | `#c8102e` | "Sale" tag background, with white text (5.9:1) |
| `--success` | `#4ade80` | Success messages (reserved) |
| `--warning` | `#fbbf24` | Warnings (reserved) |
| `--error` | `#ff8a9b` | Form error text and invalid input borders |
| `--stage` | `#ffffff` | Background behind product photos |
| `--stage-ink` | `#18181b` | Placeholder product icons on the stage |

Rules:
- White is the brand's "primary color". Don't add a second brand color.
- Green is used only for things that open WhatsApp.
- Red is used only for sale tags. "New" tags are black.
- No gradients on buttons or text. The only gradient is the soft glow behind the hero logo.

## Typography

- **Heebo** (400, 500, 700, 900) for everything. It's self-hosted in `fonts/`, with Hebrew and Latin subsets.
- **Arial Black** only for the large "MAYO" wordmark in the hero, to match the logo.

| Token | Size | Use |
|---|---|---|
| `--text-xs` | 13px | Tags, categories, small notes |
| `--text-sm` | 14px | Buttons on cards, footer, old prices |
| `--text-base` | 16px | Body text, product names |
| `--text-lg` | 18px | Hero intro, box headings, cart total |
| `--text-xl` | 20px | Prices, drawer title, logo text |
| `--text-2xl` | 28px | Section titles |
| `--text-3xl` | 28–40px | Page titles on content pages |

The hero wordmark uses its own size (64–150px). Line height is `--leading`
(1.5) for text and `--leading-tight` (1.1) for big headings. Weights: 900
for headings and prices, 700 for buttons and names, 500 for labels, 400 for
body text. Text pages are capped at `--content-text` (760px), about 70
Hebrew characters per line.

## Spacing

A 4px scale: `--space-1` (4px) up to `--space-18` (72px). The token number
times 4 gives the pixels.

- Page gutter: `--space-4` (16px)
- Content width: `--content` (1120px)
- Section spacing: `--space-12` (48px) top and bottom. The hero gets `--space-18` / `--space-14`.
- Card padding: `--space-3`. Box padding: `--space-5`. Product grid gap: `--space-4` (`--space-2` on phones).
- Anchor jumps leave `--header-offset` (112px) for the sticky header.

## Shape and depth

| Token | Value | Use |
|---|---|---|
| `--radius-sm` | 6px | Quantity buttons, focus ring |
| `--radius-md` | 10px | Card buttons, inputs, cart thumbnails |
| `--radius-lg` | 14px | Cards, boxes |
| `--radius-pill` | 999px | Primary buttons, chips, tags, cart button |
| `--shadow-lift` | white glow | Hover on primary buttons |
| `--shadow-lift-wa` | green glow | Hover on WhatsApp buttons |

Cards are flat: a border, no shadow. On hover a card moves up 3px.

## Components

- **Primary button** (`.btn`): white pill with dark text, min height 44px. On hover it lifts 2px with `--shadow-lift`.
- **Secondary button** (`.btn.ghost`): transparent with a `--line-strong` border.
- **WhatsApp button** (`.btn.wa`): green pill, only for opening WhatsApp.
- **Card button** (`.add`): white, `--radius-md`. On hover it turns `--primary-hover`.
- **Disabled buttons:** none for now. Actions stay enabled and explain the problem in an error message.
- **Focus** (all controls): 3px white outline with a 3px offset, visible on keyboard focus only.
- **Filter chip** (`.chip`): pill with a `--line-strong` border. The active chip is white (`aria-pressed`).
- **Product card**: white photo stage (4:3), with an optional tag in the top corner. Below it: category, name, price (900 weight), and an add-to-cart button.
- **Input** (`.field`): visible label above the field, `--surface-2` background, `--line-strong` border, min height 44px. When invalid the border turns `--error` and an error message appears under the form.
- **Category tile** (`.cat`): a card with a white photo stage (7:5), the category name and how many products it has. Clicking it filters the shop and jumps there. On phones the tiles become a horizontal scrolling row.
- **Sort select** (`.sort`): a visible label next to a pill-shaped select, using the input colors.
- **Step** (`.step`): a numbered white circle, a short heading and one line of text. Three in a row, stacked on phones.
- **FAQ** (`.faq details`): native `details`/`summary` with a "+" and "−" marker, max width `--content-text`.
- **Placeholder** (`.todo`): a yellow `--warning` mark for facts the shop hasn't confirmed yet. Remove every one before launch.
- **Navigation:** a sticky header with the logo, anchor links (hidden on phones) and the cart button with its count.
- **Cart drawer:** a dialog that slides in from the left, traps focus and closes with Esc. The total and the order form are pinned at the bottom.
- **Footer:** centered, with links to the privacy policy and the accessibility statement.
- **Links in text:** underlined.

## Imagery and icons

- **Product photos:** transparent or white background, shown with `object-fit: contain` on the white stage. They're saved as WebP, at full size and at 280px for phones.
- **Missing photos:** a simple line icon for the product's category, in `--stage-ink`.
- **Icons:** inline SVG line icons, 24×24 viewBox, 2px stroke, round caps, `currentColor`, shown at 20px (`.ico`). No emoji anywhere on the site.
- **Logo:** the MAYO wordmark with controllers, keyboard and cursor, drawn in SVG and text. It isn't stored as an image file.
- **Share image:** `og.png` (1200×630), the logo on the dark background.
