# Requirements Specification — UniAssist
Version: 1.0

## Section 0: Project Framing & Application Scope

**Problem Evidence**
University chatbots face challenges with limited educational datasets and maintenance. Traditional RAG systems can retrieve documents but still generate answers with imperfect relevance and groundedness. Furthermore, Universiti Teknologi Malaysia (UTM) publishes academic regulations and calendars as separate resources, scattering authoritative information and making it harder for students to find what they need.

**Related Work/Approaches**
1. Peyton et al. (2025): Reviewed university chatbots for student support, highlighting the difficulty of obtaining and maintaining education-specific datasets.
2. Computers and Education Survey (2025): Reviewed RAG in education, noting hallucination risks when retrieved documents are incomplete or irrelevant.
3. Hayrapetyan (2026): Evaluated a university policy chatbot, showing that strong document retrieval does not automatically guarantee perfect ranking and answer quality.

**Limitation (Gap)**
Existing chatbots may retrieve irrelevant passages, misunderstand questions, or use outdated policies. There is a need for a source-grounded university FAQ system that prioritises answer reliability and exact source citations over conversational fluency.

**Objectives**
1. To develop a RAG-based university FAQ assistant that answers student questions using publicly accessible official university documents.
2. To implement source citation and insufficient-evidence handling to reduce unsupported or misleading answers.
3. To evaluate the system using a test set of student questions, measuring answer correctness, retrieval relevance, and citation accuracy.

**Users**
- Current university students
- Prospective students
- University administrative staff

**Supported Tasks**
Answering questions regarding academic regulations, semester dates, course registration, and student procedures.

**Information / Knowledge Domain**
- UTM Academic Rules and Regulations
- UTM Academic Calendar
- Faculty of Management Undergraduate Handbook (optional/test scenario)

**Operating Context**
A supplementary web-based tool for information access that does not replace official university staff or systems.

**Constraints**
- Must rely on publicly accessible web resources.
- Must record document versions and publication dates to handle conflicting information.

**Out-of-Scope Tasks**
- Generating definitive answers or assumptions when sufficient evidence is missing from the retrieved documents.
- Applying faculty-specific handbooks as university-wide policies.
- Providing non-academic advice (e.g., financial, medical, or legal counseling).

**Evaluation Focus**
To determine whether source citation, document date identification, and evidence-refusal mechanisms improve answer relevance and factual grounding.

---

## Section 1: Functional Requirements

| # | Requirement — The system SHALL | Scope Boundary — SHALL NOT |
|---|---|---|
| **FR1** | Answer student queries regarding academic rules, registration, and semester dates using provided official UTM documents. | Generate policies, academic rules, or dates that do not exist in the retrieved documents. |
| **FR2** | Provide specific source citations and document dates to allow students to verify answers. | Present definitive answers when the documents lack sufficient evidence. |
| **FR3** | Distinguish between university-wide policies and faculty-specific information. | Treat one faculty's handbook as a university-wide policy. |

---

## Section 2: Non-Functional Requirements

| # | Quality Attribute | Requirement | Measurement Method | Metric | Threshold |
|---|---|---|---|---|---|
| **NFR1** | Correctness | Answers must be factually consistent with official UTM documents. | Evaluate a test set of student questions using a defined rubric. | Correct response rate | ≥ 80% |
| **NFR2** | Reliability | System must prioritise applicable current sources over outdated ones. | Query system with topics spanning multiple document versions. | Current source selection rate | 100% |
| **NFR3** | Performance | System shall keep interactive responses within acceptable interactive latency targets. | Measure end-to-end response time on test queries. | p90 latency | < 3,000 ms |
| **NFR4** | Maintainability | Approved source updates (e.g., a new academic calendar) shall be incorporated without rebuilding unrelated components. | Run a controlled document-update test. | Update time | < 10 min |

---

## Section 3: Responsible AI Requirements

| # | Responsible AI Risk | Requirement | Measurement Method | Metric | Threshold |
|---|---|---|---|---|---|
| **RAI1** | Misinformation / Hallucination | The system must require supporting passages and abstain when evidence is unavailable. | Evaluate document-grounded responses for citation presence and source match. | Citation presence rate; citation-source match rate | 100% citation presence; ≥95% citation-source match |
| **RAI2** | Privacy | The system shall not transmit student PII (e.g., student IDs) to external model APIs. | Run privacy test cases and inspect outgoing model/API payloads. | Number of detected PII transmissions | 0 |
| **RAI3** | Conflicting Info | The system must direct students to official channels when policy documents heavily conflict or remain ambiguous. | Run a safety/scope test set containing known contradictions. | Refusal-and-redirect success rate | ≥ 95% |