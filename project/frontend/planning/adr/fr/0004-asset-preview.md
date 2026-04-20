# ADR FR-0004: Interactive Asset Previews

## Status
Proposed

## Requirement Context
Users need to evaluate the quality and utility of a digital asset before purchase. Static images are often insufficient for code snippets, UI kits, or interactive components. We need a way to provide rich, safe, and performant previews.

## Decision
We will implement an **Extensible Preview Architecture**:
1. **Preview Providers:** Create a registry of "Preview Providers" based on asset MIME types (e.g., `ImageGalleryProvider`, `CodePreviewProvider`, `ComponentSandboxProvider`).
2. **Sandboxing:** For code and component previews, use `<iframe>` with the `sandbox` attribute to prevent script injection into the main application context.
3. **Progressive Loading:** Previews will use low-resolution placeholders or "blurred" versions until the user explicitly interacts with the preview pane to save bandwidth.
4. **Fullscreen Mode:** Implement a "Focus Mode" using the Browser Fullscreen API for detailed inspection.

## Consequences
- **Positive:** Higher conversion rates due to better evaluation; keeps the main app bundle small by lazy-loading heavy preview logic.
- **Negative:** Increased complexity in handling multiple media types and ensuring cross-browser iframe compatibility.
- **Neutral:** Requires specific metadata from the backend (e.g., `previewType`, `sandboxConfig`).

## Implementation Details
- **Core Symbols:** `PreviewRegistry`, `SafeIframe`, `MediaGallery`.
- **Data Flow:** `AssetDetail` fetches metadata -> `PreviewRegistry` selects provider -> Lazy-load provider component.
- **Validation:** Ensure `previewURL` is from a trusted CDN via CSP.
- **Testing:** Visual regression tests for different preview types.

## References
- [ADR 0004: Security](../nfr/0004-security.md) (for Sandboxing)
