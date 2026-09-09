# Project Governance, RACI & Escalation Model

> **Purpose:** Define who is responsible, who approves, at what level decisions are made, and when escalation is required.  
> **Applies alongside:** `project_management_operating_model.md`  
> **Status:** Baseline Draft  
> **Version:** 1.0.0  
> **Date:** 2026-09-08

---

## 1. Governance Principles

1. Each decision has **only one Accountable owner** at any given time.
2. `Accountable` does not mean the person who directly executes the task.
3. Governance roles, personnel job titles, and system permissions are three separate layers.
4. Individuals holding multiple roles must be explicitly declared; this does not compromise the separation of duties.
5. Requesters shall not self-approve changes that affect their own interests or KPIs.
6. Approvals must be based on artifacts/evidence, not merely UI status.
7. Delegation must include scope, validity duration, and an audit trail.
8. AI / OPAgent does not hold `A` or `R` roles; AI only generates proposals and evidence.

---

## 2. Role Directory

| Code | Role | Primary Responsibility | Not Default Accountable For |
| :--- | :--- | :--- | :--- |
| **PB** | Portfolio Board / Steering Committee | Investment prioritization, funding allocation, stopping or pivoting major initiatives | Daily task coordination |
| **SP** | Project Sponsor | Business case, sponsorship, decision exceeding tolerance, and closure acceptance | Managing sprint/backlog |
| **BO** | Business Owner / Product Owner | Value, scope priority, acceptance, and benefit realization | Approving budget beyond delegated authority |
| **PMO** | PMO / Governance Office | Standards, assurance, portfolio reporting, coaching, and audit | Operating projects on behalf of PM |
| **PGM** | Program Manager | Inter-project benefits and dependencies | Detailed management of every task |
| **PM** | Project Manager | Planning, baselining, RAID, change control, forecasting, and delivery coordination | Owning business benefits |
| **SM** | Scrum Master / Flow Facilitator | Process efficiency, impediment removal, Scrum/Kanban coaching | HR evaluations, owning scope or budget |
| **TL** | Team/Technical Lead | Execution solution, estimation, technical quality, and team technical capability | Approving business scope |
| **TM** | Team Member / Contributor | Execution, status updates, evidence submission, blocker alerts | Self-confirming final acceptance |
| **QA** | QA/Test Lead | Test strategy, quality evidence, and release recommendation | Accepting business outcome |
| **FIN** | Finance/Commercial | Funding control, cost validation, invoice/contract checks | Product priority ranking |
| **HR** | HR/People Operations | Evaluation policy, calibration, privacy, and HRM export | Modifying source task telemetry |
| **WA** | Workspace/System Admin | Permission configuration, integration, and technical operations | Approving business decisions or KPIs |

### 2.1 Multi-Role Assignment Rules

- Startups may assign `SP + BO` or `PM + TL` to a single individual; this must be documented in the Governance Profile.
- `PM + SM` dual role is recommended only when the team clearly understands the conflict between delivery accountability and process coaching.
- `HR`, `Direct Manager`, and `Employee` must not be the same person at the step of approving their own evaluation score.
- `WA` holds technical privileges and is not automatically granted rights to read detailed salary/KPI data.

---

## 3. Lifecycle RACI

**Legend:** 
- `R` — Responsible (execution); 
- `A` — Accountable (ultimate ownership); 
- `C` — Consulted; 
- `I` — Informed; 
- `—` — Not applicable / optional.

| Activity | PB | SP | BO | PMO | PGM | PM | TL/TM | QA | FIN |
| :--- | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| Proposal intake & screening | A | C | R | R | C | I | — | — | C |
| Business case & funding approval | A | R | C | C | C | I | — | — | C |
| Assigning Sponsor and PM | I | A | C | R | C | I | — | — | — |
| Developing Project Charter | I | A | C | C | C | R | C | — | C |
| Selecting methodology / governance profile | I | A | C | C | C | R | C | C | — |
| Establishing scope/WBS & acceptance plan | I | C | A | C | C | R | R | C | C |
| Establishing schedule/resource/cost baseline | I | A | C | C | C | R | R | C | C |
| Approving Gate G3 | I | A | C | C | C | R | I | C | C |
| Project execution & forecasting | I | C | C | C | C | A/R | R | C | C |
| Managing cross-project dependencies | I | C | C | C | A/R | R | C | — | — |
| Quality verification | I | I | C | C | I | C | R | A/R | — |
| Business acceptance | I | C | A/R | I | I | C | I | C | — |
| Project closure | I | A | C | C | C | R | I | C | C |
| Benefit review | C | C | A/R | C | R | I | — | — | C |

### 3.1 HR KPI RACI Matrix

| Activity | Direct Manager | Employee | HR | Data Owner | PM/Delivery Lead | System Admin |
| :--- | :---: | :---: | :---: | :---: | :---: | :---: |
| Define metric contract | C | C | A | R | C | I |
| Validate data source | C | I | C | A/R | C | C |
| Automated score calculation | I | I | A | C | I | R |
| Explain anomaly / data quality | C | C | A | R | C | C |
| Review evaluation period score | A/R | C | C | C | C | I |
| Submit dispute / grievance | C | A/R | I | C | I | — |
| Resolve dispute / grievance | C | C | A | C | C | I |
| Calibration | R | I | A | C | C | — |
| Approve final score | R | I | A | C | I | — |
| Export to HRM | I | I | A | C | — | R |

Automatically calculated scores do not imply automatic approval. HRM receives scores only in `Approved` status.

---

## 4. Decision Rights

| Decision | Within Tolerance | Exceeding Tolerance | Mandatory Evidence |
| :--- | :--- | :--- | :--- |
| Adjust task plan without changing baseline milestones | PM/TL per delegated rights | Sponsor if impacting milestones | Task/dependency impact |
| Modify baselined scope | PM if within delegated tolerance | Sponsor / Change Control Board; PB if exceeding funding envelope | Change Request and impact analysis |
| Utilize management reserve | PM per threshold | Sponsor / Finance / PB per threshold | Cost forecast and approval |
| Accept residual risk | PM for Low/Medium | Sponsor for High; PB / Security authority for Critical | Risk assessment and response |
| Waive defect | BO + QA per release policy | Sponsor or risk authority for high severity | Defect record, impact, and expiry |
| Pause project | Sponsor within funding envelope | PB if impacting major portfolio / contract | Issue/risk, options, and transition plan |
| Cancel project | Sponsor proposes | PB decides | Updated business case and closure impact |
| Override KPI | Direct Manager proposes with rationale | HR / Calibration authority approves | Evidence, delta, and audit trail |
| Export KPI to HRM | HR post-approval | Export of Draft/Disputed prohibited | Approved cycle and export manifest |

---

## 5. Tolerances

Tolerance is the threshold delegated by higher authorities to subordinates. Each project must configure tolerance across six dimensions:

- **Time:** Milestone/end date variance.
- **Cost:** Budget or forecast at completion variance.
- **Scope:** Extent of deliverable/requirement changes.
- **Quality:** Defect, acceptance, or service thresholds.
- **Risk:** Residual exposure and risk appetite.
- **Benefit:** Variance in expected outcome/ROI.

### 5.1 Configuration Template

| Dimension | Baseline | Lower/Upper Tolerance | Measurement | Escalation Owner |
| :--- | :--- | :--- | :--- | :--- |
| Time | Approved finish date | Per Governance Profile | Forecast finish variance | Sponsor |
| Cost | Budget at Completion | Per funding policy | EAC vs BAC | Sponsor / Finance |
| Scope | Approved scope baseline | Change category / impact | Approved vs requested scope | BO / Sponsor |
| Quality | Acceptance / DoD targets | Per severity / SLA | Open defects and test evidence | BO / QA |
| Risk | Risk appetite | Exposure threshold | Probability × impact or approved model | Sponsor / Risk authority |
| Benefit | Business case target | Benefit range | Actual / forecast outcome | BO / PB |

A single default threshold shall not be applied across all industries or projects. Templates may suggest initial values, but the Sponsor must confirm prior to G3.

---

## 6. Escalation Model

### 6.1 Escalation Tiers

| Level | Condition | Example | Action |
| :--- | :--- | :--- | :--- |
| **E1 — Team** | Within tolerance, resolvable within team | Blocker task, short-term missing info | TL/SM coordinates and records actions |
| **E2 — Project** | Risk of milestone impact or requires PM decision | Dependency likely delayed, WIP bottleneck | PM formulates corrective action & forecast |
| **E3 — Sponsor/Program** | Tolerance breached or forecasted breach | Scope/cost/time breach, High risk | Exception Report & Sponsor/PGM decision |
| **E4 — Portfolio/Crisis** | Strategic, legal, safety, data, or project viability impact | Critical security incident, funding failure, regulatory breach | Triggers crisis process & PB/risk authority |

### 6.2 Default Target Response Times

The targets below are **suggested configuration baselines**, not mandatory SLAs for all organizations:

| Tier | Acknowledge Target | Decision / Update Target | Channel |
| :--- | :--- | :--- | :--- |
| E1 | Within business day | Prior to next daily coordination | Board / internal chat |
| E2 | 4 business hours | 1 business day | Project alert + action record |
| E3 | 1 business hour | 4 business hours or Sponsor-confirmed time | Exception notification |
| E4 | Immediate | Per crisis/incident policy | Paging + crisis channel |

Security, safety, legal, and privacy incidents must follow specialized incident policies if those policies are stricter.

### 6.3 Escalation Content Requirements

A valid escalation must include:

1. Issue and discovery timestamp.
2. Affected baseline / tolerance.
3. Current impact and forecast.
4. Containment measures executed.
5. Evaluated options and trade-offs.
6. Owner's recommendation.
7. Decision-maker and decision deadline.

Lack of a complete solution is not a reason to delay E3/E4 reporting.

---

## 7. Change Control Board

CCB is not required to be a permanent standing committee. Composition is selected based on change type:

- Sponsor: chairs decision.
- Business Owner / Product Owner: value and priority.
- PM: overall impact and recommendation.
- TL / Architect: feasibility and technical impact.
- QA / Security / Legal: when change impacts corresponding domain.
- Finance / Commercial: when impacting budget, pricing, or contracts.
- PMO: assurance and policy.

CCB must record `Approve`, `Reject`, `Defer`, or `Request More Information`; Change Requests must not be left in an ambiguous state.

---

## 8. Separation of Duties and Conflict of Interest

The following actions require at least two independent actors:

- Creating and approving sensitive API credentials / integrations.
- Proposing and approving KPI overrides.
- Approving scores and exporting to payroll.
- Creating payment / invoice data and confirming financial closure.
- Proposing and approving waivers for Critical defects / risks.

If organizational scale lacks sufficient personnel, exceptions must be documented by Sponsor/HR, with expiration and post-review required.

---

## 9. Mapping Roles to System Capabilities

| Capability | Default Business Role | Condition |
| :--- | :--- | :--- |
| Create project | PM / PMO | Within assigned workspace and portfolio |
| Approve project / gate | Sponsor / PB | Has approval assignment |
| Modify baseline | PM | Creates new version; overwrite prohibited |
| Approve scope / change | BO / SP / CCB | Per decision threshold |
| View task | Project participant / guest | Per project membership |
| View individual KPI | Employee, Direct Manager, appropriate HR | Least privilege |
| Modify metric definition | Data Owner / HR governance | Versioned change and effective date |
| Override KPI | Direct Manager proposes, HR approves | Rationale / evidence mandatory |
| Export HRM | HR integration operator | Score cycle in Approved state |
| Manage integration secret | Authorized WA | No default access to business data |

Rights must be enforced server-side; hiding UI buttons is not access control.

---

## 10. Governance Audit

PMO or governance owner periodically audits:

- Every project has a clear Sponsor, PM, and Business Owner.
- No gate decision lacks evidence/approver.
- No baseline has been overwritten.
- E3/E4 escalations are closed with decision and actions.
- Delegations have not expired and remain within scope.
- KPI override / HRM export complies with separation of duties.
- Guest and departed user accounts have had permissions revoked.
- Governance Profile remains appropriate when scope/risk changes.
