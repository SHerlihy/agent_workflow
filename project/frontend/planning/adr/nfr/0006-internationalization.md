# ADR 0006: Internationalization (i18n)

## Status
Accepted

## Context
To become a global marketplace, we must support multiple languages, regional formats (dates, numbers), and localized currencies. Hard-coding strings is a significant technical debt risk.

## Decision
We will use **`react-i18next`** with a **JSON-based Translation Strategy**:
1. **Tooling:** Use `i18next` with `i18next-browser-languagedetector` for automatic locale detection.
2. **Storage:** Store translation keys in JSON files (e.g., `locales/en/common.json`). Use "Namespaces" to split large translation files (e.g., `marketplace`, `auth`, `dashboard`).
3. **Currency & Dates:** Use the native `Intl` API (e.g., `Intl.NumberFormat`, `Intl.DateTimeFormat`) to handle localized formatting dynamically based on the current locale.
4. **Fallback:** Default to `en-US` if a specific translation or locale is unavailable.
5. **Key Management:** Use descriptive, hierarchical keys (e.g., `checkout.modal.title`) rather than using the original text as the key.

## Consequences
- **Positive:** Scalability to new markets; cleaner component code (no hard-coded strings).
- **Negative:** Overhead in managing translation files; potential layout issues due to varying text lengths across languages.
- **Neutral:** Requires a systematic approach to adding new strings during development.

## Compliance
- **Linting:** Custom ESLint rule or `i18next-parser` to ensure no hard-coded strings exist in `src/`.
- **CI:** Automated check to ensure all translation files have matching keys across languages.
- **Manual:** Verified "Right-to-Left" (RTL) layout support if Arabic or Hebrew are added.

## References
- [react-i18next Documentation](https://react.i18next.com/)
