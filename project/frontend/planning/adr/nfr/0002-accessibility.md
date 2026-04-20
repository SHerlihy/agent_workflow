# ADR 0002: Accessibility (A11y)

## Status
Accepted

## Context
Accessibility is a core functional requirement, not just a "nice to have". The marketplace must be usable by all users, including those using screen readers or keyboard-only navigation.

## Decision
We will adhere to **WCAG 2.1 Level AA** standards using the following toolkit:
1. **Semantic HTML:** Strict enforcement of semantic tags over generic `<div>`s.
2. **ARIA & Headless UI:** Use `react-aria` or `@radix-ui` for complex components (modals, dropdowns) to ensure correct keyboard behavior and screen reader support out of the box.
3. **Contrast & Typography:** Use CSS variables for colors that are pre-validated for a 4.5:1 (AA) ratio. Ensure font sizes are relative (`rem`) to support browser zooming.
4. **Focus Management:** Implement a consistent, high-visibility "Focus Ring" for all interactive elements. Use "Focus Traps" correctly in modals.
5. **Alt-Text:** Require alt-text for all decorative and informative images via ESLint.

## Consequences
- **Positive:** Legal compliance, improved SEO, and a better experience for users with temporary or permanent impairments.
- **Negative:** Increases development time for complex custom components.
- **Neutral:** Requires specific training and tools for the development team.

## Compliance
- **Dev:** `eslint-plugin-jsx-a11y` and Storybook A11y addon.
- **CI:** `axe-core` integration in Playwright E2E tests.
- **Manual:** Monthly manual audit using screen readers (VoiceOver/NVDA) and keyboard-only navigation tests.

## References
- [WCAG 2.1 Guidelines](https://www.w3.org/WAI/WCAG21/quickref/)
- [ADR 0008: Testing Strategy](./0008-testing-strategy.md)
