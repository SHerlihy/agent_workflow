# ADR FR-0003: User Inventory Persistence Strategy

## Status
Proposed

## Requirement Context
Users need immediate access to their purchased assets without waiting for full API synchronization every time they visit the dashboard.

## Decision
We will implement an **Offline-First Inventory Cache**:
1. **Primary Source:** The API remains the source of truth for ownership.
2. **Local Cache:** Use `IndexedDB` (via Dexie.js or similar) to store a local copy of the user's asset metadata.
3. **Reconciliation:** On application mount, the client will fetch the "Latest Transaction ID" from the server. If it differs from the local cache, a full background sync is triggered.
4. **Optimistic Updates:** When a purchase succeeds, the asset is immediately added to the local inventory cache before the global state refreshes.

## Consequences
- **Positive:** Instant load times for the User Dashboard; works offline for browsing owned assets.
- **Negative:** Potential for "Stale Data" if a purchase is refunded on another device.
- **Neutral:** Requires handling storage quota limits in the browser.

## Implementation Details
- Service: `InventoryService` for DB interactions.
- Hook: `useInventory` to bridge TanStack Query and IndexedDB.
