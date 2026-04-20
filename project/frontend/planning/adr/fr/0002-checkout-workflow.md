# ADR FR-0002: Multi-Step Checkout Workflow

## Status
Proposed

## Requirement Context
Purchasing a digital asset involves several steps: Preview confirmation, License selection, Payment detail entry, and Final download. We need to ensure data integrity across these steps and handle network failures gracefully.

## Decision
We will use a **Finite State Machine (FSM)** pattern for the checkout workflow:
1. **State Machine:** Implement the workflow using a simple reducer or a library like XState (if complexity grows).
2. **Persistence:** The checkout progress will be stored in `sessionStorage` to allow recovery if the page is accidentally refreshed.
3. **Validation:** Each step must pass a Zod validation schema before the user can proceed to the next "node" in the state machine.
4. **Atomic Transactions:** The final "Purchase" action will be a single atomic API call to the gateway.

## Consequences
- **Positive:** Eliminates "impossible states" (e.g., being on the download page without payment).
- **Negative:** Higher initial boilerplate for setting up the state machine.
- **Neutral:** Requires clear visual indicators for the current step (Progress Bar).

## Implementation Details
- Context Provider: `CheckoutProvider` to wrap the modal.
- Schema: `CheckoutSchema` defining data requirements for each step.
