This page documents the **visual ontology** conventions for Draw.AI: how to represent entities, attributes, relationships, multiplicity, operations, and navigation in diagrams so models are both human‑readable and machine‑actionable. 
Use these conventions to keep diagrams consistent, traceable, and ready for export (JSON Schema, Ecore) or runtime binding.

---

## Principles

- **Visual clarity first.** - diagrams are communication artifacts for SMEs and engineers. Use color, shape, and layout to make intent obvious.  
- **Diagrams are views of a single metamodel.** - notation is flexible; the underlying metamodel (entities, attributes, relationships, operations, types) is authoritative.  
- **Documentation travels with the model.** - every class, attribute, and relationship links to a details documentation which may have human and agentic flavors.  
- **Scale with hierarchy.** - large ontologies use a diagram hierarchy: root diagram shows core classes and relationships; class context diagrams add more classes and may show attributes and operations. 

---

## Attributes: Visual vs. Properties

- **Small ontologies:** show attributes visually inside the class box. Use colored pills for types and small icons for computed/derived attributes.  
- **Large ontologies:** show only **entities and relationships** on diagrams. **Attributes** are defined in YAML in files or properties or Excel spreadsheets.

### Defining attributes in Excel

Excel spreadsheets may have drop-down lists for data types and conditional formatting to hightliht data type cells using the same naming convention as in diagrams.
Documentation cells may use a convention to reference external resources. E.g. if the value starts with ``@`` then it is treated as a documentation resource URL
relative to the spreadsheet location.
Excel spreadsheets may also have columns for agents to map attributes to agents.
One workbook may have multiple sheets - one per ontology class.

Operations can be defined in Excel spreadsheets as well.

---

## Operations and Behavior

- **Operations** are first‑class model elements. Represent them with a gear icon inside the class or as a separate operation node linked to the class.  
- **Operation signature** can be defined using nested nodes in the operation container similar to how attributes can be placed inside the class node. Color coding can be used to indicate operation type and parameter types. Parameters may have default values.  
- **Agent wrapping:** you can **wrap an agent into an operation** — the containing object becomes the agent’s context. That means the operation executes with the class instance as context (e.g., `Order.processPayment()` becomes `PaymentAgent.process(order)` under the hood).  

---

## Agent Bounded Contexts

Ontology elements can be associated with agents using tags or mapping YAML in properties and files or Excel spreadsheets. 
The Excel approach might be more convenient than the YAML approach, but the YAML approach is more flexible. It may be used to provide bindings to operation parameters.

---

## Diagram Hierarchy and Navigation

- **Root diagram** - shows core classes and high‑level relationships.  
- **Class context diagram** (click a class) - shows attributes, operations, and local relationships.  
- **Element links** - a class can appear on multiple diagrams; use page links to navigate. Each element instance includes a link back to its canonical documentation page.  

---

## Documentation: Human and Agentic Flavors

- **Human flavor**: narrative, examples, edge cases, business rules, legal/regulatory notes. Use markdown pages linked from the class or attribute.  
- **Agentic flavor**: prompt templates, expected slot values, validation rules, example tool calls, and test cases. Store these as structured properties so generators can consume them.  

---

## Libraries and Reuse

- **Create libraries** of diagram elements: attribute types, common entities (Customer, Transaction), operation templates, UI field components.  
- **Example library elements:** `StringField`, `CurrencyField`, `DatePicker`, `ComputedRiskScore`.

---

## Icons and Visual Cues

- **Operation icon** — gear.  
- **Computed attribute icon** — calculator.  
- **External API/tool** — cloud or hexagon.  

---

## Traceability: From Diagram to Artifacts

- **Attributes and operations** defined in YAML, Excel or properties are the single source of truth for code generation (JSON Schema, Ecore) and runtime bindings.  
- **Export mapping**: classes → Ecore/JSON Schema; attributes → properties; operations → methods or runtime operations; tags → agent bindings.

---

## Generation from existing schemas

You may manually create or generate initial ontologies from existing schemas such as SQL database, XML and JSON schemas, APIs - Java, OpenAPI.

Examples:

* [A2a](https://a2a.models.nasdanika.org/) - generated from the A2a JSON Schema
* [Jira](https://jira.models.nasdanika.org/index.html) - manually created from [Jira Java API](https://mvnrepository.com/artifact/com.atlassian.jira/jira-rest-java-client-api)
* [GitLab](https://gitlab.models.nasdanika.org/default-graph.html) - manually created from [gitlab4j](https://github.com/gitlab4j/gitlab4j-api)
* [Database](https://sql.models.nasdanika.org/demos/sample-database-docs/index.html) - generated from [JDBC Metadata](https://docs.oracle.com/en/java/javase/21/docs/api/java.sql/java/sql/DatabaseMetaData.html) with [Nasdanika SQL](https://sql.models.nasdanika.org/) - no diagram yet, generated to an Ecore model.

You can also implement merging of modifications in the source and manual modifications in the ontology using the three-way-merge:

* Root revision - when the diagram was originally generated without human edits
* Current revision with human edits
* New diagram generated from the source

Merge rules:

* If external source adds something → add it
* If external source changes something → update semantic properties but preserve human edits
* If humans add something → keep it
* If both changed the same thing → conflict resolution. Present to a human
* If external source deletes something → configurable
    * Soft delete
    * Mark deprecated
    * Or remove

[EMF Compare](https://compare.models.nasdanika.org/) might be used for merging:

* Convert the diagram revisions to Ecore models (there is a model and a method)
* Compare
* Create a list of changes
* Apply changes - may present changes to the user before applying

Generating ontologies from existing sources—such as SQL databases—and then enriching them with documentation or visualizations has tremendous value on its own.

---

## Practical Modeling Guidelines

1. **Start with the root diagram**: core classes and relationships only.  
2. **Create class context diagrams** for each core class with attributes and operations. Link them from the root.  
3. **Define attributes in YAML or Excel** for large models; show only key attributes visually.  
4. **Tag classes** with agent mappings early to enable agentic flows and bounded contexts.  
5. **Document adjacent to elements**: every attribute should have at least a short description and one example.  
6. **Use libraries** for UI components and common attribute types to speed modeling.  
7. **Validate** diagrams for unbound references, missing docs, and type mismatches before generation.

---

## When to Model Attributes Visually

- **Yes**: small models, quick prototypes, UI‑driven screens where attributes are few.  
- **No**: large enterprise ontologies — show entities and relationships only; keep attributes and operations in YAML or Excel files and link to class context diagrams.

---

## Linking Ontology to UI and Flows

- **Color coding**: use the same color for an ontology type and any UI field bound to it.  
- **Field binding**: wireframe fields reference ontology attributes.  
- **Flow contracts**: agentic flows reference ontology types for inputs/outputs and tooll parameters and return values.

---

## Navigation and UX Tips
- **Click a class** on the root diagram to open its context diagram.  
- **Hover an attribute** to see a tooltip with short description and link to full docs.  

---

## Final Notes
- **Diagrams are living documentation.** Treat them as the canonical source for domain knowledge.  
- **Balance visual detail with maintainability.** Use hierarchy and YAML to keep large models navigable.  
- **Make documentation discoverable.** The value of the ontology is in the depth of its documentation — both human and agentic.
