# Use Case Specification: UC-17

* **ID / Code:** UC-17
* **Use Case Name:** Override Locked Period
* **Description:** Extends UC-14 or UC-15 when an invoice operation targets a locked financial period. A Super-Administrator authorizes an explicit, audited exception (FR-2.7).
* **Primary Actor:** Super-Administrator
* **Scope:** Subscription Management & Invoicing System
* **Level:** User Goal (extends UC-14 at extension point *period locked*)
* **Stakeholders & Interests:**
  * *Super-Administrator:* Wants to correct exceptional errors in closed periods in a controlled way.
  * *Administrator:* Needs the correction to be possible without reopening the whole period.
  * *External accounting service / Auditor:* Needs exceptions affecting closed financial periods to remain traceable.
* **Preconditions:** The target period is locked (UC-16); the actor has the Super-Administrator role.
* **Postconditions:** A one-time, audited exception exists for the specific operation, or the request is rejected.
* **Success Guarantee:** The authorized operation is permitted through an explicit, audited Super-Administrator exception (FR-2.7). The financial period remains locked for other operations.
* **Minimal Guarantee:** The period stays locked for any other operation; no override is applied without justification.
* **Trigger:** An invoice operation in UC-14 or UC-15 is blocked because the financial period is locked and an override is requested.
* **Main Success Scenario:**
1. **Super-Administrator:** Opens the override request generated from UC-14 or UC-15
2. **System:** Displays the locked period, the requested operation, the affected invoice and the requesting Administrator.
3. **Super-Administrator:** Enters a mandatory justification and authorizes the override.
4. **System:** Grants a one-time exception limited to that operation and invoice, and records it in the audit trail.
5. **System:** Allows the authorized operation to continue in UC-14 or UC-15.
6. **System:** Marks the accounting packages of that period as outdated so that a new version is generated (UC-18, FR-6.3.2) and notifies the requesting Administrator.

* **Extensions:**
  * 3a. Super-Administrator rejects the override:
    * 3a1. System records the rejection and the reason; the UC-14 operation is cancelled.
  * 3b. Justification is empty (Assumption):
    * 3b1. System does not allow the override to be authorized.
