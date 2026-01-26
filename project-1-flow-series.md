# 🚀 5-Part Enterprise Automation Series
**Role:** Lead Developer & Architect | **Stack:** Advanced Flow, Custom Metadata, Tableau, HTTP Callouts

## Overview
This series demonstrates 5 real-world solutions to complex enterprise problems, utilizing 100% declarative tools (No-Code). Each episode focuses on a specific bottleneck—from CPQ margin protection to burnout prevention—and solves it using scalable architecture.

---

## 📺 Episode 1: Smart Discount Guardrails for CPQ
**The Problem:** Sales reps were applying high discounts without justification, eroding margins.
**The Solution:**
* [cite_start]**Before-Save Flow:** Validates discounts against a policy stored in **Custom Metadata**[cite: 124, 125].
* [cite_start]**Logic:** If the discount exceeds the threshold and no "Discount Reason" is provided, the Flow blocks the save with a custom error message[cite: 127].
* [cite_start]**Impact:** Protects revenue and creates a clean approval history[cite: 136, 137].

### 🎥 [Watch the Video Demo](https://drive.google.com/file/d/1xUdjBekTDRHmkHYyrLMM9cvpnLT7uWAI/view?usp=sharing)

---

## 📺 Episode 2: Smart Case Escalation (Scheduled Paths)
[cite_start]**The Problem:** High-priority cases were missing SLAs because escalation relied on manual tracking[cite: 150].
**The Solution:**
* [cite_start]**Scheduled Path Flow:** Checks if a Case is still open as the SLA approaches[cite: 155].
* [cite_start]**Routing:** Automatically reassigns the case to an Escalation Queue based on priority mapping in Custom Metadata[cite: 153].
* [cite_start]**Impact:** Ensures 100% SLA compliance without human intervention[cite: 165].

### 🎥 [Watch the Video Demo](https://drive.google.com/file/d/1EcAovQMf7OBIQvslsD5t7OkhRYwUArT4/view?usp=sharing)

---

## 📺 Episode 3: Customer Health Signal Hub (Platform Events)
[cite_start]**The Problem:** Customer health data (usage, billing) lived in external systems, leaving Sales blind to churn risks[cite: 177].
**The Solution:**
* [cite_start]**Platform Events:** Created `Account_Health_Signal__e` to ingest signals from external apps[cite: 181].
* **Event-Triggered Flow:** Updates the Account's health status in real-time and auto-generates high-priority tasks for Account Owners if health turns "Red"[cite: 188, 198].
* [cite_start]**Impact:** Proactive churn prevention and real-time visibility[cite: 210].

### 🎥 [Watch the Video Demo](https://drive.google.com/file/d/1QonNytsyBKvcuyf-y-dOGGs7590XVSV4/view?usp=sharing)

---

## 📺 Episode 4: Fair Workload Engine (Tableau Integration)
[cite_start]**The Problem:** Support cases were piling up on the same few people, leading to burnout[cite: 237].
**The Solution:**
* **Scoring Logic:** A Scheduled Flow calculates a "Workload Score" for every user based on open cases and complexity[cite: 241].
* [cite_start]**Visualization:** Data is pushed to **Tableau** to generate a heat map for managers to visualize team capacity[cite: 247].
* [cite_start]**Impact:** Prevents burnout and ensures fair case distribution[cite: 268].

### 🎥 [Watch the Video Demo](https://drive.google.com/file/d/10bP5eluKT8ZAW30VhqUvD7x9gRf1ut6d/view?usp=sharing)

---

## 📺 Episode 5: Real-Time Credit Risk Engine (HTTP Callouts)
[cite_start]**The Problem:** Sales reps were negotiating deals with clients who had poor credit, leading to rejected contracts[cite: 285].
**The Solution:**
* [cite_start]**HTTP Callout (GET):** Connects Salesforce to an external banking API via **External Services**[cite: 297].
* **Automation:** Triggered instantly when an Opportunity reaches "Negotiation," fetching the credit score without code[cite: 289].
* [cite_start]**Impact:** Reduces the credit check cycle from days to seconds[cite: 296].

### 🎥 [Watch the Video Demo](https://drive.google.com/file/d/1a12sz3d75qFqJhTP-zynUyzGtTZw3g6m/view?usp=sharing)

---
[Return to Home](./)
