# VELoop_DataAnakyticsTask_01
Product analytics, data readiness blueprint, and event tracking specification for VELOOP Rewards ecosystem (Task 01).


# VELOOP Rewards – Product Analytics & Data Readiness Blueprint (Task 01)

**Analyst:** Mitali Gehani  
**Milestone:** Days 1 to 12 Progress Submission (Work Packages A through F)  
**Mandatory Authenticity Policy:** VELOOP is an active rewards and engagement product under development. All numbers, user counts, activity metrics, and transaction values presented in this repository originate from simulated test datasets (`VELoop_Rewards_Data_01.xlsx` and `VELOOP_Simulated_User_Behavior_1000.xlsx`) and represent analytical telemetry design rather than company production performance.

---

## Repository Structure & Deliverables

* 📁 **`data/`**: Official simulated datasets (`VELoop_Rewards_Data_01.xlsx`, `VELOOP_Simulated_User_Behavior_1000.xlsx`).
* 📄 **[Days 1–2: Source & Verification Register](docs/Day_01_02_Source_and_Verification_Register.md)**  
  Classifies product facts, telemetry assumptions, and engineering dependencies into Confirmed, Proposed, and To Be Verified states.
* 📄 **[Days 3–4: Product Data Readiness Audit & Coverage Matrix](docs/Day_03_04_Product_Data_Readiness_Audit.md)**  
  Maps product features to system outcomes and telemetry events; documents the top 10 critical analytics gaps.
* 📄 **[Days 5–6: User & Account Analytics Specification](docs/Day_05_06_User_Analytics_Specification.md)**  
  Defines identity architecture (`user_id`, `session_id`, `event_id`, `transaction_id`), user profile schemas, and baseline cohort metrics across 1,000 simulated accounts.
* 📄 **[Days 7–8: Earning & Reward Analytics Specification](docs/Day_07_08_Earning_Reward_Analytics.md)**  
  Traces the task lifecycle (`Viewed` -> `Started` -> `Completed` -> `Validated` -> `Credited`), standardizes failure taxonomy across 9,846 task records, and models reward auditing.
* 📄 **[Days 9–10: Wallet & Withdrawal Analytics Specification](docs/Day_09_10_Wallet_Withdrawal_Analytics.md)**  
  Establishes the double-entry transaction ledger model, withdrawal state machine (`Requested` -> `Under Review` -> `Completed`/`Rejected`), and core payout turnaround KPIs.
* 📄 **[Days 11–12: Referral Funnel & Production Event Tracking Plan](docs/Day_11_12_Referrals_Event_Tracking_Plan.md)**  
  Specifies the 4-stage referral conversion funnel and catalogs the core 25 production telemetry events using the standardized `object_action` convention.



