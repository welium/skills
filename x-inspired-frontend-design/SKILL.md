---
name: x-inspired-frontend-design
description: Design and implement general-purpose frontends with X-inspired (formerly Twitter) visual restraint, crisp typography, responsive layouts, and accessible interactions across dashboards, forms, commerce, documentation, landing pages, and social products. Use when the user requests this aesthetic or explicitly invokes this skill, regardless of product domain; do not override a different requested design direction.
---

# X-Inspired Frontend Design

Build polished, general-purpose interfaces inspired by X's visual language, not its social-media information architecture or branding. Borrow restrained surfaces, crisp typography, fine borders, and clear action hierarchy. Choose layouts, density, and interactions from the user's product needs. These are design defaults, not claims about X's current implementation or exact specifications.

**Core rule:** borrow the visual grammar, not the product structure. Feeds, avatars, composers, engagement counts, three-column shells, and bottom navigation are optional domain-specific patterns—not defaults.

## Start with the product

1. Read project instructions, existing UI, styling tokens, components, and relevant tests before editing. Load applicable coding skills when implementing code.
2. Identify the audience, main content object, primary action, and user journey. Choose the appropriate structure: a table for record comparison, a form for configuration, a grid for product browsing, or a reading column for documentation. Never invent social features to express the aesthetic.
3. Preserve the project's framework, component library, brand, and established accessibility patterns. Do not add dependencies or replace the design system just to reproduce this aesthetic.
4. If screenshots are provided, treat them as the visual reference. Otherwise use the defaults below. Ask for a reference only when exact fidelity matters.
5. Implement only the requested screens and interactions. Do not add authentication, messaging, subscriptions, or recommendation engines without a requirement.

## Visual direction

- **Content over containers:** use flat surfaces and fine separators. Use cards when they meaningfully group independent objects, not as a wrapper around every heading or row.
- **Quiet chrome, strong hierarchy:** near-black and near-white surfaces, readable muted metadata, bold names and headings, and one restrained accent.
- **Appropriate density:** use compact rows for operational tools and more breathing room for reading, onboarding, shopping, and marketing. Maintain consistent alignment, readable line height, and generous hit targets.
- **Shape with purpose:** consider pill-shaped primary actions and filter controls, modest radii for fields and panels, and rectangular working areas. Use circular avatars only when people are part of the domain.
- **Minimal effects:** avoid decorative gradients, glass-heavy panels, oversized shadows, excessive motion, and dashboard-style card grids unless the product needs them.
- **Independent identity:** retain the user's logo, name, copy, and assets. Do not introduce the X logo, proprietary fonts, misleading verification badges, or claims of affiliation.

## Suggested design tokens

Map these roles into the existing token system. Values are starting points; validate actual foreground/background combinations.

| Role | Light | Dark |
| --- | --- | --- |
| Canvas | `#FFFFFF` | `#000000` |
| Secondary surface | `#F7F9F9` | `#16181C` |
| Primary text | `#0F1419` | `#E7E9EA` |
| Secondary text | `#536471` | `#8B98A5` |
| Subtle divider | `#EFF3F4` | `#2F3336` |
| Accent | `#1D9BF0` | `#1D9BF0` |

- Accent blue is not automatically suitable for small text or white button labels. For example, use a darker blue such as `#006FBA` with white text in light mode, or near-black text on a bright-blue button, after contrast verification.
- Subtle dividers are decorative separators, not sufficient boundaries for every form control. Use stronger borders where control identification requires contrast.
- Default to the project's current theme. If none exists, use light mode; support dark mode only when requested or already supported. Do not add a theme toggle unnecessarily.
- Use the existing sans-serif font or a system stack. Do not depend on proprietary X fonts.
- Body: roughly 15–16px with 1.4–1.55 line height. Metadata: 13–14px. Section titles: 20–24px, bold. Reading pages may need more line height; marketing pages may use larger responsive headlines when justified by the content.
- Spacing rhythm: 4, 8, 12, 16, 24, and 32px, with larger section gaps where appropriate. Compact row padding: usually 12–16px. Icons: usually 20–24px within larger hit areas.
- Preserve meaningful semantic colors for errors, warnings, success, and data visualization. A restrained palette must not erase information or force every chart series to blue.

## Choose the structure by task

| Product or task | Suitable starting structure |
| --- | --- |
| Admin, finance, issue tracking | Sidebar or top navigation, page toolbar, table/list, optional detail panel |
| Analytics | Filter bar, prioritized metrics, charts and supporting tables in a purposeful grid |
| Settings, onboarding, checkout | Clearly grouped forms, readable field widths, explicit progression or save behavior |
| Commerce, catalogs, portfolios | Responsive item grid, relevant filtering, focused item details and primary action |
| Documentation, editorial | Comfortable reading column, optional section navigation and table of contents |
| Marketing, landing pages | Clear value proposition, deliberate section rhythm, relevant proof and focused calls to action |
| Community or activity products | Feed/list and optional composer only when required by the actual workflow |

Do not force every product into this table or introduce every listed component. Choose the smallest structure that supports the requested journey.

## Responsive structure

Choose breakpoints based on content fit, not device names. The following are useful starting points:

| Available width | Layout |
| --- | --- |
| Below approximately 700px | Stack content by priority; use a compact header and accessible navigation menu where needed; adapt grids and forms |
| Approximately 700–1099px | Use available space for a compact sidebar, split view, or two-column grid only if content fits comfortably |
| Approximately 1100px and above | Expand tables, charts, grids, or working panels; add supporting navigation or context only when useful |

- Choose widths by content: reading columns around 60–75 characters; forms often around 480–720px; general shells around 1200–1440px; data-heavy workspaces may use the available width. These are starting points, not universal constraints.
- Use thin separators where they clarify regions. A single-column page or top-navigation layout is as valid as a sidebar shell; do not add a third column merely to resemble X.
- Headers may be sticky with an opaque or subtly translucent surface, but must remain readable and must not obscure focused elements.
- Use bottom navigation only for a small set of frequent destinations when it fits the product. If present, reserve space for it and floating actions, including safe-area insets; avoid overlapping inputs, the keyboard, or final content rows.
- Allow columns and long text to shrink and wrap. Prevent page-level horizontal overflow from URLs, identifiers, media, and nested flex/grid children. Wide tables may use a clearly bounded, keyboard-accessible horizontal scroll region when preserving comparison is important.
- Do not hide essential actions or information solely to make a small-screen screenshot cleaner.

## Component patterns

### Navigation and headers

- Pair consistent outline icons with clear labels on wide screens; indicate the active destination with weight or fill as well as color.
- Icon-only navigation still needs accessible names and visible keyboard focus.
- Make the primary product action prominent, usually a filled pill. Avoid multiple competing primary actions in the same region.
- Use compact page titles and optional tabs with a short accent underline. Use tab semantics only for actual tab panels; use links for navigation.

### Tables, lists, and record details

- Prioritize the record's title or identifier, key attributes, status, and relevant actions. Do not prepend avatars to objects that do not represent people.
- Use semantic tables for genuinely tabular comparisons, with clear headers, aligned numeric columns, units, and accessible sorting state when sorting is implemented.
- Let secondary metadata wrap or truncate without crowding actions offscreen; keep essential values available without hover.
- Separate items with fine horizontal rules and subtle hover feedback rather than shadows.
- Use realistic, varied content lengths. Include a long name, multiline text, missing image, and long unbroken string when testing.
- Keep media inside the content width with appropriate aspect ratios, rounded corners, and meaningful alternative text. Preserve important image content rather than cropping indiscriminately.
- Keep row actions quiet but discoverable. Add selection, bulk actions, filtering, sorting, and pagination only as required; distinguish no records from no matching results.
- Avoid nested interactive elements. If a row opens a detail view, its links and buttons must still operate independently and be reachable by keyboard.

### Forms and task flows

- Group related fields under meaningful headings, use persistent labels, and distinguish required from optional input. Prefer a single column unless side-by-side fields have a clear relationship.
- Match input types and autocomplete to the data. Explain formats and constraints before failure; associate field errors with their controls and retain entered values.
- Distinguish placeholder copy from an accessible label. Follow the project's validation strategy; never leave users with an unexplained disabled submit button.
- Make save, cancel, and destructive actions unambiguous. Prevent duplicate submissions, preserve input after recoverable failures, and show progress and success/error feedback without disruptive layout shifts.
- Use multistep flows only when task complexity warrants them. Add attachment tools, rich-text editors, or counters only if needed.

### Dashboards and data visualization

- Organize around the decisions users need to make, not an arbitrary grid of metric cards. Surface the most useful summary, then supporting detail.
- Label units, time ranges, axes, and data freshness where relevant. Distinguish zero, missing data, and loading states.
- Use accessible series colors with labels or additional encodings. Provide readable summaries or tabular alternatives for important chart information; do not rely exclusively on hover tooltips.

### Catalogs, content, and landing pages

- Use grids when visual browsing or comparison benefits from them. Keep image ratios and item metadata consistent without making all content the same height at the expense of readability.
- Detail pages should prioritize the product, document, or project itself, then its main action and supporting information.
- Reading pages need a comfortable measure and clear heading hierarchy. Marketing pages need specific copy and deliberate section rhythm, not a social feed or a generic wall of cards.
- Use relevant provided assets or clearly identified placeholders. Do not invent testimonials, customer logos, prices presented as real, or performance claims.

### Supporting panels

- Search, filters, contextual help, summaries, and inspectors may appear inline, in a sidebar, or in a drawer according to the workflow. Do not create a supporting column without a purpose.
- Use understated backgrounds or borders and compact section headings. Avoid competing with the primary content.
- Use provided data or clearly identified fictional fixtures; never present fabricated metrics or live information as real.

### Optional social patterns

- Only for social or activity workflows, use an avatar-and-content list, quiet metadata, compact actions, and a simple composer where required.
- Do not transfer likes, follower counts, trends, verification badges, or posting controls into unrelated products.

## Interaction and accessibility requirements

- Every visible control must work within the agreed scope. For a prototype, local state is acceptable; identify it as demo behavior and do not imply server persistence. Omit or clearly disable unsupported actions.
- Cover applicable default, hover, focus-visible, pressed/selected, disabled, loading, empty, error, and success states.
- Use semantic landmarks, logical headings, native buttons and links, and labels for inputs and icon controls. Represent toggle state accessibly, such as with `aria-pressed`.
- Aim for 44×44px touch targets. Meet WCAG AA contrast: 4.5:1 for normal text, 3:1 for large text, and applicable 3:1 contrast for meaningful UI boundaries and indicators.
- Do not use color alone to communicate active, error, or success states.
- Dialogs and menus need appropriate keyboard operation, focus management, Escape behavior, and focus restoration; prefer existing accessible primitives.
- Keep microinteractions short, usually 120–180ms. Respect reduced-motion preferences. Do not make essential information hover-only.
- For dynamically updated content, preserve reading position, avoid unsolicited focus changes, and provide a keyboard-accessible loading mechanism. Do not build infinite scrolling unless required.

## Verification and delivery

1. Run the project's relevant checks and interaction tests. Do not introduce a test framework merely for this skill.
2. When browser tooling is available, inspect representative narrow, medium, and wide viewports (for example 390, 820, and 1440px), plus a 320px-width overflow check. Test supported themes, keyboard navigation, and 200% zoom/reflow.
3. Check alignment, wrapping, focus visibility, contrast, sticky-header overlap, bottom-navigation clearance, and loading/error/empty states—not just the default screenshot.
4. Exercise the main user journey and confirm that secondary controls do not accidentally trigger parent-row navigation.
5. Fix issues found before delivery. Report what was implemented, what was actually checked, and any demo-only behavior or remaining limitations. If browser checks were unavailable, say so; never claim visual verification without performing it.

## Example requests

- “Use x-inspired-frontend-design for an invoice app with a conventional sidebar, invoice table, and detail panel. No social features.”
- “Design an analytics dashboard with restrained surfaces, readable charts, and accessible filters.”
- “Apply this skill to a checkout flow with clear form grouping and responsive order summaries.”
- “Restyle our documentation with crisp typography, fine separators, and comfortable reading widths.”
- “Create a product landing page using this visual language, with a strong headline and focused calls to action.”
- “Use x-inspired-frontend-design to build a community feed with a mobile composer.”
