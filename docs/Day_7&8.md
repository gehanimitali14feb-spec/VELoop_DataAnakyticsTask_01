---

### 2. File 4: `docs/Day_07_08_Earning_Reward_Analytics.md`

```markdown
# Days 7–8: Earning & Reward Analytics Specification
**Work Package Reference:** Work Package C (C1–C4)  
**Deliverable:** Task-Level Analytics, Failure Taxonomies, and Reward State Ledger  
**Mandatory Authenticity Policy:** Data metrics reflect baseline profiling from the simulated task dataset (`05_Task_Activity`).

---

## 1. Task Lifecycle State Machine (C1)
Every earning feature follows a five-stage telemetry progression:
$$\text{Task Viewed} \longrightarrow \text{Task Started} \longrightarrow \text{Task Completed} \longrightarrow \text{Completion Validated} \longrightarrow \text{Reward Credited}$$

* **Discovery (`task_viewed`):** Offer card displayed in feed/offerwall.
* **Initiation (`task_started`):** User engages link/outbound SDK.
* **Completion (`task_completed`):** User achieves completion condition.
* **Validation (`task_validated`):** Server validates proof or receives third-party callback.
* **Reward (`reward_credited`):** Balance added to ledger.

---

## 2. Task Failure Taxonomy (C2)
Profiling of the 9,846 records in `05_Task_Activity` reveals a 57.1% success rate and four primary non-success states:

| Task Status | Record Count | Percentage | Description |
| :--- | :--- | :--- | :--- |
| **Completed** | 5,627 | 57.15% | Successfully executed and verified |
| **Abandoned** | 2,051 | 20.83% | User exited session prior to meeting threshold |
| **Failed** | 1,520 | 15.44% | Terminated by validation error, timeout, or unavailability |
| **Pending** | 648 | 6.58% | Completed by user; awaiting third-party webhook confirmation |

### Standardized Failure Reasons Logged
* **Validation failed (732 records):** Proof criteria rejected by anti-fraud, VPN detection, or provider check.
* **Task unavailable (722 records):** Offer reached partner quota or was deprecated before launch.
* **Timeout (710 records):** Elapsed execution time exceeded maximum allowable attribution window.
* **Incomplete action (706 records):** User performed partial action without triggering postback threshold.
* **User exited (701 records):** Explicit manual exit from the task screen.

---

## 3. Reward Audit Ledger States (C3)
A strict separation is maintained between **User Action** and **Financial Ledger Crediting**:
* `reward_pending` (648 records in baseline): Held during cooldown or partner review.
* `reward_credited` (5,627 records in baseline): Immutable balance credit posted.
* `reward_reversed`: Clawback applied following postback fraud or partner chargeback.
* `reward_corrected`: Administrative balance correction with reference to original transaction.

---

## 4. Third-Party Dependency & Fraud Risk (C4)
* **Offerwall Postback Reliance:** Off-platform tasks (Surveys, External Games) rely on external webhooks. A failure at the partner server must be captured as `ERR_THIRD_PARTY_TIMEOUT` rather than generic app failure.
* **Idempotency Safeguard:** Third-party postbacks MUST include a deduplication hash (`partner_transaction_id`) to prevent duplicate reward crediting on retry pings.