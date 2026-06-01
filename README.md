# Incident Response Interface
### Designing a PICERL-Based IR Management Tool for CIRT Teams

🔵 **[Live App → logicalcoders--incident-response-interface.retool.app](https://logicalcoders--incident-response-interface.retool.app/)**

**Role:** Digital Product Designer (UX Research · Interaction Design · Prototype)  
**Tools:** Adobe XD · Miro · Excel · Retool · Supabase  
**Timeline:** 9 weeks  
**Target Companies:** Palo Alto Networks · CrowdStrike · SecOps Startups · MSSP Platforms  

---

## The Problem

When a security incident occurs, time is the most critical variable. Every minute between detection and containment is a minute the attacker is still moving through the environment.

Yet the tools most CIRT teams use to manage incident response are not purpose-built for the job:

- **Ticketing systems** (Jira, ServiceNow) designed for IT operations — not security incident workflows
- **Spreadsheets** with manually tracked status fields and no real-time collaboration
- **Standalone SIEM alerts** with no case management or playbook integration
- **Email chains** that create fragmented records and delay escalation

The consequence is that the **human coordination layer** of incident response — who is doing what, at which phase, right now — breaks down precisely when it needs to work most reliably.

This case study documents the design of a dedicated Incident Response interface built around the **NIST PICERL lifecycle** — designed for the way CIRT teams actually work during a live incident.

> **The design goal: Give every CIRT team member a single shared view of where the incident is, what has been done, and what needs to happen next.**

---

## Domain Knowledge Foundation

This project is grounded in the NIST Computer Security Incident Handling Guide (SP 800-61) and the PICERL incident response lifecycle:

| Phase | What Happens |
|---|---|
| **P — Preparation** | IR plan, team training, tooling setup, playbook development |
| **I — Identification** | Detect and confirm the incident; classify severity |
| **C — Containment** | Stop the spread; short-term and long-term containment actions |
| **E — Eradication** | Remove root cause; close exploited vulnerabilities |
| **R — Recovery** | Restore operations; monitor for reinfection |
| **L — Lessons Learned** | Post-incident review; improve preparation for next time |

The design reflects this lifecycle at every level — from the navigation structure to the individual task card design.

---

## Research

### User Interviews

I interviewed 6 security professionals across three role types:

- **2 Incident Responders** (hands-on investigation and containment)
- **2 CIRT Team Leads** (coordination, escalation, communication)
- **2 Security Operations Managers** (oversight, reporting, stakeholder communication)

**Key findings:**

| Pain Point | Frequency |
|---|---|
| No single view of incident status visible to whole team | 6/6 |
| Difficult to track which phase the incident is in | 5/6 |
| Playbook steps not accessible during live incident | 5/6 |
| Post-incident documentation takes hours to reconstruct from notes | 6/6 |
| No automated timeline — must manually log every action | 4/6 |
| Escalation path unclear during fast-moving incidents | 4/6 |

**Most critical finding:** Every team lead described the same problem — during a live incident, they spend 30–40% of their time answering status questions from team members and management instead of directing the response. **The tool should answer those questions automatically.**

### Observational Research

I observed two tabletop exercise sessions — structured simulations of security incidents — and documented the coordination breakdowns that occurred:

1. **Phase transition confusion** — team members unsure whether the incident had moved from Identification to Containment; some continued identifying while others had already begun containing
2. **Duplicate action overlap** — two analysts performed the same containment action without knowing the other had already done it
3. **Evidence documentation lag** — actions taken during the incident were not logged until after the session, resulting in incomplete timelines
4. **Escalation hesitation** — junior analysts unsure of escalation threshold; delayed reporting by 20+ minutes

All four breakdowns became design requirements.

---

## Design Process

### Design Requirements from Research

1. Every team member must see the current incident phase in real time
2. Every action must be assigned to a named individual
3. Playbook steps must be accessible within the incident view — not in a separate document
4. The timeline must populate automatically from logged actions
5. Escalation triggers must be defined and visible before they are needed
6. Post-incident report must be auto-generated from logged data

### Information Architecture

```
INCIDENT COMMAND CENTER (Active Incident View)
├── Phase Indicator (current PICERL phase, prominent)
├── Incident Summary (classification, severity, affected assets)
├── Task Board (by phase, by assignee, by status)
├── Live Timeline (auto-populated from completed tasks)
├── Playbook Panel (phase-specific recommended actions)
└── Escalation Panel (thresholds, contacts, status)

INVESTIGATION HUB
├── Evidence Locker (artifacts, logs, screenshots, notes)
├── Asset Map (affected systems, connections, scope)
└── MITRE ATT&CK Mapping (tactic and technique tagging)

COMMUNICATIONS
├── Internal Incident Chat (timestamped, preserved)
├── Stakeholder Updates (templated, one-click send)
└── External Notification Tracker (regulators, partners)

LESSONS LEARNED CENTER
├── Auto-Generated Timeline Report
├── Findings Form (what happened, what worked, what failed)
├── Improvement Actions (assigned owners, due dates)
└── Historical Incident Library
```

### Key Design Decisions

**Decision 1: The Phase Indicator**
A persistent, prominent phase indicator at the top of every incident view — showing the current PICERL phase in large type with a visual progress bar. Every team member sees the same phase in real time. Phase transitions require deliberate confirmation from the team lead — preventing accidental phase skipping.

**Decision 2: The Task Board**
A Kanban-style task board organized by PICERL phase — not by assignee or date. Each task card shows: description, assigned analyst, status (not started / in progress / complete / blocked), and timestamp. Blocked tasks surface with a flag that immediately notifies the team lead.

**Decision 3: Inline Playbook**
Phase-specific playbook steps appear in a collapsible side panel within the incident view — not in a separate document or wiki. Analysts can mark steps complete, add notes, and flag deviations without leaving the incident context.

**Decision 4: Auto-Generated Timeline**
Every completed task, phase transition, escalation, and communication is automatically logged with a timestamp and the name of the analyst who performed it. The timeline requires no manual documentation — it builds itself during the incident.

**Decision 5: Auto-Generated Post-Incident Report**
When the incident closes, the tool generates a structured post-incident report from the logged data — incident summary, phase-by-phase timeline, actions taken, evidence collected, and a findings section for the team to complete. What previously took hours to reconstruct takes minutes to finalize.

---

## High-Fidelity Prototype — Key Screens

### Screen 1: Incident Command Center
Phase indicator bar at top (Preparation → Identification → Containment → Eradication → Recovery → Lessons Learned) with current phase highlighted. Incident severity badge. Active task count. Live elapsed time since detection. Three-panel layout: task board center, playbook right, timeline left.

### Screen 2: Task Board — Containment Phase
Tasks organized in columns: Not Started / In Progress / Complete / Blocked. Each card shows task name, assigned analyst avatar, timestamp, and status. Blocked cards display in red with escalation prompt. Team lead sees all tasks; analysts see their own queue prominently with team context visible.

### Screen 3: Evidence Locker
Drag-and-drop evidence submission. Each artifact tagged with: type (log file, screenshot, memory image, network capture), collection method, chain of custody, and associated incident phase. Evidence is timestamped and analyst-attributed automatically.

### Screen 4: Auto-Generated Post-Incident Report
Pre-populated report with incident timeline, affected assets, phase durations, actions taken, and evidence collected. Editable findings section for team input. Export to PDF in one click. Structured to meet standard incident reporting requirements.

---

## Usability Testing

### Method
Moderated usability testing with 5 participants (3 incident responders, 2 team leads) using a clickable Adobe XD prototype during a tabletop exercise simulation.

### Results

| Metric | Current Tools | Redesigned Interface |
|---|---|---|
| Time for team lead to answer "what phase are we in?" | 2–5 min (checking notes/chat) | Instant (persistent display) |
| Duplicate actions during simulation | 3 occurrences | 0 occurrences |
| Evidence documentation completeness | 60% (reconstructed after) | 98% (logged in real time) |
| Post-incident report generation time | 3–5 hours | Under 30 minutes |
| Junior analyst escalation confidence | Low (3/5 rating) | High (4.5/5 rating) |

### Feedback

> *"The phase indicator alone would change how my team communicates during an incident. Everyone would finally be looking at the same thing."*  
> — CIRT Team Lead

> *"The auto-generated report is going to save me half a day every incident. I spend more time writing about what happened than I spend fixing it."*  
> — Incident Responder, Financial Services

---

## Outcomes

| Metric | Before | After |
|---|---|---|
| Team phase alignment during incident | Low | Real-time, shared |
| Duplicate actions | Common | Eliminated by task assignment |
| Evidence documentation lag | Hours | Real-time |
| Post-incident report time | 3–5 hours | Under 30 minutes |
| Junior analyst escalation confidence | Low | Significantly improved |

---

## Reflection

**What made this project different:** I did not approach this as a generic task management problem. I approached it as a PICERL problem. The lifecycle is not just an organizing concept — it is the mental model that every trained incident responder already carries. The interface should reinforce that model, not replace it with something new.

**My unfair advantage:** I have studied incident response from the security practitioner perspective — not just as a designer observing a domain. I understand what MITRE ATT&CK tactics mean, why phase transitions matter, and what a post-incident report needs to contain for it to be useful. That knowledge shaped every design decision in this case study.

**What I would build next:** Integration with SIEM alert feeds to automatically pre-populate the incident summary and initial evidence when an alert crosses the severity threshold — reducing the manual work of incident creation during the highest-pressure moment of the response.

---

## About the Designer

**Anél Henning** — Digital Product Designer · MS Cybersecurity (Purdue Global, 2026) · BFA Graphic Design (MICA) · BS Computer Science · HIPAA Business Associate Certified · ISC2 Member · ISACA Member. Based in Tampa, FL.

[Portfolio](https://anel-henning.github.io/ux-cybersecurity-portfolio) · [GitHub](https://github.com/AnelHenning2-collab) · [Email](mailto:logicalcoders@outlook.com)
