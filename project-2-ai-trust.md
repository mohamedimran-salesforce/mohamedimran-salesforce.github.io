# 🛡️ Agentforce AI Trust & Compliance Audit System
**Role:** Senior Salesforce Administrator & Consultant
**Tools:** Agentforce (Einstein Copilot), Einstein Trust Layer, Salesforce Flow, Custom Objects

![Cover Image](assets/ai-cover%20image.jpg)

## 📌 Project Objective
**Architect an automated governance framework** to capture, audit, and adjudicate AI-generated interactions in real-time. This system ensures Enterprise AI is safe, auditable, and compliant with strict regulatory requirements.

---

## 🚫 1. Business Problem & Solution
**The Problem:**
Enterprises deploying Generative AI face strict regulatory requirements to monitor LLM outputs for toxicity, bias, and data leakage. Standard logging often lacks the granularity required for legal auditing or immediate remediation.

**The Solution:**
I built a custom **"Human-in-the-Loop" architecture**. This system captures the raw prompt and model response from Agentforce, commits them to a permanent audit log, and executes a real-time safety evaluation using Salesforce Flow.

---

## 📂 2. Data Model Configuration
I created a custom object **`AI_Interaction_Audit__c`** to serve as the immutable ledger for all AI conversations.

| Field Label | API Name | Data Type | Description |
| :--- | :--- | :--- | :--- |
| **Prompt Context** | `Prompt_Context__c` | Long Text | Stores the raw user input sent to the LLM. |
| **Model Response** | `Model_Response__c` | Long Text | Stores the generated response from the LLM. |
| **Toxicity Score** | `Toxicity_Score__c` | Number (3,2) | Ingests the safety score from the Einstein Trust Layer. |
| **Action Taken** | `Action_Taken__c` | Picklist | Values: *New, Automated Approval, Flagged for Review*. |
| **Timestamp** | `Interaction_Timestamp__c` | DateTime | Captures exact execution time. |

---

## 🌉 3. Integration Layer: Autolaunched Flow (The Bridge)
**Flow Label:** `Subflow: Log AI Interaction Audit`
**Type:** Autolaunched Flow (No Trigger)

**Configuration Rationale:**
I selected an Autolaunched Flow to act as the synchronous API between Agentforce and the Salesforce database. This ensures the Agent waits for a successful write operation before confirming to the user.

**Logic Design:**
1.  **Start:** Invoked by Agentforce Action.
2.  **Inputs:** Accepts `varPromptContext` (User utterance) and `varModelResponse` (LLM generation).
3.  **Create Records:** Creates one `AI_Interaction_Audit__c` record.
4.  **End:** Returns success status to the Agent.

![Autolaunched Flow Diagram](assets/ai-2.jpg)

---

## 🧠 4. Agentforce Configuration (The Brain)
**Topic Name:** `Compliance Logging`
**Scope:** Defined a strict scope to prevent hallucination. *"My job is only to log every interaction for compliance..."*

**Instructions:**
1.  **Log Interaction:** Explicit command to execute the Log AI Compliance Audit action.
2.  **Input Mapping:** Dynamic mapping of conversational context to the Flow variables defined in Section 3.

![Agentforce Debugger](assets/ai-3.jpg)

---

## ⚙️ 5. Automation Layer: Record-Triggered Flow (The Engine)
**Flow Label:** `AI Interaction Audit - Safety Check`
**Trigger:** After-Save (Actions & Related Records) on `AI_Interaction_Audit__c`

**Logic Design:**
1.  **Decision (Check Safety Scores):** Evaluates `Toxicity_Score__c` and Masking flags.
2.  **Path 1 (High Risk):** If Score > 80 OR Masking = True:
    * Update `Action_Taken__c` to **"Flagged for Review"**.
    * **Action:** Send Custom Notification to the Compliance Team queue.
3.  **Path 2 (Compliant):** Default outcome.
    * Update `Action_Taken__c` to **"Automated Approval"**.

![Record-Triggered Flow Diagram](assets/ai-1.jpg)

---

## ✅ 6. Validation & Project Achievements
**Testing Scenario:** User requests *"Check the compliance logs for today."*
**Result:**
* **Planner Reasoning:** Correctly identified "Compliance Logging" topic.
* **Data Integrity:** Confirmed prompts were passed correctly in the JSON input.
* **Record Verification:** Validated record was created with status **"Automated Approval"**.

![Audit Record Result](assets/ai-4.jpg)

### 🏆 Key Outcomes
* **100% Visibility:** Eliminated the "black box" risk by capturing every user prompt and AI response into a permanent, legal-grade audit log.
* **Automated Compliance:** Replaced manual review with real-time logic, instantly segregating safe interactions from toxic ones.
* **Scalable Architecture:** Decoupled the AI layer from the data layer using an Autolaunched Flow API, allowing for rapid logic updates without redeploying the Agent.

---
[Return to Home](./)
