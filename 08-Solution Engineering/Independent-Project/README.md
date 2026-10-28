# KinderLink — Kindergarten Communication Automation

> An n8n-based automation prototype designed to streamline communication between kindergarten staff, administrators, and parents through Telegram, with Supabase as the data layer and AI-assisted daily notes.

---

## 🎯 Project Overview

KinderLink is an AI-powered workflow automation project designed to improve routine communication in kindergarten environments.

Kindergarten staff often need to communicate attendance updates, share daily observations about children, and request announcements for parents. When these tasks are handled manually, they can become repetitive, time-consuming, and difficult to track consistently.

KinderLink explores how workflow automation can organize these processes through a Telegram bot, database-backed records, and AI-assisted text refinement.

**Project status:** Prototype — requires further testing and improvements before production use.

---

## 🎯 Problem

### The Context

Kindergartens regularly communicate with parents about children's attendance, daily activities, observations, and important announcements.

These tasks require coordination between teachers and administrators, along with accurate recipient selection and reliable message delivery.

### The Problem

Manual communication workflows can lead to repetitive administrative work, inconsistent messages, missed notifications, and limited visibility into whether communication tasks have been completed successfully.

### Why It Matters

A structured communication workflow can reduce repetitive work, improve consistency, and help staff manage routine updates more efficiently.

KinderLink demonstrates an initial approach to automating these tasks while identifying the reliability and security considerations that must be addressed before real-world deployment.

---

## ⚙️ Solution

KinderLink uses n8n to coordinate Telegram interactions, database operations, conditional routing, and AI-assisted text processing.

The prototype includes three main communication workflows:

### 1. Absence Notifications

- Teachers can report a child's absence using Arabic or English command prefixes.
- The workflow looks up the child in the database.
- It checks attendance records for the current day using the `Asia/Gaza` time zone.
- If no attendance record is found, it creates an absence record.
- It identifies eligible parent records and sends an absence notification through Telegram when the required data is available.
- It updates the attendance record's notification flag after the notification path completes.

### 2. AI-Assisted Daily Notes

- Teachers submit a child's name and a daily observation.
- An AI node rewrites the note in a warm, parent-friendly tone.
- The AI instructions emphasize preserving the original facts and avoiding invented details or medical diagnoses.
- The workflow identifies eligible parents and sends the resulting note through Telegram.
- Successfully processed messages are recorded in the database.

### 3. Announcement Approval Workflow

- Staff submit announcement requests using Arabic or English commands.
- The workflow validates the request and creates a pending announcement record.
- An administrator receives an approval or rejection request.
- The workflow checks the request status before processing the administrator's decision.
- Approved announcements are sent to active parent records with available Telegram IDs, and message records are created.
- Rejected requests are marked accordingly.

---

## 🏗️ Workflow Architecture

The prototype follows this general processing flow:

```text
Teacher / Administrator
          |
          v
     Telegram Bot
          |
          v
       n8n Workflow
          |
          v
   Staff Authorization
          |
          v
    Role-Based Routing
          |
    +-----+------+----------------+
    |            |                |
    v            v                v
  Absence    Daily Notes     Announcements
    |            |                |
    v            v                v
 Attendance   OpenAI Text      Admin Review
   Lookup      Refinement      and Decision
    |            |                |
    +------------+----------------+
                 |
                 v
       Supabase / PostgreSQL
                 |
                 v
       Parent Notifications
          via Telegram
```

The diagram represents the intended high-level workflow structure. Actual delivery, error handling, and end-to-end behavior still require additional testing.

---

## 🛠️ Technologies Used

| Technology | Purpose |
|---|---|
| **n8n** | Workflow orchestration, conditional routing, and automation logic |
| **Telegram Bot API** | Staff interaction and parent notifications |
| **Supabase / PostgreSQL** | Structured data storage and database queries |
| **OpenAI** | AI-assisted rewriting of daily notes |
| **JavaScript** | Data parsing, transformations, and workflow logic |

---

## 🔐 Authorization and Data Handling

The current workflow includes an authorization step that checks whether the Telegram user corresponds to an active staff record. It also routes authorized staff according to their assigned role.

Database records are used to identify children, attendance entries, parent records, announcement requests, and message logs.

The prototype also includes checks intended to prevent duplicate absence registration and to ensure that announcement requests are processed only while pending.

These controls require further validation, particularly around edge cases, database access policies, notification preferences, and partial failures.

**Privacy note:** Any real deployment should use appropriate access controls, secure credential management, data minimization, and verified database security policies. Public repository files should not contain API tokens, secret keys, or unnecessary personal data.

---

## 🧪 Current Implementation

The exported workflow contains the following implemented components:

- Telegram-triggered workflow entry.
- Database-backed staff authorization.
- Role-based command routing.
- Arabic and English command prefixes for supported operations.
- Child lookup and daily attendance checks.
- Absence record creation and parent notification paths.
- AI-assisted daily note rewriting.
- Announcement submission and administrator approval/rejection paths.
- Database-backed message logging for supported notification paths.

The presence of these components in the workflow export does not, by itself, establish that every path has been successfully tested under real operating conditions.

---

## ⚠️ Known Limitations

The current version is an initial prototype and has several areas that require attention.

### 1. Error Handling and Retries

A consistent error-handling strategy and automatic retries for failed message deliveries need further implementation and validation.

### 2. Partial Notification Failures

The announcement workflow needs stronger handling for cases where some parents receive a message while others do not. A final request status should accurately reflect the outcome of the entire delivery process.

### 3. Attendance Status Validation

The current absence check looks for an attendance record for the child on the current day. It should distinguish an existing absence record from other attendance statuses before deciding that the absence has already been recorded.

### 4. Staff Authorization Feedback

The unauthorized-user path needs a clear response so that an unrecognized or inactive staff member does not receive no feedback from the bot.

The workflow should also handle cases where no active administrator is available to review an announcement request.

### 5. Recipient Selection

Parent selection should be reviewed to ensure that recipients match the intended child relationships, active status, and notification preferences for each communication type.

### 6. Child Record Validation

The daily note workflow should consistently apply the intended child eligibility rules, including whether inactive child records may be processed.

### 7. Database Security

Supabase Row Level Security (RLS), database permissions, and the handling of sensitive information require a dedicated security review before production use.

### 8. Additional Features

Automated fee reminders and other potential administrative workflows are outside the current implemented scope and may be considered in future iterations.

---

## 🚀 Future Improvements

The next development phase will focus on reliability, security, and operational readiness.

- [ ] Implement structured error handling and retry logic.
- [ ] Track notification outcomes per recipient.
- [ ] Support partial-success states for announcement delivery.
- [ ] Improve attendance status validation and duplicate prevention.
- [ ] Add explicit feedback for unauthorized users.
- [ ] Handle missing or inactive administrator accounts.
- [ ] Refine recipient filtering and notification preferences.
- [ ] Apply consistent child eligibility validation.
- [ ] Review and test Supabase RLS policies.
- [ ] Remove hardcoded personal information and improve configuration management.
- [ ] Add automated tests and end-to-end workflow tests.
- [ ] Introduce monitoring and operational logs for failed executions.
- [ ] Evaluate a separate fee-reminder workflow.

---

## 🧪 Testing Strategy

Before production deployment, the following scenarios should be tested:

- Authorized and unauthorized Telegram users.
- Active and inactive staff accounts.
- Valid and invalid child names.
- Repeated absence reports for the same child and date.
- Existing attendance records with different statuses.
- Daily notes with missing or malformed fields.
- Children without eligible parent recipients.
- Parents without Telegram IDs or with notifications disabled.
- Announcement approval, rejection, and repeated decisions.
- Missing administrator accounts.
- Telegram delivery failures and partial broadcast failures.
- Database errors, retry behavior, and duplicate message prevention.
- Access restrictions and sensitive-data exposure.

The workflow should be tested in a controlled environment with test accounts and non-sensitive data before being used with real staff or parents.

---

## 📦 Repository Contents

The repository includes the exported n8n workflow:

```text
Independent-Project/
└── kinderlink-main-workflow.json
```

The JSON export provides a starting point for inspecting and importing the workflow into n8n.

When importing it into another environment, configure the required Telegram, Supabase, and OpenAI credentials. Review environment-specific settings and validate each workflow path before enabling it.

---

## ⚙️ Setup Overview

1. Install or access an n8n instance.
2. Import `kinderlink-main-workflow.json`.
3. Configure the required Telegram, Supabase, and OpenAI credentials.
4. Prepare the required database tables and fields used by the workflow.
5. Verify the Telegram bot configuration and database queries.
6. Test each command and workflow path with non-sensitive test data.
7. Validate authorization, notification delivery, and failure handling.
8. Keep the workflow disabled in production until the required security and reliability checks are complete.

The workflow export alone may not include every database schema, external configuration, or deployment requirement needed for a complete installation.

---

## 📚 What This Project Demonstrates

KinderLink demonstrates practical exploration of:

- Workflow automation with n8n.
- Integration between Telegram, AI services, and a relational database.
- Role-based routing and database-backed authorization.
- Conditional business logic and duplicate checks.
- AI-assisted text transformation with constraints on generated content.
- Notification workflows and message logging.
- Reliability analysis and identification of production-readiness gaps.

An important part of this project is recognizing that a workflow is not production-ready simply because its main path has been implemented. Reliable automation also requires validation, error handling, security, observability, and testing of failure scenarios.

---

## 📌 Project Status

**Current stage:** Initial prototype and iterative development.

KinderLink demonstrates the core workflow design for kindergarten communication automation. Further implementation, security review, and end-to-end testing are required before the system can be considered production-ready.

---

## 👩‍💻 Author

Developed as part of a practical AI Automation learning and portfolio journey, exploring how AI, databases, messaging platforms, and workflow automation can be combined to solve real-world administrative problems.

