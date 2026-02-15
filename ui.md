### Overview
**Draw.AI wireframing** focuses on **functional, not pixel‑perfect** UI prototypes that are directly traceable to your ontology and agentic flows. Wireframes are **executable artifacts**: they document UX intent for stakeholders, generate functional UI code or runtime descriptors, and enable SMEs to iterate quickly in a safe, local environment (Docker Desktop or sandbox). The goal is fast, validated UX that maps to typed domain models and agent contracts.

---

### Principles
- **Function over form** — prioritize fields, bindings, and behavior over visual polish.  
- **One source of truth** — wireframes reference ontology types and use the same color coding so UI, data, and logic stay aligned.  
- **Traceable UX** — every field, action, and screen links back to ontology attributes, operations, and agentic flows.  
- **Executable by design** — wireframes are first‑class artifacts that can be exported to a runtime or code generator.  
- **SME friendly** — easy to learn notation so domain experts can prototype and iterate without heavy engineering support.

---

### Notation and Color Coding
| **Element** | **Visual** | **Color / Cue** |
|---|---:|---|
| **Screen** | Large rounded rectangle | **Background:** `#F8FAFF` |
| **Field (bound)** | Rectangular field with label; small color pill | **Type color**: string `#FFFFFF`; number `#FFF7E6`; date `#E8F8F5`; enum `#F0F0F0` |
| **Button / Action** | Rounded button with icon | **Primary:** `#2B8CFF`; **Secondary:** `#6C757D` |
| **Bound label** | Small tag next to field | **Text:** `typeRef: Customer.name` |
| **Computed field** | Field with calculator icon | **Icon color:** `#7D3C98` |
| **Validation hint** | Small inline text under field | **Color:** `#FF6B6B` |
| **Navigation link** | Arrow icon with page link | **Color:** `#2B8CFF` |

**Multiplicity and optional fields**  
- Show multiplicity with a small suffix on the bound label (e.g., `addresses[0..*]`).  
- Optional fields use lighter opacity.

---

### Wireframe Elements and Ontology Binding
- **Field binding**  
  - Each UI field has a **typeRef** that points to an ontology attribute (e.g., `Customer.email`).  
  - The field inherits validation, examples, and documentation from the ontology attribute.  
- **Actions and operations**  
  - Buttons map to **operations** (ontology operations or agentic operations) with typed inputs and outputs.  
  - Example: `Submit -> Order.create(orderPayload)` where `orderPayload` is typed by `Order` schema.  
- **Computed and derived fields**  
  - Mark computed fields with an icon and reference the operation that computes them (e.g., `riskScore computedBy: RiskAgent.calculateRisk`).  
- **UI state and flows**  
  - Wireframes can include simple state diagrams (loading, error, success) that reference validation rules and agent responses.  
- **Documentation for UX discussions**  
  - Each screen and field links to a documentation page with: purpose, acceptance criteria, edge cases, sample data, and agentic prompt guidance. Use this material in stakeholder reviews.

**Example field binding snippet**
```json
{
  "fieldId": "customerEmail",
  "label": "Email",
  "typeRef": "Customer.email",
  "multiplicity": "1",
  "validation": { "pattern": "^[^@\\s]+@[^@\\s]+\\.[^@\\s]+$" }
}
```

---

### From Wireframe to Runtime
- **Export targets**  
  - **Functional UI descriptor** (JSON) that a renderer or generator consumes.  
  - **Prototype code** (React/Vue) or runtime descriptor for a UI runtime that interprets the descriptor.  
- **Generation flow**  
  1. Wireframe → **UI descriptor** (fields, bindings, actions, state).  
  2. UI descriptor + ontology → **form validation**, **API contract**, and **mock data**.  
  3. Descriptor → **code generator** or **runtime interpreter**.  
- **Demo and execution**  
  - A working demo shows wireframes exported to a functional UI that binds to generated JSON Schema and calls agentic flows.  
  - SMEs edit the wireframe, push changes, and the generator updates the running prototype.  
- **Local deployment option**  
  - Use **Docker Desktop** to run the UI runtime locally and isolated. SMEs can iterate offline: edit wireframe → regenerate → container redeploys automatically.  
- **Safety and governance**  
  - Sandbox runtimes enforce rate limits, mock tool adapters, and human‑in‑the‑loop gates before any production calls.

**Example UI descriptor fragment**
```json
{
  "screenId": "customerProfile",
  "title": "Customer Profile",
  "fields": [
    { "id": "name", "label": "Name", "typeRef": "Customer.name" },
    { "id": "email", "label": "Email", "typeRef": "Customer.email" }
  ],
  "actions": [
    { "id": "save", "label": "Save", "operationRef": "Customer.save" }
  ]
}
```

---

### Getting Started and Best Practices
- **Start small** — prototype one screen bound to one core entity and one operation.  
- **Stabilize color and type mapping** — agree on type colors and field styles so wireframes and ontology remain consistent.  
- **Document adjacent to elements** — attach acceptance criteria and examples to fields for UX reviews and agent prompts.  
- **Iterate in sandbox** — run the prototype locally in Docker Desktop; SMEs make changes, push, and see the updated UI quickly.  
- **Use libraries** — maintain reusable UI components (TextField, Lookup, DatePicker) that carry binding metadata.  
- **Version and validate** — run CI checks on UI descriptors to ensure all `typeRef` links resolve to ontology attributes and operations.

**Quick checklist**
- Create or pick an ontology type for the screen.  
- Bind each field to an ontology attribute.  
- Add validation and examples in attribute properties.  
- Export UI descriptor and run locally in Docker.  
- Review UX with stakeholders using generated documentation.

---

**Result:** functional wireframes become living artifacts — documentation for UX conversations, a bridge to engineering, and a fast path to runnable prototypes. SMEs can capture intent visually, validate behavior with stakeholders, and iterate until the UI and agentic flows meet real needs.