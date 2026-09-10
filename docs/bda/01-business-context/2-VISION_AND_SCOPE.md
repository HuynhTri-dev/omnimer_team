# Product Vision & Scope Document
**Project Name:** OmniMer Enterprise PMIS  
**Date:** 2026-09-09  
**Status:** Baseline  
**Version:** 2.0.0  

---

## 1. Business Need & Core Philosophy (Slogan)

### 1.1 The Problem
Many organizations suffer from disconnected project execution where:
- **"Vibe Coding" & Ambiguity:** Development teams execute tasks blindly without understanding the broader project intent. Tasks are vague, leading to assumptions, missed edge cases, and technical debt.
- **Siloed Communication:** Knowledge exists only in the minds of specific individuals. Handover is often just a transfer of source code, forcing newcomers to reverse-engineer business logic.
- **Blind-Spot Governance:** Leadership and PMs lack a clear, real-time understanding of where the project is heading, where the bottlenecks are, and whether the team's daily efforts align with the strategic goals.

### 1.2 The OmniMer Philosophy
OmniMer is built on a single, uncompromising philosophy:
> *"Quản lý task, giao tiếp và tài liệu đội ngũ hiệu quả. Quản trị chiến lược cho Ban Lãnh đạo. Một đội ngũ toàn diện nơi ai cũng nắm được ý của nhau, không nhắm mắt làm bừa. Không có task mơ hồ. Lãnh đạo luôn nắm rõ luồng và biết team đang đi đâu."*
> 
> *(Efficient task, communication, and documentation management. Strategic governance for leadership. A comprehensive team where everyone understands the shared intent, not working blindly. No ambiguous tasks. Leadership always understands the workflow and knows where the team is heading.)*

## 2. Product Vision Statement

**For** CEOs, Portfolio Managers, and Project Teams  
**Who** struggle with disconnected execution, opaque project health, and poor documentation  
**The OmniMer PMIS** is an Enterprise Project Management Information System  
**That** enforces end-to-end traceability from strategic objectives down to individual code commits, paired with visual management-by-exception dashboards.  
**Unlike** basic task trackers (e.g., Trello, standard Jira) that just move tickets across a board without enforcing business logic,  
**Our product** guarantees that no task is ambiguous, no project is handed over without documentation, and leadership has a real-time, one-glance RAG dashboard to govern risk, resources, and changes strategically.

## 3. Major Features (In Scope)

OmniMer will provide the following core capabilities to enforce its philosophy:

1. **End-to-End Traceability Engine:**
   - Enforces strict linkage: Objective → Business Requirement (BR) → Functional Requirement (FR) → User Story (US) → Test Case.
   - Rejects "orphan tasks" (tasks not linked to a business requirement) to prevent vibe coding.

2. **Mandatory Handover Quality Gates:**
   - Automated checklist enforcing the completion of all 18 mandatory documentation artifacts before a project phase can transition or be handed over.
   - Blocks transitioning if documentation quality is sub-standard.

3. **Strategic Leadership Dashboards (Management by Exception):**
   - **Risk Heatmap:** Single-glance RAG (Red-Amber-Green) composite scores for portfolio risk.
   - **Resource Capacity:** Conflict detection highlighting over-allocated resources (e.g., >100% capacity) and single points of failure (Bus Factor).
   - **Financial EVM:** Burn rate and Schedule/Cost Performance Index (SPI/CPI) tracking.

4. **Change Control Board (CCB) Workflow:**
   - Formal Impact Assessment process to prevent scope creep.
   - Proportional approval authority matrix based on change magnitude (PM vs Sponsor vs Portfolio Board).

5. **Anti-Gaming Metric Contracts:**
   - Hardcoded mathematical formulas for KPIs to prevent data manipulation (e.g., measuring cycle time vs raw commit counts).

## 4. Out of Scope

To maintain focus on project management and governance, OmniMer will **NOT** include:
1. **Source Code Hosting:** It is not a replacement for GitHub, GitLab, or Bitbucket (but will integrate with them for traceability).
2. **HR Payroll & Benefits Administration:** It tracks capacity and allocation but does not handle payroll, taxes, or compensation logic.
3. **Internal Instant Messaging:** It tracks formal communication, decisions, and escalation, but is not a real-time chat replacement for Slack or MS Teams.
4. **General Accounting System:** It tracks project budgets (EVM) but is not a general ledger/ERP accounting software.

## 5. Release Strategy & Boundaries

- **Release 1 (Foundation):** Traceability Engine, Core Task Management, and Mandatory Handover Gates. (Ensures the team understands the intent and stops vibe coding).
- **Release 2 (Governance):** Visual Leadership Dashboards (RAG Heatmaps) and Resource Capacity Management. (Ensures leadership knows where the team is going).
- **Release 3 (Control):** Financial EVM, CCB Workflow, and Advanced KPI Metric Contracts. (Ensures strict anti-gaming and cost control).
