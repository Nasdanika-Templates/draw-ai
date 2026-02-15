**Draw.AI wireframing** focuses on **functional, not pixel‑perfect** UI prototypes that are directly traceable to your ontology and agentic flows. 
Wireframes are **executable artifacts**: they document UX intent for stakeholders, generate functional UI code, and enable SMEs to iterate quickly in a safe, local environment (Docker Desktop or sandbox). The goal is fast, validated UX that maps to typed domain models and agent contracts.

[Wireframes demo](https://nasdanika-demos.github.io/wireframes/)

---

## Principles

- **Function over form** — prioritize fields, bindings, and behavior over visual polish.  
- **One source of truth** — wireframes reference ontology types and use the same color coding so UI, data, and logic stay aligned.  
- **Traceable UX** — every field, action, and screen links back to ontology attributes, operations, and agentic flows.  
- **Executable by design** — wireframes are first‑class artifacts that can be exported to a runtime or code generator.  
- **SME friendly** — easy to learn notation so domain experts can prototype and iterate without heavy engineering support.

---

## Getting Started and Best Practices
- **Start small** — prototype one screen bound to one core entity and one operation.  
- **Stabilize color and type mapping** — agree on type colors and field styles so wireframes and ontology remain consistent.  
- **Document adjacent to elements** — attach acceptance criteria and examples to fields for UX reviews and agent prompts.  
- **Iterate in sandbox** — run the prototype locally in Docker Desktop; SMEs make changes, push, and see the updated UI quickly.  
- **Use libraries** — maintain reusable UI components (TextField, Lookup, DatePicker) that carry binding metadata.  

---

**Result:** functional wireframes become living artifacts — documentation for UX conversations, a bridge to engineering, and a fast path to runnable prototypes. SMEs can capture intent visually, validate behavior with stakeholders, and iterate until the UI and agentic flows meet real needs.