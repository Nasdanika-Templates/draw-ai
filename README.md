This is a template repository for visual modeling of agentic systems.
It is based on [Drawio Site](https://nasdanika-templates.github.io/drawio-site/) template - use it for the general purpose diagramming documentation.
This page focuses on the agentic aspect of diagramming.

[TOC levels=6]


### Draw.AI Template Home

#### Welcome
**Draw.AI** is a practical, lightweight platform for capturing and operationalizing the *knowledge* that makes systems work. Use familiar visual tools to **draw agentic flows**, **define rich ontologies**, and **sketch functional UI wireframes** — then turn those diagrams into executable artifacts: JSON schemas, Ecore models, functional UI prototypes, and agentic runtimes.

You are looking at a ready‑to‑use template. Start by opening the Draw.io site created from this repository and begin capturing your team’s secret sauce.

---

#### What Draw.AI Does
- **Draw agentic flows** — visually model agents, tools, knowledge sources, LLM calls, and handovers between agents.  
- **Draw ontologies** — model entities, attributes, relationships, and attach longform documentation to each element.  
- **Draw functional UI wireframes** — create pixel‑functional (not pixel‑perfect) screens that reference ontology elements and use the same color coding as your domain model.  
- **Link flows, ontologies, and UI** — flows reference ontology elements in inputs and outputs; wireframes reference the same ontology elements so UI and logic stay aligned.  
- **From diagram to artifact** — once notation is established, generate Ecore or JSON Schema from ontologies, generate functional UI from wireframes, and generate an agentic runtime from flows.

---

#### How It Works
1. **Model Visually**  
   - Use Draw.io to create three interlinked model types: **Flows**, **Ontologies**, **Wireframes**.  
   - Use color coding and consistent notation so elements are unambiguous and machine‑readable.

2. **Document Deeply**  
   - Attach documentation to ontology elements. An attribute can link to pages of explanation, examples, and edge cases.  
   - Keep documentation *next to* the model so stakeholders see it immediately.

3. **Validate and Export**  
   - Validate diagrams against the template notation.  
   - Export ontologies to **JSON Schema** or **Ecore**. Export wireframes to a functional UI descriptor. Export flows to an agentic runtime descriptor.

4. **Execute or Hand Over**  
   - Run diagrams in a governed sandbox for safe experimentation.  
   - Or hand generated artifacts to engineering for production hardening.

---

#### Notation Guidelines
- **Agents** — rounded rectangle, color **#2B8CFF**. Label with role and capabilities.  
- **Tools** — hexagon, color **#FFB000**. Include API contract or tool spec.  
- **Knowledge Sources** — document icon, color **#6C757D**. Link to ontology elements.  
- **LLM Calls** — cloud icon, color **#7D3C98**. Include prompt template and expected outputs.  
- **Handovers** — arrow with label describing the contract (inputs, outputs, SLA).

**Wireframe color mapping**  
- Use the same colors for UI components that reference ontology types (e.g., fields bound to an entity attribute use the attribute color). This makes traceability visible at a glance.

---

#### Example Artifacts
**JSON Schema snippet for an ontology entity**
```json
{
  "$id": "https://example.org/schemas/Customer.json",
  "title": "Customer",
  "type": "object",
  "properties": {
    "customerId": { "type": "string" },
    "name": { "type": "string" },
    "riskScore": { "type": "number" }
  },
  "required": ["customerId", "name"]
}
```

**Ecore snippet for the same entity**
```xml
<ecore:EPackage name="domain" nsURI="http://example.org/domain" nsPrefix="d">
  <eClassifiers xsi:type="ecore:EClass" name="Customer">
    <eStructuralFeatures xsi:type="ecore:EAttribute" name="customerId" eType="ecore:EDataType http://www.eclipse.org/emf/2002/Ecore#//EString"/>
    <eStructuralFeatures xsi:type="ecore:EAttribute" name="name" eType="ecore:EDataType http://www.eclipse.org/emf/2002/Ecore#//EString"/>
    <eStructuralFeatures xsi:type="ecore:EAttribute" name="riskScore" eType="ecore:EDataType http://www.eclipse.org/emf/2002/Ecore#//EDouble"/>
  </eClassifiers>
</ecore:EPackage>
```

**Agentic flow fragment (conceptual)**
- **Agent: FraudDetector** → calls **Tool: TransactionDB** → consults **KnowledgeSource: FraudRules** → if suspicious, calls **Agent: CaseManager** with `casePayload` referencing `Customer.customerId` and `Transaction.id`.

---

#### Demos and Proven Patterns
- **Diagram as executable artifact** — diagrams exported to runtime descriptors have been shown to run in sandboxed agentic environments.  
- **Ontology to schema** — ontology exports to JSON Schema and Ecore have been validated against sample data sets.  
- **Wireframe to functional UI** — wireframes exported to a functional UI descriptor can be rendered as interactive prototypes that bind to the generated schema.

Each piece has been demonstrated independently; this template shows how to combine them into a single workflow that solves real problems: capture domain knowledge, validate it, prototype UI, and run agentic flows safely.

---

#### Governance and Safety
- **Model validation** — templates include validation rules to catch missing documentation, unbound references, and unsafe LLM calls.  
- **Sandbox execution** — run agentic flows in a controlled environment with logging, rate limits, and human‑in‑the‑loop gates.  
- **Audit trail** — every model change is versioned; exported artifacts include provenance metadata linking back to the diagram and documentation.

---

#### Getting Started Right Now
- **Open the Draw.io site** included in this template.  
- **Pick a template**: Ontology, Flow, or Wireframe.  
- **Start modeling**: add a few entities, a short flow, and a single wireframe screen.  
- **Document**: attach a short description to each element. Even a paragraph is valuable.  
- **Export**: try exporting the ontology to JSON Schema and the flow to a runtime descriptor to see the end‑to‑end loop.

---

#### Best Practices
- **Start small** — model one process end‑to‑end before scaling.  
- **Keep documentation adjacent** — link examples and edge cases to attributes.  
- **Reuse patterns** — build a library of agentic templates and ontology fragments.  
- **Teach SMEs visual modeling** — it’s faster to teach SMEs to draw and document than to teach engineers decades of domain nuance.

---

#### Roadmap for Advanced Users
- **Notation stabilization** — agree on a small, consistent set of symbols and colors.  
- **Automated generation** — add scripts to convert diagrams to Ecore, JSON Schema, UI descriptors, and runtime manifests.  
- **CI for models** — validate diagrams in CI pipelines and fail builds on unsafe patterns.  
- **Runtime integration** — connect generated agentic manifests to a sandbox runtime with telemetry and governance hooks.

---

#### Contribute and Extend
- Add new templates for domain ontologies.  
- Share wireframe components and color palettes.  
- Contribute validation rules and export scripts for additional runtimes.

---

#### Contact and Support
If you need help mapping your domain, stabilizing notation, or automating exports, use the repository issues to request examples or a short consultation. This template is designed to be practical and immediately useful — start capturing your team’s DNA today.

---

#### License
This template is provided under an open license. Check the repository README for details.

---

**You are looking at the model, the documentation, and the export tools — everything you need to start capturing and operationalizing your knowledge is available right away.**
