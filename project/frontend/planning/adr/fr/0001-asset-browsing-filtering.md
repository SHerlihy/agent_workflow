# ADR FR-0001: Asset Browsing and Filtering Logic

## Status
Accepted

## Requirement Context
The marketplace requires users to browse a large catalog of digital assets. Users must be able to filter by category, price range, and search by keywords. The experience must be fast and shareable via URLs.

## Decision
We will implement a **Hybrid Filtering Strategy**:
1. **Initial Load:** Fetch the first page of assets from the API using TanStack Query.
2. **URL Synchronization:** All filter states (category, search, min/max price) will be mirrored in the URL search parameters using a `useURLState` custom hook.
3. **Server-Side Search:** Keyword search and broad category filters will trigger a new API request to ensure the entire database is searchable.
4. **Client-Side Refinement:** Small refinements (e.g., sorting by "Recent" or "Price Low-High" on the current page) will be performed client-side to provide instant feedback.

## Consequences
- **Positive:** Deep-linking works out of the box; users can share specific filtered views.
- **Negative:** Increased complexity in keeping the UI state, URL, and API results in sync.
- **Neutral:** Requires robust debounce logic for the search input to prevent API hammering.

## Implementation Details
- Hook: `useAssetFilters` to manage `Record<string, any>` state.
- Debounce: 300ms for text inputs.
- Validation: Zod schema to parse URL parameters into typed filter objects.
