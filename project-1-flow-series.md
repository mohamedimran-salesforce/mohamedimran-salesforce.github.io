# 🚀 5-Part Enterprise Automation Series
**Role:** Lead Developer & Architect | **Stack:** Advanced Flow, Custom Metadata, Tableau, External Services

## Overview
This series demonstrates 5 real-world solutions to complex enterprise problems, utilizing 100% declarative tools (No-Code). Each episode focuses on scalable architecture, separating business logic (Custom Metadata) from automation (Flow) to ensure maintainability.

---

## 📺 Episode 1: Smart Discount Guardrails (CPQ)
**The Business Problem:**
Sales reps were pushing high discounts to close deals without justification, eroding margins. Leadership needed a clear "approval story," but the logic lived in people's heads, leading to inconsistent enforcement.

**The Solution:**
I built a lightweight guardrail on the **Quote** object using a **Before-Save Flow** (Fast Field Updates) for maximum performance.
* **Configuration:** The discount threshold (e.g., 30%) is stored in a **Custom Metadata Type** (`Quote_Discount_Policy__mdt`), not hard-coded.
* **Logic:** The Flow fetches the active policy using a "Get Records" element.
* **Validation:** A Decision element checks if `Additional Disc %` ≥ `Threshold Percent`.
* **UX:** If the validation fails, a **Custom Error** displays the message: *"A Discount Reason is required when Additional Discount is at or above the configured threshold."*

**Tech Stack:**
* `Quote` Object (Fast Field Updates)
* `Quote_Discount_Policy__mdt` (Governance)
* `Custom Error` Element (Inline Field Validation)

### 🎥 [Watch the Video Demo](https://drive.google.com/file/d/1xUdjBekTDRHmkHYyrLMM9cvpnLT7uWAI/view?usp=sharing)

---

## 📺 Episode 2: Smart Case Escalation (Scheduled Paths)
**The Business Problem:**
High-priority cases were missing SLAs because escalation relied on manual tracking. There was no consistent way to route overdue cases to the right queue at the right time.

**The Solution:**
* **Routing Logic:** A **Scheduled Path Flow** runs on the Case object. It checks if the Case is still open as the SLA approaches.
* **Configuration:** A Custom Metadata Type maps Priority → SLA Minutes → Target Queue.
* **Action:** Automatically reassigns the case to the correct `Escalation_Queue` and stamps an escalation reason without human intervention.

**Tech Stack:**
* Scheduled Paths (Batch Processing)
* `Escalation_Target__c` (Dynamic SLA Formula)
* Queue Routing via `Group` object

### 🎥 [Watch the Video Demo](https://drive.google.com/file/d/1EcAovQMf7OBIQvslsD5t7OkhRYwUArT4/view?usp=sharing)

---

## 📺 Episode 3: Customer Health Signal Hub (Event-Driven)
**The Business Problem:**
Customer health data (usage, billing, NPS) lived in external systems. Sales reps were "blind" to churn risks until it was too late.

**The Solution:**
I architected an Event-Driven architecture using **Platform Events**:
* **Ingestion:** External systems publish to `Account_Health_Signal__e` (High Volume Platform Event).
* **Processing:** A Platform Event-Triggered Flow receives the signal, finds the related Account, and updates the `Health_Status__c`.
* **Action:** If the status turns "Red," the Flow auto-generates a High-Priority Task for the Account Owner.
* **Audit:** A child object `Account_Health_History__c` logs every signal for trend reporting.

**Tech Stack:**
* `Account_Health_Signal__e` (Pub/Sub Architecture)
* `Account_Health_History__c` (Audit Trail)
* Asynchronous Processing

### 🎥 [Watch the Video Demo](https://drive.google.com/file/d/1QonNytsyBKvcuyf-y-dOGGs7590XVSV4/view?usp=sharing)

---

## 📺 Episode 4: Fair Workload Engine (Tableau Integration)
**The Business Problem:**
Support cases and urgent tasks were piling up on the same few high-performers, leading to burnout. Managers lacked data to prove overload.

**The Solution:**
* **Scoring Engine:** A Scheduled Flow runs nightly to calculate a "Workload Score" for every user based on Open Cases, Complexity, and Overdue Tasks.
* **Snapshotting:** The score is saved to a `User_Workload_Snapshot__c` record.
* **Visualization:** Data is pushed to **Tableau** to generate a "Heat Map," allowing managers to visualize burnout risk across the team.

**Tech Stack:**
* `User_Workload_Snapshot__c` (Historical Data)
* `Workload_Policy_mdt` (Risk Thresholds)
* Tableau Integration for Analytics

### 🎥 [Watch the Video Demo](
