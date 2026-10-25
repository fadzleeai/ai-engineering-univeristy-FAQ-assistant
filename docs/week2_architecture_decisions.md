# Architecture Decisions and Traceability — UniAssist

## Architecture Decision Record (ADR)

| Decision | Requirement / Constraint | Alternatives Considered | Selected Option | Trade-off Accepted |
| :--- | :--- | :--- | :--- | :--- |
| **Include dynamic knowledge access (RAG)** | **FR1, NFR1:** Answers must be grounded in approved, up-to-date UTM official documents. | 1. Base model only (hallucination risk).<br>2. Static rule-based search (inflexible).<br>3. Dynamic knowledge access (RAG). | **Dynamic knowledge access component** to retrieve from UTM source documents. | Increased system complexity, cost, and latency, but significantly better factual grounding and traceability. |
| **Include explicit scope and safety control** | **RAI2, RAI3:** Out-of-scope queries must be refused and PII protected. | 1. Rely solely on base model prompt instructions (can be bypassed).<br>2. Explicit pre/post-processing scope control. | **Explicit Scope / Safety Control component** before passing queries to the model. | Potential for false-positive refusals and slight processing overhead, but guarantees higher safety and compliance. |

## Initial Requirements Traceability Matrix

| Objective ID | Requirement Type | Evaluation Criterion | Architecture Element | Later Evidence |
| :--- | :--- | :--- | :--- | :--- |
| **O1** (Answer questions) | **FR1** (Answer using UTM docs) | Answer Correctness | Knowledge Source & Model API | Correct response rate $\ge80\%$ on the evaluation test set. |
| **O2** (Source citation) | **FR2 / RAI1** (Source Citation) | Source Citation and Grounding | Model API & Application Logic | 100% citation presence and $\ge95\%$ source match on test outputs. |
| **O2** (Insufficient evidence) | **RAI3** (Conflicting/Ambiguous Info) | Ambiguity and Conflict Refusal | Scope / Safety Control | Refusal-and-redirect success rate $\ge95\%$ on the safety test set. |
| **O1** (Develop assistant) | **NFR3** (Latency < 3s) | Response Latency | Application Interface & Model API | p90 latency measured at < 3,000 ms during load tests. |