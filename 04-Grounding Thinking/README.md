# U4 — GROUND ITS KNOWLEDGE

## Knowledge Grounding & Reliability Evaluation

> Before trusting an AI answer, understand where its knowledge comes from.

In this unit, I learn how to build AI systems that rely on specific knowledge sources, retrieve relevant information, and generate answers grounded in available evidence.

The goal is not simply to build a chatbot, but to understand how knowledge is prepared, how information is retrieved, how answers are evaluated, and how system limitations can be identified through testing.

---

## 🎯 Capability

**Knowledge Grounding & Reliability Evaluation**

The ability to build knowledge-grounded AI systems, evaluate retrieval quality, verify answer reliability, recognize knowledge limitations, and improve system behavior through evidence-based testing.

---

## 🧠 What I Learned

Throughout this unit, I developed my ability to:

- **Design the Knowledge Base:** Select relevant knowledge sources and evaluate their quality.
- **Prepare Knowledge:** Organize documents and prepare content for effective retrieval.
- **Build RAG Systems:** Connect knowledge bases to AI applications that retrieve information before generating answers.
- **Configure Retrieval:** Understand retrieval settings and evaluate the relevance of retrieved context.
- **Ground AI Answers:** Verify that generated answers are supported by available knowledge.
- **Control Hallucinations:** Test whether the system can acknowledge insufficient information instead of inventing answers.
- **Evaluate Reliability:** Design test cases and compare actual responses against expected results.
- **Analyze Failures:** Investigate limitations in retrieval, context selection, and answer generation.
- **Improve Through Evidence:** Use evaluation findings to guide improvement decisions instead of changing settings arbitrarily.

---

## 🛠️ Projects

### 01 — Guided Project

**Project:** TECHFIX — AI Computer Troubleshooting Assistant

A knowledge-grounded assistant designed to help users troubleshoot common computer problems using a specialized knowledge base.

- **Problem:** Users may struggle to identify appropriate troubleshooting steps when facing common computer issues.
- **Solution:** Build an AI assistant that retrieves relevant technical information and uses it to generate problem-specific guidance.
- **Tools:** Dify, Retrieval-Augmented Generation (RAG), Knowledge Base.

[Explore the Project](./Course-Project/)

### 02 — Independent Project

**Project:** Git Merge Rescue — Knowledge Assistant

A knowledge-grounded assistant that helps developers understand Git branches, pull requests, merge conflicts, and related commands using curated technical documentation.

- **Problem:** Developers may struggle to choose appropriate conflict-resolution steps and distinguish between resolving conflicts and completing a pull request merge.
- **Solution:** Build a Dify RAG application that retrieves relevant information from six Markdown documents and generates answers grounded in the retrieved context.
- **Tools:** Dify, Hybrid Search, Embeddings, Reranking, Gemini, Markdown.

[Explore the Project](./Independent-Project/)

---

## 🔍 Engineering Focus

Throughout this unit, I focus on the following questions:

1. Which knowledge sources does the system need, and why were they selected?
2. How should documents be prepared for effective retrieval?
3. Does the system retrieve relevant information before generating an answer?
4. Is the generated answer supported by the available knowledge?
5. What happens when the required information is missing?
6. How can I distinguish a retrieval problem from an answer-generation problem?
7. How can I evaluate reliability using diverse test cases?
8. How can I use evaluation results to make evidence-based decisions?

---

## 📌 Key Takeaway

**A reliable AI system must retrieve relevant knowledge, ground its answers, and recognize when the evidence is insufficient.**

Building a knowledge-grounded AI system requires more than generating plausible answers. It requires evaluating the sources, inspecting retrieved context, testing actual responses, and documenting limitations honestly.

---

## 📈 Capability Progress

- [x] Select knowledge sources relevant to a defined problem.
- [x] Build knowledge-based AI applications using Dify.
- [x] Configure a RAG system to retrieve information before generating answers.
- [x] Test questions with answers available in the knowledge base.
- [x] Test questions that require combining related information.
- [x] Test questions that cannot be answered from the available knowledge.
- [x] Compare actual responses against expected results.
- [x] Identify and document an incomplete response.
- [x] Document test results and improvement opportunities.

---

## 🔗 Related Projects

- [Guided Project — TECHFIX](./Course-Project/)
- [Independent Project — Git Merge Rescue](./Independent-Project/)
- [Independent Project — Test Cases & Results](./Independent-Project/TEST_CASES.md)

---

**Next:** U5 — APPLY AI AUTOMATION
