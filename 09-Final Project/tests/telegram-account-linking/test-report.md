# Workflow 1 — Telegram Account Linking
## Test Report

**Project:** Tiny Wins  
**Workflow:** Telegram Account Linking  
**Platform:** n8n, Supabase, Telegram Bot API  
**Testing result:** 7/7 Passed

---

## 1. Testing Objectives

The purpose of this testing phase was to verify that the Telegram account-linking workflow:

- Successfully links a Tiny Wins account to a Telegram chat.
- Rejects invalid, expired, and previously used tokens.
- Prevents one Telegram chat from being linked to multiple accounts.
- Handles repeated linking attempts correctly.
- Provides an appropriate welcome message when users start the bot without a linking token.

## 2. Test Cases and Results

### TC-01: First-Time Telegram Linking

**Objective:** Verify that a user can successfully link their Tiny Wins account using a valid token.

- **Input:** Valid, unused, non-expired token.
- **Expected Result:** Supabase creates the Telegram link and returns `ok: true`.
- **Actual Result:** The account was successfully linked. A new record appeared in `telegram_links`, and the token's `used_at` field was populated.
- **Status:** PASS

### TC-02: Reusing the Same Token

**Objective:** Ensure that a token cannot be used more than once.

- **Input:** Previously consumed token.
- **Expected Result:** The request is rejected with `invalid_or_expired`.
- **Actual Result:** Supabase returned `ok: false` and `reason: invalid_or_expired`. Telegram displayed the corresponding rejection message.
- **Status:** PASS

### TC-03: Expired Token

**Objective:** Verify that expired tokens are rejected even if they have never been used.

- **Input:** Unused token with an expiration timestamp in the past.
- **Expected Result:** The request is rejected with `invalid_or_expired`.
- **Actual Result:** Supabase rejected the expired token, and Telegram displayed the appropriate message.
- **Status:** PASS

### TC-04: Invalid or Random Token

**Objective:** Ensure that arbitrary tokens that do not exist in the database cannot be used.

- **Input:** `RANDOMTOKEN123456789`
- **Expected Result:** The request is rejected with `invalid_or_expired`.
- **Actual Result:** The bot displayed the invalid-or-expired link message.
- **Status:** PASS

### TC-05: Welcome Message Without a Token

**Objective:** Verify that users can start the bot without initiating an account-linking operation.

- **Input:** `/start`
- **Expected Result:** The message is classified as `welcome` and routed to the Welcome branch. No Supabase linking RPC call is made.
- **Actual Result:** The `Parse Message` node returned `kind: welcome` and `token: null`. The `Route Message` node selected the Welcome branch, and Telegram displayed the welcome message.
- **Status:** PASS

### TC-06: Telegram Chat Already Linked to Another Account

**Objective:** Prevent a Telegram chat from being linked to a different Tiny Wins account.

- **Input:** A valid token belonging to Account B, sent from a Telegram chat already linked to Account A.
- **Expected Result:** The operation is rejected with `chat_already_linked`.
- **Actual Result:** Telegram displayed the message indicating that the chat is already linked to another Tiny Wins account.
- **Status:** PASS

### TC-07: Account Already Linked to the Same Telegram Chat

**Objective:** Ensure that repeating the linking operation for the same account and Telegram chat does not create a new link or modify the original linking timestamp.

- **Input:** A new valid token belonging to the same account, used from the already-linked Telegram chat.
- **Expected Result:** The operation returns `already_linked`, consumes the new token, and preserves the existing `linked_at` value.
- **Actual Result:** Telegram displayed the already-linked confirmation message. The existing `telegram_links` record retained its original `linked_at` value.
- **Status:** PASS

---

## 3. Final Test Summary

| Test Case | Description | Result |
|---|---|---|
| TC-01 | First-time linking | PASS |
| TC-02 | Token reuse | PASS |
| TC-03 | Expired token | PASS |
| TC-04 | Invalid token | PASS |
| TC-05 | Welcome without token | PASS |
| TC-06 | Chat linked to another account | PASS |
| TC-07 | Already linked to the same account | PASS |

**Total Test Cases:** 7  
**Passed:** 7  
**Failed:** 0  
**Pass Rate:** 100%

## 4. Conclusion

All seven test cases passed.

The workflow successfully handles normal account linking, token validation, duplicate requests, and account-conflict scenarios.

The tests also verified that repeated linking attempts do not unnecessarily modify an existing Telegram link.

**Overall Status: PASSED**