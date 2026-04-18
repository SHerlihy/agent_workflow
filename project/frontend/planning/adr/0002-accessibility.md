# ADR 0002: Accessibility

## Status
Draft

## Context
Ensuring the application is usable by everyone, including people with disabilities, is a core requirement for inclusivity and legal compliance.

## Decision
[Clearly state the chosen path. Include technical details, libraries, or patterns to be used.]

### Compliance Level

The application must meet the key requirements for compliance level AA and additional key requirements.
Below are the key requirements for compliance the application must meet:
       * Alt Text: Non-text content (images) must have text alternatives.
       * Captions: Prerecorded video must have captions.
       * Keyboard Accessible: Everything must be usable via keyboard (no "keyboard traps").
       * Meaningful Sequence: Content must be presented in a logical reading order.
       * No Flashing: Nothing flashes more than three times per second (prevents seizures).
       * Enhanced Contrast: Text contrast ratio must be at least 7:1.
       * Resizing Text: Users must be able to zoom text up to 200% without losing functionality or content.
       * Navigation: Consistent navigation menus across the site and multiple ways to find a page (e.g., search + sitemap).
       * Headings & Labels: Forms and pages must have clear, descriptive headings and labels.
       * Focus Visible: It must be visually obvious which element currently has keyboard focus (the "focus ring").
       * No Background Audio: Audio shouldn't play automatically, or it must be easily muted.
       * Context-Sensitive Help: Providing help for complex forms or interactions.
       * Lower Reading Level: Content should be understandable by someone with a lower secondary education level.

## Consequences
- **Positive:** Wider audience reach, better SEO, and cleaner HTML structure. Adhering to compliance level AA will allow screen reader support.
- **Negative:** Restriction on component design and usage patterns.
- **Neutral:** Requires specialized testing tools and knowledge.

## Compliance

### Dev

Linting using eslint-plugin-jsx-a11y to address missing alt text, incorrect ARIA roles, and un-labeled inputs in real-time.
   * Storybook A11y Addon: If you use Storybook for your component library, this addon runs an audit on every component state automatically, ensuring your "building blocks" are accessible before they are used in the app.

### CI

   * Pa11y: A CLI tool that can be configured to fail a build if accessibility errors are found. It’s great for scanning multiple URLs or a sitemap automatically.
   * axe-playwright / axe-cypress: If you have End-to-End (E2E) tests, you can integrate these libraries to run accessibility audits as part of your functional test suite.
   * WebAIM Contrast Checker: A simple web tool to check if your foreground/background hex codes meet the 4.5:1 (AA) or 7:1 (AAA) ratios.
   * WhoCanUse: A great tool that shows how your color choices affect people with different types of color blindness and situational visual impairments (like glare).

### Manual

Choosing not to mandate


## References
[Links to related ADRs, documentation, or external resources]
