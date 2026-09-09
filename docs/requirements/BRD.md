# Business Requirements Document (BRD)
**Project Name:** OmniMer Enterprise PMIS  
**Date:** 2026-09-09  
**Status:** Baseline  
**Version:** 2.0.0  

---

## 1. Executive Summary

Organizations face a critical disconnect between strategic intent and daily execution. Development teams often fall into the trap of "vibe coding"—implementing features based on assumptions because tasks are vague. Communication is siloed, documentation is treated as an afterthought, and leadership is left in the dark, unable to discern the true health, risks, and resource bottlenecks of the project.

**OmniMer PMIS** is designed to solve this by enforcing a strict operating philosophy:
> *"Quản lý task, giao tiếp và tài liệu đội ngũ hiệu quả. Quản trị chiến lược cho Ban Lãnh đạo. Một đội ngũ toàn diện nơi ai cũng nắm được ý của nhau, không nhắm mắt làm bừa. Không có task mơ hồ. Lãnh đạo luôn nắm rõ luồng và biết team đang đi đâu."*

This document defines the core Business Objectives (OBJ) and Business Rules (BR) that the system must satisfy to realize this philosophy.

---

## 2. Stakeholder Analysis

| Stakeholder Role | Core Need | Key Challenge |
| :--- | :--- | :--- |
| **CEO / Portfolio Manager** | Strategic governance, financial oversight | Blind spots regarding project health; unable to see cross-project resource conflicts. |
| **Project Manager / Scrum Master** | Effective task management, clear capacity planning | Scope creep; managing CCB approvals; ensuring resources aren't burned out. |
| **Developer / QA** | Clear intent, unambiguous tasks, solid documentation | "Vibe coding" due to vague tasks; impossible handovers due to missing documentation. |
| **System Administrator (PMO)** | Process compliance, traceability | Teams circumventing gates; manipulating KPI data. |

---

## 3. Business Objectives (OBJ)

These objectives define the fundamental success criteria for OmniMer. Every functional requirement must trace back to one of these OBJs.

### **OBJ-01: Eradicate "Vibe Coding" via Strict Traceability**
- **Description:** Ensure that every team member understands the overarching intent of the project and their specific tasks. No task shall be ambiguous or created in isolation.
- **Success Metric:** 100% of Development Tasks and Test Cases are linked to a validated Functional Requirement and Business Objective in the Traceability Engine.

### **OBJ-02: Mandate Documentation for Handovers**
- **Description:** Prevent the "source code only" handover anti-pattern. Guarantee effective communication and documentation for the team.
- **Success Metric:** 100% compliance with the 18-artifact Handover Checklist before any project phase transition or resource onboarding is approved.

### **OBJ-03: Provide Strategic Governance & Clear Workflow for Leadership**
- **Description:** Leadership must always know the workflow and where the team is heading without micromanaging. 
- **Success Metric:** Real-time generation of RAG Heatmaps for Risk, Resource Capacity, and Financial EVM across all portfolios.

### **OBJ-04: Enforce Controlled Change via CCB**
- **Description:** Stop silent scope creep. Any change in intent or scope must be formally assessed and approved based on proportional authority.
- **Success Metric:** 0% of major/critical changes bypass the Change Control Board (CCB) workflow.

---

## 4. High-Level Business Rules (BR)

Business Rules constrain how the business operates and dictate system behavior.

| BR ID | Rule Statement | Enforces Objective |
| :---: | :--- | :---: |
| **BR-001** | A User Story or Task cannot transition to "In Progress" unless it is explicitly linked to a parent Functional Requirement. | OBJ-01 |
| **BR-002** | The system must block the approval of Gate G4 (Handover) if the Documentation Quality Score is less than 100%. | OBJ-02 |
| **BR-003** | Any resource allocated to more than 100% capacity across concurrent projects must trigger an immediate Amber/Red conflict alert on the Leadership Dashboard. | OBJ-03 |
| **BR-004** | Change Requests (CR) that impact the budget or schedule by more than 5% must require Sponsor approval; >15% requires Portfolio Board approval. | OBJ-04 |
| **BR-005** | KPI Metrics (e.g., Velocity, Defect Escape Rate) must be calculated using locked, hardcoded formulas (Metric Contracts) that cannot be altered by project teams. | OBJ-03 |

---

## 5. Risks and Assumptions

- **Risk:** Teams may resist the strict documentation and traceability enforcement, perceiving it as overhead.
  - *Mitigation:* The system must make traceability linking and document template generation as frictionless as possible (e.g., via automation and clear UI cues).
- **Assumption:** All projects managed in OmniMer follow the standard gate lifecycle (G0-G6) defined in the Operating Model.
