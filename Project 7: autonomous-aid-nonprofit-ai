# 📺 Project: Autonomous Aid (Agentforce & Orchestrator)
![Cover Image](assets/NP cover image.png)

## The Business Problem
Humanitarian organizations face a "Black Box" problem during crises. Grant approvals sit in email inboxes while field teams wait for funds (latency), and donors rarely receive specific updates on how their money was used until months later (transparency), leading to poor donor retention.

## The Solution
* **Event-Driven Trigger:** I engineered a Platform Event (`Disaster_Signal__e`) that simulates integration with weather systems to auto-initialize relief grants instantly.
* **Orchestration Engine:** A **Flow Orchestrator** manages the lifecycle, enforcing a "Stage Lock" where Finance cannot approve funds until Field Assessments are verified.
* **AI Stewardship:** I deployed **Agentforce Prompt Builder** to read specific grant outcomes (e.g., "1,000 Tarps") and auto-generate personalized, hallucination-free impact emails to donors.

### 🎥 [Watch the Video Demo](#) *(Link coming soon)*

---

### 📸 Implementation Gallery

#### 1. Architecture & Data Model
*A lean, custom schema designed for high-speed data entry, triggered by external signals.*
![Schema & Fields](assets/np-01.png)
![Platform Event Definition](assets/np-02.png)
![Event Listener Flow](assets/np-07.png)

#### 2. The Engine (Flow Orchestrator)
*The master workflow that manages state transitions between Field Officers and Finance Managers.*
![Orchestrator Canvas](assets/NP-03.png)

#### 3. Sub-Flow Automation
*Decoupled screen flows that capture structured data at every stage of the lifecycle.*
![Field Assessment Flow](assets/np-06.png)
![Finance Approval Flow](assets/np-05.png)
![Impact Verification Flow](assets/np-04.png)

#### 4. AI Layer (Agentforce)
*The "Glass Box" solution: Converting raw field data into emotional donor impact stories.*
![Prompt Builder Template](assets/np-08.png)
![Einstein Generation Action](assets/np-09.jpg)
![Final AI Generated Email](assets/np-10.png)

---
[Return to Home](./)
