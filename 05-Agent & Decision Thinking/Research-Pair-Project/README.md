# Future Me — A Personal Growth Journey

> An interactive personal growth application that transforms life goals into a realistic, structured journey with actionable tasks, progress tracking, and future-self reflections.

---

## 🎯 Problem

### The Context

People often have personal ambitions and a vision of the person they want to become. However, turning that vision into consistent daily action can be difficult, especially when time, energy, priorities, and circumstances change.

### The Problem

Long-term goals can feel overwhelming when they are not divided into manageable steps. Traditional to-do lists may help organize tasks, but they do not always connect daily actions to a broader personal growth journey.

### Why It Matters

A realistic and flexible plan can help people make steady progress without feeling that they must accomplish everything at once. Connecting goals to small, actionable steps makes personal growth easier to organize, review, and sustain.

---

## 💡 Solution

Future Me is an interactive application that helps users define who they want to become and build a structured journey toward that vision.

What does the system do?

1. Guides users through defining their future identity, personal qualities, and goals across different areas of life.
2. Collects information about available time, preferred pace, weekly schedule, and constraints.
3. Organizes goals into chapters and actionable tasks using a deterministic, rules-based planning approach.
4. Tracks completed tasks, unlocks subsequent stages when requirements are met, and allows users to review their progress and write letters to their future selves.

---

## 👤 Users

**Primary Users:**  
Individuals who want to organize their personal development goals and make gradual, measurable progress.

**User Need:**  
Users need a practical way to turn personal ambitions into manageable tasks, track their progress, adjust their plans as life changes, and reflect on their growth over time.

---

## 🧠 How I Designed the Solution

The application was designed around the idea that personal growth should be structured but flexible.

Instead of presenting users with a large, overwhelming list of goals, Future Me guides them through a step-by-step onboarding process:

- **Identity first:** Understand the person the user wants to become.
- **Goals second:** Capture desired outcomes and organize them by life area.
- **Realistic planning:** Consider available time, preferred pace, weekly availability, and constraints.
- **Progressive execution:** Divide the journey into chapters and smaller tasks.
- **Continuous reflection:** Let users review progress and adjust their plans without losing their completed work.

The initial planning process uses explicit rules rather than relying on AI to make planning decisions. This keeps the planning behavior structured and predictable.

---

## ⚙️ How It Works

```text
User Input
   ↓
Define Identity, Goals, and Priorities
   ↓
Collect Available Time, Schedule, and Constraints
   ↓
Rules-Based Planning Logic
   ↓
Organize Goals into Chapters and Tasks
   ↓
Save the Journey
   ↓
Complete Tasks and Track Progress
   ↓
Unlock Eligible Chapters and Review the Plan
```

---

## 🤖 Role of AI

The application was built using Replit's AI-assisted development capabilities. AI supported the process of turning natural-language instructions into an application that could be refined and previewed.

AI's role in the development process included:

- Supporting application creation from natural-language descriptions.
- Helping refine the interface and application behavior during development.
- Supporting iterative building and testing through the Replit environment.

### What AI Should NOT Do

- Replace explicit planning rules with unpredictable decisions when the application is expected to follow deterministic logic.
- Make assumptions about a user's available time, priorities, or constraints without using the information provided by the user.

**Important distinction:** The initial journey planner is described in the application as rules-based, not AI-generated. Replit's AI-assisted building process is separate from the runtime planning logic.

---

## 🔄 Automation

The application automates several steps in the personal planning process:

- Organizing user-provided goals into a structured journey.
- Generating chapters and actionable tasks through predefined planning rules.
- Tracking progress based on completed required tasks.
- Unlocking subsequent chapters when the required conditions are satisfied.
- Saving journey information so users can return to their plans.
- Supporting plan adjustments while preserving completed work.

---

## 🗂️ Data

### Input

The application collects information such as:

- User profile and future-self description.
- Personal qualities and desired outcomes.
- Goals, descriptions, life areas, priorities, and target dates.
- Current experience and desired progress.
- Available time, weekly availability, and preferred pace.
- Routine details, constraints, and upcoming deadlines.
- Task completion and reflection entries.
- Future-self letter content and optional reading dates.

### Output

The application produces and maintains:

- A structured personal growth journey.
- Chapters and actionable tasks.
- Daily task lists and progress indicators.
- Journey reviews and adjustable planning settings.
- Records of completed tasks and achievements.
- Letters written to the user's future self.

---

## 🛠️ Tools & Technologies

| Tool | Purpose |
|---|---|
| Replit | AI-assisted development, browser-based coding environment, application preview, and deployment |
| Supabase | Database and backend services for storing application data |
| Replit AI Agent | Assistance with building and refining the application from natural-language instructions |

---

## 🔑 Key Design Decisions

### Decision 1 — Rules-Based Initial Planning

**Decision:**  
Use a deterministic, rules-based approach to generate the initial journey plan.

**Why:**  
Personal planning should be predictable and explainable. A rules-based approach helps the application organize goals into stages without presenting the plan as an AI-generated recommendation.

### Decision 2 — Progressive Chapters and Tasks

**Decision:**  
Divide the journey into chapters with smaller required tasks, and make chapter progression depend on completion requirements.

**Why:**  
Smaller steps make long-term goals easier to approach and give users a visible sense of progress.

### Decision 3 — Flexible Planning and Reflection

**Decision:**  
Allow users to review their progress and adjust planning parameters as their circumstances change.

**Why:**  
A useful personal growth plan should adapt to real life. Users should be able to change their pace without treating previous effort as lost.

### Decision 4 — Persistent User Data

**Decision:**  
Use Supabase-backed data storage for the application's core records.

**Why:**  
The journey, tasks, progress, and personal reflections need to remain available when users return to the application.

---

## 🧪 Testing

The team manually tested the application's main workflows and confirmed that the tested features worked as expected.

### Test 1 — Journey Creation

**Input:**  
Enter the user's identity information, define one or more goals, set a preferred pace and available time, and complete the journey setup flow.

**Expected Result:**  
The application should create a structured journey based on the supplied information and display the resulting plan.

**Actual Result:**  
The team tested the journey creation workflow and confirmed that it worked as expected.

**Status:** ✅ Passed

---

## 🧪 Test 2 — Task Completion and Chapter Progression

**Input:**  
Complete the required tasks in a journey chapter.

**Expected Result:**  
The application should update task completion and progress, and unlock the next chapter when its requirements are satisfied.

**Actual Result:**  
The team tested task completion and chapter progression and confirmed that the workflow worked as expected.

**Status:** ✅ Passed

---

## 🧪 Test 3 — Plan Review and Adjustment

**Input:**  
Open the reflection area, change planning parameters, and adjust the journey.

**Expected Result:**  
The application should apply the permitted adjustments while preserving completed work.

**Actual Result:**  
The team tested the review and adjustment workflow and confirmed that it worked as expected.

**Status:** ✅ Passed

---

## 🧪 Test 4 — Data Persistence

**Input:**  
Create journey data and related records, then return to the relevant application pages.

**Expected Result:**  
Saved information should remain available instead of disappearing when the user navigates away or returns later.

**Actual Result:**  
The team tested the relevant data-saving workflows and confirmed that they worked as expected.

**Status:** ✅ Passed

---

## 🧪 Test 5 — Future-Self Letters

**Input:**  
Open the letters section, enter a letter title and message, optionally select a reading date, and save the letter.

**Expected Result:**  
The application should save the letter and make it available through the letters section.

**Actual Result:**  
The team tested the letter-writing workflow and confirmed that it worked as expected.

**Status:** ✅ Passed

---

## 📸 Evidence

The following screenshots should be placed in the project's `screenshots/` directory. The filenames below are suggested names for organizing the supplied evidence.

### Final Result

![Future Me Landing Page](./screenshots/final-result.png)

### Workflow

![Future Me Journey Setup Workflow](./screenshots/workflow.png)

### Additional Screenshots

Suggested screenshots for documenting the main application features:

- `./screenshots/sign-up.png` — Account creation interface.
- `./screenshots/dashboard.png` — Daily dashboard and task progress.
- `./screenshots/journey-setup-identity.png` — Future identity setup.
- `./screenshots/journey-setup-goals.png` — Goal definition.
- `./screenshots/journey-setup-rhythm.png` — Available time and preferred pace.
- `./screenshots/journey-preview.png` — Initial journey preview.
- `./screenshots/reflection.png` — Review and plan adjustment.
- `./screenshots/future-letters.png` — Future-self letters.
- `./screenshots/proof-of-becoming.png` — Achievement and progress record.
- `./screenshots/supabase-database-tables.png` — Database tables in Supabase.

---

## ⚠️ Challenges & Failures

### What didn't work as expected?

The team completed manual testing of the main workflows. No specific unresolved application failure has been documented in the information available for this README.

### How did I solve it?

- Used iterative development and application previews to inspect the interface and behavior.
- Tested the main workflows after building them.
- Reviewed the application's database structure in Supabase.

These points describe the development and validation approach; they do not imply that a particular undocumented bug was encountered or fixed.

---

## 📚 What I Learned

### Technical Lesson

I learned how an AI-assisted development environment can support the process of building an interactive application, connecting it to a backend database, and iteratively testing its behavior.

### Problem-Solving Lesson

I learned the importance of translating a broad idea into smaller workflows with clear inputs, expected outcomes, and observable behavior. Separating journey setup, planning, task completion, and reflection made the system easier to build and validate.

### AI Lesson

I learned that AI-assisted building works best when instructions are clear and the developer evaluates the resulting application. AI can accelerate implementation, but the developer remains responsible for checking whether the output meets the intended requirements.

I also learned to distinguish between using AI to build an application and using AI inside the application itself. In Future Me, the initial planning logic is rules-based rather than AI-generated.

---

## 🔮 Future Improvements

If I continued developing this project, I would:

- Expand automated tests for authentication, data isolation, journey creation, task completion, chapter unlocking, and plan adjustment.
- Improve error handling and feedback for database operations and unexpected failures.
- Add clearer explanations of the rules used to organize goals into chapters and tasks.
- Improve accessibility and verify responsive behavior across more screen sizes.
- Add more detailed progress analytics and a timeline of completed milestones.
- Consider optional AI-powered reflection or goal refinement while keeping users in control of their plans.

---

## 🔗 Project Links

**Live Demo:** [Future Me](https://future-me--hebanedal224.replit.app/)

**Repository:** [Add repository link when available]

---

## 👩‍💻 Authors

- **Heba Ismail**
- **Dina Al-Maghrabi**
- **Raghad Muhanna**

**Built collaboratively using Replit as part of the U3 — Prove It Works tool exploration activity.**
