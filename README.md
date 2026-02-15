[TOC levels=6]

## Welcome

[**Draw.AI**](https://docs.nasdanika.org/ai/draw-ai/index.html) is a pragmatic, lightweight methodology with supporting tooling for capturing and operationalizing the *knowledge* that makes systems work. 
Use familiar visual tools to [**draw agentic flows**](flow/index.html), [**define rich ontologies**](ontology/index.html), and [**sketch functional UI wireframes**](flow/swimlanes/user/user-input/index.html) — then turn those diagrams into executable artifacts: JSON schemas, Ecore models, functional UI prototypes, and agentic runtimes.

You are looking at a ready‑to‑use template. 
Create a new repository from [this template](https://github.com/Nasdanika-Templates/draw-ai) and begin capturing your team’s secret sauce.

This template is based on [Drawio Site](https://nasdanika-templates.github.io/drawio-site/) template - use it for the general purpose diagramming documentation.
This templates focuses on the agentic aspect of diagramming.

---

## What Draw.AI Does

- [**Draw agentic flows**](flow/index.html) — visually model agents, tools, knowledge sources, LLM calls, and handovers between agents.  
- [**Draw ontologies**](ontology/index.html) — model entities, attributes, relationships, and attach detailed documentation to each element.  
- [**Draw functional UI wireframes**](flow/swimlanes/user/user-input/index.html) — create functional (not pixel‑perfect) screens that reference ontology elements and use the same type color coding as your domain model.  
- **Link flows, ontologies, and UI** — flows reference ontology elements in inputs and outputs; wireframes reference the same ontology elements so UI and logic stay aligned.  
- **From diagram to artifact** — once notation is established, generate [Ecore](https://docs.nasdanika.org/core/mapping/index.html#emf-ecore) or JSON Schema from ontologies, generate functional UI from wireframes, and generate an agentic runtime from flows or use flows as a runtime artifact for Java-based agentic systems.

---

## How It Works

### Model Visually

- Use Draw.io to create three interlinked model types: **Flows**, **Ontologies**, **Wireframes**.  
- Use color coding and consistent notation so elements are unambiguous and machine‑readable.

### Document Deeply

- Attach documentation to ontology elements. An attribute can link to pages of explanation, examples, and edge cases.  
- Keep documentation *next to* the model so stakeholders see it immediately.

### Generate

- Generate documentation - readily available.
- Export ontologies to **JSON Schema** or [**Ecore**](https://docs.nasdanika.org/core/mapping/index.html#emf-ecore). Easy to implement once the ontology notation is stable.

### Execute or Hand Over
   - Run diagrams in a governed sandbox for safe experimentation.  
   - Or hand generated artifacts to engineering for production hardening.

