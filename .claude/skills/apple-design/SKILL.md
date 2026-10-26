---
name: apple-design
description: Design interfaces the way Apple would, grounded in the Human Interface Guidelines (HIG) and Apple's WWDC design talks. Use when designing or reviewing any UI (iOS/macOS/visionOS apps or web UIs that should feel native), choosing layout, typography, color, spacing, navigation, motion, or accessibility, or when asked to make something "feel like Apple" / "more polished".
---

# Apple Design

Apple's design as the foundation. Two sources of truth:

| Source | What it gives you |
|---|---|
| **HIG** — [Human Interface Guidelines](https://developer.apple.com/design/human-interface-guidelines) | Platform conventions, components, layout, typography, color, accessibility |
| **WWDC** — [Design talks](https://developer.apple.com/videos/design/) | The reasoning behind the rules: hierarchy, motion, materials, "Liquid Glass", fluid interfaces |

When a decision is unclear, look it up in the HIG first, then check the matching WWDC talk. Don't invent a pattern where Apple already has one.

## Core principles

1. **Hierarchy** — Content first, controls recede. One primary action per screen.
2. **Harmony** — Match the platform: system fonts, system colors, standard components, concentric corner radii.
3. **Consistency** — Same gesture, same result, everywhere. Reuse platform idioms instead of custom ones.
4. **Clarity** — Legible text, precise icons, generous whitespace, no decoration without purpose.
5. **Deference & depth** — Translucent materials and layering convey context; motion explains where things come from and go.

## Concrete rules

**Layout**
- Respect safe areas; standard margins (16pt compact, 20pt regular).
- 8pt spacing grid; group related items, separate unrelated ones with space, not lines.
- Minimum hit target **44×44pt**.

**Typography**
- SF Pro / SF Pro Rounded (web: `-apple-system, BlinkMacSystemFont, "SF Pro Text", system-ui`).
- Use the Dynamic Type scale (Large Title 34, Title 28/22/20, Headline 17 semibold, Body 17, Callout 16, Subheadline 15, Footnote 13, Caption 12/11). Support text scaling.
- Hierarchy via weight and size, not color alone.

**Color**
- Semantic system colors (`label`, `secondaryLabel`, `systemBackground`, `tint`) that adapt to light/dark and increased contrast.
- One accent/tint color for interactive elements.
- Contrast ≥ 4.5:1 for text.

**Navigation**
- Tab bar for top-level sections (2–5), navigation stack for drill-down, sheets for focused tasks, alerts only for critical decisions.
- Back always works; destructive actions are confirmed and styled destructive.

**Materials & shape**
- Use system materials (blur/vibrancy, Liquid Glass) for chrome floating over content, not for content itself.
- Continuous ("squircle") corners; nested radii stay concentric (inner = outer − padding).

**Motion**
- Springs over linear easing; animations are interruptible and short (≈0.2–0.5s).
- Motion has meaning (spatial continuity), honors Reduce Motion.

**Accessibility (non-negotiable)**
- VoiceOver labels for every control, Dynamic Type, Reduce Motion/Transparency, sufficient contrast, no color-only signals.

## Workflow

1. Identify the platform and the matching HIG pages (component + pattern).
2. Sketch hierarchy: what is the one thing the user came to do?
3. Build from standard components; customize only tint, content, and imagery.
4. Review against the checklist below.

## Review checklist

- [ ] One clear primary action; secondary actions visually quieter
- [ ] Standard components and navigation patterns used
- [ ] System fonts + Dynamic Type; system/semantic colors; dark mode works
- [ ] 44pt targets, safe areas, 8pt grid
- [ ] Concentric corners, materials only on chrome
- [ ] Spring motion, Reduce Motion respected
- [ ] VoiceOver labels and contrast verified
