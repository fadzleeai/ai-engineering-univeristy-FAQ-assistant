# UniAssist: An AI-Powered University FAQ Assistant

## 1. Project Name and Domain

**Project Name:** UniAssist: An AI-Powered University FAQ Assistant

**Application Domain:** Higher education and student information services.

The proposed system uses Natural Language Processing (NLP) and Retrieval-Augmented Generation (RAG) to help students obtain information from official university documents. It will answer questions about academic regulations, semester dates, course registration and student procedures, while providing citations to relevant sources.

## 2. Problem Statement

University students often need to search through multiple websites, academic handbooks and policy documents to find information about university procedures. These documents may contain lengthy explanations and formal terminology, making it difficult for students to identify the exact information they need.

Traditional FAQ systems are generally limited to predefined questions and answers, while general-purpose AI chatbots may generate inaccurate answers that are not supported by the university's official policies.

Therefore, this project proposes an AI-powered university FAQ assistant that retrieves relevant information from official documents and generates clear, contextual answers with source citations. This approach aims to improve access to university information while reducing the risk of unsupported answers.

## 3. Evidence of the Problem

Three sources support the motivation for this project:

1. **Peyton, Unnikrishnan and Mulligan (2025)** reviewed university chatbots used for student support. Their review identified challenges involving limited educational datasets, maintaining FAQ content and the relatively underdeveloped use of chatbots for university administration.

2. **Hayrapetyan (2026)** evaluated a RAG chatbot using university policy documents. The study reported moderate answer relevance (0.64) and groundedness (0.66), highlighting that retrieving information does not automatically guarantee accurate, well-supported answers.

3. **Universiti Teknologi Malaysia (UTM)** publishes academic regulations and academic calendars as separate resources. Students may need to consult different documents depending on their questions. These resources demonstrate the availability of authoritative information that can be consolidated into a question-answering system.

Together, these sources support the need for more accessible information retrieval and reliable answers. They do not, by themselves, establish how frequently UTM students experience this problem; that could be investigated through a student survey.

## 4. Initial Related Work

### Study 1: A Review of University Chatbots for Student Support: FAQs and Beyond (2025)

**Authors:** Peyton, Unnikrishnan and Mulligan

- **Approach:** Reviews existing university chatbot implementations, including administrative and student-support systems.
- **Limitation:** Identifies difficulties in obtaining and maintaining education-specific datasets and keeping predefined FAQs updated.
- **Relevance:** Supports the need for a document-based assistant that can use existing university resources.

**Link:** https://link.springer.com/article/10.1007/s44217-025-00397-7

### Study 2: Retrieval-Augmented Generation for Educational Application: A Systematic Survey (2025)

**Publication:** Computers and Education: Artificial Intelligence

- **Approach:** Reviews RAG applications and their challenges in educational settings.
- **Limitation:** RAG can still produce hallucinations when retrieved documents are incomplete, outdated or irrelevant.
- **Relevance:** Motivates source citations, retrieval-quality checks and the ability to abstain when evidence is insufficient.

**Link:** https://doi.org/10.1016/J.CAEAI.2025.100417

### Study 3: Label-Free Evaluation of Retrieval-Augmented Generation in a University Policy Chatbot (2026)

**Author:** Lusine Hayrapetyan

- **Approach:** Evaluates a university-policy chatbot using relevance, groundedness and retrieval metrics.
- **Limitation:** The reported results show that retrieval coverage can be strong while ranking and answer quality remain imperfect.
- **Relevance:** Demonstrates the importance of evaluating both retrieved evidence and the final answer rather than assuming the chatbot works because it can retrieve documents.

**Link:** https://doi.org/10.1145/3770761.3777161

## 5. Engineering Gap / Limitation

Existing university chatbots and RAG systems provide useful foundations, but practical reliability remains a challenge. A chatbot may retrieve irrelevant passages, misunderstand a student's question, or generate an answer using outdated policies.

The engineering gap addressed by UniAssist is the development of a **small, source-grounded university FAQ system that prioritises answer reliability over conversational fluency**.

The proposed system will focus on:

- Retrieving relevant passages from official university documents.
- Providing source citations that allow students to verify answers.
- Refusing to provide definitive answers when the documents do not contain sufficient evidence.
- Identifying document titles and dates to help distinguish current information from outdated policies.

The project will evaluate whether these mechanisms improve answer relevance and factual grounding on a defined set of university questions.

## 6. Project Objectives

1. To develop a RAG-based university FAQ assistant that answers student questions using publicly accessible official university documents.
2. To implement source citation and insufficient-evidence handling to reduce unsupported or misleading answers.
3. To evaluate the system using a test set of student questions, measuring answer correctness, retrieval relevance and citation accuracy.

## 7. Target Users

- **Current university students:** To find academic rules, registration procedures and semester dates.
- **Prospective students:** To obtain general information about university procedures and requirements.
- **University administrative staff:** As a supplementary tool for answering repetitive questions and locating relevant policy documents.

The system is intended to support information access, not replace official university staff or systems.

## 8. Data Sources

The initial prototype can use the following publicly accessible UTM resources.

### Source 1: UTM Academic Rules and Regulations

**Content:** Academic rules for undergraduate and other listed study programmes, depending on the document selected.

**Use:** Answer questions about academic requirements, progression and university procedures.

**URL:** https://ugs.utm.my/academic-rules/

### Source 2: UTM Academic Calendar

**Content:** Semester schedules, lecture periods, examination periods and academic breaks.

**Use:** Answer questions about semester dates and academic schedules.

**URL:** https://amd.utm.my/academic-calendar/

### Optional Source 3: Faculty of Management Undergraduate Handbook

**Content:** Faculty-specific academic information, policies and procedures.

**Use:** Test whether the assistant can handle information that applies only to a particular faculty.

**URL:** https://management.utm.my/download-academic-guide/

These sources are publicly accessible web resources. Before implementation, the documents should be downloaded or processed from the official pages, and their applicable programmes, versions and publication dates should be recorded. The prototype should not treat one faculty's handbook as a university-wide policy.

## 9. Comparison with EduAdvisor

EduAdvisor provides educational guidance and information to help students explore study options and make informed decisions. UniAssist shares the broader goal of making educational information easier to access, but its scope and implementation differ.

| Aspect | EduAdvisor | Proposed UniAssist |
|---|---|---|
| Main purpose | Education guidance and study-option discovery | Answer university FAQ questions |
| Target users | Students exploring education options | Current and prospective university students |
| Information | Education pathways, institutions and programme information | Official university policies, handbooks and academic calendars |
| Proposed AI approach | Educational information platform; implementation details should be verified separately | RAG with a language model and document retrieval |
| Main output | Guidance and information for education decisions | Contextual answers with supporting source citations |
| Main limitation | Users may still need to consult individual institutions for specific or updated policies | Limited by document coverage, retrieval quality and the freshness of source documents |

**Similarity:** Both aim to make educational information more accessible and help students find relevant information.

**Difference:** EduAdvisor focuses on broader education guidance, whereas UniAssist focuses on answering specific university questions using official documents as its evidence base.

*Note:* The comparison describes EduAdvisor at a high level. It does not claim that EduAdvisor lacks AI or particular technical features.

## 10. Responsible AI Risks

### Risk 1: Misinformation and Hallucination

The chatbot may generate incorrect academic deadlines, eligibility requirements or procedural instructions. Students could miss important deadlines or make incorrect academic decisions.

**Mitigation:** Require supporting document passages, display source citations and dates, and abstain when sufficient evidence is unavailable.

### Risk 2: Privacy and Data Security

Students may accidentally submit personal details, student identification numbers or sensitive academic information while interacting with the chatbot.

**Mitigation:** Avoid collecting unnecessary personal information, minimise conversation logging, protect stored data and warn users not to submit sensitive details.

### Risk 3: Outdated or Conflicting Information

Old handbooks or conflicting university documents may cause the chatbot to provide information that is no longer valid.

**Mitigation:** Record document versions and publication dates, prioritise applicable current sources, and direct students to official university channels when policies conflict.

---

## References

1. Peyton, K., Unnikrishnan, S., & Mulligan, B. (2025). *A review of university chatbots for student support: FAQs and beyond.* Discover Education. https://link.springer.com/article/10.1007/s44217-025-00397-7
2. *Retrieval-augmented generation for educational application: A systematic survey.* (2025). Computers and Education: Artificial Intelligence. https://doi.org/10.1016/J.CAEAI.2025.100417
3. Hayrapetyan, L. (2026). *Label-Free Evaluation of Retrieval-Augmented Generation in a University Policy Chatbot.* Proceedings of the ACM Technical Symposium on Computer Science Education. https://doi.org/10.1145/3770761.3777161
4. Universiti Teknologi Malaysia. *Academic Rules and Regulations.* https://ugs.utm.my/academic-rules/
5. Universiti Teknologi Malaysia. *Academic Calendar.* https://amd.utm.my/academic-calendar/