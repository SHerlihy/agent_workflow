# ADR FR-0005: User Ratings and Review System

## Status
Proposed

## Requirement Context
Social proof is critical for a marketplace. Users need to rate assets they've purchased and read reviews from others to gauge quality.

## Decision
We will implement an **Optimistic Review System**:
1. **Verification:** The "Write Review" button will only be visible if the `Asset` is present in the `UserInventory` aggregate.
2. **Optimistic UI:** Use TanStack Query's `onMutate` to immediately show a user's review in the list before the server confirms the transaction.
3. **Rate Limiting/Spam:** Implement client-side debounce and use a "Report" flag for community moderation.
4. **Summary Aggregate:** The star rating summary (average/count) will be computed server-side to ensure accuracy, but cached client-side for performance.

## Consequences
- **Positive:** Enhances user trust and engagement; provides immediate feedback to reviewers.
- **Negative:** Handling "Review Squatting" or negative review bombs requires backend intervention.
- **Neutral:** Requires updating the `Asset` entity to include `RatingSummary` data.

## Implementation Details
- **Core Symbols:** `ReviewList`, `StarRating`, `ReviewForm`.
- **Data Flow:** `useReviews` hook for fetching; `useSubmitReview` for optimistic updates.
- **Validation:** Zod schema for 1-5 star range and 10-500 character comment length.
- **Testing:** Integration tests for the optimistic update flow and verified-purchase logic.

## References
- [ADR FR-0003: User Inventory Persistence Strategy](./0003-inventory-persistence.md)
