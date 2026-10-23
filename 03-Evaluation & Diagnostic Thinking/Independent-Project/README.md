# Tiny Wins — Museum of Small Wins

> An AI-powered personal growth application that helps users record achievements, reflect on their progress, and build a visual story of personal growth.

---

## 🎯 Problem

### The Context

People experience small achievements every day, but they often forget to record them or underestimate their importance. Over time, it can become difficult to recognize personal progress and reflect on positive changes.

### The Problem

Users need a simple, personal space to document their achievements and revisit them over time. Traditional notes and journals can preserve individual moments, but they may not provide an engaging way to visualize growth or support reflection.

### Why It Matters

Recognizing small achievements can help users appreciate their progress, maintain motivation, and develop a clearer picture of their personal growth.

---

## 💡 Solution

Tiny Wins is a web application that helps users record and manage personal achievements and explore their growth through visual and AI-powered features.

What does the system do?

1. Allows users to create an account and access their personal space.
2. Enables users to record and manage their achievements.
3. Visualizes personal growth through features such as Win Garden and My Growth Story.
4. Provides AI-powered reflections and assistance to help users explore their achievements and progress.

---

## 👤 Users

**Primary Users:**  
Individuals who want to document personal achievements and reflect on their growth over time.

**User Need:**  
A personal, accessible, and engaging application for recording achievements, reviewing progress, and gaining useful reflections from their experiences.

---

## 🧠 How I Designed the Solution

Tiny Wins was designed around the idea that small achievements deserve to be recognized and preserved.

The application combines structured achievement records with a visual interface and AI-powered functionality. Authentication separates each user's personal space, while database policies help enforce ownership of stored records.

The design distinguishes between recording achievements and reflecting on them. The database stores the user's information, the interface presents it visually, and AI features provide additional assistance without replacing the user's own experiences or judgment.

---

## ⚙️ How It Works

```text
User Input
    ↓
Authentication and Input Validation
    ↓
Create and Store Achievements
    ↓
Retrieve Personal Records
    ↓
Visualize Growth and Progress
    ↓
AI-Powered Reflection
    ↓
Personal Growth Experience
```

---

## 🤖 Role of AI

What does AI do in this solution?

- Supports users in reflecting on their achievements and personal progress.
- Provides AI-powered assistance as part of the personal growth experience.
- Adds an interactive layer beyond basic data entry and retrieval.

### What AI Should NOT Do

- Invent achievements or personal experiences that the user has not provided.
- Replace the user's judgment or present generated reflections as objective facts about their life.

---

## 🔄 Automation

What parts of the process are automated?

- Authentication and access to the user's personal workspace are handled by the application and its authentication service.
- Achievement records are stored and retrieved through the connected database.
- Growth visualizations use stored achievement data to present personal progress.
- AI-powered features generate assistance based on the information and context provided to them.

---

## 🗂️ Data

### Input

- User authentication information.
- Achievement title, description, category, and date.
- Future-letter information, including its title, message, and scheduled delivery details where applicable.
- Context supplied to AI-powered features.

### Output

- Saved and displayed achievement records.
- Visual representations of personal growth through Win Garden and My Growth Story.
- AI-generated reflections and assistance.
- Future letters and their associated status, where applicable.

---

## 🛠️ Tools & Technologies

| Tool | Purpose |
|---|---|
| Lovable | AI-assisted application development |
| React | Building the user interface |
| Supabase | Database, authentication, and Row Level Security |
| PostgreSQL | Relational data storage through Supabase |
| Lovable AI | Supporting AI-powered application features |
| Recus | Automated browser testing and issue discovery |
| PageSpeed Insights | Performance, accessibility, best-practices, and SEO audits |
| GitHub | Source control and project documentation |

---

## 🔑 Key Design Decisions

### Decision 1 — Protect User-Owned Data

**Decision:**  
Use Supabase Authentication and user-specific Row Level Security (RLS) policies.

**Why:**  
Achievements and future letters contain personal information. Authentication identifies the user, while database policies help restrict access to records according to ownership.

### Decision 2 — Combine Visual Growth with AI Assistance

**Decision:**  
Combine achievement management with visual growth features and AI-powered assistance.

**Why:**  
The application should offer more than a basic CRUD interface. Visualizations help users review their progress, while AI adds another way to reflect on their experiences.

---

## 🧪 Testing

### Test 1 — Authentication and User Data Isolation

**Input:**  
Sign in using separate user accounts and inspect the achievements associated with each account.

**Expected Result:**  
Each user should access their own personal records without seeing another user's private data.

**Actual Result:**  
Manual testing confirmed that each account displayed its own data.

**Status:** ✅ Pass

---

### Test 2 — Data Persistence

**Input:**  
Create an achievement, refresh the page, and revisit the relevant section.

**Expected Result:**  
The saved achievement should remain available after refreshing the application.

**Actual Result:**  
Manual testing confirmed that saved records remained available after refreshing.

**Status:** ✅ Pass

---

### Test 3 — Create, Update, and Delete Operations

**Input:**  
Create an achievement, modify its information, and delete a test record.

**Expected Result:**  
The application should perform the requested operations and display the updated data.

**Actual Result:**  
The tested create, update, and delete operations behaved as expected.

**Status:** ✅ Pass

---

### Test 4 — Input Validation

**Input:**  
Submit required fields without values or with whitespace-only input.

**Expected Result:**  
Invalid submissions should be rejected, and required information should be provided before saving.

**Actual Result:**  
Manual testing confirmed that empty and whitespace-only values in the tested required fields were rejected.

**Status:** ✅ Pass

---

### Test 5 — Delete Cancellation and Database Verification

**Input:**  
Cancel a deletion, then delete a test record and inspect the database.

**Expected Result:**  
Canceling should preserve the record. Confirmed deletion should remove the intended record and associated data according to the application's implemented behavior.

**Actual Result:**  
Manual testing confirmed that canceling preserved the record. After a confirmed deletion, the relevant database records were verified in Supabase.

**Status:** ✅ Pass

---

### Test 6 — Authentication Route Protection

**Input:**  
Sign out and attempt to open a protected application route directly, including in a private browsing session.

**Expected Result:**  
Unauthenticated users should be redirected to authentication rather than being shown private application data.

**Actual Result:**  
The tested routes displayed the sign-in experience without exposing private application data.

**Status:** ✅ Pass

---

### Test 7 — Progress Tracking and AI Features

**Input:**  
Inspect the progress visualization and preview the AI-powered features.

**Expected Result:**  
Progress should reflect stored achievement data, and AI-powered features should render and provide their intended experience.

**Actual Result:**  
Manual testing confirmed that the tested progress behavior updated as expected and persisted after refreshing. The AI-powered features were also previewed successfully.

**Status:** ✅ Pass

---

### Test 8 — Row Level Security Configuration Review

**Input:**  
Inspect the Supabase schema and Row Level Security policies for the `achievements` and `future_letters` tables.

**Expected Result:**  
Appropriate policies should be configured to restrict access to user-owned records.

**Actual Result:**  
RLS was enabled on both tables. The `achievements` table displayed read, insert, update, and delete policies. The `future_letters` table displayed read, insert, and conditional delete policies. The policy definitions were not fully validated through adversarial database-access tests, and no update policy was visible in the provided `future_letters` screenshot.

**Status:** ⚠️ Configuration reviewed; further verification recommended

---

### Test 9 — Automated Browser Testing with Recus

**Input:**  
Run automated browser checks against the deployed Tiny Wins application.

**Expected Result:**  
The tool should exercise relevant interface and authentication scenarios and report observed outcomes, failures, and warnings.

**Actual Result:**  
The shared report recorded 55 checked browser checks and nine issues for review. The landing-page presentation and gallery-navigation checks passed. Other findings involved unverified login credentials, password-handling scenarios, a timed-out sign-in test, repeated sign-in submissions, network-interruption handling, and a return-to-sign-in interaction.

These findings were documented for review. They have not all been confirmed as application defects.

**Status:** ⚠️ Review required

**Report:** [View the Recus test run](https://www.recus.app/shared/runs/qxoJfPvX96EbVBBxFF8-wrazs-hd6TbP2Jc9NHyA8XY)

---

### Test 10 — Performance and Quality Audit

**Input:**  
Run PageSpeed Insights against the deployed Tiny Wins application on mobile and desktop.

**Expected Result:**  
Evaluate performance, accessibility, best practices, and SEO.

**Actual Result:**

| Metric | Mobile | Desktop |
|---|---:|---:|
| Performance | 92 | 99 |
| Accessibility | 96 | 96 |
| Best Practices | 100 | 100 |
| SEO | 100 | 100 |

The reports also showed Agentic Browsing results of 2/2. Real-user field data was unavailable, so the scores represent the reported audit results rather than real-user performance measurements.

**Status:** ✅ Audit completed; further accessibility and performance improvements remain possible.

**Report:** [View PageSpeed Insights — Mobile](https://pagespeed.web.dev/analysis/https-tiny-win-by-heba-lovable-app/b0pyt1elvn?form_factor=mobile)

---

## 📸 Evidence

### Final Result — Landing Page

![Tiny Wins landing page](./Screenshots/03-landing-page.png)

### Authentication

![Tiny Wins sign up page](./Screenshots/04-sign-up-page.png)

![Tiny Wins sign in page](./Screenshots/05-sign-in-page.png)

### Dashboard and Progress

![Tiny Wins dashboard progress overview](./Screenshots/06-dashboard-progress-overview.png)

![Tiny Wins recent achievements](./Screenshots/11-dashboard-recent-wins.png)

### Achievement Management

![Add a new achievement](./Screenshots/07-add-win-form.png)

![Achievements gallery](./Screenshots/12-wins-gallery.png)

![Achievement details and AI action](./Screenshots/13-win-details-and-ai-action.png)

![AI achievement reflection](./Screenshots/14-ai-win-reflection.png)

### Personal Growth Features

![My Growth Story timeline](./Screenshots/08-growth-story-timeline.png)

![AI monthly reflection](./Screenshots/09-ai-monthly-reflection.png)

![Win Garden](./Screenshots/10-win-garden.png)

### Future Letters

![Future letters page](./Screenshots/15-letters-page.png)

![Write a letter to your future self](./Screenshots/16-write-future-self-letter.png)

![Future letter confirmation](./Screenshots/17-letter-sealed-confirmation.png)

### Supabase Project and Database

![Supabase project overview](./Screenshots/supabase-project-overview.png)

![Supabase database schema](./Screenshots/supabase-database-schema.png)

![Supabase database tables](./Screenshots/supabase-database-tables.png)

### Database Access Policies

![Achievements RLS policies](./Screenshots/supabase-achievements-rls-policies.png)

![Future letters RLS policies](./Screenshots/supabase-future-letters-rls-policies.png)

### Automated Testing

![Recus automated testing results](./Screenshots/recus-automated-testing-results.png)

### Performance Audit

![Mobile PageSpeed results](./Screenshots/01-pagespeed-mobile.png)

![Desktop PageSpeed results](./Screenshots/02-pagespeed-desktop.png)

---

## ⚠️ Challenges & Failures

### What Didn't Work as Expected?

- Recus reported nine issues, but some authentication tests relied on credentials that were not verified as valid registered accounts.
- The sign-in test using purported valid credentials timed out before producing a conclusive result.
- Password-handling and repeated-submission behaviors require further investigation before they can be classified as confirmed defects.
- The network-interruption test did not conclusively demonstrate the application's behavior under a simulated connection failure.
- The available RLS screenshots showed policy configuration, but did not prove resistance to every unauthorized-access scenario.
- PageSpeed Insights showed room for accessibility and performance improvements, particularly in the mobile experience.

### How Did I Respond?

- Completed manual testing of core application behavior, including authentication, user data isolation, persistence, CRUD operations, validation, and route protection.
- Verified the observed database changes in Supabase where applicable.
- Previewed the AI-powered features successfully.
- Reviewed Recus and PageSpeed Insights results as additional evidence.
- Documented unresolved issues as future improvements instead of making unverified changes to the application.

---

## 📚 What I Learned

### Technical Lesson

Reliable applications require more than a functional interface. Authentication, persistent data, validation, relationships, and database access policies must work together to protect data and support the intended workflow.

### Problem-Solving Lesson

A failed automated test is a signal to investigate, not automatically proof of a bug. Invalid test data, interrupted execution, or an incomplete interaction can produce inconclusive results. Findings should be evaluated against actual application behavior before changes are made.

### AI Lesson

AI-powered features can add value by supporting reflection and making the user experience more interactive. However, AI-generated output and AI-assisted test reports still require human review and evidence-based evaluation.

---

## 🔮 Future Improvements

If I continued developing this project, I would:

- Investigate the nine Recus findings, beginning with repeated sign-in submissions and inconclusive authentication scenarios.
- Add repeatable automated tests using dedicated test accounts with verified credentials.
- Improve and re-test network-error handling and recovery behavior.
- Verify password handling, including long passwords and significant whitespace, using controlled test cases.
- Review the intended behavior and full definitions of all RLS policies, including whether `future_letters` requires an update policy.
- Review accessibility findings and prioritize improvements based on their measured impact.
- Investigate mobile performance opportunities identified by PageSpeed Insights.
- Continue evaluating AI-generated reflections for relevance, reliability, and alignment with the information provided by users.

---

## 🔗 Project Links

**Live Demo:** [Tiny Wins](https://tiny-win-by-heba.lovable.app)

**Workflow / Automated Testing:** [Recus Shared Run](https://www.recus.app/shared/runs/qxoJfPvX96EbVBBxFF8-wrazs-hd6TbP2Jc9NHyA8XY)

**PageSpeed Insights:** [Mobile Audit](https://www.recus.app/shared/runs/qxoJfPvX96EbVBBxFF8-wrazs-hd6TbP2Jc9NHyA8XY)

**Repository:** [Github Repository](https://github.com/heba-nedal/tiny-wins.git)

---

## 👩‍💻 Author

**Heba Nedal**

[LinkedIn](https://www.linkedin.com/in/heba-n-ismail-b836b2377/) · [GitHub](https://github.com/heba-nedal)
