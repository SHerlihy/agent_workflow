# ADR 0003: Browser Support

## Status
Accepted

## Context
Supporting every browser version is unsustainable. We need to target the most common browsers while ensuring a baseline experience for others, allowing us to use modern CSS and JS features.

## Decision
We will support the **"Last 2 Major Versions"** of all modern evergreen browsers:
1. **Target Browsers:** Chrome, Firefox, Safari, and Edge.
2. **IE Support:** Explicitly NO support for Internet Explorer. Users will be shown a "Browser Outdated" message.
3. **Transpilation:** Use `browserslist` with `@vitejs/plugin-legacy` to generate polyfills only when necessary.
4. **CSS Features:** Use PostCSS for autoprefixing. Prefer CSS Grid/Flexbox but provide fallback layouts (or simplified stacks) if key features are missing.

## Consequences
- **Positive:** Reduces bundle size by avoiding unnecessary polyfills; allows use of modern features like Optional Chaining, Nullish Coalescing, and CSS Variables.
- **Negative:** Users on outdated corporate or legacy systems may be unable to use the site.
- **Neutral:** Requires updating the `browserslist` configuration every 6 months.

## Compliance
- **CI:** Automated checks against `browserslist` during the build phase.
- **Analytics:** Monthly review of user agent data to ensure we aren't excluding a significant segment of our audience.

## References
- [Browserslist Documentation](https://github.com/browserslist/browserslist)
