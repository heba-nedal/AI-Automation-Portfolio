# Tiny Wins — Workflow 2 Test Report

> Telegram achievement capture, AI categorization, Supabase persistence, and reply workflow.

## 1. Overview

- **Workflow:** Workflow 2 — Record Wins through Telegram
- **Platform:** n8n Cloud
- **Integrations:** Telegram Bot, Google Gemini API, Supabase
- **AI model used:** `gemini-3.5-flash-lite`
- **Test evidence:** Screenshots are grouped by test case in this archive.

## 2. Test Summary

| Test Case | Scenario | Status |
|---|---|---|
| TC-01 | Short Achievement — AI Classification and Save | **PASS** |
| TC-02 | Long Achievement — AI Title and Original Description | **PASS** |
| TC-03 | Gemini Failure — Fallback Save | **PASS** |
| TC-04 | Duplicate Prevention | **PASS** |
| TC-05 | Message Length Limit — More Than 1000 Characters | **PASS** |
| TC-06 | Unsupported Input — Photo | **PASS** |
| TC-07 | Unsupported Input — Voice Message | **PASS** |
| TC-08 | Unsupported Input — Sticker | **PASS** |
| TC-09 | Account Language — Arabic | **PASS** |

**Executed test result: 9/9 PASS.**

This result covers only the test cases listed in this report. It does not mean every planned test in the original workflow specification has been executed.

## 3. Detailed Test Cases

### TC-01 — Short Achievement — AI Classification and Save

**Input**  
أنهيت أول مقابلة عمل اليوم

**Expected Result**  
The short message is saved with its original text as the title, a valid AI category, null description, Telegram source, and is_publishable=false. A confirmation is sent in the linked account's language.

**Actual Result**  
The message was classified as work_projects, saved successfully in Supabase, and the confirmation was generated and sent in English while the linked account language was en.

**Status:** PASS

**Evidence:**
- Result confirmed during execution; no screenshot was included in this evidence archive.

### TC-02 — Long Achievement — AI Title and Original Description

**Input**  
A long Arabic achievement describing completion of a programming course chapter, learning database concepts, and applying them in a small project.

**Expected Result**  
A concise title of at most 8 words is generated; the full original message is stored unchanged in description; category is correctly classified.

**Actual Result**  
The title was shortened to «أنهيت دراسة فصل كامل من دورة البرمجة», category was learning, and the full original Arabic message was preserved in description.

**Status:** PASS

**Evidence:**
- `TC-02/01-title-category-date.png`
- `TC-02/02-original-description.png`

### TC-03 — Gemini Failure — Fallback Save

**Input**  
A test achievement was sent while the model name was temporarily changed to invalid-model-for-testing.

**Expected Result**  
Gemini failure does not stop the workflow. Decide applies the fallback category everyday and derives a title from the original text; the achievement is saved and a confirmation is sent.

**Actual Result**  
Gemini returned 404 for the intentionally invalid model. The workflow continued, saved the achievement with category Everyday Wins, and sent the confirmation.

**Status:** PASS

**Evidence:**
- `TC-03/01-gemini-failure-output.png`

### TC-04 — Duplicate Prevention

**Input**  
The same n8n execution/message was retried using the original Telegram message ID.

**Expected Result**  
No second achievement row is inserted and no second confirmation is sent.

**Actual Result**  
No new Supabase row was created; only one achievement remained, and no second confirmation was sent.

**Status:** PASS

**Evidence:**
- `TC-04/01-duplicate-workflow-execution.png`

### TC-05 — Message Length Limit — More Than 1000 Characters

**Input**  
A repeated Arabic text message exceeding 1000 characters.

**Expected Result**  
The message is rejected with the bilingual length-limit response. Gemini and Save win are not executed, and no row is inserted.

**Actual Result**  
The bot returned the Arabic and English length-limit response. The execution followed Switch → Static Reply → Send; no achievement row was added.

**Status:** PASS

**Evidence:**
- `TC-05/01-telegram-length-limit-response.png`
- `TC-05/02-workflow-fallback-path.png`

### TC-06 — Unsupported Input — Photo

**Input**  
A photo sent without a text caption.

**Expected Result**  
The bot responds with bilingual guidance to send a plain-text achievement; no AI processing or achievement save occurs.

**Actual Result**  
The bot sent the bilingual plain-text guidance. No achievement row was created.

**Status:** PASS

**Evidence:**
- `TC-06/01-photo-guidance-response.png`

### TC-07 — Unsupported Input — Voice Message

**Input**  
A short Telegram voice message.

**Expected Result**  
The bot responds with bilingual plain-text guidance; no achievement is saved.

**Actual Result**  
The bot sent the expected bilingual guidance. The execution followed the Static Reply path.

**Status:** PASS

**Evidence:**
- `TC-07/01-voice-guidance-response.png`
- `TC-07/02-static-reply-path.png`

### TC-08 — Unsupported Input — Sticker

**Input**  
A Telegram sticker.

**Expected Result**  
The bot responds with bilingual plain-text guidance; no achievement is saved.

**Actual Result**  
The bot sent the expected bilingual guidance. The execution followed the Static Reply path.

**Status:** PASS

**Evidence:**
- `TC-08/01-sticker-guidance-response.png`
- `TC-08/02-static-reply-path.png`

### TC-09 — Account Language — Arabic

**Input**  
The linked account language was changed to ar; then a new Arabic achievement was sent.

**Expected Result**  
The achievement is saved and the confirmation message is sent in Arabic based on telegram_links.language.

**Actual Result**  
The achievement was saved and the confirmation was delivered in Arabic, including the Arabic category label «التعلّم».

**Status:** PASS

**Evidence:**
- `TC-09/01-arabic-confirmation.png`

## 4. Implementation Behaviors Verified

- Short messages (up to 80 characters, without a newline) use the original message as the title and store `description = null`.
- Long messages use an AI-generated concise title and preserve the full original text in `description`.
- Allowed categories are `learning`, `personal_growth`, `work_projects`, `health_habits`, and `everyday`.
- Telegram-created records use `source = 'telegram'` and `is_publishable = false`.
- `source_ref` identifies the Telegram message to prevent duplicate records.
- Gemini failure falls back to `everyday` and a title derived from the original text, while allowing saving to continue.
- Messages over 1000 characters and unsupported non-text messages are handled through static replies.
- The final confirmation language follows the linked account's `telegram_links.language` value.
- A shared Telegram `Send` node is used by the reply-producing branches.

## 5. Planned Tests Not Yet Executed

The following items were included in the broader Workflow 2 plan but were not confirmed as completed in this test session:

- Unlinked Telegram chat receives the `not_linked` response and creates no record.
- Prompt-injection message is treated as untrusted achievement text and cannot override the classification instructions.
- Prompt comparison experiment: simple prompt vs. detailed prompt using the specified 10 sample messages.
- Any additional language or edge-case tests not listed above.

## 6. Operational Notes

- Restore the production model name to `gemini-3.5-flash-lite` after the intentional failure test.
- The intentional invalid-model test used `invalid-model-for-testing` only to verify fallback behavior.
- Do not include Gemini or Supabase secret keys in screenshots, documentation, or source control.
- The Gemini free-tier privacy limitations discussed during setup should be considered before using real personal achievement text in production.

## 7. Conclusion

The executed Workflow 2 tests passed. The evidence demonstrates successful achievement saving, long-message handling, Gemini failure fallback, duplicate prevention, length validation, unsupported-input handling, and account-language-based replies. The unexecuted cases listed above remain open and should be completed before declaring the full planned test suite complete.

