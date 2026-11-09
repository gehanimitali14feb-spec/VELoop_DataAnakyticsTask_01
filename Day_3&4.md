# Days 3–4: Product Data Readiness Audit & Coverage Matrix
**Work Package Reference:** Work Package A (A1–A4)  
**Deliverable:** Product Coverage Matrix & Analytics Gaps  
**Mandatory Authenticity Policy:** Telemetry event coverage models future production readiness using simulated baseline schemas.

---

## 1. Product Area & Telemetry Coverage Matrix

| Product Area | Feature / Module | User Action | System Outcome | Business Outcome | Required Telemetry Fields | Proposed Event | Priority | Status |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **Auth** | Registration | Enters credentials and submits | Creates DB record, issues token | User acquired | `user_id`, `email`, `acquisition_source`, `device` | `user_registered` | Critical | Confirmed |
| **Auth** | Login | Submits credentials | Authenticates session, generates `session_id` | Session initialized | `user_id`, `session_id`, `login_method`, `timestamp` | `user_logged_in` | Critical | Confirmed |
| **Onboarding** | Welcome Flow | Taps through onboarding tutorial | Increments onboarding progress state | Early engagement | `user_id`, `step_number`, `completion_status` | `onboarding_completed` | High | Confirmed |
| **Gamification** | Daily Check-In | Clicks "Claim Daily Reward" | Increments streak counter, credits XP | Habit retention | `user_id`, `streak_day`, `xp_credited` | `daily_reward_claimed` | High | Confirmed |
| **Earning** | Offerwall / Tasks | Taps on partner task card | Initializes task tracking session | Task discovery | `user_id`, `task_id`, `partner_name`, `task_type` | `task_started` | Critical | Confirmed |
| **Earning** | Task Verification | Satisfies external criteria | Receives postback, validates proof | Monetization achieved | `user_id`, `task_id`, `payout_rate`, `status` | `task_completed` | Critical | Confirmed |
| **Earning** | Mini-Games / Spins | Spends token on wheel spin | Executes RNG calculation, assigns prize | Sinks token balance | `user_id`, `spin_cost`, `prize_type`, `prize_value` | `spin_completed` | Medium | Confirmed |
| **Wallet** | Balance Ingestion | Clicks wallet screen | Queries real-time balance ledger | Financial visibility | `user_id`, `xp_balance`, `liquid_balance` | `wallet_viewed` | Low | Confirmed |
| **Payouts** | Cashout Request | Enters payout address and submits | Locks funds in escrow, flags payout queue | Liability claimed | `user_id`, `withdrawal_id`, `amount`, `method` | `withdrawal_requested` | Critical | Confirmed |
| **Payouts** | Payout Settlement | Admin / Gateway approval | Dispatches funds, marks transaction completed | Liability settled | `withdrawal_id`, `gateway_ref_id`, `settled_at` | `withdrawal_completed` | Critical | Confirmed |
| **Referrals** | Invite Program | Shares referral link / code | Generates referral tracking payload | Viral acquisition | `user_id`, `referral_code`, `channel` | `referral_created` | Medium | Confirmed |
| **Referrals** | Referral Conversion | Referred user meets criteria | Credits commission bonus to referrer | Verified viral growth | `referrer_id`, `referee_id`, `commission_amount` | `referral_converted` | High | Confirmed |

---

## 2. Top 10 Critical Analytics Gaps
1. **Absence of Webhook Idempotency Keys:** Lack of unique postback deduplication keys can lead to multiple reward payouts on retried network requests.
2. **Missing Session Heartbeat Telemetry:** No intermittent ping exists during active sessions, preventing accurate measurement of foreground vs. background app usage.
3. **Off-Platform Task Abandonment Blindspot:** Users leaving the application to complete third-party offers without completing them cannot be tracked until timeout expiration.
4. **Unclassified Task Failure Codes:** Errors currently aggregate into generic failure statuses without separating network drops, fraud flags, or regional ineligibility.
5. **Referral Attribution Loss on Deferred Installs:** Inability to match installs if the user installs the app outside immediate redirect sessions.
6. **No Escrow Balance Audit Trail:** Balances requested for withdrawal are not distinctly flagged in an escrow ledger prior to settlement.
7. **Client-Side Ad Impression Verification Gap:** Video ad views logged on initiation without client-side end-card rendering verification.
8. **Device ID Duplication Risk:** Inability to detect multiple account registrations originating from the same physical device hardware fingerprint.
9. **Missing Financial Reversal Audit Ledger:** When rewards are clawed back due to postback fraud, prior balance states cannot be historically reconstructed.
10. **Inconsistent Timestamp Timezone Standards:** Ingestion logs combine local client timestamps with server UTC timestamps without standardized offsets.