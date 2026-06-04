# Merchant Portal Design Specification
## Document Basic Info
| Item | Content |
| ---- | ---- |
| Document Name | merchant_portal_design.md - Merchant Portal Design Specification |
| Version | V1.2 (Advanced Production-Density Typography Standard) |
| Updated Date | 2026-06-04 |
| Reference UI | https://demo-remote.e-com365.com/vinnia/galaxiaslabs-dashboard/index.html |
| Scope | All pages, new pages, and iteration pages of the Merchant Portal |
| Users | Frontend Developers, AI Code Agents, UI Designers, CodeX |
| Core Rules | All new components/pages MUST strictly follow the Design Tokens and component rules in this document. Custom colors, font sizes, border radius, shadows, and spacing are forbidden. Page layout and interactions must fully align with the reference HTML page. |

---

# Table of Contents
1. 【Basic Design Tokens】Global Variables (Color / Font / Spacing / Radius / Shadow / Border)
2. 【Layout System Specification】Grid, Layout, Space, Divider
3. 【Typography Specification】Full-level text rules & High-Density Visual Spacing
4. 【General Basic Components】Button, Icon, BackTop, Breadcrumb, Dropdown, Menu, Pagination, Tabs
5. 【Form Components】Autocomplete, Cascader, Checkbox, DatePicker, Form, Input, Radio, Select, SelectInput, Slider, Textarea, TimePicker, TreeSelect, Upload
6. 【Data Display Components】Avatar, Badge, Calendar, Card, Collapse, Comment, Descriptions, Image, ImageViewer, List, Loading, Skeleton, Statistic, Table, Timeline, Tooltip
7. 【Popup & Overlay Components】Dialog, Drawer, Message, Notification, PopConfirm, Popup
8. 【Global Interaction States】Hover / Active / Focus / Disabled / Loading
9. 【AI Code Generation Mandatory Clauses】AI-specific rules to ensure unified page style

---

# 1. Basic Design Tokens (AI reads this chapter first, all styles from here)
> Note: All CSS styles MUST use the Tokens below; hardcoded color values and px values are forbidden. For missing components, derive designs using the same Token system — do NOT add custom variables.

## 1.1 Color System
### Primary Colors (Business actions, highlighted buttons, selected states, nav highlights)
- Primary-100: Light background #E6F0FF (Used for table row hover states, token tags background, active inline link text blocks)
- Primary-300: Light hover #94C1FF (Used for default button borders on hover, sub-interactive state highlights)
- Primary-500: Standard primary (buttons / tag highlights) #1677FF (Used for primary buttons, active tabs line, radio/checkbox checked status)
- Primary-700: Dark hover #0F52BA (Used for primary button hover/active states, text link focus highlights)
- Primary-900: Text highlight #062D66 (Used for deeply embedded operational action links, system brand text anchors)

### Functional Status Colors
- Success-500: Success, approved, completed #00B42A (Used for active metrics positive trends, approved badges, file upload completion progress)
- Warning-500: Warning, pending #FF7D00 (Used for warning notification blocks, pending review badges, popconfirm alert icons)
- Danger-500: Delete, error, failed #F53F3F (Used for destructive action buttons, form validation error texts, unread indicator counts)
- Info-500: Info, auxiliary text #86909C (Used for standard informational alerts, default unselected icon fills)

### Neutral Grays (Text, borders, backgrounds, dividers)
- Neutral-0: Pure white #FFFFFF (Used for page cards background, dropdown list wraps, dialog inner contents, table body cell rows)
- Neutral-100: Page background #F2F3F5 (Used for global portal background wrapper, table header row backgrounds, card tab unselected blocks)
- Neutral-200: Card light gray background #E5E6EB (Used for inside border segments, collapse separators, disabled component backgrounds)
- Neutral-300: Dividers, light borders #C9CDD4 (Used for global horizontal/vertical dividers, default button borders)
- Neutral-400: Input default border #86909C (Used for input fields border, unselected checkbox/radio outer borders, placeholder text)
- Neutral-500: Secondary text #4E5969 (Used for sub-descriptions, chart metadata fields, table headers text color, neutral status labels)
- Neutral-600: Body text #272E3B (Used for grid core rows text data, default description paragraph segments)
- Neutral-700: Title text #1D2129 (Used for card titles, standard modal main labels, unselected active page history crumbs)
- Neutral-900: Deepest text, bold titles #0A0C10 (Used for page main title highlights, crucial analytical metric summaries, form group master headers)

## 1.2 Font Specification
### Font Family
- **Sans-Serif Stack (Proportional Text):** `Inter, -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica, Arial, sans-serif`
- **Monospace Stack (Data / IDs / Metrics):** `JetBrains Mono, SFMono-Regular, Menlo, Monaco, Consolas, monospace`

### Font Size Levels & Core Typography Tokens (Strictly Prohibited to customize)
| Level / Token | Font Size | Line Height | Weight | Letter Spacing | Usage / Tailwind Mapping |
| ---- | ---- | ---- | ---- | ---- | -------- |
| text-display-h1 | 24px | 32px (1.33) | 700 (Bold) | `-0.025em` | Page main title / `text-[24px] leading-[32px] font-bold tracking-[-0.025em] text-neutral-900` |
| text-section-h2 | 18px | 24px (1.33) | 600 (SemiBold) | `-0.015em` | Module card title / `text-[18px] leading-[24px] font-semibold tracking-[-0.015em] text-neutral-900` |
| text-card-h3 | 16px | 22px (1.38) | 600 (SemiBold) | `0` / `normal` | Sub-section / Modal Title / `text-[16px] leading-[22px] font-semibold tracking-normal text-neutral-900` |
| text-form-h4 | 14px | 20px (1.43) | 500 (Medium) | `0` / `normal` | Inline title, strong block title / `text-[14px] leading-[20px] font-medium tracking-normal text-neutral-900` |
| text-body-main | 14px | 20px (1.43) | 400 (Regular) | `0` / `normal` | **Core System Text (Grid data, default paragraph)** / `text-[14px] leading-[20px] font-normal text-neutral-600` |
| text-body-bold | 14px | 20px (1.43) | 500 (Medium) | `0` / `normal` | Primary Keys inside cells, highlighted parameters / `text-[14px] leading-[20px] font-medium text-neutral-900` |
| text-label-form | 12px | 16px (1.33) | 500 (Medium) | `0` / `normal` | Form Input Labels (Strictly above inputs) / `text-[12px] leading-[16px] font-medium text-neutral-700` |
| text-caption | 12px | 16px (1.33) | 400 (Regular) | `0` / `normal` | Sub-descriptions, help notes, placeholders, grid headers / `text-[12px] leading-[16px] font-normal text-neutral-500` |
| text-tiny | 11px | 14px (1.27) | 400 / 500 | `0` / `normal` | Mini labels, tag counts, charts, metadata / `text-[11px] leading-[14px] font-normal` |

## 1.3 Spacing System (Base unit: 8px, absolute strict multi-grid)
### Base Spacing Variables
- Space-XS: 4px
- Space-S: 8px
- Space-M: 16px
- Space-L: 24px
- Space-XL: 32px
- Space-XXL: 48px

### Component Inner Spacing Rules
1. Form input padding: Vertical Space-XS (4px), Horizontal Space-S (8px)
2. Card padding: Vertical Space-M (16px), Horizontal Space-M (16px)
3. Table cell padding: Vertical 14px or 16px, Horizontal Space-M (16px)
4. Modal header/footer padding: Vertical Space-M (16px), Horizontal Space-L (24px)
5. Section margin: Space-L (24px)

## 1.4 Border Radius
| Variable | Value | Usage |
| ---- | ---- | -------- |
| Radius-XS | 2px | Table cell components, dynamic micro-tags |
| Radius-S | 4px | Inputs, dropdown rows, checkbox/radio boxes, status badges |
| Radius-M (Default) | 6px | Buttons, normal layout cards, modal wraps, slide drawers |
| Radius-L | 8px | Image upload card placeholders, large feature panels |
| Radius-Circle | 50% | User profiles, user avatars, action dot shortcuts |

## 1.5 Shadow
### Shadow-1 (Light shadow: dropdowns, menus, tooltips)
`0 1px 4px rgba(0,0,0,0.08)`
### Shadow-2 (Standard card shadow: page cards, list containers)
`0 2px 8px rgba(0,0,0,0.1)`
### Shadow-3 (Heavy overlay: Dialog, Drawer)
`0 4px 16px rgba(0,0,0,0.15)`

## 1.6 Border
Default border width: 1px; Default color: Neutral-300
- Border-Solid: Solid line (global default)
- Border-Dashed: Dashed line (upload areas, placeholder boxes only)

---

# 2. Layout System Specification
## 2.1 Grid System
1. Total columns: 24 columns, optimized for 1920px large screens
2. Grid gutter: Space-M (16px)
3. Max container width: 1680px, auto margin left/right
4. Responsive breakpoints (3 levels only)
    - XL: ≥1600px, full 24 columns
    - LG: 1200px ~ 1599px, 24 columns, auto shrink
    - MD: <1200px, sidebar collapsed, content full width
5. All new pages (forms, cards, lists) MUST use 24-column Grid; custom float layouts forbidden.

## 2.2 Page Layout
Global fixed 3-column structure (Sidebar + Header + Content)
1. Sider: Fixed width 240px, collapsed 64px, bg Neutral-700, text Neutral-0
2. Header: Height 60px, bg Neutral-0, bottom 1px Neutral-300 border
3. Content: Padding Space-L (24px), bg Neutral-100
4. All modules MUST be wrapped in Card components; naked tables/text forbidden.

## 2.3 Space Component
1. Only use Space variables (XS/S/M/L/XL)
2. Horizontal Space: Inline buttons, tags, input groups
3. Vertical Space: Form rows, sections, paragraphs
4. All components MUST use Space; manual margin forbidden.

## 2.4 Divider
1. Horizontal divider: 1px height, Neutral-300, margin top/bottom Space-M
2. Vertical divider: 1px width, Neutral-300, margin left/right Space-S
3. Divider with text: Text Style map to `text-tiny`, Neutral-500, line padding Space-M
4. Custom divider color/thickness forbidden.

---

# 3. Typography Specification (High-Density Visual Spacing)
> Note: This section governs the strict typographic layout rules required to preserve screen real estate while creating crisp informational hierarchy.

## 3.1 Heading Rules & Tracking Control
1. Only H1–H4 allowed; no H5/H6.
2. Heading bottom margin: Space-M (16px); top margin: Space-L (24px).
3. **Tracking Rules:**
   - Large Headers (`text-display-h1`, `text-section-h2`): Must enforce negative tracking (`-0.025em` to `-0.015em`) via custom CSS or Tailwind tracking classes. This counters the optical tracking gaps caused by the anti-aliasing of medium-to-large geometric sans-serif fonts.
4. **Visual Anchoring Margin:** Card Header Title to Card Subtitle/Description vertical gap must be exactly **Space-XS (4px)** or **6px** maximum (Tailwind `margin-bottom: 1px` to `2px` depending on paragraph line-heights).

## 3.2 Body Text & Legibility Rules
1. Default text: `text-body-main` (14px) with tightly bounded line height `20px` (1.43 ratio), rendered in Neutral-600.
2. Secondary text: `text-caption` (12px) with sharp line height `16px` (1.33 ratio), rendered in Neutral-500. Standard character tracking (`0` or `tracking-normal`) MUST be forced to ensure readability when packing multi-row strings.
3. Link text: Primary-500, hover Primary-700, underline on hover only.
4. **Color Boundaries:** Pure black (`#000000`) is strictly illegal. Use Neutral-900 (`#0A0C10`) for deep bold highlights and Neutral-700 (`#1D2129`) for default titles.

## 3.3 Micro-Spacing & Text Vertical Margins 
CodeX and AI Agents must strictly compute element boundaries based on the rules below:
- **Form Label to Input Container:** Vertical structural gap must be exactly **Space-XS (4px)** (Tailwind `space-y-1` or `mb-1` on label block).
- **Form Group Stack Row to Row:** Vertical partition distance must be exactly **Space-M (16px)** (Tailwind `space-y-4` on form panel).
- **Section Structural Header to Block Content:** Vertical spacing must be **Space-M (16px)** or **Space-L (24px)** (Tailwind `mb-4` or `mb-6`).

## 3.4 Numerical Typography & Alignment Semantics 
- **Financial/Data Precision:** All metrics, performance stats, conversion rates, counts, and primary identifiers (IDs) MUST explicitly override the font family to the Monospace stack (`font-mono`). This guarantees structured numerical columns that do not wiggle visually during layout rendering.
- **Alignment Rules:**
  - Standard text strings, data tags, descriptive fields, names: **Left-aligned** (`text-left`).
  - Monetary values, item quantities, analytics percentages, performance indicators: **Right-aligned** (`text-right`). This rule mandates strict alignment mapping across corresponding table column headers (`<th>`) and table body cells (`<td>`).

---

# 4. General Basic Components
## 4.1 Button
### Sizes
- Large: H40px, padding H20px, `text-body-large`, Radius-L
- Default: H32px, padding H16px, `text-body-main`, Radius-M
- Small: H24px, padding H12px, `text-caption`, Radius-S

### Types
1. Primary: Bg Primary-500, text white; hover Primary-700; disabled opacity 0.5
2. Default: White bg, 1px Neutral-300 border, text Neutral-600; hover border Primary-300
3. Text: No bg/border, text Primary-500; hover bg Primary-100
4. Link: No padding, text highlight, hover underline
5. Danger: Solid/outline using Danger-500

### Rules
- Icon button: Icon 16px, space Space-XS
- Button group: No gap between buttons; only first/last have radius
- Loading state: Built-in loading, text opacity reduced

## 4.2 Icon
1. Fixed sizes: 12px / 16px / 24px; 90% use 16px
2. Color follows parent text
3. Use only the official icon set; third-party icons forbidden
4. Icon-text spacing: Space-XS

## 4.3 BackTop
1. Fixed bottom-right: bottom 24px, right 24px
2. Size 40px circle, Radius-Circle, bg Neutral-0, Shadow-2
3. Icon 16px Neutral-600; hover bg Primary-100
4. Auto show after scroll 400px

## 4.4 Breadcrumb
1. Text: `text-body-main`, separator “/”, color Neutral-400
2. History page: Neutral-500, hover Primary-500
3. Current page: Neutral-700, no hover
4. Bottom margin: Space-L

## 4.5 Dropdown
1. Container: Radius-M, Shadow-2, bg Neutral-0, min-width 120px
2. Item: H32px, padding H16px, `text-body-main`
3. Hover: bg Primary-100, text Primary-500
4. Divider: 1px Neutral-200, margin Space-XS

## 4.6 Menu
### Sidebar Menu
1. Bg Neutral-700, text Neutral-300; selected bg rgba(255,255,255,0.1), text white
2. Item height: 44px, padding Space-M
3. Collapsed: icons only; hover show tooltip

### In-page Tabs Menu
1. White bg, text Neutral-600; selected text Primary-500, bottom 2px Primary-500

## 4.7 Pagination
1. Text: `text-body-main`, button H32px, Radius-S
2. Default: White bg, 1px Neutral-300 border; hover border Primary-300
3. Current: Bg Primary-500, text white
4. Top margin: Space-M, align right
5. Page size selector: Select component, space Space-M

## 4.8 Tabs
### Line Tabs (Default)
- Tab H40px; active bottom 2px Primary-500, text Primary-500
- Inactive: Neutral-500, hover Primary-300

### Card Tabs
- Bg Neutral-100; active white bg, Radius-S, Shadow-1
- Horizontal gap: Space-XS

### Rules
- Tab content top margin: Space-M; wrap content in Card

---

# 5. Form Components
## General Form Rules
1. Label: `text-label-form` Token (12px, Medium 500, Neutral-700).
2. Label Position: Placed strictly **above** the input field with an explicit vertical structural gap of exactly **Space-XS (4px)**.
3. Required: Red * suffix (Danger-500)
4. Input height: 32px, Radius-S, 1px Neutral-400 border. Content text mapping: `text-body-main` (14px).
5. Focus: Border Primary-500, glow `box-shadow: 0 0 0 2px rgba(22,119,255,0.2)`
6. Disabled: Bg Neutral-100, text Neutral-400
7. Error tip: `text-caption` Danger-500, margin Space-XS (4px) strictly below input container
8. Form row vertical spacing: Space-L (24px) (Distance from the bottom of one row's input/error-tip to the top of the next row's label)

## 5.1 Input / SelectInput
1. Padding: Horizontal Space-S (8px), Vertical Space-XS (4px)
2. Placeholder: `text-caption` Neutral-400
3. Prefix/suffix icon: 16px Neutral-400, space Space-XS (4px)
4. Character count: `text-caption` Neutral-400 at bottom-right

## 5.2 Textarea
1. Default H80px, vertical resize only
2. Style matches Input
3. Character count at bottom-right

## 5.3 Checkbox
1. Box 16×16px, Radius-XS, border Neutral-300
2. Checked: Bg Primary-500, white check icon
3. Checkbox-text gap: Space-S (8px), text `text-body-main`

## 5.4 Radio
1. Circle 16px, border Neutral-300; checked inner 8px Primary-500
2. Group spacing: Space-M (16px) between parallel options
3. Radio.Button: Default button style; selected bg Primary-500

## 5.5 Select
1. Style matches Input; dropdown uses Dropdown rules
2. Multiple: Tags use Badge, close icon 12px
3. Search: Built-in input, dropdown icon 16px

## 5.6 Autocomplete
Style same as Input; dropdown same as Dropdown

## 5.7 Cascader
Style same as Select; multi-level menu, indent Space-M

## 5.8 TreeSelect
Style same as Select; tree node hover bg Primary-100

## 5.9 DatePicker / TimePicker
1. Style same as Input; calendar icon 16px
2. Calendar popup: White bg Shadow-2; hover bg Primary-100
3. Range picker: dual calendar, separator “~”

## 5.10 Slider
1. Track H4px, bg Neutral-200; selected track Primary-500
2. Drag dot: 14px circle, white bg Shadow-1; hover 16px
3. Scale text: `text-caption` Neutral-500

## 5.11 Upload
### Drag Area
1. 1px Neutral-300 dashed border, Radius-M, padding Space-XL
2. Icon 24px Neutral-400, text `text-body-main` Neutral-500
3. Hover: dashed border Primary-300, bg Primary-100

### File List Card
1. Item H48px; thumbnail, filename, delete Danger-500
2. Progress bar: H4px, bg Neutral-200, progress Success-500

## 5.12 Form Container
1. Two layouts: Horizontal (label left), Vertical (label top)
2. Action buttons: Align right, gap Space-M (16px) between main/secondary actions, top margin Space-L (24px)
3. Large forms: Wrap in Card, padding Space-L

---

# 6. Data Display Components
## 6.1 Avatar
1. Sizes: 24px / 32px / 40px / 64px, Radius-Circle
2. Text avatar: Bg Primary-300, white text
3. Status badge: Small dot at bottom-right

## 6.2 Badge / Status Tags
1. Number badge: Bg Danger-500, white `text-caption`, min-width 16px, Radius-Circle
2. Status dot: 8px circle (Success/Warning/Danger/Info)
3. **Status Badges & Tags (高密度标签规范):**
   - Text Style: Enforce `text-[12px] leading-none` (12px font size with direct explicit vertical string alignment).
   - Component Padding: Vertical padding **4px**, Horizontal padding **8px** (`px-2 py-1`).
   - Border Radius: Enforce exactly **Radius-S (4px)** micro-rounded corners. *Capsule / Full-rounded pills (`rounded-full`) are strictly banned*, except for unread indicator counts.

## 6.3 Card
1. Bg Neutral-0, Radius-M, Shadow-2
2. Header: padding V Space-M, bottom 1px Neutral-200 border; title H4
3. Body: padding V Space-M, H Space-L
4. Footer: padding V Space-M, top 1px Neutral-200 border
5. No-shadow card: White bg radius only (for inner modals)

## 6.4 Table (High-Density Grid Layout)
1. Radius-M, 1px Neutral-200 outer container border. Vertical grid separation lines between cells are forbidden.
2. **Table Header Row (`<th>`):**
   - Background Fill: Neutral-100 (`#F2F3F5`). 
   - Typography: Map to `text-caption` Token (12px, Regular/Medium), Text Color `#4B5563` or Neutral-500.
   - Sorting Icons: 12px, color aligned with header text.
   - Alignment: Left-aligned for text/names, Right-aligned **only** for metrics, metrics parameters, percentages, and currencies.
3. **Table Body Cell Rows (`<td>`):**
   - Background Fill: Pure Neutral-0 (`#FFFFFF`). Row Hover Background transition state must be smooth Primary-100.
   - Typography: Map to `text-body-main` (14px, Regular).
   - Font for Numbers: Force Monospace stack (`font-mono`) tracking for operational alignment precision (Currencies, IDs, Timestamps).
   - Height Padding: Vertical top/bottom padding must be strictly locked to **14px or 16px** (`py-3.5` or `py-4`) to produce high information density while retaining structural elegance.
4. Cell text layout: Vertical alignment center. Long string text fallback uses standard ellipsis clip, opening full text block on hover via Tooltip.
5. Action buttons within Rows: Small size button specifications, inline row layout gap: Space-S (8px).
6. Top filter container header: Inline horizontal form, with secondary creation/export actions aligned to the far right.

## 6.5 Collapse
1. Header H40px, padding H Space-M; hover bg Neutral-100
2. Arrow icon 16px, rotate on expand/collapse
3. Content: padding Space-M, top 1px Neutral-200 border

## 6.6 Descriptions
1. 2/3 column layout; label Medium, value Regular
2. Cell bottom 1px Neutral-200 border, padding V Space-S
3. Wrap in Card, title H4 in header

## 6.7 List
1. Item padding V Space-M, bottom 1px Neutral-200 border
2. Left avatar/icon, middle title + `text-caption`, right text button
3. **No Vertical Visual Borders:** Separate text segments or metrics inside list items using light horizontal lines (`border-b border-gray-100`) or generous horizontal gaps (`space-x-6`), avoiding harsh visual column borders.
4. Wrap in Card

## 6.8 Loading
1. Local: 16px spinner, text `text-caption` Neutral-500
2. Global: 40px spinner, mask rgba(255,255,255,0.7)

## 6.9 Skeleton
1. Gradient animation Neutral-200 ~ Neutral-100
2. Match real layout height and radius
3. Full page skeleton for tables/cards

## 6.10 Statistic
1. Value H2 SemiBold, title `text-caption` Neutral-500
2. Trend: Success/Danger text with arrow
3. Multiple stats: gap Space-M, wrap in Card

## 6.11 Timeline
1. Left line 2px Neutral-200, node 12px status color
2. Title `text-body-main` Medium, content `text-caption` Neutral-500
3. Vertical spacing Space-M

## 6.12 Tooltip
1. Container Radius-S, Shadow-3, bg Neutral-700, white `text-caption`
2. Auto position, delay 200ms

## 6.13 Calendar
Same as DatePicker calendar, with month switch

## 6.14 Image / ImageViewer
1. Image container Radius-S, 1px Neutral-200 border
2. Viewer: Full screen mask, center image, close button top-right

## 6.15 Comment
1. Top: Avatar + name + time
2. Content: `text-body-main`
3. Bottom: Like/reply text buttons
4. Bottom margin Space-M, divider 1px Neutral-200

---

# 7. Popup & Overlay Components
## 7.1 Dialog
1. Mask: Mask-Bg, click to close
2. Container: White bg, Radius-M, Shadow-3
    - Header: H60px, padding H Space-L, title H3, close icon 16px
    - Body: padding H Space-L, V Space-M; max height 60vh, scrollable
    - Footer: padding V Space-M, H Space-L; buttons align right, gap Space-M (16px)
3. Sizes: Small 480px, Standard 720px, Large 1000px

## 7.2 Drawer
1. Slide from right; width 480px / 720px
2. Structure same as Dialog; top radius Radius-M
3. Slide animation, click mask to close

## 7.3 PopConfirm
1. Based on Tooltip, with Confirm/Cancel small buttons
2. Warning icon Warning-500, text `text-body-main`

## 7.4 Popup
Base container same as Dropdown, padding Space-M

## 7.5 Message
1. Top center, auto close 3s
2. 4 types: Success/Warning/Danger/Info
3. White bg, Shadow-2, Radius-S, padding Space-M

## 7.6 Notification
1. Top-right stacked, auto close 5s
2. White bg, Shadow-2, Radius-M
3. Title `text-body-main` Medium, content `text-caption` Neutral-500

---

# 8. Global Interaction States
All components MUST implement these 5 states — NO EXCEPTIONS:
1. Default: Base token values
2. Hover: Light primary bg / border change
3. Active: Darker color, scale 0.98
4. Focus: Input glow; others text color change
5. Disabled: Opacity 0.5, no hover, no click
6. Loading: Animation, locked interaction

---

# 9. AI Code Generation Mandatory Clauses (Highest Priority)
## 9.1 Token Rules
1. NO hardcoded colors, sizes, radius; use only Tokens in Chapter 1.
2. Derive new components from existing Tokens; no custom variables.

## 9.2 Layout & Typography Rules
1. All pages MUST use Sider + Header + Content.
2. All forms/cards MUST use 24-column Grid.
3. All modules MUST be wrapped in Card.
4. **No Inline Font Styles:** CodeX/AI Agents are strictly forbidden from writing custom inline font-size or line-height declarations (e.g., `font-size: 13px` or `line-height: 18px`). All formatting must strictly reference the typography tokens defined in Section 1.2.
5. **Enforce Text Color Semantics:** Primary dark text must be strictly bound to `#111827` or `#1A1A1A` (Neutral-900 / Neutral-700 equivalent ranges). Secondary muted descriptive text must be `#6B7280` or `#4B5563` (Neutral-500).
6. **No Vertical Borders in Lists/Tables:** Data separation should rely purely on light horizontal divider borders or padded spatial layout rules (`space-x-*`).

## 9.3 Component Rules
1. Strictly follow component specs in Chapters 4–7.
2. Derive missing components from similar styles.
3. Forms, tables, modals must 1:1 match reference UI.

## 9.4 Output Rules
1. Component-based code, reuse Tokens.
2. Add comments referencing spec sections.
3. Provide visual check list: color, size, radius, states.

## 9.5 Forbidden Actions (AI MUST NOT DO)
1. No custom hex/rgba colors.
2. No non-8px spacing / custom font sizes.
3. No undefined radius/shadow.
4. No modified Layout/Grid rules.
5. No removed interaction states.
6. No third-party UI/icon libraries.

---

# Supplementary Notes
1. For special business components not covered, derive from similar base components and update this document after delivery.
2. This spec will be updated with page iterations; update version number each time.
3. UI designers will verify all pages against this document before release.
