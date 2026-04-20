# ADR 0005: Responsiveness

## Status
Accepted

## Context
Marketplace users browse assets on everything from mobile phones on public transit to ultra-wide 4K monitors in design studios. A "one size fits all" layout is not acceptable.

## Decision
We will implement a **Mobile-First, Fluid-Responsive Design**:
1. **Mobile-First:** Start all CSS with mobile styles and use `min-width` media queries to add complexity for larger screens.
2. **Standard Breakpoints:** Use a consistent set of CSS variables for breakpoints:
    - `--bp-sm`: 640px (Tablet Portrait)
    - `--bp-md`: 768px (Tablet Landscape)
    - `--bp-lg`: 1024px (Laptop)
    - `--bp-xl`: 1280px (Desktop)
3. **Fluid Typography & Spacing:** Use the `clamp()` function for font sizes and margins to ensure they scale smoothly between breakpoints without jarring jumps.
4. **Grid & Flexbox:** Use CSS Grid for high-level page layouts and Flexbox for component-level alignment. Avoid fixed pixel widths for containers.
5. **Interaction Optimization:** Ensure touch targets are at least 44x44px and implement specific hover-state logic for mouse-enabled devices.

## Consequences
- **Positive:** Improved UX across all device types; better performance by loading smaller assets for mobile users.
- **Negative:** Increased design and testing effort; requires more complex CSS logic.
- **Neutral:** Requires close collaboration with the design team on breakpoint behaviors.

## Compliance
- **Dev:** Responsive mode in Chrome DevTools and Storybook Viewports addon.
- **CI:** Screenshot comparisons (Visual Regression Testing) at multiple viewports using Playwright.
- **Peer Review:** Every UI PR must be verified on at least two different screen widths.

## References
- [MDN Responsive Design](https://developer.mozilla.org/en-US/docs/Learn/CSS/CSS_layout/Responsive_Design)
