# 🚀 5-Part Enterprise Automation Series
**Role:** Sr.salesforce Admin/Consultant & Architect | **Stack:** Advanced Flow, Custom Metadata, Tableau, External Services

## Overview
This series demonstrates 5 real-world solutions to complex enterprise problems, utilizing 100% declarative tools (No-Code). Each episode focuses on scalable architecture, separating business logic (Custom Metadata) from automation (Flow) to ensure maintainability.

---

## 📺 Episode 1: Smart Discount Guardrails (CPQ)
![Cover Image](assets/Episode1-1%20cover%20pictures.png)
### The Business Problem
Sales teams were pushing high discounts to close deals without justification, eroding margins. Leadership needed a clear "approval story," but the logic lived in people's heads, leading to inconsistent enforcement.

### The Solution
I built a lightweight guardrail on the **Quote** object using a **Before-Save Flow** (Fast Field Updates).
* **Configuration:** The discount threshold (e.g., 30%) is stored in **Custom Metadata** (`Quote_Discount_Policy__mdt`), allowing Admins to update the % without editing the Flow.
* **Logic:** The Flow blocks the save if `Additional Disc %` > Threshold AND `Discount Reason` is blank.

### 🎥 [Watch the Video Demo](https://drive.google.com/file/d/1xUdjBekTDRHmkHYyrLMM9cvpnLT7uWAI/view?usp=sharing)

### 📸 Implementation Gallery
#### 1. Data Model & Governance
*Custom Metadata stores the policy (Rule Separation), while the Quote object holds the validation field.*
![Discount Reason Field](assets/1.png)
![Custom Metadata Type](assets/2.png)
![Threshold Field](assets/3.png)

#### 2. Flow Architecture
*The "Fast Field Update" Flow fetches the policy and validates input before the database commit.*
![Full Flow Canvas](assets/11.png)
![Start Element](assets/6.png)
![Get Active Policy](assets/7.png)
![Decision Logic](assets/8.png)
![Custom Error Configuration](assets/9.png)

#### 3. User Experience
*The result: A clean, inline error message that guides the user to fix the data.*
![Error Message in Action](assets/10.png)
![Additional Config](assets/4.png)
![Additional Config](assets/5.png)

---

## 📺 Episode 2: Smart Case Escalation (Scheduled Paths)
![Cover Image](assets/Episode2%20cover%20pictures.jpg)

### The Business Problem
High-priority cases were missing SLAs because escalation relied on manual tracking. There was no consistent way to route overdue cases to the right queue at the right time.

### The Solution
* **Routing Logic:** A **Scheduled Path Flow** runs on the Case object. It checks if the Case is still open as the SLA approaches.
* **Configuration:** A Custom Metadata Type maps Priority → SLA Minutes → Target Queue.
* **Action:** Automatically reassigns the case to the correct `Escalation_Queue` and stamps an escalation reason without human intervention.

### 🎥 [Watch the Video Demo](https://drive.google.com/file/d/1EcAovQMf7OBIQvslsD5t7OkhRYwUArT4/view?usp=sharing)

### 📸 Implementation Gallery
#### Logic & Configuration
*The Flow manages both immediate updates and scheduled escalation checks.*
![Flow Canvas](assets/Episode2-1.jpg)
![Custom Metadata Policy](assets/Episode2-2.jpg)
![Queue Configuration](assets/Episode2-3.jpg)

---

## 📺 Episode 3: Customer Health Signal Hub (Event-Driven)
![Cover Image](assets/Episode3-cover%20picture.jpg)

### The Business Problem
Customer health data (usage, billing, NPS) lived in external systems. Sales reps were "blind" to churn risks until it was too late.

### The Solution
I architected an Event-Driven architecture using **Platform Events**:
* **Ingestion:** External systems publish to `Account_Health_Signal__e` (High Volume Platform Event).
* **Processing:** A Platform Event-Triggered Flow receives the signal, finds the related Account, and updates the `Health_Status__c`.
* **Action:** If the status turns "Red," the Flow auto-generates a High-Priority Task for the Account Owner.

### 🎥 [Watch the Video Demo](https://drive.google.com/file/d/1QonNytsyBKvcuyf-y-dOGGs7590XVSV4/view?usp=sharing)

### 📸 Implementation Gallery
#### Architecture & Automation
*Handling high-volume events and automating the response.*
![Platform Event Definition](assets/Episode3-3.jpg)
![Subscriber Flow](assets/Episode3-1.jpg)
![Screen Flow Publisher](assets/Episode3-2.jpg)

#### The User Experience
*Sales reps see real-time history and get immediate tasks for risks.*
![Send Signal Action](assets/Episode3-4.jpg)
![Input Screen](assets/Episode3-5.jpg)
![Health History Record](assets/Episode3-6.jpg)
![Auto-Generated Task](assets/Episode3-7.jpg)

---

## 📺 Episode 4: Fair Workload Engine (Tableau Integration)
![Cover Image](assets/Episode%204%20cover%20picture.jpg)

### The Business Problem
Support cases and urgent tasks were piling up on the same few high-performers, leading to burnout. Managers lacked data to prove overload.

### The Solution
* **Scoring Engine:** A Scheduled Flow runs nightly to calculate a "Workload Score" for every user based on Open Cases, Complexity, and Overdue Tasks.
* **Snapshotting:** The score is saved to a `User_Workload_Snapshot__c` record.
* **Visualization:** Data is pushed to **Tableau** to generate a "Heat Map," allowing managers to visualize burnout risk across the team.

### 🎥 [Watch the Video Demo](https://drive.google.com/file/d/10bP5eluKT8ZAW30VhqUvD7x9gRf1ut6d/view?usp=sharing)

### 📸 Implementation Gallery
#### Analytics & Logic
*Calculating the score and visualizing the risk.*
![Tableau Heatmap](assets/Episode%204-4.jpg)
![Calculation Flow](assets/Episode%204-1.jpg)
![Risk Assignment Logic](assets/Episode%204-2.jpg)
![Routing Logic](assets/Episode%204-3.jpg)

---

## 📺 Episode 5: Real-Time Credit Risk Engine (No-Code Integration)
![Cover Image](assets/Episode%205-1.jpg)

### The Business Problem
Sales reps were negotiating deals with clients who had poor credit, leading to rejected contracts. The credit check process was manual and slow (email-based).

### The Solution
I built a No-Code Integration using **External Services**:
* **Integration:** Ingested a Swagger/OpenAPI schema to connect Salesforce to an external Banking API.
* **Automation:** When an Opportunity reaches "Negotiation," an **HTTP Callout (GET)** fetches the real-time credit score.
* **Security:** Uses **Named Credentials** to handle authentication securely without Apex.

### 🎥 [Watch the Video Demo](https://drive.google.com/file/d/1a12sz3d75qFqJhTP-zynUyzGtTZw3g6m/view?usp=sharing)

### 📸 Implementation Gallery
#### Integration Architecture
*Connecting Salesforce to the Banking API securely.*
![External Services Setup](assets/Episode%205-7.jpg)
![Named Credentials](assets/Episode%205-6.jpg)
![Permission Sets](assets/Episode%205-2.jpg)
![Mocking Rules](assets/Episode%205-5.jpg)

#### Flow Automation
*Handling the API call asynchronously to prevent timeouts.*
![Async Path Flow](assets/Episode%205-3.jpg)
![Data Cleanup Flow](assets/Episode%205-4.jpg)

#### Final Result
*Real-time credit data appears instantly on the Opportunity.*
![Opportunity View](assets/Episode%205-8.jpg)
![Details Panel](assets/Episode%205-9.jpg)

---
[Return to Home](./)
