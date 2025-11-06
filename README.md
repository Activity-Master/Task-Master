# TaskMaster

An abstract, transport-agnostic Task Group processor for the ActivityMaster platform. It generalizes `MultiTimedComPortSender` into a module capable of orchestrating heterogeneous executors (COM/Serial, HTTP, MQ, File, etc.), with reactive APIs, persistence, and domain feedback.

## What is here (Design First)
This folder contains design documents that architect, design, and demonstrate TaskMaster before implementation. Mermaid diagrams illustrate structure and flows.

- 00-Overview.md — goals, scope, and high-level architecture
- 01-Features-Inventory.md — parity checklist from `MultiTimedComPortSender`
- 02-Architecture.md — C4-style context and container diagrams, flows
- 03-Domain-Model.md — entities, relationships, and lifecycle state machines
- 04-API-Design.md — facade and SPI, DTOs, reactive contracts
- 05-Persistence-Strategy.md — relational model (phase 1), indexing, retention
- 06-Eventing-Observability.md — events, debouncing, metrics, logs, tracing
- 07-Migration-Plan.md — stepwise cutover from legacy
- 08-Demonstrations.md — end-to-end examples and usage flows

## Quick Start (Conceptual)
- Read 00-Overview.md to understand objectives and principles.
- Skim 02-Architecture.md and 03-Domain-Model.md for core shapes.
- Review 04-API-Design.md for the intended interfaces and DTOs.
- See 07-Migration-Plan.md for how we will integrate with `MultiTimedComPortSender`.

## Design Guarantees
- Consumer-agnostic: TaskMaster does not depend on, or require changes to, any consumer module (e.g., Cerial Master). It is a standalone orchestration module.
- Transport-agnostic: No executor is privileged; executors are plugins registered via the SPI. The COM bridge is optional and out-of-core.
- Task = anything runnable: A task is any unit of work that a `TaskExecutor` can run. Payloads and headers are opaque to TaskMaster and interpreted only by the executor.

## Next Steps (after design sign-off)
- Implement the Facade, Orchestrator, and SPI scaffolding; optionally add a `ComPortGroupHandler` plugin to bridge `MultiTimedComPortSender` for `serial:` keys without altering the legacy.
- Add minimal persistence (tables from 05-Persistence-Strategy.md) and publishers.
- Provide sample wiring in ActivityMasterClient.

## Status
Design documents are ready for review. No implementation code has been generated yet.
