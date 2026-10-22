# AI Workshop Registration & Participant Request Router

> An AI-assisted automation workflow that validates workshop registrations, summarizes learning goals, and routes incomplete submissions for human review.

---

## 🎯 Problem

### The Context

Workshop organizers collect registrations from participants with different learning goals and expectations. Managing these submissions requires collecting participant information, checking data completeness, maintaining organized records, and communicating the appropriate next steps.

### The Problem

A registration form may accept values containing only whitespace in required fields. If these submissions are treated as valid, organizers may receive incomplete records, and automated confirmation emails may contain missing information.

Manually checking every submission also introduces repetitive work and increases the chance of overlooking incomplete data.

### Why It Matters

A reliable registration workflow should distinguish valid submissions from incomplete ones, maintain accurate records, and direct exceptional cases to human review instead of treating every submission as valid.

---

## 💡 Solution

This project uses Zapier to automate the workshop registration process, JavaScript to validate required fields, and AI to summarize participants' learning goals.

What does the system do?

1. Receives a participant submission through Google Forms and immediately creates an initial record in Google Sheets.
2. Uses AI by Zapier to summarize the participant's learning goals, followed by JavaScript validation of required registration fields.
3. Routes the submission into either the `Valid Registration` or `Human Review Required` path.
4. Updates the existing spreadsheet record and sends the appropriate email through Gmail.

The workflow preserves the original submission before processing and records the resulting validation and routing information afterward.

---

## 👤 Users

**Primary Users:**

- Workshop organizers responsible for managing registrations.
- Participants registering for workshops and sharing their learning goals.

**User Need:**

Organizers need to identify incomplete registrations, maintain reliable records, and follow up on exceptional cases. Participants need a simple registration process and clear communication about whether their submission has been received.

---

## 🧠 How I Designed the Solution

I designed the workflow around data integrity, privacy, and controlled automation.

The initial registration is stored before processing so that the submitted information is recorded even before the workflow determines its validation status.

I separated the responsibilities of AI and JavaScript:

- **AI processing:** Summarizes learning goals to make participant expectations easier to review.
- **JavaScript validation:** Checks required fields, identifies missing information, and determines the validation status.
- **Path-based routing:** Sends valid submissions and incomplete submissions through different workflow branches.
- **Human oversight:** Ensures incomplete registrations are flagged for organizer review rather than treated as valid.

To minimize unnecessary exposure of participant information, the AI step is intended to receive only the learning-goals text required for summarization, rather than the complete registration record.

---

## ⚙️ How It Works

```text
Google Forms Submission
          ↓
Google Sheets: Create Initial Row
          ↓
AI by Zapier: Summarize Learning Goals
          ↓
Code by Zapier: JavaScript Validation
          ↓
Paths: Evaluate Validation Results
          ↙                    ↘
 Valid Registration      Human Review Required
          ↓                    ↓
 Update Existing Row     Update Existing Row
          ↓                    ↓
 Send Participant Email  Notify Workshop Organizer
```

### Workflow Steps

| Step | Tool | Responsibility |
|---|---|---|
| 1 | Google Sheets | Creates an initial record for the new submission. |
| 2 | AI by Zapier | Summarizes the participant's learning goals. |
| 3 | Code by Zapier | Validates required fields and prepares routing information. |
| 4 | Paths | Selects the appropriate branch based on the validation results. |
| 5 | Google Sheets | Updates the existing record in the selected branch. |
| 6 | Gmail | Sends a participant acknowledgment or an organizer review notification. |

The spreadsheet update steps modify the previously created record rather than intentionally creating a second record for the processed submission.

---

## 🤖 Role of AI

AI has one specific responsibility in this workflow: summarizing participant learning goals.

- Converts free-text learning goals into a concise summary.
- Makes participants' learning expectations easier for organizers to review.
- Provides a summary that can be stored alongside the registration record.

### What AI Should NOT Do

- Determine whether required registration fields are complete.
- Decide whether a submission should enter the valid or human-review path.
- Approve or reject registrations or guarantee a participant's place.

These responsibilities remain with deterministic JavaScript validation and the workflow's configured routing conditions.

### Privacy Considerations

The AI step should receive only the learning-goals field needed for summarization. Participant names, email addresses, and other unnecessary registration fields should not be mapped into the AI request.

This minimizes the information exposed to the AI step while keeping validation logic separate from AI processing.

---

## 🔄 Automation

The workflow automates the following tasks:

- Capturing new form submissions and storing them in Google Sheets before processing.
- Summarizing learning goals using AI.
- Checking required fields and identifying missing information using JavaScript.
- Routing submissions based on validation results.
- Updating the original spreadsheet record with processing outcomes.
- Sending a registration acknowledgment to the participant or a review notification to the organizer.

---

## 🗂️ Data

### Input

The Google Forms submission contains the following registration information:

- `participant_name`: Participant's name.
- `email`: Participant's email address.
- `workshop_name`: Selected workshop.
- `learning_goals`: Participant's learning goals.

The workflow also uses the submission timestamp and a registration identifier where available.

### Output

The Google Sheets record contains the original registration data and processing fields, including:

- `registration_id`
- `learning_goals_summary`
- `missing_information`
- `validation_status`
- `requires_human`
- `routing`
- `review_reason`

These fields allow the organizer to distinguish valid registrations from submissions requiring review.

Example validation outcomes:

| Field | Valid Submission | Incomplete Submission |
|---|---|---|
| `validation_status` | `VALID` | `NEEDS_REVIEW` |
| `requires_human` | `False` | `True` |
| `routing` | `normal` | `human_review` |
| `missing_information` | `NONE` | `email, workshop_name` |

The workflow also generates an email acknowledgment for valid submissions and a review notification for incomplete submissions.

---

## 🛠️ Tools & Technologies

| Tool | Purpose |
|---|---|
| Google Forms | Collect workshop registration submissions. |
| Google Sheets | Store initial submissions and updated processing results. |
| Zapier | Orchestrate the workflow and connect the individual steps. |
| AI by Zapier | Summarize participant learning goals. |
| Code by Zapier | Execute JavaScript validation and prepare routing data. |
| Paths by Zapier | Separate valid submissions from those requiring review. |
| Gmail | Send participant acknowledgments and organizer notifications. |

---

## 🔑 Key Design Decisions

### Decision 1: Store Before Processing

**Decision:**

Create an initial Google Sheets record immediately after receiving a form submission, then update that same record after processing.

**Why:**

This preserves the original submission before validation and AI processing are completed. Updating the existing record also keeps the registration and its processing results together.

### Decision 2: Use JavaScript for Validation

**Decision:**

Use deterministic JavaScript logic to validate required fields instead of asking AI to determine whether the registration is complete.

**Why:**

Required-field validation follows explicit rules and should produce predictable results. It also avoids sending participant names, email addresses, and other unnecessary registration details to AI.

### Decision 3: Limit the AI Input

**Decision:**

Use AI only to summarize the `learning_goals` field.

**Why:**

The summarization task does not require the participant's full registration record. Limiting the input supports data minimization and keeps AI processing separate from validation.

### Decision 4: Route Incomplete Submissions for Human Review

**Decision:**

Use separate Zapier Paths for valid registrations and submissions requiring review.

**Why:**

Incomplete submissions need organizer attention rather than an ordinary registration acknowledgment. Explicit routing makes the workflow easier to test and maintain.

---

## 🧪 Testing

The following tests were executed using the configured Zapier workflow. The documented outcomes are based on the observed spreadsheet records, workflow run history, and email screenshots.

### Test 1: Complete Registration

**Input:**

A registration submission with a participant name, valid email address, workshop name, and learning goals.

**Expected Result:**

- An initial spreadsheet record is created.
- AI summarizes the learning goals.
- JavaScript validation identifies the required fields as complete.
- The record is updated with `validation_status = VALID`, `requires_human = False`, and `routing = normal`.
- The participant receives a registration acknowledgment email.

**Actual Result:**

The spreadsheet record was updated with a `VALID` status and normal routing. The record showed `NONE` for missing information and `False` for `requires_human`. The participant acknowledgment email was received.

**Status:** ✅ Passed

---

### Test 2: Required Fields Containing Whitespace

**Input:**

A submission in which the email and workshop name fields contained spaces instead of meaningful values. The form accepted the submission, allowing the workflow to test the validation logic.

**Expected Result:**

- An initial spreadsheet record is created.
- JavaScript identifies the whitespace-only values as missing required information.
- The record is updated with `validation_status = NEEDS_REVIEW`, `requires_human = True`, and `routing = human_review`.
- The missing fields and review reason are recorded.
- The organizer receives a human-review notification instead of the normal participant acknowledgment.

**Actual Result:**

The spreadsheet showed `NEEDS_REVIEW`, `True`, and `human_review`. The `missing_information` field identified `email, workshop_name`, and the review reason indicated missing required information. The organizer review notification was received.

**Status:** ✅ Passed

---

## 📸 Evidence

The screenshots below document the configured workflow and the two tested scenarios.

### Final Result

![Final Result](./screenshots/final-result.png)

*Replace this placeholder with a screenshot of the completed workflow or the resulting registration records.*

### Workflow

![Workflow](./screenshots/workflow.png)

*Replace this placeholder with a screenshot of the full Zapier workflow, including both routing paths.*

### Test Evidence

Recommended additional screenshots:

- `./screenshots/test-1-valid-registration.png` — Valid spreadsheet record and participant acknowledgment email.
- `./screenshots/test-2-human-review.png` — Incomplete spreadsheet record and organizer notification.
- `./screenshots/zap-run-history.png` — Successful Zapier execution details.

---

## ⚠️ Challenges & Failures

### What Didn't Work as Expected?

- Google Forms accepted whitespace-only values in required text fields, even though those values did not contain meaningful information.
- The workflow needed to distinguish between a submitted field and a field containing a valid, non-whitespace value.

### How Did I Solve It?

- Added JavaScript validation to identify missing or whitespace-only required values.
- Used explicit validation fields to control the workflow's routing decisions.
- Configured a separate human-review path to update the record and notify the organizer when required information was missing.

---

## 📚 What I Learned

### Technical Lesson

A multi-step automation workflow can preserve an initial record and enrich it later with validation results, summaries, and routing information. Updating the existing record helps maintain a consistent view of each submission.

### Problem-Solving Lesson

Checking whether a field exists is not enough. Input validation must also consider whether the value contains meaningful information. Testing whitespace-only values helped verify this edge case.

### AI Lesson

AI does not need to control every part of an AI-powered workflow. Assigning it a narrow summarization task while using deterministic code for validation makes the system more predictable and supports data minimization.

---

## 🔮 Future Improvements

If I continued developing this project, I would:

- Add stronger error handling and notifications for failed workflow steps.
- Introduce more validation tests for missing fields, whitespace-only values, and unexpected input formats.
- Add safeguards against duplicate records when submissions are retried or workflow steps fail.
- Improve monitoring and recordkeeping to make troubleshooting easier.

---

## 🔗 Project Links

**Live Demo:** Not available yet; the workflow currently uses Google Forms as its input interface: https://docs.google.com/forms/d/e/1FAIpQLSeLICnaQs28CzoHjc-0nJ5UXB94GrhuwjujPxMH6kdiTYOBXw/viewform?usp=dialog

**Workflow:** https://zapier.com/editor/383170822/published

**Repository:** Add the GitHub repository URL after publishing this project.

---

## 👩‍💻 Author

**Heba Nedal**

[LinkedIn](https://www.linkedin.com/in/heba-n-ismail-b836b2377/) · [GitHub](https://github.com/heba-nedal)
