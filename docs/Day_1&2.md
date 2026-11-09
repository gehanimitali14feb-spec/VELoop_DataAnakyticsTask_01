# Days 1–2: Source & Verification Register
**Work Package Reference:** Section 6 & Work Package S  
**Internship Role:** Data Analyst Intern  
**Project:** VELOOP Rewards (Task 01)  
**Mandatory Authenticity Policy:** VELOOP is an active product under development. All numbers, user metrics, and activity records presented in this analysis originate from simulated/fictional datasets and must never be represented as actual VELOOP company production performance.

---

## 1. Product Source & Evidence Discipline
Every data assumption is logged and categorized under one of three verified states:
* **Confirmed:** Verified directly in the official project documentation or confirmed in simulated baseline files.
* **Proposed:** Recommended analytical structure, event schema, or taxonomy designed by the analyst for engineering evaluation.
* **To Be Verified:** Existing implementation state that requires direct verification with the engineering team.

---

## 2. Source & Verification Register Table

| Item ID | Product Area | Information / Specification | Source Type | Status | Analytical Notes & Risk Assessment |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **S-001** | User Accounts | Unique identifier `user_id` persists across all user sessions | Internal / Simulated | Confirmed | Essential for user stitching and longitudinal cohort retention tracking. |
| **S-002** | User Accounts | Session tracking via unique `session_id` | Simulated Data (`02_Sessions`) | Confirmed | 7,913 session records present; mobile background session timeout logic requires engineering validation. |
| **S-003** | Earning | Task lifecycle follows `Viewed` -> `Started` -> `Completed` | Product Specs / Simulated | Confirmed | Validated against 9,846 records in `05_Task_Activity`. |
| **S-004** | Earning | Third-party survey completion callbacks | External Postbacks | To Be Verified | Callback dropouts and latency require server-side postback validation. |
| **S-005** | Wallet | Currency segregation (VES, XP, Gems, Tokens, Spins) | Product Specification | Confirmed | XP (progression points) must remain segregated from liquid withdrawable balances. |
| **S-006** | Wallet | Idempotency keys assigned to transaction records | Proposed Specification | Confirmed | Critical to prevent double-crediting during network retries or duplicate webhook pings. |
| **S-007** | Withdrawals | Payout state machine (`Requested` -> `Under Review` -> `Completed` / `Rejected`) | Product Specification | Confirmed | Compliance and anti-fraud hold stage must be captured before gateway dispatch. |
| **S-008** | Referrals | Attribution cookie / code persistence window | Internal Architecture | Proposed | Attribution persistence window (e.g., 30-day cookie vs. immediate app install) requires engineering review. |
| **S-009** | Platform Telemetry | Native mobile instrumentation (Android / iOS SDKs) | Simulated Dataset Audit | To Be Verified | Current simulated user records reflect Web platform telemetry; mobile client event SDK status must be verified. |
| **S-010** | Rewards | Ledger adjustments and chargeback reversal events | Proposed Specification | Confirmed | Financial ledger must maintain double-entry immutability for audited balances. |