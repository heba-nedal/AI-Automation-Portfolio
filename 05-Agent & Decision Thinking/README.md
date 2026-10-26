# U5 — BUILD AI AGENTS

## AI Agents & Tool Use

> An AI Agent should know what to do, when to use a tool, and when to wait for confirmation.

In this unit, I learn how to build AI Agents that understand user requests, maintain conversational context, make appropriate decisions, and use external tools to perform real-world tasks.

The goal is not simply to connect a language model to a tool. It is to design a system that determines the next step, applies business rules, verifies outcomes, and handles unexpected situations before reporting success.

---

## 🎯 Capability

**AI Agent Design & Controlled Tool Use**

The ability to design AI agents that understand requests, use memory and external tools, and make decisions according to clear rules while controlling actions and verifying their results.

---

## 🧠 What I Learned

Throughout this unit, I developed my ability to:

- **Design an AI Agent:** Define the agent's role, responsibilities, instructions, and action boundaries.
- **Manage Conversation Context:** Use memory to retain previous information and apply it across messages.
- **Use Tools Intentionally:** Connect the agent to external tools and determine when they are needed.
- **Apply Business Rules:** Enforce conditional rules and validate data before taking action.
- **Control Tool Execution:** Define the conditions that must be met before an action affects an external system.
- **Handle Exceptions:** Respond to missing information, unavailable appointments, and technical errors.
- **Verify Results:** Check tool execution results instead of treating a conversational response as proof that an external action succeeded.
- **Test Agent Behavior:** Evaluate agent decisions using practical scenarios and verify outcomes in connected systems.

---

## 🛠️ Projects

### 01 — Course Project

**Project:** XYZ Real Estate AI Agent

An AI agent for a real estate company that receives customer messages through Telegram, progressively collects property requirements, validates the information, and saves it to Google Sheets only after the customer confirms the final summary.

- **Problem:** Collecting real estate lead information manually, checking completeness, and ensuring customer approval before recording it.
- **Solution:** Build an AI agent that uses memory to understand conversation context, asks for missing information, applies conditional rules, and requests confirmation before using the Google Sheets tool.
- **Tools:** n8n, Telegram, OpenRouter, Simple Memory, Google Sheets.

**Key Focus:** Context Management, Data Validation & Confirmation-Gated Tool Use.

[Explore the Course Project](./Course-Project/)

### 02 — Independent Project

**Project:** Lamsa Salon AI Booking Agent

An AI booking agent for Lamsa Salon that communicates through Telegram, checks appointment availability, suggests alternatives when a requested slot is occupied, collects booking details, and records confirmed appointments in Google Calendar and Google Sheets.

- **Problem:** Manually managing appointment requests, handling unavailable time slots, and maintaining booking records across multiple systems.
- **Solution:** Build an AI agent connected to a calendar and spreadsheet to check availability, guide the conversation, present a booking summary, and carry out booking actions while reporting the outcome.
- **Tools:** n8n, Telegram, OpenRouter, Simple Memory, Google Calendar, Google Sheets.

**Key Focus:** Availability Checking, Alternative Suggestions & Multi-Tool Booking Automation.

[Explore the Independent Project](./Independent-Project/)

---

## 🔍 Engineering Focus

In this unit, I focus on the following questions:

1. How does an agent determine the next step in a conversation?
2. How can it retain previous information without mixing data between users?
3. When should it use an external tool instead of returning a text response?
4. How should it apply business rules and handle missing or invalid information?
5. How can it prevent actions from running before the required confirmation?
6. How can it verify an external action before reporting success?
7. How should it handle tool failures and retries without creating duplicate records?

---

## 📌 Key Takeaway

**An AI Agent is more than a chatbot: it combines reasoning, context, tools, and controlled actions.**

A successful AI agent is measured not only by the quality of its responses, but also by its ability to make appropriate decisions, use tools under clear conditions, and verify real outcomes before reporting success.

---

## 📈 Capability Progress

- [x] Design an AI agent with clear instructions.
- [x] Connect the agent to a language model and memory.
- [x] Use external tools to work with data and appointments.
- [x] Apply business rules and validate information.
- [x] Require user confirmation before key actions.
- [x] Test actual agent behavior through practical conversations.
- [x] Verify outcomes in Google Sheets and Google Calendar.
- [ ] Strengthen error handling and prevent duplicate operations in all cases.
- [ ] Expand testing to cover partial failures, concurrent requests, and retries.

---

## 🔗 Related Projects

- [Course Project — XYZ Real Estate AI Agent](./Course-Project/)
- [Independent Project — Lamsa Salon AI Booking Agent](./Independent-Project/)

---

**Next:** U6 — Automation & Integration Thinking

