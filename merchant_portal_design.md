# Merchant Portal Design Specification
## Document Basic Info
| Item | Content |
| ---- | ---- |
| Document Name | merchant_portal_design.md - Merchant Portal Design Specification |
| Version | V1.0 |
| Updated Date | 2026-06-02 |
| Reference UI | https://demo-remote.e-com365.com/vinnia/galaxiaslabs-dashboard/index.html |
| Scope | All pages, new pages, and iteration pages of the Merchant Portal |
| Users | Frontend Developers, AI Code Agents, UI Designers |
| Core Rules | All new components/pages MUST strictly follow the Design Tokens and component rules in this document. Custom colors, font sizes, border radius, shadows, and spacing are forbidden. Page layout and interactions must fully align with the reference HTML page. |

---

# Table of Contents
1. 【Basic Design Tokens】Global Variables (Color / Font / Spacing / Radius / Shadow / Border)
2. 【Layout System Specification】Grid, Layout, Space, Divider
3. 【Typography Specification】Full-level text rules
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
- Primary-100: Light background #E6F0FF
- Primary-300: Light hover #94C1FF
- Primary-500: Standard primary (buttons / tag highlights) #1677FF
- Primary-700: Dark hover #0F52BA
- Primary-900: Text highlight #062D66

### Functional Status Colors
- Success-500: Success, approved, completed #00B42A
- Warning-500: Warning, pending #FF7D00
- Danger-500: Delete, error, failed #F53F3F
- Info-500: Info, auxiliary text #86909C

### Neutral Grays (Text, borders, backgrounds, dividers)
- Neutral-0: Pure white #FFFFFF
- Neutral-100: Page background #F2F3F5
- Neutral-200: Card light gray background #E5E6EB
- Neutral-300: Dividers, light borders #C9CDD4
- Neutral-400: Input default border #86909C
- Neutral-500: Secondary text #4E5969
- Neutral-600: Body text #272E3B
- Neutral-700: Title text #1D2129
- Neutral-900: Deepest text, bold titles #0A0C10

### Transparent Mask Color
- Mask-Bg: Modal background overlay rgba(0,0,0,0.45)

## 1.2 Font Specification
### Font Family
`Inter, -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif`

### Font Size Levels (Global unified, custom sizes forbidden)
| Level | Font Size | Line Height | Weight | Usage |
| ---- | ---- | ---- | ---- | -------- |
| H1 | 32px | 40px | 600 | Page top-level title (rarely used) |
| H2 | 24px | 32px | 600 | Page main title, card header title |
| H3 | 20px | 28px | 600 | Modal title, section subtitle |
| H4 | 18px | 26px | 500 | Form group title, table header |
| Body-L | 16px | 24px | 400 | Large body text, table content |
| Body-M (Default) | 14px | 22px | 400 | Most page text, input default text |
| Body-S | 12px | 18px | 400 | Auxiliary text, notes, small tips |
| Caption | 11px | 16px | 400 | Tag small text, timestamp, footer copyright |

### Font Weight Enums
- Regular: 400 (Normal body text)
- Medium: 500 (Subtitles, input labels)
- SemiBold: 600 (All headings)

## 1.3 Spacing System (Base unit: 8px, all multiples of 8)
### Base Spacing Variables
- Space-XS: 4px
- Space-S: 8px
- Space-M: 16px
- Space-L: 24px
- Space-XL: 32px
- Space-XXL: 48px

### Component Inner Spacing Rules
1. Form input padding: Vertical Space-XS, Horizontal Space-S
2. Card padding: Vertical Space-M, Horizontal Space-M
3. Table cell padding: Vertical Space-S, Horizontal Space-M
4. Modal header/footer padding: Vertical Space-M, Horizontal Space-L
5. Section margin: Space-L

## 1.4 Border Radius
| Variable | Value | Usage |
| ---- | ---- | -------- |
| Radius-XS | 2px | Table cells, tiny tags |
| Radius-S | 4px | Inputs, dropdowns, checkboxes, radios |
| Radius-M (Default) | 6px | Buttons, cards, modals, drawers |
| Radius-L | 8px | Large buttons, upload image containers |
| Radius-Circle | 50% | Avatars, circular icon buttons |

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
3. Divider with text: Body-S, Neutral-500, line padding Space-M
4. Custom divider color/thickness forbidden.

---

# 3. Typography Specification
## 3.1 Heading Rules
1. Only H1–H4 allowed; no H5/H6
2. Heading bottom margin: Space-M; top margin: Space-L
3. All headings: 600 weight, no changes allowed.

## 3.2 Body Text Rules
1. Default text: Body-M (14px) Neutral-600
2. Secondary text: Body-S (12px) Neutral-500
3. Link text: Primary-500, hover Primary-700, underline on hover only
4. Forbidden: Pure black #000; use Neutral-900 for darkest text.

## 3.3 Special Text Styles
- Bold text: 500 weight, keep original color
- Error text: Danger-500 (form errors, failure tips)
- Success text: Success-500 (success status)
- Warning text: Warning-500 (risk warnings)

---

# 4. General Basic Components
## 4.1 Button
### Sizes
- Large: H40px, padding H20px, Body-L, Radius-L
- Default: H32px, padding H16px, Body-M, Radius-M
- Small: H24px, padding H12px, Body-S, Radius-S

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
1. Text: Body-M, separator “/”, color Neutral-400
2. History page: Neutral-500, hover Primary-500
3. Current page: Neutral-700, no hover
4. Bottom margin: Space-L

## 4.5 Dropdown
1. Container: Radius-M, Shadow-2, bg Neutral-0, min-width 120px
2. Item: H32px, padding H16px, Body-M
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
1. Text: Body-M, button H32px, Radius-S
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
1. Label: Body-M Medium 500 Neutral-600; vertical space Space-XS
2. Required: Red * suffix (Danger-500)
3. Input height: 32px, Radius-S, 1px Neutral-300 border
4. Focus: Border Primary-500, glow 0 0 0 2px rgba(22,119,255,0.2)
5. Disabled: Bg Neutral-100, text Neutral-400
6. Error tip: Body-S Danger-500, margin Space-XS below input
7. Form row vertical spacing: Space-L

## 5.1 Input / SelectInput
1. Padding: H Space-S, V Space-XS
2. Placeholder: Neutral-400
3. Prefix/suffix icon: 16px Neutral-400, space Space-XS
4. Character count: Body-S Neutral-400 at bottom-right

## 5.2 Textarea
1. Default H80px, vertical resize only
2. Style matches Input
3. Character count at bottom-right

## 5.3 Checkbox
1. Box 16×16px, Radius-XS, border Neutral-300
2. Checked: Bg Primary-500, white check icon
3. Checkbox-text gap: Space-S, text Body-M

## 5.4 Radio
1. Circle 16px, border Neutral-300; checked inner 8px Primary-500
2. Group spacing: Space-M
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
3. Scale text: Body-S Neutral-500

## 5.11 Upload
### Drag Area
1. 1px Neutral-300 dashed border, Radius-M, padding Space-XL
2. Icon 24px Neutral-400, text Body-M Neutral-500
3. Hover: dashed border Primary-300, bg Primary-100

### File List Card
1. Item H48px; thumbnail, filename, delete Danger-500
2. Progress bar: H4px, bg Neutral-200, progress Success-500

## 5.12 Form Container
1. Two layouts: Horizontal (label left), Vertical (label top)
2. Action buttons: Align right, gap Space-M, top margin Space-L
3. Large forms: Wrap in Card, padding Space-L

---

# 6. Data Display Components
## 6.1 Avatar
1. Sizes: 24px / 32px / 40px / 64px, Radius-Circle
2. Text avatar: Bg Primary-300, white text
3. Status badge: Small dot at bottom-right

## 6.2 Badge
1. Number badge: Bg Danger-500, white Body-S, min-width 16px, Radius-Circle
2. Status dot: 8px circle (Success/Warning/Danger/Info)
3. Text tag: H24px, padding H Space-S, Radius-S; default bg Neutral-200

## 6.3 Card
1. Bg Neutral-0, Radius-M, Shadow-2
2. Header: padding V Space-M, bottom 1px Neutral-200 border; title H4
3. Body: padding V Space-M, H Space-L
4. Footer: padding V Space-M, top 1px Neutral-200 border
5. No-shadow card: White bg radius only (for inner modals)

## 6.4 Table
1. Radius-M, 1px Neutral-200 outer border
2. Header: Bg Neutral-100, text Medium 500 Neutral-700
3. Body: White bg, text Body-M Neutral-600; row hover bg Primary-100
4. No zebra stripe by default
5. Cell text vertical center; long text ellipsis, tooltip on hover
6. Action buttons: Small size, gap Space-S
7. Top filter: Inline form, with add/export buttons on right

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
2. Left avatar/icon, middle title + Body-S, right text button
3. Wrap in Card

## 6.8 Loading
1. Local: 16px spinner, text Body-S Neutral-500
2. Global: 40px spinner, mask rgba(255,255,255,0.7)

## 6.9 Skeleton
1. Gradient animation Neutral-200 ~ Neutral-100
2. Match real layout height and radius
3. Full page skeleton for tables/cards

## 6.10 Statistic
1. Value H2 SemiBold, title Body-S Neutral-500
2. Trend: Success/Danger text with arrow
3. Multiple stats: gap Space-M, wrap in Card

## 6.11 Timeline
1. Left line 2px Neutral-200, node 12px status color
2. Title Body-M Medium, content Body-S Neutral-500
3. Vertical spacing Space-M

## 6.12 Tooltip
1. Container Radius-S, Shadow-3, bg Neutral-700, white Body-S
2. Auto position, delay 200ms

## 6.13 Calendar
Same as DatePicker calendar, with month switch

## 6.14 Image / ImageViewer
1. Image container Radius-S, 1px Neutral-200 border
2. Viewer: Full screen mask, center image, close button top-right

## 6.15 Comment
1. Top: Avatar + name + time
2. Content: Body-M
3. Bottom: Like/reply text buttons
4. Bottom margin Space-M, divider 1px Neutral-200

---

# 7. Popup & Overlay Components
## 7.1 Dialog
1. Mask: Mask-Bg, click to close
2. Container: White bg, Radius-M, Shadow-3
    - Header: H60px, padding H Space-L, title H3, close icon 16px
    - Body: padding H Space-L, V Space-M; max height 60vh, scrollable
    - Footer: padding V Space-M, H Space-L; buttons align right, gap Space-M
3. Sizes: Small 480px, Standard 720px, Large 1000px

## 7.2 Drawer
1. Slide from right; width 480px / 720px
2. Structure same as Dialog; top radius Radius-M
3. Slide animation, click mask to close

## 7.3 PopConfirm
1. Based on Tooltip, with Confirm/Cancel small buttons
2. Warning icon Warning-500, text Body-M

## 7.4 Popup
Base container same as Dropdown, padding Space-M

## 7.5 Message
1. Top center, auto close 3s
2. 4 types: Success/Warning/Danger/Info
3. White bg, Shadow-2, Radius-S, padding Space-M

## 7.6 Notification
1. Top-right stacked, auto close 5s
2. White bg, Shadow-2, Radius-M
3. Title Body-M Medium, content Body-S Neutral-500

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
1. NO hardcoded colors, sizes, radius; use only Tokens in Chapter 1
2. Derive new components from existing Tokens; no custom variables

## 9.2 Layout Rules
1. All pages MUST use Sider + Header + Content
2. All forms/cards MUST use 24-column Grid
3. All modules MUST be wrapped in Card

## 9.3 Component Rules
1. Strictly follow component specs in Chapters 4–7
2. Derive missing components from similar styles
3. Forms, tables, modals must 1:1 match reference UI

## 9.4 Output Rules
1. Component-based code, reuse Tokens
2. Add comments referencing spec sections
3. Provide visual check list: color, size, radius, states

## 9.5 Forbidden Actions (AI MUST NOT DO)
1. No custom hex/rgba colors
2. No non-8px spacing / custom font sizes
3. No undefined radius/shadow
4. No modified Layout/Grid rules
5. No removed interaction states
6. No third-party UI/icon libraries

---

# Supplementary Notes
1. For special business components not covered, derive from similar base components and update this document after delivery.
2. This spec will be updated with page iterations; update version number each time.
3. UI designers will verify all pages against this document before release.