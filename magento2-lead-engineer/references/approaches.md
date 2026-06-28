# Override Approaches and Trade-offs

## Quick decision rules
- Change existing behavior safely: prefer a plugin.
- React to system events or extend workflows: use an observer.
- Change output/structure: use layout XML, UI components, or ViewModels.
- Add frontend behavior: use JS mixins or component-level overrides.
- Use a preference only when no other safe option exists.

## Plugin (before/after/around)
Use when:
- Altering public method behavior without rewriting the class.
Pros:
- Upgrade-safe, isolated, easy to disable.
Cons/Risks:
- Cannot intercept protected/private methods.
- Around plugins can change control flow and create conflicts.
- Ordering conflicts with other modules.

## Observer (event)
Use when:
- Extending workflows that dispatch events.
Pros:
- Decoupled, integrates with event-driven logic.
Cons/Risks:
- Requires an existing event; may fire in multiple areas.
- Harder to trace if many observers exist.

## Preference (class replacement)
Use when:
- No plugin/event/layout alternative can achieve the requirement.
Pros:
- Full control over class behavior.
Cons/Risks:
- High conflict risk with other modules.
- Upgrade risk if core class changes.
- Avoid for shared services and framework classes.

## Layout XML / UI Components
Use when:
- Adding/removing blocks, containers, or UI components.
Pros:
- Safe, declarative, theme-aware.
Cons/Risks:
- Requires correct handles and area context.
- UI component configuration can be verbose.

## ViewModel / Block
Use when:
- Supplying data or logic to templates.
Pros:
- Clean separation of logic from PHTML.
- Works well with Hyva and modern Magento patterns.
Cons/Risks:
- Requires layout wiring and proper DI.

## JS mixin / override
Use when:
- Modifying frontend component behavior.
Pros:
- Non-invasive and update-safe.
Cons/Risks:
- RequireJS overrides can be fragile.
- Hyva does not use RequireJS; provide theme-specific JS.

## Configuration / DI virtual type
Use when:
- Altering dependency wiring or configuration-driven behavior.
Pros:
- Centralized, low code changes.
Cons/Risks:
- Can be hard to debug if overused.
