# Compatibility — betav3 3.7.5.42

This repository distinguishes the existing API from the newer reference specification. It is not a promise of complete compatibility with another product.

| Area | Status |
| --- | --- |
| Existing lowercase API | Preserved; see legacy-api.md for the recovered reference and its uncertainty notes |
| New math value types and mathlib | 15 modules ported; 461 behavior checks passed; 682 documented named members found |
| New math FFI requirement | Existing Allow Insecure setting must be enabled; otherwise these types are not installed |
| New non-mutating queries | ui.GetAlpha, ui.GetPosition, ui.GetSize, ui.GetCursorPosition, engine.GetScreenSize, engine.GetViewAngles |
| Passing new FFI values to old native methods | Not automatically supported; old methods can require native vector/color userdata |
| New UI constructors, control overrides, callbacks | Not ported |
| Other new native namespaces | Reference only; not verified as implemented |
| New ragebot/menu/Skinchanger/grenade core from the supplied dump | Not ported |

The new-api pages preserve the supplied docs.zip specification. Argument tables and signatures were converted from MDX to plain Markdown for GitHub. Engine schema dumps and interface catalogs are not included in this API-only bundle.

Test counts establish only their stated scope. A presence check does not verify every method's semantics. No in-game validation is claimed for the new API port.
