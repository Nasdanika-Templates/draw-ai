# Agentic Flows

This page explains how **agentic flows** work in Draw.AI: the simple core model (LLMs + tools + prompts), the swimlane notation used here, the core concepts and contracts, and how diagrams become executable artifacts (Python via CrewAI demos, Java runtimes, JSON/Ecore exports). The examples and patterns below are grounded in the Draw.AI approach and mapping capabilities.   [nasdanika-templates.github.io](https://nasdanika-templates.github.io/draw-ai/flow/index.html)  [docs.nasdanika.org](https://docs.nasdanika.org/ai/draw-ai/index.html)

---

## Overview
At its heart, an **agentic flow** is a sequence of **LLM calls** and **tool calls** organized so that agents can collaborate, hand off work, and produce typed inputs and outputs. The flow is a **visual, machine‑readable specification** that:

- Defines **agents** and the **tasks** they perform.   [docs.nasdanika.org](https://docs.nasdanika.org/ai/draw-ai/index.html)  
- Declares **tools** (APIs, DBs, microservices, LLMs) and their contracts.   [nasdanika-templates.github.io](https://nasdanika-templates.github.io/draw-ai/flow/index.html)  
- Binds **inputs** and **outputs** to ontology types so data is validated and traceable.   [github.com](https://github.com/Nasdanika-Templates/draw-ai)

**Key idea:** syntactic constructs like “agent”, “crew”, or “task” are organizational sugar — they structure LLM + tool interactions so humans can reason about them. Under the hood, everything is LLMs provided with prompts and tools.   [docs.nasdanika.org](https://docs.nasdanika.org/ai/draw-ai/index.html)

---

## Core Concepts and Definitions
- **LLM**  
  A language model used to interpret prompts, generate text, or orchestrate logic. In flows, LLMs are invoked via **LLM calls** (prompt + context + constraints).   [docs.nasdanika.org](https://docs.nasdanika.org/ai/draw-ai/index.html)

- **Tool**  
  Any callable capability: HTTP API, database query, file store, or a wrapped LLM. Tools have **typed parameters** and **typed return values** defined in the ontology.   [nasdanika-templates.github.io](https://nasdanika-templates.github.io/draw-ai/flow/index.html)

- **Agent**  
  A logical actor that performs tasks by issuing LLM calls and tool calls. An agent receives typed inputs, uses tools/LLMs, and produces typed outputs. Agents are swimlanes in the notation used on this page.   [nasdanika-templates.github.io](https://nasdanika-templates.github.io/draw-ai/flow/index.html)  [docs.nasdanika.org](https://docs.nasdanika.org/ai/draw-ai/index.html)

- **Task**  
  A unit of work inside an agent swimlane. Tasks map to one or more LLM/tool calls and have explicit input/output contracts.

- **Tool Call**  
  A direct invocation of a tool with typed parameters; returns typed results.

- **Agent Call**  
  A logical invocation of another agent. An agent call can be **wrapped as a tool call** (i.e., the callee agent is exposed as a callable tool), enabling uniform orchestration.   [docs.nasdanika.org](https://docs.nasdanika.org/ai/draw-ai/index.html)

- **Hand‑over**  
  The explicit transfer of an output from one agent/task to another agent/task. Hand‑overs are typed and validated against the ontology.

---

## Swimlane Notation Explained
This page uses a **swimlane notation** where:

- Each **swimlane** represents an **Agent** (label at top).  
- Inside a swimlane, **tasks** are boxes connected by arrows.  
- **Tool icons** sit beside tasks and are connected with labeled arrows describing the call contract.  
- **Hand‑overs** are arrows between swimlanes with labels referencing ontology types (e.g., `CustomerProfile -> RiskAssessment`).   [nasdanika-templates.github.io](https://nasdanika-templates.github.io/draw-ai/flow/index.html)

**Why swimlanes?** They align naturally with process thinking and make responsibilities explicit. Other notations are valid — the important part is that the notation maps to the same underlying model: LLM calls + tool calls + typed contracts.   [docs.nasdanika.org](https://docs.nasdanika.org/ai/draw-ai/index.html)

---

## Inputs, Outputs, and Ontology Binding
- **Typed Contracts**  
  Every input, output, tool parameter, and return value should reference an ontology element (entity, attribute, or relationship). Ontology types include descriptions, examples, and validation rules.   [github.com](https://github.com/Nasdanika-Templates/draw-ai)

- **Documentation**  
  Attributes may link to longform documentation pages explaining edge cases, business rules, and examples. This documentation is part of the model and travels with exported artifacts.   [github.com](https://github.com/Nasdanika-Templates/draw-ai)

- **Traceability**  
  Because wireframes and flows reference the same ontology types (and use the same color coding), stakeholders can trace a UI field to the exact ontology attribute and to the agentic flow that produces or consumes it.   [nasdanika-templates.github.io](https://nasdanika-templates.github.io/draw-ai/flow/index.html)

---

## Agent Calls and Tool Calls Relationship
- **Agent call as tool call**  
  Exposing an agent as a tool makes orchestration uniform: the caller issues a tool‑style request to the callee agent, receives a typed response, and continues. This pattern simplifies runtime wiring and enables reuse.   [docs.nasdanika.org](https://docs.nasdanika.org/ai/draw-ai/index.html)

- **Tool wrapping**  
  Tools can wrap LLMs or other agents. For example, a “Summarize” tool might internally call an LLM with a prompt template; a “CaseManager” tool might wrap an agent that coordinates human review.   [nasdanika-templates.github.io](https://nasdanika-templates.github.io/draw-ai/flow/index.html)

---

## From Diagram to Executable Artifact
Draw.AI flows are designed to be **first‑class artifacts** that can be exported or executed:

- **Generation targets**  
  - **CrewAI Python** — diagrams can generate executable Python orchestrations (demoed with CrewAI).   [docs.nasdanika.org](https://docs.nasdanika.org/ai/draw-ai/index.html)  
  - **LangGraph, Semantic Kernel, Java runtimes** — flows can be mapped to other runtimes; sometimes you generate code, sometimes you run the flow directly in a runtime that interprets the diagram.   [docs.nasdanika.org](https://docs.nasdanika.org/ai/draw-ai/index.html)  [nasdanika-templates.github.io](https://nasdanika-templates.github.io/draw-ai/flow/index.html)

- **What is generated**  
  - **Agent runtime manifest** (calls, tool bindings, prompts)  
  - **Prompt templates** with placeholders bound to ontology attributes  
  - **Tool adapters** (HTTP client stubs, DB queries)  
  - **Glue code** (Python/Java) or runtime descriptors that an orchestration engine can execute

- **No code required**  
  You do not always need to generate code. Some runtimes can **interpret** the diagram directly and execute it as an artifact. Other times you generate code for a target platform. Both approaches are supported.   [docs.nasdanika.org](https://docs.nasdanika.org/ai/draw-ai/index.html)

---

## Example Flow Fragment (Conceptual)
```text
Swimlane: FraudAgent
  Task: AnalyzeTransaction
    - Input: Transaction (ontology: Transaction)
    - Tool Call: TransactionDB.query(transactionId)
    - LLM Call: prompt: "Given transaction and history, assess fraud risk"
    - Output: RiskAssessment (ontology: RiskAssessment)

Hand-over -> CaseAgent.receiveCase(RiskAssessment)
```
- **Notes:** `Transaction`, `RiskAssessment` are ontology types with attributes and documentation. The LLM prompt uses typed placeholders (e.g., `{Transaction.amount}`).   [nasdanika-templates.github.io](https://nasdanika-templates.github.io/draw-ai/flow/index.html)  [github.com](https://github.com/Nasdanika-Templates/draw-ai)

---

## Validation, Governance, and Safety
- **Model validation**  
  Diagrams are validated for missing documentation, unbound references, and type mismatches before export or execution.   [nasdanika-templates.github.io](https://nasdanika-templates.github.io/draw-ai/flow/index.html)

- **Sandbox execution**  
  Run flows in a controlled environment with logging, rate limits, and human‑in‑the‑loop gates. This prevents unsafe or uncontrolled LLM/tool behavior.   [docs.nasdanika.org](https://docs.nasdanika.org/ai/draw-ai/index.html)

- **Provenance**  
  Exported artifacts include metadata linking back to the diagram, author, and version so audits and reviews are straightforward.   [github.com](https://github.com/Nasdanika-Templates/draw-ai)

---

## Multiple Notations and Interoperability
- **Notations vary**  
  Crews, swimlanes, node graphs, or process diagrams are all valid notations. They are different views on the same underlying model: sequences of LLM and tool calls with typed contracts. This page documents the **swimlane** view; other pages show node‑based or capability‑based notations.   [docs.nasdanika.org](https://docs.nasdanika.org/ai/draw-ai/index.html)

- **Interchange**  
  Because diagrams map to a metamodel, you can convert between notations, export to Ecore/JSON Schema, and target multiple runtimes. The mapping layer supports Draw.io as a source and Ecore/JSON Schema as targets.   [github.com](https://github.com/Nasdanika-Templates/draw-ai)

---

## CrewAI Demo and Generation Targets
- **CrewAI Python demo**  
  The functional demo shows a swimlane diagram converted into executable Python orchestrations and documentation. Use it as a reference for how prompts, tool adapters, and agent manifests are generated. CrewAI is one of several generation targets; you can also target Java runtimes or runtime interpreters that execute diagrams directly.   [docs.nasdanika.org](https://docs.nasdanika.org/ai/draw-ai/index.html)

- **Choose your target**  
  - **Prototype fast:** generate Python via CrewAI and run in a sandbox.   [docs.nasdanika.org](https://docs.nasdanika.org/ai/draw-ai/index.html)  
  - **Enterprise production:** export manifests for Java runtimes or generate typed adapters and hand them to engineering.   [nasdanika-templates.github.io](https://nasdanika-templates.github.io/draw-ai/flow/index.html)

---

## Practical Guidance
- **Start small** — model one end‑to‑end flow with clear ontology bindings. Validate and run in sandbox.   [nasdanika-templates.github.io](https://nasdanika-templates.github.io/draw-ai/flow/index.html)  
- **Stabilize notation** — pick a small set of symbols and color codes and document them in the template.   [docs.nasdanika.org](https://docs.nasdanika.org/ai/draw-ai/index.html)  
- **Document adjacent to the model** — attach examples and edge cases to ontology attributes so prompts and tools have context.   [github.com](https://github.com/Nasdanika-Templates/draw-ai)  
- **Treat agents as organizational helpers** — they structure work; don’t confuse notation with runtime semantics. The runtime executes LLMs and tools.   [docs.nasdanika.org](https://docs.nasdanika.org/ai/draw-ai/index.html)

---

## References and Further Reading
- Draw.AI Flow examples and template site.   [nasdanika-templates.github.io](https://nasdanika-templates.github.io/draw-ai/flow/index.html)  
- Nasdanika Draw.AI conceptual overview and demos.   [docs.nasdanika.org](https://docs.nasdanika.org/ai/draw-ai/index.html)  
- Mapping and Ecore export documentation (semantic mapping).   [github.com](https://github.com/Nasdanika-Templates/draw-ai)

---

If you want, I can:
- produce a **downloadable swimlane example** (Draw.io XML) that demonstrates a Fraud → Case hand‑over with ontology bindings,  
- generate a **CrewAI Python manifest** from that diagram as a runnable demo, or  
- create a **validation checklist** for model governance and sandbox execution.