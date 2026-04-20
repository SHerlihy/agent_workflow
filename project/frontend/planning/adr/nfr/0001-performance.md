# ADR 0001: Performance

## Status
Accepted

## Context
A digital marketplace lives and dies by its speed. Slow catalog loading or sluggish filtering directly impacts conversion rates. We need to define strict performance targets and the architectural choices to meet them.

## Decision
We will adopt a **"Core-First" Performance Strategy**:
1. **Bundling & Splitting:** Use Vite for ESM-based development and Rollup-based production builds. Implement route-based code splitting and "Feature-based" lazy loading (e.g., loading the checkout logic only when the user clicks 'Buy').
2. **Data Fetching:** TanStack Query for smart caching, background revalidation (Stale-While-Revalidate), and request deduplication.
3. **Image Optimization:** Use modern formats (WebP/AVIF) with `srcset` for responsive images. Implement lazy loading for all images outside the initial viewport.
4. **State Management:** Keep state local to features whenever possible. Avoid global providers that cause app-wide re-renders. Use "Signals" or localized `Context` for reactive updates.
5. **Target Metrics:**
    - LCP (Largest Contentful Paint) < 2.5s
    - FID (First Input Delay) < 100ms
    - CLS (Cumulative Layout Shift) < 0.1

## Consequences
- **Positive:** Improved SEO rankings, higher user retention, and better experience on low-end devices.
- **Negative:** Requires disciplined component design and regular performance profiling.
- **Neutral:** Shifts more complexity into the build pipeline and asset management.

## Compliance
- **CI/CD:** Automated Lighthouse/Web-Vitals audit on every PR. Builds fail if metrics drop below established baselines.
- **Linting:** Rules to prevent large third-party imports (e.g., `import { map } from 'lodash'` vs `import map from 'lodash/map'`).
- **Monitoring:** RUM (Real User Monitoring) via the Observability stack.

## References
- [ADR 0007: Observability](./0007-observability.md)
- [Vite Performance Guide](https://vitejs.dev/guide/performance.html)
