# 💸 Event-Driven Revenue Provisioning (Multi-Cloud Ready)
**Role:** Senior Salesforce Administrator & Consultant | **Stack:** Platform Events, Flow Orchestrator, Async Apex/Flow

![Cover Image](assets/image.png)

## 📌 Project Objective
**Architecting Enterprise RevOps:** I designed an enterprise-grade "Lead-to-Cash" engine to decouple high-volume sales transactions from financial processing. By transitioning from synchronous record-triggered flows to an **Event-Driven Architecture (EDA)**, the system eliminates database locking errors and establishes a scalable foundation for future ERP integrations (e.g., NetSuite/SAP).

### 🎥 [Watch the Project Demo](https://drive.google.com/file/d/1UuQH5x9_qPhjVdDo6uUaw1JVe2Gtjp4k/view?usp=sharing)

---

## 🚫 1. The Business Problem
**The Monolithic Bottleneck:**
The legacy system processed Invoices and Revenue Ledger entries *synchronously* when an Opportunity was Closed-Won.
* **Performance:** During End-of-Quarter spikes, huge transaction volumes caused "CPU Time Limit" errors and record locking.
* **Scalability:** The system was tightly coupled; changes to the Finance logic broke the Sales process.

**The Solution:**
I implemented a **Pub/Sub (Publish-Subscribe)** architecture using Salesforce Platform Events to decouple the domains.

---

## 🏗️ 2. Event-Driven Architecture
**The "Fire and Forget" Pattern:**
1.  **Sales Domain:** Closes the Opportunity -> Publishes a `Revenue_Transaction__e` event.
2.  **Event Bus:** Acts as a resilient message queue.
3.  **Finance Domain:** An Asynchronous Subscriber Flow picks up the message and processes the heavy lifting (Ledgers/Invoices) in a separate transaction.

![Architecture Diagram](assets/Screenshot%202026-01-04%20183730.png)

---

## 🔄 3. Technical Implementation
### The Data & Event Layer
I configured a high-volume Platform Event object to carry the transaction payload neutral of the source system.
![Platform Event Definition](assets/Screenshot%202026-01-04%20183833.png)

### The Publisher (Sales)
* **Trigger:** Record-Triggered Flow on Opportunity (After-Save).
* **Action:** Transforms Opportunity Data into a JSON-neutral payload and publishes the Platform Event.
* **Benefit:** Zero delay for the Sales Rep. The "Save" is instant.

![Publisher Flow](assets/Screenshot%202026-01-04%20183756.png)

### The Subscriber (Finance)
* **Trigger:** Platform Event-Triggered Flow.
* **Logic:** Receives `Revenue_Transaction__e` and generates `Invoice__c` and double-entry `Revenue_Ledger__c` records.

![Subscriber Flow](assets/Screenshot%202026-01-04%20183811.png)

---

## 🎼 4. Governance with Flow Orchestrator
**The Audit Layer:**
For high-value transactions (>$50k), simple automation isn't enough. I used **Flow Orchestrator** to inject a "Finance Review" stage.
* **Logic:** If `Amount > $50,000`, the Orchestrator pauses the activation and assigns an interactive "Review Invoice" step to the CFO.

### 📸 Orchestration Logic
![Orchestrator Trigger](assets/Screenshot%202026-01-04%20183849.png)
![Interactive Step](assets/Screenshot%202026-01-04%20183858.png)

---

## 📊 5. CFO Command Center
**Real-Time Revenue Recognition:**
The system provides immediate financial visibility without waiting for nightly batches.
![Revenue Dashboard](assets/Screenshot%202026-01-04%20183945.png)

### 🏆 Key Outcomes
* **Scalability:** Processed 10,000+ transactions during stress testing with zero lock errors.
* **Integration Ready:** The Platform Event bus is ready to hook into MuleSoft for external ERP syncing without changing a single line of Salesforce configuration.

---
[Return to Home](./)
