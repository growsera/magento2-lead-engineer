# Frontend stacks and patterns

## Luma / Blank
- Layout XML: `app/design/frontend/<Vendor>/<theme>/Magento_Theme/layout/*.xml`
- Templates: `.../templates/*.phtml`
- UI Components: `view/frontend/ui_component/*.xml`
- JS: RequireJS mixins via `requirejs-config.js`
- Use Knockout for UI Components where applicable

## Hyva
- Prefer ViewModels and Alpine.js for interactivity
- Avoid RequireJS; use Hyva theme conventions
- Keep logic in ViewModels and pass data into templates

## Cross-theme compatibility
- Keep business logic in backend ViewModels/Blocks
- Provide theme-specific templates when needed
- Use layout updates per theme to wire the right templates
- Avoid shared JS assumptions across Luma and Hyva
