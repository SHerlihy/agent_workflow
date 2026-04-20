# ADR 0007: Observability

## Status
Accepted

## Context
We cannot fix what we cannot see. Once in production, we need real-time data on errors, performance bottlenecks, and user interaction flows to maintain a high-quality marketplace.

## Decision
We will implement a **Multi-Tier Observability Stack**:
1. **Error Tracking:** Integrate Sentry for real-time error reporting, capturing breadcrumbs, user context, and release tracking.
2. **Instrumentation:** Use OpenTelemetry (OTEL) for vendor-neutral tracing. Instruments all API calls and key user transactions (e.g., Checkout flow).
3. **User Analytics:** Implement a privacy-conscious event collector (e.g., PostHog or internal gateway) to track feature usage (button clicks, search queries).
4. **RUM (Real User Monitoring):** Capture Core Web Vitals directly from users' browsers to detect performance regressions in the wild.
5. **Health Checks:** Implement a `/health` endpoint and use synthetic monitoring (pinging) for critical routes.

## Consequences
- **Positive:** Drastically reduced MTTR (Mean Time To Resolution); data-driven product decisions; proactive detection of outages.
- **Negative:** Minor performance impact from SDKs; potential privacy concerns (GDPR/CCPA).
- **Neutral:** Requires careful management of "Log Volume" to control costs.

## Compliance
- **Security:** Ensure PII (names, emails) and secrets are stripped from logs and error reports before transmission.
- **Review:** Every new feature must include "Analytics Hooks" as part of its Definition of Done.
- **Dashboarding:** Maintain a "Team Health" dashboard in Grafana/Sentry showing error rates and LCP.

## References
- [OpenTelemetry Documentation](https://opentelemetry.io/docs/instrumentation/js/)
- [ADR 0001: Performance](./0001-performance.md)
