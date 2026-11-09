# Days 5–6: User & Account Analytics Specification
**Work Package Reference:** Work Package B (B1–B2)  
**Deliverable:** User Lifecycle Model, Identity Architecture & Cohort Metrics  
**Mandatory Authenticity Policy:** Figures provided reflect baseline profiling from the simulated user dataset (`Users_1000_Clean`).

---

## 1. Telemetry Identity Architecture (B1)
To track user behavior across devices, sessions, and financial ledgers, four distinct identifiers are defined:

* **`user_id` (Primary User Identifier):**
  * *Format:* 11-character string starting with `VLUSR` (e.g., `VLUSR000001`).
  * *Purpose:* Immutable identifier assigned at registration. Never recycled or modified.
* **`session_id` (Session Identifier):**
  * *Format:* `{user_id}_{epoch_timestamp}`.
  * *Purpose:* Bounds user activity within a discrete engagement window. Regenerated after 30 minutes of user inactivity.
* **`event_id` (Event Telemetry Identifier):**
  * *Format:* Standard UUIDv4 string.
  * *Purpose:* Identifies every atomic event packet to guarantee deduplication at ingestion.
* **`transaction_id` (Financial Ledger Identifier):**
  * *Format:* Alphanumeric UUID prefixed by transaction type (e.g., `TXN_REW_...`).
  * *Purpose:* Tracks all debits, credits, and escrow adjustments with strict auditability.

---

## 2. User Profile Field Specification (B2)

| Field Name | Data Type | Required? | Analytical Purpose | Source Layer | Validation Rule | Status |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `user_id` | String | Yes | Primary key across all analytical models | Auth DB | Match `^VLUSR[0-9]{6}$` | Confirmed |
| `registration_datetime` | Timestamp (UTC) | Yes | Cohort grouping and registration vintage | Auth DB | Valid ISO-8601 UTC timestamp | Confirmed |
| `acquisition_source` | String | Yes | Attribution channel ROI calculation | Auth / Attribution | Allowed: Organic Search, Direct, Social Media, Referral, WhatsApp, Telegram, Other | Confirmed |
| `account_status` | String | Yes | Account lifecycle tracking | User State Engine | Allowed: Active, Inactive, Suspended, Pending Verification | Confirmed |
| `onboarding_status` | String | Yes | Onboarding drop-off analysis | User State Engine | Allowed: Not Started, Started, Completed | Confirmed |
| `xp_balance` | Integer | Yes | User progression and gamification level | Gamification DB | Non-negative integer (>= 0) | Confirmed |
| `referral_code` | String | Yes | Referral generation and viral attribution | Referral Engine | Unique 8-character string | Confirmed |
| `lifetime_sessions` | Integer | Yes | Long-term engagement frequency | Session Aggregator | Non-negative integer (>= 0) | Confirmed |
| `active_days` | Integer | Yes | Frequency of active usage days | Activity Aggregator | Non-negative integer (<= days_since_registration) | Confirmed |

---

## 3. Baseline Simulated Cohort Metrics (1,000 User Profile Audit)
Based on profiling of `Users_1000_Clean` (Date range: 01 Apr 2026 to 15 Sep 2026):

* **Total Registered User Cohort:** 1,000 simulated accounts.
* **Account Status Distribution:**
  * Active: **568 users (56.8%)**
  * Inactive: **283 users (28.3%)**
  * Suspended: **77 users (7.7%)**
  * Pending Verification: **72 users (7.2%)**
* **Onboarding Funnel Performance:**
  * Completed: **722 users (72.2%)**
  * Started (Incomplete): **146 users (14.6%)**
  * Not Started: **132 users (13.2%)**
* **Acquisition Channel Distribution:**
  * Organic Search: 244 users (24.4%)
  * Direct: 217 users (21.7%)
  * Social Media: 160 users (16.0%)
  * Referral: 119 users (11.9%)
  * WhatsApp: 103 users (10.3%)
  * Other: 102 users (10.2%)
  * Telegram: 55 users (5.5%)