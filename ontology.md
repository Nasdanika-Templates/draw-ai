### Visual Ontology

This page documents the **visual ontology** conventions for Draw.AI: how to represent entities, attributes, relationships, multiplicity, operations, and navigation in diagrams so models are both human‑readable and machine‑actionable. Use these conventions to keep diagrams consistent, traceable, and ready for export (JSON Schema, Ecore) or runtime binding.

---

#### Principles
- **Visual clarity first.** Diagrams are communication artifacts for SMEs and engineers. Use color, shape, and layout to make intent obvious.  
- **Diagrams are views of a single metamodel.** Notation is flexible; the underlying metamodel (entities, attributes, relationships, operations, types) is authoritative.  
- **Documentation travels with the model.** Every class, attribute, and relationship links to longform documentation (human and agentic flavors).  
- **Scale with hierarchy.** Large ontologies use a diagram hierarchy: root diagram shows core classes and relationships; class context diagrams show attributes, operations, and edge cases.

---

### Visual Styles (Quick Reference)

| **Element** | **Shape / Style** | **Color / Visual Cue** |
|---|---:|---|
| **Entity (class)** | Rounded rectangle; solid border | **Background:** `#F6F8FF` (light blue) |
| **Attribute** | Small pill inside class or listed in properties panel | **Background by type:** string `#FFFFFF`; number `#FFF7E6`; date `#E8F8F5`; enum `#F0F0F0` |
| **Relationship** | Solid line with arrow; label = role name | **Line color:** `#2B8CFF` |
| **Multiplicity** | Line style indicates multiplicity | **Dashed** = `0..1`; **Solid** = `1`; **Double line or asterisk** = `*` |
| **Operation (behavior)** | Gear icon or function icon inside class; bold name | **Icon color:** `#FF6B6B` |
| **Computed attribute** | Attribute with calculator icon | **Icon color:** `#7D3C98` |
| **Agent context** | Thick left border or shadow on entity | **Border color:** `#2B8CFF` (agent bounded context) |
| **External tool / API** | Hexagon or cloud icon | **Background:** `#FFF0D9` |
| **Deprecated / optional** | Strikethrough or lighter opacity | **Opacity:** 50% |

---

### Multiplicity and Borders
- **0..1** — **dashed** border or dashed relationship line.  
- **1** — **solid** line.  
- **\*** or **1..*** — **solid** line with asterisk marker near the target or a double line.  
- **Cardinality labels** (e.g., `0..1`, `1..*`) should appear near the relationship arrow for clarity.  
- **Visual hint:** use a faint multiplicity glyph next to the attribute name when attributes are shown inside a class.

---

### Attributes: Visual vs. Properties
- **Small ontologies:** show attributes visually inside the class box. Use colored pills for types and small icons for computed/derived attributes.  
- **Large ontologies:** show only **entities and relationships** on diagrams. **Attributes** are defined in YAML or properties panels and linked to the class diagram via element links.  
- **Attribute metadata (in properties/YAML):**
  - **name**: `string`  
  - **type**: `string | number | date | enum | object`  
  - **multiplicity**: `0..1 | 1 | 0..* | 1..*`  
  - **description**: `markdown`  
  - **examples**: `[]`  
  - **validation**: regex or constraints  
  - **computed**: boolean  
  - **operation**: optional reference to an operation that computes the value

**Example YAML attribute definition**
```yaml
Customer:
  attributes:
    customerId:
      type: string
      multiplicity: 1
      description: "Unique identifier assigned by the CRM system."
    riskScore:
      type: number
      multiplicity: 0..1
      description: "Computed risk score between 0 and 100."
      computed: true
      computedBy: "RiskEngine.calculateRisk"
```

---

### Operations and Behavior
- **Operations** are first‑class model elements. Represent them with a gear icon inside the class or as a separate operation node linked to the class.  
- **Operation signature** (properties/YAML): `name`, `inputs` (typed), `outputs` (typed), `sideEffects` (boolean), `security` (roles), `timeout`.  
- **Agent wrapping:** you can **wrap an agent into an operation** — the containing object becomes the agent’s context. That means the operation executes with the class instance as context (e.g., `Order.processPayment()` becomes `PaymentAgent.process(order)` under the hood).  
- **Computed attributes** should reference the operation that computes them (see YAML example above).

**Operation example (YAML)**
```yaml
Order:
  operations:
    calculateTax:
      inputs:
        - items: OrderItem[]
        - shippingAddress: Address
      outputs:
        - taxAmount: number
      sideEffects: false
      description: "Calculate tax using jurisdiction rules."
```

---

### Agent Bounded Contexts and Tags
- **Tag classes and features** with agent mapping properties (e.g., `agent: FraudAgent`) to create **agent bounded contexts**.  
- Use tags to generate agent manifests or to filter diagrams by agent ownership. Tags live in the class/feature properties and are searchable.  
- **Example tag usage:** `tags: [fraud, realtime, agent:FraudAgent]`

---

### Diagram Hierarchy and Navigation
- **Root diagram** shows core classes and high‑level relationships.  
- **Class context diagram** (click a class) shows attributes, operations, and local relationships.  
- **Edge diagrams** show cross‑cutting concerns (audit, security, lifecycle).  
- **Element links**: a class can appear on multiple diagrams; use page links to navigate. Each element instance includes a link back to its canonical documentation page.  
- **Best practice:** keep root diagrams minimal; use context diagrams for detail and longform documentation.

---

### Documentation: Human and Agentic Flavors
- **Human flavor**: narrative, examples, edge cases, business rules, legal/regulatory notes. Use markdown pages linked from the class or attribute.  
- **Agentic flavor**: prompt templates, expected slot values, validation rules, example tool calls, and test cases. Store these as structured properties so generators can consume them.  
- **Documentation depth:** a single attribute may have multiple pages: definition, examples, prompt guidance, test vectors, and sub‑diagrams. Link them from the attribute properties.

---

### Libraries and Reuse
- **Create libraries** of diagram elements: attribute types, common entities (Customer, Transaction), operation templates, UI field components.  
- **Version libraries** and reference them in diagrams so updates propagate. Use library tags to indicate stability (`stable`, `beta`, `deprecated`).  
- **Example library elements:** `StringField`, `CurrencyField`, `DatePicker`, `ComputedRiskScore`.

---

### Icons and Visual Cues
- **Operation icon** — gear.  
- **Computed attribute icon** — calculator.  
- **External API/tool** — cloud or hexagon.  
- **Agent context** — left thick border or shadow.  
- **Documentation link** — small book icon next to element name.

---

### Traceability: From Diagram to Artifacts
- **Attributes and operations** defined in YAML or properties are the single source of truth for code generation (JSON Schema, Ecore) and runtime bindings.  
- **Diagram element metadata** must include `id`, `typeRef` (ontology type), `docLink`, and `tags`.  
- **Export mapping**: classes → Ecore/JSON Schema; attributes → properties; operations → methods or runtime operations; tags → agent bindings.

**JSON Schema fragment example**
```json
{
  "$id": "https://example.org/schemas/Order.json",
  "title": "Order",
  "type": "object",
  "properties": {
    "orderId": { "type": "string" },
    "items": {
      "type": "array",
      "items": { "$ref": "OrderItem.json" }
    }
  },
  "required": ["orderId", "items"]
}
```

---

### Practical Modeling Guidelines
1. **Start with the root diagram**: core classes and relationships only.  
2. **Create class context diagrams** for each core class with attributes and operations. Link them from the root.  
3. **Define attributes in YAML** for large models; show only key attributes visually.  
4. **Tag classes** with agent mappings early to enable agentic flows and bounded contexts.  
5. **Document adjacent to elements**: every attribute should have at least a short description and one example.  
6. **Use libraries** for UI components and common attribute types to speed modeling.  
7. **Validate** diagrams for unbound references, missing docs, and type mismatches before export.

---

### Example: Class Context Diagram (conceptual)
- **Class:** `Customer` (rounded rectangle, light blue)  
  - **Attributes (not shown visually on root):** `customerId` (string), `name` (string), `riskScore` (computed)  
  - **Operations:** `calculateRisk()` (gear icon)  
  - **Tags:** `tags: [customer, agent:RiskAgent]`  
  - **Links:** `customerId` → documentation page; `riskScore` → prompt template page

---

### Governance and Versioning
- **Version every diagram and YAML artifact.** Include `author`, `timestamp`, and `changeLog`.  
- **Validation rules** should run in CI: missing docs, untyped attributes, or dangling links fail the build.  
- **Provenance metadata** travels with exported artifacts for auditability.

---

### When to Model Attributes Visually
- **Yes**: small models, quick prototypes, UI‑driven screens where attributes are few.  
- **No**: large enterprise ontologies — show entities and relationships only; keep attributes in YAML/property files and link to class context diagrams.

---

### Linking Ontology to UI and Flows
- **Color coding**: use the same color for an ontology type and any UI field bound to it.  
- **Field binding**: wireframe fields reference ontology attributes by `typeRef`.  
- **Flow contracts**: agentic flows reference ontology types for inputs/outputs; these references are validated against the ontology.

---

### Example: Attribute Documentation Structure
- **Title**: `riskScore`  
- **Type**: `number`  
- **Multiplicity**: `0..1`  
- **Description**: longform markdown with examples  
- **ComputedBy**: `RiskEngine.calculateRisk` (operation reference)  
- **PromptGuidance**: agentic prompt template and slot mapping  
- **TestVectors**: sample inputs and expected outputs  
- **Diagrams**: links to sub‑diagrams showing calculation logic

---

### Navigation and UX Tips
- **Click a class** on the root diagram to open its context diagram.  
- **Hover an attribute** to see a tooltip with short description and link to full docs.  
- **Search** by tag (e.g., `agent:FraudAgent`) to find all classes and features owned by an agent.  
- **Breadcrumbs** show diagram hierarchy and provenance.

---

### Example Workflows
- **SME documents an attribute** in YAML → links it to a class context diagram → tags it with `agent:CaseAgent` → the attribute appears as a bindable field in wireframes and as a typed input in agentic flows.  
- **Engineer exports** the ontology to JSON Schema → generates API contracts → runtime adapters bind to tools referenced in flows.

---

### Libraries and Templates to Include
- **Core types**: Identifier, Currency, DateTime, Enum, TextBlob  
- **UI components**: TextField, CurrencyField, DatePicker, LookupField  
- **Operation templates**: ComputeScore, ValidateAddress, EnrichCustomer  
- **Agent templates**: RiskAgent, CaseAgent, OrchestrationAgent

---

### Final Notes
- **Diagrams are living documentation.** Treat them as the canonical source for domain knowledge.  
- **Balance visual detail with maintainability.** Use hierarchy and YAML to keep large models navigable.  
- **Make documentation discoverable.** The value of the ontology is in the depth of its documentation — both human and agentic.

---

**Reference:** This visual ontology guidance aligns with the Draw.AI template and ontology examples available in the Draw.AI site. 