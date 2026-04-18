# ADR 0004: Security

## Status
Proposed

## Context
The application handles sensitive data, including Personally Identifiable Information (PII) and payment information. Failure to secure this data would lead to significant customer dissatisfaction, legal liability, and operational overhead. Web applications are primary targets for Cross-Site Scripting (XSS), Cross-Site Request Forgery (CSRF), and data exfiltration. We need a multi-layered security strategy to minimize the attack surface.

## Decision
We will implement the following security layers:

1.  **Content Security Policy (CSP):** Implement a strict CSP via HTTP headers to prevent unauthorized script execution and data injection. We will use a "nonce-based" or "hash-based" approach for inline scripts and restrict `script-src` to trusted domains.
2.  **XSS Protection:**
    *   Rely on framework-level auto-encoding (React/TypeScript).
    *   Explicitly prohibit `dangerouslySetInnerHTML` via ESLint rules.
    *   Use `DOMPurify` for any mandatory rendering of user-provided HTML.
3.  **Secure Session Management:**
    *   Store session tokens in `HttpOnly`, `Secure`, and `SameSite=Strict` cookies.
    *   Avoid storing sensitive data or JWTs in `localStorage` or `sessionStorage`.
4.  **Dependency & Supply Chain Security:**
    *   Enable automated vulnerability scanning (GitHub Dependabot).
    *   Enforce `npm audit` checks in the CI/CD pipeline, failing builds on 'High' or 'Critical' vulnerabilities.
    *   Use Subresource Integrity (SRI) for any scripts loaded from external CDNs.
5.  **Transport & Framing:**
    *   Enforce HSTS (HTTP Strict Transport Security) to ensure all traffic is encrypted.
    *   Set `X-Frame-Options: DENY` or use CSP `frame-ancestors 'none'` to prevent Clickjacking.

## Consequences
- **Positive:** Robust protection of user PII and payment data; significant reduction in the risk of automated attacks (XSS/CSRF).
- **Negative:** Strict CSP may require more configuration for third-party analytics or widgets; `HttpOnly` cookies require a backend-for-frontend (BFF) or specific API architecture.
- **Neutral:** Security becomes a mandatory part of the "Definition of Done" for every feature.

## Compliance
- **CI/CD:** Automated `npm audit` and CSP validation scripts.
- **Linting:** ESLint rules to block dangerous patterns (e.g., `react/no-danger`).
- **Peer Review:** Security-focused checklist for all Pull Requests involving data handling or authentication.
- **Dependency Tracking:** Monthly manual audit of third-party script usage.

## References
- OWASP Top 10 Web Application Security Risks
- MDN Web Security Guidelines
- [ADR 0008: Testing Strategy](./0008-testing-strategy.md) (for security-focused E2E tests)
