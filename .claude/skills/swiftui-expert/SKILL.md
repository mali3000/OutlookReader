---
name: swiftui-expert
description: Write SwiftUI code the way an experienced Apple-platform developer would — idiomatic, native components, modern state management, no unnecessary custom UI. Use whenever writing, refactoring, or reviewing SwiftUI/Swift code for iOS, iPadOS, macOS, watchOS, or visionOS apps. Pair with the apple-design skill for visual decisions.
---

# SwiftUI Expert

Write SwiftUI the way an experienced developer would: lean on the framework, let the system do the styling, and keep state simple.

```swift
// ContentView.swift
Button("Weiter") {
    isPresented = true
}
.buttonStyle(.borderedProminent)
.sheet(isPresented: $isPresented) {
    DetailView()
}
```

Native button style, native sheet, one `@State` bool — no custom shapes, gestures, or overlays reinventing what SwiftUI already provides.

## Rules

**Prefer built-ins over custom UI**
- `Button` + `.buttonStyle(.borderedProminent / .bordered / .plain)`, never `Text().onTapGesture` for actions.
- `.sheet`, `.fullScreenCover`, `.alert`, `.confirmationDialog`, `.popover`, `.inspector` for presentation.
- `NavigationStack` (+ `navigationDestination(for:)`) or `NavigationSplitView`; never the deprecated `NavigationView`.
- `List`, `Form`, `Section`, `LabeledContent`, `Toggle`, `Picker`, `Label`, `ContentUnavailableView`, `ShareLink`, `TabView`.
- SF Symbols via `Image(systemName:)`; semantic fonts (`.font(.headline)`) and colors (`.foregroundStyle(.secondary)`, `.tint`).

**State & data flow (Swift 5.9+/Observation)**
- `@State` for view-local value state; `@Binding` to pass write access down.
- `@Observable` classes for models, held with `@State` at the owner and passed as plain properties or via `@Environment`.
- Avoid `ObservableObject`/`@Published`/`@StateObject` in new code unless targeting < iOS 17.
- Single source of truth; derive, don't duplicate.
- `.task {}` for async work tied to view lifetime (auto-cancelled), not `onAppear` + `Task {}`.

**Structure**
- Small views: extract subviews as `struct`s, not computed `some View` properties, once they grow.
- Keep `body` cheap and side-effect free; no heavy work or formatting allocations inside it.
- Use `ViewModifier`/extensions for repeated styling.
- Stable identity in `ForEach` (`Identifiable`, never `\.self` on mutable data or indices).

**Layout**
- Stacks + `Spacer` + `.padding()` with system defaults; `Grid`, `ViewThatFits`, `containerRelativeFrame` before `GeometryReader`.
- No hard-coded frame sizes for text; support Dynamic Type.

**Accessibility & polish**
- `.accessibilityLabel` for icon-only buttons; group with `.accessibilityElement(children: .combine)`.
- Animations via `withAnimation(.spring)` / `.animation(_:value:)`; respect `accessibilityReduceMotion`.
- Provide `#Preview` for every view, including dark mode and large text variants where relevant.

**Concurrency**
- UI types are `@MainActor`; use `async/await`, never completion-handler pyramids or `DispatchQueue.main.async` in new code.

## Review checklist

- [ ] Could a built-in component/modifier replace any custom code?
- [ ] State lives in exactly one place; `@Observable` used for models
- [ ] `NavigationStack`, `.task`, `.foregroundStyle` (modern APIs, no deprecated ones)
- [ ] Views small, `body` pure, `ForEach` identity stable
- [ ] Dynamic Type, dark mode, VoiceOver, Reduce Motion work
- [ ] `#Preview` present
