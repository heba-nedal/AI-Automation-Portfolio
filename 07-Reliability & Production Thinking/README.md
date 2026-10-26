# U7 — RELIABILITY & PRODUCTION THINKING

## Building Reliable AI Automation Systems

> Building an AI solution is not enough; it must behave reliably and handle uncertainty responsibly.

In this unit, I apply reliability and production thinking to an AI-powered knowledge assistant. I focus on testing actual system behavior, evaluating source-grounded responses, handling questions outside the knowledge base, and identifying improvements that can make an AI automation more dependable.

The goal is to move beyond building a working workflow and understand how to evaluate its behavior, communicate its limitations, and prepare it for more reliable use.

---

## 🎯 Capability

**Reliability & Production Thinking**

The ability to evaluate AI automation systems, test expected behavior, identify limitations, and design improvements that support reliable operation.

---

## 🧠 What I Learned

Through this unit, I developed my ability to:

- **Evaluate System Behavior:** Verify that the workflow produces the expected results.
- **Test Different Scenarios:** Test questions supported by the knowledge base and questions outside its scope.
- **Handle Uncertainty:** Make the distinction between source-grounded information and general knowledge clear to users.
- **Inspect Workflow Execution:** Review execution results and connected components in n8n.
- **Identify Improvements:** Use observed behavior to determine what could improve reliability.
- **Document Evidence:** Support project claims with actual screenshots and test results.

---

## 🛠️ Guided Project

### 01 — Course Knowledge Assistant

**Project:** Course Knowledge Assistant — RAG-Powered AI Agent

An AI-powered course assistant that retrieves information from course materials and generates answers, while explicitly identifying topics not covered by the source.

- **Problem:** Users need to find information in course documents efficiently and understand whether an answer is supported by the available materials.
- **Solution:** Build two n8n workflows: one processes PDF documents and stores embeddings in Supabase, while the other uses an AI agent to retrieve relevant content and answer questions.
- **Tools:** n8n, Google Drive, Supabase Vector Store, OpenAI Embeddings, Google Gemini Chat Model, and Simple Memory.

**Reliability Focus:**

- Verify answers to questions covered by the source.
- Test questions about topics not mentioned in the guide.
- Confirm that the assistant distinguishes missing source information from general explanations.
- Inspect successful workflow executions.
- Identify opportunities to improve retrieval quality and source transparency.

[Explore the Course Project](./course-project/)

---

## 🔍 Engineering Focus

In this unit, I focus on the following questions:

1. Does the system behave as expected for supported questions?
2. How does it respond when the source does not contain the requested information?
3. Can users distinguish source-based answers from general explanations?
4. What evidence demonstrates that the workflow executed successfully?
5. Which limitations should be documented?
6. What changes would improve the system's reliability in future iterations?

---

## 📌 Key Takeaway

**A working AI workflow is only the beginning; reliability comes from testing its behavior, understanding its limitations, and improving it based on evidence.**

---

## 📈 Capability Progress

- [ ] Define expected behavior for different input scenarios.
- [ ] Test questions supported by the knowledge base.
- [ ] Test questions outside the source material.
- [ ] Inspect workflow execution results.
- [ ] Document actual outcomes and supporting evidence.
- [ ] Identify limitations and prioritize future improvements.

---

## 🔗 Related Projects

- [Guided Project — Course Knowledge Assistant](./Course-Project/)

---

**Next:** Continue to the next unit in the AI Automation learning path.
