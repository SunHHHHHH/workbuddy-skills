# Product register

When design SERVES the product: app UIs, admin dashboards, settings panels, data tables, tools, authenticated surfaces, anything where the user is in a task.

## The product slop test

Would a user fluent in the category's best tools (Linear, Figma, Notion, Raycast, Stripe) sit down and trust this interface, or pause at every subtly-off component? The tool should disappear into the task.

## Typography

- **One family is often right.** A well-tuned sans carries headings, buttons, labels, body, data.
- **Fixed rem scale, not fluid.** Users view at consistent DPI.
- **Tighter scale ratio.** 1.125-1.2 between steps.
- **Line length still applies for prose** (65-75ch). Tables at 120ch+ are fine.

## Color

Product defaults to Restrained. State-rich semantic vocabulary: hover, focus, active, disabled, selected, loading, error, warning, success, info.
- Accent color used for primary actions, current selection, and state indicators only.
- A second neutral layer for sidebars, toolbars, panels.

## Layout

Responsive behavior is structural (collapse sidebar, responsive table, breakpoint-driven columns), not fluid typography.

## Components

Every interactive component has: default, hover, focus, active, disabled, loading, error.
- Skeleton states for loading, not spinners.
- Empty states that teach the interface.
- Consistent affordances across the surface.

## Motion

- 150-250 ms on most transitions. Users are in flow.
- Motion conveys state, not decoration.
- No orchestrated page-load sequences.

## Product bans

- Decorative motion that doesn't convey state.
- Inconsistent component vocabulary across screens.
- Display fonts in UI labels, buttons, data.
- Reinventing standard affordances for flavor.
- Heavy color or full-saturation accents on inactive states.
- Modal as first thought.

## Product permissions

- System fonts and familiar sans defaults (Inter, SF Pro, system-ui stacks).
- Standard navigation patterns: top bar + side nav, breadcrumbs, tabs, command palettes.
- Density. Tables with many rows, panels with many labels.
- Consistency over surprise.
