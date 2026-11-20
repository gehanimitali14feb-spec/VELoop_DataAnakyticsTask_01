# VELoop Rewards — Day 1 to 20 Complete Project Blueprint & Milestone Log

---

### Phase 1: Architecture Discovery & Event Tracking Blueprint (Days 1 to 6)

#### Day 1 & Day 2: Business Scoping & Core Objectives
* Mapped the business model of the VELoop GPT (Get-Paid-To) rewards platform, focusing on user acquisition, daily task engagement, referral traffic, and reward redemptions.
* Defined the target performance KPIs: Total Registered Users, Active User Rate (30-day window), Total Tasks Attempted, and Task Completion Rate.
* Established the project plan across programmatic data auditing, Python ETL cleaning, star schema data modeling, and Power BI dashboard development.

#### Day 3 & Day 4: Multi-Sheet Schema Exploration
* Analyzed the 15 sheets across both raw workbooks: `VELoop_Rewards_Data_01.xlsx` and `VELoop_Simulated_User_Behavior_1000.xlsx`.
* Evaluated entity schemas across users, daily activities, sessions, feature events, and task activity.
* Identified common linking keys: `user_id`, `session_id`, and `event_id`.

#### Day 5 & Day 6: Event Tracking Specification Blueprint
* Designed the event telemetry tracking plan for user actions across the app:
  * Lifecycle Events: `session_start`, `session_end`, `account_created`, and `onboarding_step`.
  * Engagement Events: `task_start`, `task_complete`, `task_fail`, `spin_wheel_spin`, `milestone_unlocked`, and `wallet_transfer`.
* Specified standard metadata parameters for all events: `device`, `platform`, `entry_point`, `task_category`, `xp_value`, and UTC timestamp.
* Formulated dropout tracking to capture where users abandon registration and onboarding funnels.

---

### Phase 2: Programmatic Audit & Python Cleaning Pipeline (Days 7 to 12)

#### Day 7 & Day 8: Automated Data Profiling & Audit Report
* Built an automated Python audit script to detect missing values, duplicate records, and schema anomalies across all 15 sheets.
* Found 8 duplicate user records in the messy audit sheet and isolated them.
* Identified 10,494 null values in task logs (confirming that `failure_reason` is intentionally blank when a task succeeds).
* Flagged data hygiene issues: mixed casing in `platform` (`Android` vs `android`, `iOS` vs `ios`) and unparsed string timestamps.

#### Day 9 & Day 10: Python ETL Pipeline Build (`Analyis_Cleaning.ipynb`)
* Developed the end-to-end data transformation pipeline in Jupyter Notebook using Pandas.
* Standardized text columns (`full_name`, `email`, `city`, `state`, `platform`, `primary_device`) to unified title casing.
* Parsed and converted all registration and session dates into standardized UTC DateTime format.
* Imputed missing values for retention tiers and eliminated orphan session IDs.

#### Day 11 & Day 12: Feature Engineering & Master Dataset Export
* Engineered activity indicators: `is_active_7d`, `is_active_30d`, and `days_since_registration`.
* Built task efficiency calculations: `task_completion_rate_pct` (tasks_completed / total_tasks_attempted).
* Segmented users into loyalty tiers: `Bronze`, `Silver`, `Gold`, and `Platinum`.
* Exported the clean multi-sheet master workbook: `VELoop_PowerBI_Master_Dataset.xlsx`.

---

### Phase 3: Star Schema Data Modeling & DAX Measures (Days 13 to 16)

#### Day 13 & Day 14: Relational Star Schema Architecture
* Imported the master dataset into Power BI Desktop and opened Model View.
* Structured the model around a central dimension table: `01_Users_Cleaned_Master` (Primary Key: `user_id`).
* Linked dimension to fact tables: `02_Sessions_Cleaned`, `03_Events_Cleaned`, `04_Daily_Activity_Cleaned`, `05_Tasks_Cleaned`, `06_Milestones_Cleaned`, and `07_Feature_Usage_Cleaned`.
* Enforced One-to-Many (1:N) relationships with single-direction cross-filtering (`Users` -> `Facts`).

#### Day 15 & Day 16: Custom DAX Metric Development
* Formulated DAX measures using `DIVIDE` and `DISTINCTCOUNT`:
  * `Total Users` = Distinct count of registered user IDs.
  * `Active User Rate` = Percentage of users active within the last 30 days.
  * `Total Tasks Attempted` = Sum of all initiated tasks.
  * `Task Completion Rate` = Sum of completed tasks divided by total attempted tasks.
* Documented initial data quality and reconciliation findings in `docs/`.

---

### Phase 4: UI Design, Chart Visuals & Bookmark Interactivity (Days 17 to 19)

#### Day 17: Theme Styling & Executive KPI Cards
* Designed the dashboard layout in Power BI using the warm terracotta palette (`#6E331B`, `#8C472A`, `#EFE2D8`).
* Formatted visual containers with transparent backgrounds and clean card borders.
* Placed 4 core KPI cards across the top: Total Users (`1K`), Active User Rate (`100%`), Total Tasks Attempted (`10K`), and Task Completion Rate (`0.57` / `57%`).
* Created top pill-button navigation bar and branded footer: `Designed by Mitali G | VELoop GPT Dashboard`.

#### Day 18: Dual Analytical Views Construction
* View 1 (User Overview):
  * Total Tasks Attempted by Month (Area Trend Chart).
  * Total Users by Acquisition Source (Bar Chart).
  * Total Users by City (Top 5 Donut Chart).
  * Total Users by Onboarding Status (Funnel Chart).
* View 2 (Task & Engagement View):
  * Tasks Completed vs Failed by Month (Stacked Area Chart).
  * Tasks by Device & Platform Ecosystem (Clustered Column Chart).
  * User Distribution by Retention Tier (Donut Chart).
  * Average Lifetime Sessions by Retention Tier (Clustered Bar Chart).

#### Day 19: Stateful Bookmarks & Selection Wiring
* Grouped visuals in the Selection pane into `Group_UserOverview` and `Group_TaskEngagement`.
* Created and updated two bookmarks: `User Overview` and `Task and Engagement View`.
* Configured bookmark settings: `Display` enabled and `Data` disabled (so active slicers and filters do not reset when switching views).
* Bound top pill buttons to their respective bookmark actions.

---

### Phase 5: Synthesis, ER Diagram & Final Sign-Off (Day 20)

#### Day 20: Architecture Verification & Technical Sign-Off
* Verified the complete Star Schema in Power BI Model View and archived the diagram asset `VELoop_Logical_ER_Diagram.JPG`.
* Finalized the project documentation, data dictionary, and entity relationship rules (1:N cardinalities from Users to transactional facts).
* Validated that all deliverables are committed and synced on GitHub:
  * `VELoop_Analysis.pbix` (Power BI workbook with interactive views).
  * `VELoop_PowerBI_Master_Dataset.xlsx` (Cleaned master Excel dataset).
  * `Analyis_Cleaning.ipynb` (Python cleaning and audit pipeline).
  * `VELoop_Logical_ER_Diagram.JPG` (Visual Star Schema diagram).
  * `veloop_analytics_dashboard.png` (High-resolution dashboard preview).
  * `docs/Day_1to20.md` (Unified master milestone log).
* Project Status: Task 01 fully executed, reviewed, and officially signed off.
* Data Analyst: Mitali Gehani
* Repository: `gehanimitali14feb-spec/VELoop_DataAnakyticsTask_01`