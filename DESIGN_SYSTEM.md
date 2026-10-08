# Nestora design system

Nestora brings groceries, clothing, and storage together for a shared household.
Its visual identity should feel welcoming, clear, and organized. Use the rounded
nest-and-home emblem, vivid indigo, and warm coral across iOS and the website.

## Brand assets

The approved source is `design/icon-concepts/nestora-nest-home.png` (1254 × 1254).
It was generated with the built-in image tool. Its prompt direction was a single
rounded roof above two bold nest curves, centered, flat coral on solid indigo,
with no text. Retain the supplied artwork rather than redrawing it from this prompt.

- App icon: `StockFoyer/Resources/Assets.xcassets/AppIcon.appiconset/AppIcon-1024.png`.
- In-app mark: `StockFoyer/Resources/Assets.xcassets/NestoraMark.imageset/nestora-mark.png`.
- Website: `nestora-site/assets/nestora-icon.png`, `apple-touch-icon.png`, and `favicon-32.png`.

Export the iOS icon as an opaque, square 1024 × 1024 PNG. Do not bake in rounded
outer corners: the system supplies its mask. For in-app and website displays,
round the square using a radius of approximately 22.5% of its width. Preserve the
original composition, background, proportions, and internal clear space. Do not
stretch, recolor, add text, or add shadows to the mark. The icon artwork stays the
same in both appearances; interface colors adapt separately.

## Color roles

| Role | Light | Dark | Use |
| --- | --- | --- | --- |
| Indigo / action | `#0C17CE` | `#AEAFFF` | Interactive tint, navigation selection, feature symbols, links, focus |
| Primary button label | `#FFFFFF` | `#131322` | Readable labels on indigo / lavender action fills |
| Coral / brand warmth | `#FF7B54` | `#FF9678` | Decorative brand accents; not small text or status |
| Canvas | `#F6F5FC` | `#131322` | Branded screen and website backgrounds |
| Surface | `#FFFFFF` | `#202035` | Cards and grouped content |
| Soft accent | `#ECEBFF` | `#2B2A50` | Icon tiles, highlighted sections |
| Website primary text | `#202035` | `#F6F5FC` | Headings and body text |
| Website secondary text | `#5D5C73` | `#B9B8CE` | Supporting copy |
| Website border | `#DEDDEE` | `#3E3D59` | Card outlines and dividers |

iOS text uses semantic `.primary` and `.secondary` colors. Native lists, forms,
alerts, sheets, and toolbars keep system surfaces and behavior. Keep semantic
red, orange, and green for errors, review warnings, and success; never substitute
brand coral for an error. Coral is decoration because it has insufficient contrast
for small text on a light surface. Dark-mode indigo is lighter for readability.

## iOS implementation

`StockFoyer/App/NestoraTheme.swift` exposes shared colors, spacing, corner radii,
`NestoraBrandIcon`, `nestoraCard()`, and `nestoraPrimaryAction()`. Color values live in the
asset catalog, with explicit light/dark variants. `AccentColor` matches
`BrandIndigo`; update both together. The app entry point applies the accent tint
to onboarding, navigation, and presented controls.

- Use `NestoraBrandIcon` for brand introductions, not feature icons. Its image is
  decorative when the nearby text already names Nestora.
- Use SF Symbols for groceries, wardrobe, scanner, storage, and household actions.
- Use `nestoraCard()` for custom content cards. Native forms and lists retain
  their own layout rather than being wrapped in additional cards.
- Use indigo symbols on soft-accent tiles for overview cards.
- Use `nestoraPrimaryAction()` for prominent buttons: it retains the native style
  and gives labels a dark foreground on lavender in dark mode.
- Maintain native tab bars, navigation, keyboard behavior, and sheets.

## Layout and typography

The shared spacing scale is 8, 16, 24, and 32 points/pixels. Custom cards have a
20-point radius; feature icon tiles use 16 points. Default screen padding is 24
points, with adaptive columns on wider screens. Use generous clear space around
the mark and group related content together.

Use system fonts. In iOS use semantic text styles (`.largeTitle`, `.title2`,
`.headline`, `.body`, `.footnote`) to support Dynamic Type. Fixed-size symbols
are decorative; do not use fixed font sizes for essential content. The website
uses responsive heading sizes and a system font stack.

## Accessibility

Keep controls at least 44 points/pixels tall. Preserve readable semantic text,
visible keyboard focus, and text labels alongside meaningful symbols. Never
convey selection, warnings, or errors with color alone. Check large text and
compact widths, including long household names. The website respects system
appearance and reduced-motion preferences. Brand images use empty alternative
text when adjacent Nestora text already gives the accessible name.

## Website implementation

The website is a separate repository in `nestora-site/`. Its CSS custom properties
mirror these tokens. All English and French home/privacy pages use the approved
mark, favicon, and Apple touch icon. Keep localized content and language navigation
in sync. A copy of this guide lives in the website repository for standalone work;
update both copies when changing shared rules.

## Future change checklist

1. Start a dedicated `codex/` branch in each repository being changed.
2. Reuse the shared tokens and approved assets before adding a new style.
3. Update this guide and its website copy whenever a visual rule changes.
4. Build the iOS simulator target and inspect onboarding and Home in light/dark
   mode, compact/wide layouts, and larger text.
5. Preview English/French home and privacy pages at desktop and phone widths;
   check image/link paths, focus states, and appearance variants.
6. Publish or release only as part of a requested deployment/release task.
