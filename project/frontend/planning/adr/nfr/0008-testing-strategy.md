# ADR 0008: Testing Strategy

## Status
Accepted

## Context
High confidence in deployments is mandatory. We need a testing strategy that balances speed, cost, and coverage to prevent regressions in a complex marketplace environment.

## Decision
We will adopt the **"Testing Trophy"** model, prioritizing Integration tests:
1. **Static (Linting/Types):** Use TypeScript (Strict Mode) and ESLint to catch syntax and type errors before execution.
2. **Unit Tests (Vitest):** Focus on pure functions, utility logic, and domain entities (e.g., price calculations, inventory logic).
3. **Integration Tests (Vitest + React Testing Library):** The bulk of our tests. Verify component interactions and hooks without full E2E overhead. Use MSW (Mock Service Worker) to intercept network calls.
4. **E2E Tests (Playwright):** Verify critical user paths: "Search -> Preview -> Checkout -> Download". Test across multiple browsers and viewports.
5. **Coverage Goal:** Target 80% line coverage for the `Entities`, `Features`, and `Shared` layers. Coverage in `Pages` is secondary to E2E verification.

## Consequences
- **Positive:** High confidence during refactors; early detection of breaking changes; serves as executable documentation.
- **Negative:** Significant time investment; requires maintaining mocks (MSW) and test environments.
- **Neutral:** Requires a "Testing-First" mindset in the development team.

## Compliance
- **CI/CD:** Every Pull Request must pass the full test suite.
- **Reporting:** Codecov or similar to track coverage trends.
- **Maintenance:** Quarterly "Test Health" audit to remove slow or flaky tests.

## References
- [Testing Library Guiding Principles](https://testing-library.com/docs/guiding-principles/)
- [MSW (Mock Service Worker)](https://mswjs.io/)
