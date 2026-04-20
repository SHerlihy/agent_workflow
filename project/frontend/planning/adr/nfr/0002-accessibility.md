# ADR 0002: Accessibility (A11y)

## Status
Accepted

## Context
Accessibility is a core functional requirement. The marketplace must be usable by all users, including those using screen readers or keyboard-only navigation. We aim for a "Level AA+" standard, intentionally exceeding base requirements in key areas to ensure maximum inclusivity.

## Decision
The application will adhere to **WCAG 2.1 Level AA** as a baseline, with specific **Level AAA** enhancements.

### Key Requirements (AA+ Ambition)
- **Enhanced Contrast (AAA):** Text contrast ratio must be at least **7:1** (exceeding the 4.5:1 AA standard).
- **Lower Reading Level (AAA):** Content must be understandable by someone with a lower secondary education level.
- **Alt Text:** Non-text content (images) must have text alternatives.
- **Keyboard Accessible:** Everything must be usable via keyboard (no "keyboard traps").
- **Meaningful Sequence:** Content must be presented in a logical reading order.
- **No Flashing:** Nothing flashes more than three times per second.
- **Resizing Text:** Users must be able to zoom text up to 200% without loss of functionality.
- **Navigation:** Consistent menus and multiple ways to find pages (search + sitemap).
- **Headings & Labels:** Clear, descriptive headings and labels for all forms and pages.
- **Focus Visible:** Visually obvious focus rings for all interactive elements.
- **No Background Audio:** Audio must not play automatically.
- **Context-Sensitive Help:** Providing help for complex interactions.

*Note: As the application does not include video content, captioning requirements are currently out of scope.*

## Consequences
- **Positive:** Superior inclusivity, exceptional SEO, and robust legal compliance.
- **Negative:** Stricter design constraints due to high contrast requirements (7:1).
- **Neutral:** Strict reliance on automated verification limits the detection of purely experiential accessibility issues.

## Compliance

### Dev (Automation)
- **ESLint:** Use `eslint-plugin-jsx-a11y` to catch errors (alt text, ARIA roles, labels) in real-time.
- **Storybook:** Use the A11y Addon to audit components during the building block phase.

### CI (Targeted Automation)
- **Pa11y:** Automated scans of the sitemap/URLs to catch regression errors.
- **axe-playwright:** Accessibility audits are **mandated for critical path E2E tests** (e.g., Asset Search, Checkout Flow, User Dashboard) to ensure zero blockers on high-value transactions.
- **Contrast Checking:** Automated validation of CSS variables against the 7:1 ratio.

### Manual
- **Not Mandated:** Compliance relies strictly on the automated suite defined above to maintain developer velocity and objective verification.

## References
- [WCAG 2.1 Guidelines](https://www.w3.org/WAI/WCAG21/quickref/)
- [ADR 0008: Testing Strategy](./0008-testing-strategy.md)
