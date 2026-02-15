
This page explains how **agentic flows** work in Draw.AI: the simple core model (LLMs + tools + prompts), the swimlane notation used here, the core concepts and contracts, and how diagrams become executable artifacts (Python via CrewAI demos, Java runtimes, JSON/Ecore exports). 
The examples and patterns below are grounded in the Draw.AI approach and mapping capabilities. 

---

## Overview
At its heart, an **agentic flow** is a sequence of **LLM calls** and **tool calls** organized so that agents can collaborate, hand off work, and produce typed inputs and outputs. 
The flow is a **visual, machine‑readable specification** that:

- Defines **agents** and the **tasks** they perform. 
- Declares **tools** (APIs, DBs, microservices, LLMs) and their contracts. 
- Binds **inputs**, **outputs**, tool **parameters** and return **values** to ontology types. 

**Key idea:** constructs like “agent”, “crew”, or “task” are syntactic sugar — they structure LLM + tool interactions so humans can reason about them. 
Under the hood, everything is LLMs provided with prompts and tools. 

---

## Core Concepts and Definitions

- **LLM** - A language model used to interpret prompts, generate text, or orchestrate logic. In flows, 
- **Tool** - Any callable capability: HTTP API, database query, file store, or a wrapped LLM. Tools have **typed parameters** and **typed return values** defined in the ontology. 
- **Agent** - A logical actor that performs tasks by issuing LLM calls and tool calls. An agent receives typed inputs, uses tools/LLMs, and produces typed outputs. Agents are swimlanes in the notation used on this page. 
- **Task** - A unit of work inside an agent swimlane. Tasks map to one or more LLM/tool calls and have explicit input/output contracts.
- **Tool Call** - A direct invocation of a tool with typed parameters; returns typed results.
- **Agent Call** - A logical invocation of another agent. An agent call can be **wrapped as a tool call** (i.e., the callee agent is exposed as a callable tool), enabling uniform orchestration. 
- **Hand‑over** - The explicit transfer of an output from one agent/task to another agent/task. Hand‑overs are typed and validated against the ontology.

---

## Swimlane Notation Explained

This page uses a **swimlane notation** where:

- Each **swimlane** represents an **Agent** (label at top).  
- Inside a swimlane, **tasks** are boxes connected by arrows.  
- **Tool icons** sit beside tasks in the same swimlane. Tools can be connected to tasks.  
- **Hand‑overs** are arrows between tasks with labels referencing ontology types (e.g., `CustomerProfile -> RiskAssessment`). 

**Why swimlanes?** They align naturally with process thinking and make responsibilities explicit. 
Other notations are valid — the important part is that the notation maps to the same underlying model: LLM calls + tool calls + typed contracts. 

## From Diagram to Executable Artifact

Draw.AI flows are designed to be **first‑class artifacts** that can be exported or executed:

### Generation targets

- **CrewAI Python** — diagrams can generate executable Python orchestrations (demoed with CrewAI). 
- **LangGraph, Semantic Kernel, Java runtimes** — flows can be mapped to other runtimes; sometimes you generate code, sometimes you run the flow directly in a runtime that interprets the diagram. 

### No code required

You do not always need to generate code. Some runtimes can **interpret** the diagram directly and execute it as an artifact. 
Other times you generate code for a target platform. Both approaches are supported. 

## CrewAI Python Demos 

There are two functional demos with [semantic mapping](https://docs.nasdanika.org/core/mapping/index.htm) to the [CrewAI model](https://crew-ai.models.nasdanika.org/) and CrewAI as the generation target:

* [Latest AI Development - swimlanes](https://nasdanika-demos.github.io/latest-ai-development-swimlanes/)
* [Latest AI Development](https://nasdanika-demos.github.io/latest-ai-development/)

The demos are dated - they were created as a proof of concept.
