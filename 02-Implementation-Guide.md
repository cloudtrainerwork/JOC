# Implementation Guide — Mission Tracker

**Operation CAJUN SHIELD · Flood Response Mission Tracking**
**Exemplar implementation package for the Plan Designer group activity**

> **EXERCISE — TRAINING USE ONLY.**
> Operation CAJUN SHIELD is notional. Every unit designation, position, name field, phone number, roster line, and figure in this document is a **placeholder** marked with square brackets — `[POSITION]`, `[NAME]`, `[DSN]`, `[CELL]` — or is modeled on publicly reported flood responses.
> **This is not an operational plan and must not be used as one.** Before any real use, every placeholder must be filled from your own authoritative sources — the unit alert roster, the current OPORD or EOP, the SEOC contact list, and your J6 communications annex — and the result must be reviewed and approved through your own process.

---

## How to use this document

This guide serves two purposes.

**For the trainer:** it is the *answer key made concrete*. Students design a mission tracking system on a worksheet; this shows what the finished staff product looks like when that design is written up properly. Hand it out at the end of the day, not the beginning — it will short-circuit the thinking if students see it first.

**For the student, afterward:** it is a **reusable template**. The structure — resources, personnel, contacts, escalation, fallback — is what any fielded system needs documented around it, whatever tool builds the system. Filling this in for a real capability is the work that turns a prototype into something a commander can rely on.

**Sections 1–3** describe the system. **Sections 4–9** are the operational wrap-around students most need practice writing: what's deployed, who's deployed, who to call, when to escalate, and what to do when it all stops working.

---

## 1. Solution overview

### 1.1 Purpose

Mission Tracker provides a single system of record for mission requests during a state-declared flood emergency. It replaces the whiteboard and shared spreadsheet currently used in the Joint Operations Center, and gives requesting parishes visibility into their own requests without calling a second channel.

### 1.2 Problem statement

> Mission requests arrive from parish emergency management on four uncoordinated channels — telephone, email, radio, and the state incident management system — and are tracked manually in the JOC. Missions are lost at shift change, requests arrive with incomplete information, duplicate tasking occurs because requesting parishes cannot see status, leadership has no current picture of committed versus available assets, and the twice-daily storyboard is compiled by hand and is stale by the time it is briefed.

### 1.3 Scope

**In scope:** mission request intake, validation, prioritization, assignment, execution tracking, and closeout. Asset and personnel status visibility. Parish-facing request submission and status lookup. Command reporting.

**Out of scope for this iteration:** logistics ordering and resupply, financial tracking and reimbursement, personnel pay actions, medical records of any kind, and any exchange of information with federal systems.

**Explicitly deferred pending authority determination:** hosting boundary and data classification, records retention schedule, and any handling of personally identifiable information belonging to rescued civilians. See §9.

### 1.4 Operating assumptions

| # | Assumption | If it proves false |
|---|---|---|
| 1 | The JOC has reliable network connectivity | Contingency mode, §7 |
| 2 | Deployed task forces have intermittent cellular data at best | Field app must queue offline; already a requirement |
| 3 | Parish emergency managers have commercial internet | They fall back to voice; the watch enters on their behalf |
| 4 | Requests are validated by the JOC before tasking | Direct-to-unit requests bypass the record and must be back-entered |
| 5 | Personnel and asset data is maintained by units, not the JOC | Data quality depends on unit discipline; build the reminder flow |

---

## 2. User roles and access

| Role | Interface | Can do | Must not see |
|---|---|---|---|
| **JOC Watch NCO** | Model-driven app | Create, validate, and update any mission; update asset status | Personnel PII beyond accountability status |
| **J3 Battle Captain** | Model-driven app + dashboards | All watch functions, plus prioritize, assign to units, escalate, cancel | — |
| **Task Force Commander** | Canvas app, mobile, offline-capable | View missions assigned to their unit; update status, results, and remarks; update their own assets | Missions assigned to other units |
| **Parish Emergency Manager** | Power Pages portal, external | Submit requests for their own parish; view status of their own parish's requests | Other parishes' requests; unit designations; asset details; any personnel data |
| **JTF Commander** | Dashboard, read-only | Everything, aggregated | — |
| **System administrator** \* | Admin | Configuration, security roles, environment | — |

\* The system administrator is a platform role, not one of the five designed user roles. Students define five; this table adds the administrator because a fielded system needs one.

**Access decisions to confirm before fielding:**

- Parish visibility is scoped to the **submitting parish only**. Confirm whether a parish may see that a mission is underway without seeing which unit is executing it. *(Recommended: yes — status without unit designation.)*
- Whether task force commanders may see the **full asset picture** or only their own.
- Who may **cancel** a mission versus mark it **Unable**. *(Recommended: Battle Captain and above for cancel; executing unit may mark Unable with a mandatory reason.)*
- Whether the **personnel accountability view** is visible below JOC level.

---

## 3. Data model

### 3.1 Tables

**Mission Request** — the system of record. Aligned to ICS 213 RR blocks so paper fallback and digital entry share the same fields.

| Column | Type | Notes |
|---|---|---|
| Mission Number | Auto | Format `[OPERATION]-[PARISH]-nnnn` |
| Requesting Parish | Lookup → Parish | |
| Requesting Official | Text | Name and position |
| Callback Number | Phone | |
| Date/Time Received | DateTime | Starts the response clock |
| Mission Type | Choice | See §3.2 |
| Priority | Choice | Immediate / Priority / Routine |
| Description | Multi-line text | |
| Location — Grid | Text | MGRS |
| Location — Address | Text | Street address if available |
| Number of Persons Affected | Number | |
| Water Depth at Access | Text | |
| Access Route / Road Status | Multi-line text | |
| Medical Needs | Yes/No + text | |
| Animals on Site | Yes/No + text | |
| Requested Arrival | DateTime | |
| Status | Choice | See §3.2 |
| Validated By | Lookup → User | |
| Assigned Unit | Lookup → Unit | |
| Assigned Assets | Multi-lookup → Asset | |
| Results | Multi-line text | Persons, pets, livestock, commodities |
| Date/Time Complete | DateTime | Stops the response clock |
| Remarks | Multi-line text | |

**Parish** — parish name, emergency management POC, phone, EOC location, declaration status, assigned liaison.

**Unit / Task Force** — unit designation, parent command, commander, current location, duty status, assigned strength, higher headquarters.

**Asset** — asset type, bumper number, owning unit, capability (fording depth, passenger capacity, lift), status, current location, operator assigned.

**Personnel** — name, rank, unit, duty status, report date, projected release date, accountability status, emergency contact. *(See §9 — this table carries PII and its handling must be determined before any real use.)*

### 3.2 Choice fields

| Field | Values |
|---|---|
| **Priority** | **Immediate** — life safety; **Priority** — property and essential services; **Routine** — all other |
| **Status** | Received → Validated → Assigned → En Route → On Scene → Complete · *Unable* · *Cancelled* |
| **Mission Type** | SAR Boat · SAR High-Water Vehicle · Aviation Hoist / MEDEVAC · Route Clearance · Levee and Sandbag Operations · Commodity Distribution (POD) · Shelter Support · Security and Traffic Control · Power and Generator Support · Communications Support |
| **Asset Status** | Available · Committed · En Route · Deadlined |
| **Duty Status** | State Active Duty · Title 32 · Title 10 |
| **Accountability** | Present · Accounted For · Not Accounted For · Released |

### 3.3 Relationships

- A **Mission Request** belongs to one **Parish** and is assigned to one **Unit**
- A **Mission Request** may commit many **Assets**
- A **Unit** owns many **Assets** and many **Personnel**

### 3.4 Automated flows

The escalation matrix in §6.5 refers to these by number.

| # | Trigger | Action |
|---|---|---|
| **Flow 1** | A mission request is submitted through the parish portal | Notify JOC watch, assign a mission number, send an acknowledgement to the requesting parish |
| **Flow 2** | A mission is validated and assigned to a unit | Notify that unit's commander and the requesting parish |
| **Flow 3** | Mission status changes to Complete | Notify the requesting parish; roll results into the running totals |
| **Flow 4** | An Immediate mission is not acknowledged or assigned within threshold | Escalate per §6.5 — Battle Captain at 10 min, Operations SGM at 20 min, JTF Commander at 30 min |
| **Flow 5** | An active mission has had no status update for 4 hours | Flag stale; notify the assigned unit commander, then the Battle Captain |
| **Flow 6** | Shift change at 0600 and 1800 | Generate the handover packet — open missions, committed assets, stale missions |
| **Flow 7** | An asset status changes to Deadlined | Notify support operations; flag every mission that asset is committed to |
| **Flow 8** | A mission is marked Unable | Notify the Battle Captain for a re-task decision |
| **Flow 9** | An individual is reported Not Accounted For | Flag the record and prompt an immediate voice report — see the note in §6.5 |

### 3.5 Business rules

1. Status may not move to **Assigned** without an assigned unit.
2. Status may not move to **Complete** without a Date/Time Complete and a Results entry.
3. **Unable** requires a mandatory reason in Remarks.
4. Priority **Immediate** requires a grid location or an address before validation.
5. An asset set to **Deadlined** must not be committed to a new mission.

---

## 4. Resources deployed

> **Placeholder table.** Quantities are notional and sized on publicly reported Louisiana flood responses. Replace with the actual task organization from the operations order.

### 4.1 Resource summary

| Capability | Type / description | Qty on hand | Committed | Available | Owning unit |
|---|---|---|---|---|---|
| High-water vehicle | LMTV / FMTV, fording capable | `[QTY]` | `[QTY]` | `[QTY]` | `[UNIT]` |
| Rescue boat | Flat-bottom / Zodiac, shallow draft | `[QTY]` | `[QTY]` | `[QTY]` | `[UNIT]` |
| Rotary wing, hoist capable | Utility helicopter with hoist | `[QTY]` | `[QTY]` | `[QTY]` | `[UNIT]` |
| Rotary wing, MEDEVAC | Air ambulance | `[QTY]` | `[QTY]` | `[QTY]` | `[UNIT]` |
| Sandbag filling machine | | `[QTY]` | `[QTY]` | `[QTY]` | `[UNIT]` |
| Generator | `[KW RATING]` | `[QTY]` | `[QTY]` | `[QTY]` | `[UNIT]` |
| Light set | | `[QTY]` | `[QTY]` | `[QTY]` | `[UNIT]` |
| Heavy equipment | Dozer / loader / dump truck | `[QTY]` | `[QTY]` | `[QTY]` | `[UNIT]` |
| Water purification | | `[QTY]` | `[QTY]` | `[QTY]` | `[UNIT]` |
| Tactical communications | Retrans / satellite / COW | `[QTY]` | `[QTY]` | `[QTY]` | `[UNIT]` |

### 4.2 Asset record — required fields

Every asset in the system carries:

| Field | Example | Why it matters |
|---|---|---|
| Asset type | `[TYPE]` | Drives which mission types it can fill |
| Bumper number | `[BUMPER]` | Unique identity for tasking and accountability |
| Owning unit | `[UNIT]` | Who releases it |
| Capability | Fording depth `[X]` in · `[N]` pax | Determines suitability before tasking |
| Status | Available / Committed / En Route / Deadlined | The Commander's question |
| Current location | `[GRID]` | Time to mission |
| Operator assigned | `[POSITION]` | Links asset to personnel accountability |

### 4.3 Resource typing note

For any resource that may be requested through, or offered to, mutual aid or a state emergency operations center, record the **NIMS resource type** alongside the local description. Typing is what makes a request legible to somebody outside your organization, and it is the difference between "send a boat" and a request another state can actually fill.

> **Design exercise for students:** where does resource type live in your data model — a column on Asset, or a separate lookup table? Defend the choice.

---

## 5. Personnel deployed

> **Placeholder.** No real roster data. Personnel strength figures are notional.

### 5.1 Strength summary

| Unit | Parent command | Mission | Assigned strength | Present | Duty status | Location |
|---|---|---|---|---|---|---|
| `[TASK FORCE]` | `[HIGHER HQ]` | `[PRIMARY MISSION]` | `[QTY]` | `[QTY]` | `[SAD / T32]` | `[PARISH]` |
| `[TASK FORCE]` | `[HIGHER HQ]` | `[PRIMARY MISSION]` | `[QTY]` | `[QTY]` | `[SAD / T32]` | `[PARISH]` |
| `[TASK FORCE]` | `[HIGHER HQ]` | `[PRIMARY MISSION]` | `[QTY]` | `[QTY]` | `[SAD / T32]` | `[PARISH]` |
| `[JOC / HQ ELEMENT]` | `[HIGHER HQ]` | Command and control | `[QTY]` | `[QTY]` | `[SAD / T32]` | `[LOCATION]` |
| **Total** | | | `[QTY]` | `[QTY]` | | |

### 5.2 Duty status — why the system tracks it

Duty status is not administrative trivia; it changes what a Guardsman may lawfully do and who pays for it. It belongs in the data model because reporting on it is a real command requirement.

| Status | Commanded by | Funded by | Domestic note |
|---|---|---|---|
| **State Active Duty (SAD)** | Governor | State | Posse Comitatus does not apply, so law enforcement support is permissible |
| **Title 32** | Governor | Federal | Federally funded, state controlled |
| **Title 10** | President | Federal | Federal control |

> **Discussion point for the AAR:** a mission requiring traffic control or site security may be executable under one status and not another. Should the system flag a mission type that is inconsistent with the assigned unit's duty status? That is a real business rule, and most teams never think of it.

### 5.3 Accountability

Accountability is a **safety function**, not a reporting function. The system exists in part to answer one question: *did everybody who went out come back?*

| Requirement | Standard |
|---|---|
| Accountability reporting frequency | `[EVERY N HOURS]`, and at every shift change |
| Trigger for immediate report | Any status change to a mission involving water entry or aviation |
| Threshold for command notification | Any individual **Not Accounted For** at `[N]` minutes |
| Responsible position | `[POSITION]` at unit level; `[POSITION]` at JOC |

---

## 6. Contact roster and escalation

> **Placeholder roster.** Positions only. Fill from the current alert roster and the SEOC contact list. Verify every line before an operation, not during one.

### 6.1 Joint task force — internal

| Position | Name | DSN / office | Cell | Email | Alternate |
|---|---|---|---|---|---|
| JTF Commander | `[NAME]` | `[DSN]` | `[CELL]` | `[EMAIL]` | `[POSITION]` |
| JTF Deputy Commander | `[NAME]` | `[DSN]` | `[CELL]` | `[EMAIL]` | `[POSITION]` |
| J3 Operations Officer | `[NAME]` | `[DSN]` | `[CELL]` | `[EMAIL]` | `[POSITION]` |
| J3 Operations SGM | `[NAME]` | `[DSN]` | `[CELL]` | `[EMAIL]` | `[POSITION]` |
| J3 Battle Captain — day | `[NAME]` | `[DSN]` | `[CELL]` | `[EMAIL]` | `[POSITION]` |
| J3 Battle Captain — night | `[NAME]` | `[DSN]` | `[CELL]` | `[EMAIL]` | `[POSITION]` |
| JOC Watch NCO — day | `[NAME]` | `[DSN]` | `[CELL]` | `[EMAIL]` | `[POSITION]` |
| JOC Watch NCO — night | `[NAME]` | `[DSN]` | `[CELL]` | `[EMAIL]` | `[POSITION]` |
| J1 Personnel | `[NAME]` | `[DSN]` | `[CELL]` | `[EMAIL]` | `[POSITION]` |
| J2 Intelligence | `[NAME]` | `[DSN]` | `[CELL]` | `[EMAIL]` | `[POSITION]` |
| J4 Logistics / SPO | `[NAME]` | `[DSN]` | `[CELL]` | `[EMAIL]` | `[POSITION]` |
| J6 Communications | `[NAME]` | `[DSN]` | `[CELL]` | `[EMAIL]` | `[POSITION]` |
| Public Affairs | `[NAME]` | `[DSN]` | `[CELL]` | `[EMAIL]` | `[POSITION]` |
| Safety Officer | `[NAME]` | `[DSN]` | `[CELL]` | `[EMAIL]` | `[POSITION]` |
| Judge Advocate | `[NAME]` | `[DSN]` | `[CELL]` | `[EMAIL]` | `[POSITION]` |

### 6.2 Subordinate task forces

| Task force | Commander | CSM / 1SG | Cell | Radio call sign | Operating area |
|---|---|---|---|---|---|
| `[TASK FORCE]` | `[NAME]` | `[NAME]` | `[CELL]` | `[CALL SIGN]` | `[PARISHES]` |
| `[TASK FORCE]` | `[NAME]` | `[NAME]` | `[CELL]` | `[CALL SIGN]` | `[PARISHES]` |
| `[TASK FORCE]` | `[NAME]` | `[NAME]` | `[CELL]` | `[CALL SIGN]` | `[PARISHES]` |

### 6.3 State and external

| Organization | Position / desk | POC | Phone | Email | Notes |
|---|---|---|---|---|---|
| State EOC | `[DESK]` | `[NAME]` | `[PHONE]` | `[EMAIL]` | Primary state coordination |
| ESF-16 Military Support desk | `[POSITION]` | `[NAME]` | `[PHONE]` | `[EMAIL]` | Guard-led ESF |
| ESF-9 Search and Rescue | `[POSITION]` | `[NAME]` | `[PHONE]` | `[EMAIL]` | State SAR lead — Dept of Wildlife and Fisheries |
| ESF-6 Mass Care / sheltering | `[POSITION]` | `[NAME]` | `[PHONE]` | `[EMAIL]` | Shelter support tasking |
| ESF-8 Public Health / Medical | `[POSITION]` | `[NAME]` | `[PHONE]` | `[EMAIL]` | Medical missions |
| ESF-1 Transportation | `[POSITION]` | `[NAME]` | `[PHONE]` | `[EMAIL]` | Route status |
| ESF-13 Public Safety | `[POSITION]` | `[NAME]` | `[PHONE]` | `[EMAIL]` | Law enforcement coordination |

> **Note on ESF structure:** in Louisiana, **ESF-16 Military Support is led by the Louisiana National Guard**, and ESF-16's role is to support all other ESF activities. That is why mission requests reach the JOC from many different ESF desks rather than only one — a point worth making to students, because it explains why the *Mission Type* choice field has to be that broad.

### 6.4 Parish emergency management

| Parish | OHSEP Director | Phone | 24-hour line | EOC location | Liaison assigned |
|---|---|---|---|---|---|
| `[PARISH]` | `[NAME]` | `[PHONE]` | `[PHONE]` | `[LOCATION]` | `[POSITION]` |
| `[PARISH]` | `[NAME]` | `[PHONE]` | `[PHONE]` | `[LOCATION]` | `[POSITION]` |
| `[PARISH]` | `[NAME]` | `[PHONE]` | `[PHONE]` | `[LOCATION]` | `[POSITION]` |
| `[PARISH]` | `[NAME]` | `[PHONE]` | `[PHONE]` | `[LOCATION]` | `[POSITION]` |
| `[PARISH]` | `[NAME]` | `[PHONE]` | `[PHONE]` | `[LOCATION]` | `[POSITION]` |
| `[PARISH]` | `[NAME]` | `[PHONE]` | `[PHONE]` | `[LOCATION]` | `[POSITION]` |
| `[PARISH]` | `[NAME]` | `[PHONE]` | `[PHONE]` | `[LOCATION]` | `[POSITION]` |

### 6.5 Mission escalation matrix

This is the escalation the **system enforces** through automated flows. Times are notional — set and defend your own.

| Condition | T + | Action | Notify | System behavior |
|---|---|---|---|---|
| **Immediate** mission received | 0 | Auto-acknowledge to parish with mission number | JOC Watch NCO | Flow 1 |
| **Immediate** not acknowledged | 10 min | Page duty officer | J3 Battle Captain | Flow 4 |
| **Immediate** not assigned | 20 min | Voice notification | J3 Operations SGM | Flow 4 |
| **Immediate** not assigned | 30 min | Voice notification, log as reportable delay | JTF Commander | Flow 4 |
| **Priority** not assigned | 2 hr | Notify | J3 Battle Captain | Flow 4 |
| **Routine** not assigned | 12 hr | Notify | JOC Watch NCO | Flow 4 |
| Any active mission, no status update | 4 hr | Flag stale | Assigned TF Commander, then Battle Captain | Flow 5 |
| Mission marked **Unable** | Immediate | Review and re-task decision | J3 Battle Captain | Flow 8 |
| Asset set to **Deadlined** | Immediate | Flag all missions committed to that asset | J4 / SPO, affected TF Commander | Flow 7 |
| Individual **Not Accounted For** | `[N]` min | Immediate voice report | TF Commander → JOC → JTF Commander | Flow 9 |
| Injury or vehicle mishap on mission | Immediate | Serious incident procedure, outside this system | Safety Officer, JTF Commander | Manual — see note |

> **Important:** a serious incident report is **not** an application workflow. The system may flag it and record that it occurred, but the report itself goes through the established chain by voice. Building a life-safety report into a software notification with no human confirmation is a design error worth naming to students explicitly.

### 6.6 Escalation of the escalation

If an escalation cannot be delivered — the position is unreachable, the network is down, the phone is dead — the fallback is:

1. Attempt the **alternate** listed for that position in §6.1
2. Attempt **radio** on the primary operations net
3. Notify the **next position up** in the chain and state that you could not reach the intended recipient
4. Log the failed attempt in the mission record's Remarks with time and method

> **Design exercise:** should the system detect a failed notification and automatically take step 3? What are the risks of it doing so?

---

## 7. Fallback plan — degraded operations (PACE)

The network will fail. Plan for it rather than discovering it.

### 7.1 The PACE plan

| | Level | Method | Who acts | Data capture |
|---|---|---|---|---|
| **P** | Primary | Mission Tracker app over state network or cellular data | All roles, normal use | Direct to the system |
| **A** | Alternate | Parish portal over any commercial internet; JOC works from the model-driven app on any connection | Parish EM, JOC | Direct to the system |
| **C** | Contingency | Voice or radio to the JOC | Requester by voice; **Watch NCO enters on their behalf** | Watch NCO enters; record flagged *entered by proxy* |
| **E** | Emergency | Paper **ICS 213 RR** passed by runner or radio relay | Requester and unit on paper | Held on paper; back-entered on restoration |

### 7.2 Trigger to change level

| Move to | When |
|---|---|
| **Alternate** | State network unavailable but commercial internet reachable |
| **Contingency** | Requester has no data connectivity but has voice or radio |
| **Emergency** | JOC has no connectivity, or the system is unavailable for more than `[N]` minutes |

**Who declares the change:** `[POSITION]` declares a move to Contingency. `[POSITION]` declares a move to Emergency. The declaration is announced on the operations net and logged.

### 7.3 Emergency mode — paper procedure

1. Requests are recorded on **ICS 213 RR**. The form's blocks map directly to the Mission Request table, so nothing is lost by dropping to paper.
2. The JOC maintains a **paper mission log** with a sequential number, in the same format as the system's mission number, and continues the number series so digital and paper numbers never collide.
3. The paper log is the **authoritative record** for the duration of emergency mode.
4. The Watch NCO photographs the mission log at every shift change and, when any connectivity exists, transmits it to `[POSITION]`.
5. Task forces continue to report status by radio; the JOC annotates the paper log.

### 7.4 Reconciliation on restoration

This is the hard part, and the part most plans skip.

| Step | Action | Responsible |
|---|---|---|
| 1 | Declare restoration on the operations net. **Stop new paper entries.** | `[POSITION]` |
| 2 | Freeze the paper log. Note the time of the last paper entry. | JOC Watch NCO |
| 3 | Back-enter every paper 213RR into the system, oldest first, flagged **entered retroactively** with the original receipt time preserved | `[POSITION]`, augmented by `[POSITION]` |
| 4 | Reconcile against active missions: identify any mission that exists both on paper and in the system | Battle Captain |
| 5 | Confirm status of every mission that changed state during the outage, **by voice with the executing unit** — do not assume the paper is current | Battle Captain |
| 6 | Verify asset status and personnel accountability independently of both records | J4 and J1 |
| 7 | Declare the system authoritative again. Announce it. | `[POSITION]` |

**Preventing duplicate tasking during the outage and during back-entry:**

- Missions received during emergency mode are numbered from the **same sequence**, so a duplicate is visible as two numbers for one location.
- The JOC maintains a **location board** during emergency mode — grid or address only — so a second request for the same location is caught by eye before it is tasked.
- Back-entry is done by **one person**, not several in parallel, and the entry is checked against the location board before the record is saved.

> **Design exercise for students:** could the system detect a probable duplicate — same parish, same grid within `[N]` metres, within `[N]` hours — and flag it for the watch rather than blocking it? Would you want it to block, or only warn? Defend the answer.

### 7.5 Field-level degraded operation

The task force commander's app must **queue updates offline** and sync when connectivity returns. This is a requirement, not a preference — a task force in a parish with no service is the normal case, not the exception.

Secondary requirement: when a unit has been offline beyond `[N]` hours, the JOC should be able to see that its mission data is **stale** rather than assuming it is current. A record that has not synced is not the same as a record that has not changed, and a system that cannot tell the difference will mislead a commander.

### 7.6 System continuity

| Risk | Mitigation | Owner |
|---|---|---|
| Environment or service outage | PACE levels C and E above | J6 |
| Loss of the single JOC workstation | Any role may work from any device with credentials; no local-only data | J6 |
| Account lockout during surge | Pre-staged accounts and a named administrator on call | `[POSITION]` |
| Data loss | Platform-native backup; confirm retention meets `[RECORDS RETENTION REQUIREMENT]` | J6 |
| Loss of the administrator | Named alternate with equivalent rights, listed in §6.1 | `[POSITION]` |

---

## 8. Battle rhythm and reporting

### 8.1 Daily rhythm

| Time | Event | System product |
|---|---|---|
| 0500 | Storyboard / commander's update brief prepared | Cumulative results, open missions by priority, asset availability |
| 0555 | Shift handover packet generated | Open missions, committed assets, stale missions, overnight changes |
| 0600 | Shift change | Handover packet briefed |
| `[TIME]` | Significant activities report to SEOC | Cumulative results by parish |
| 1700 | Storyboard / commander's update brief prepared | As 0500 |
| 1755 | Shift handover packet generated | As 0555 |
| 1800 | Shift change | Handover packet briefed |
| `[TIME]` | Personnel accountability report | Accountability by unit |

### 8.2 Standing reports

| Report | Audience | Frequency | Contents |
|---|---|---|---|
| Open mission summary | JOC floor | Continuous | Count by status and parish, aged Immediates highlighted |
| Asset availability | J3, J4, Commander | Continuous | Committed vs available by type and location |
| Personnel accountability | J1, Commander | `[FREQUENCY]` | Assigned, present, duty status by unit |
| Response time by priority | J3, Commander | Daily | Mean and worst-case receipt-to-complete by priority |
| Cumulative results | Commander, PAO, SEOC | Twice daily | Persons assisted, pets, livestock, commodities, sandbags, routes cleared |

> **Reminder:** Plan Designer will *recommend* a Power BI report but does not build or connect one. These metrics still need defining up front, because they determine which columns the data model must carry — and because somebody will have to build the report by hand.

---

## 9. Information handling — determine before any real use

This section is deliberately unfinished. It is not an oversight: these are decisions that belong to authorities outside the room, and pretending otherwise is the most common failure in prototype-to-production.

| Question | Decision authority | Status |
|---|---|---|
| Data classification of mission records | `[AUTHORITY]` | **Undetermined** |
| Handling of civilian PII in mission records (names, addresses, medical needs) | `[AUTHORITY]` + Judge Advocate | **Undetermined** |
| Hosting boundary and approval to operate | J6 / information assurance | **Undetermined** |
| Records retention schedule | `[AUTHORITY]` | **Undetermined** |
| Release authority for mission data to media, parishes, or other agencies | Public Affairs + Judge Advocate | **Undetermined** |
| External user account provisioning for parish officials | J6 | **Undetermined** |
| Retention and disposal of paper 213RRs after back-entry | `[AUTHORITY]` | **Undetermined** |

**Teaching point.** A prototype that works is not a system that can be fielded. Every line in this table is a real gate, and none of them are solved by the tool that generated the app. Students who leave the day understanding that have learned the most valuable thing available to them.

---

## Appendix A — Implementation checklist

Use this as the bridge from generated prototype to something a commander could rely on.

**Design**

- [ ] Problem statement agreed and written in one or two sentences
- [ ] All user roles identified, including external users
- [ ] Access decisions made and documented (§2)
- [ ] Data model complete with choice values written out
- [ ] Relationships defined
- [ ] Business rules listed

**Automation**

- [ ] Every workflow written as a trigger–action pair
- [ ] Escalation matrix complete with named positions and defended times
- [ ] Escalation-of-the-escalation defined
- [ ] Serious incident path deliberately kept out of software notification

**Operations**

- [ ] Resource list populated from the task organization
- [ ] Personnel strength and accountability reporting defined
- [ ] Contact roster complete and **verified within the last `[N]` days**
- [ ] Battle rhythm mapped to system products
- [ ] Reporting metrics defined and traced to specific columns

**Continuity**

- [ ] PACE plan written with triggers and declaring authority
- [ ] Paper fallback procedure written and 213RR stocks on hand
- [ ] Reconciliation procedure written with a single named back-entry role
- [ ] Duplicate-detection approach decided
- [ ] Offline behavior specified for the field app
- [ ] Stale-data visibility specified for the JOC

**Governance**

- [ ] Every item in §9 assigned to a decision authority
- [ ] Administrator and alternate named
- [ ] Training plan for the watch floor
- [ ] Rehearsal conducted, including a deliberate degraded-mode drill

---

## Appendix B — Fill-in tracker

| Placeholder | Source | Filled by | Date | Verified |
|---|---|---|---|---|
| `[OPERATION]` | Operations order | | | |
| Unit designations | Task organization | | | |
| Personnel strengths | J1 | | | |
| Resource quantities | J4 / property book | | | |
| Internal contact roster | Alert roster | | | |
| Parish contacts | Parish OHSEP / SEOC list | | | |
| State and ESF contacts | SEOC contact list | | | |
| Escalation timings | J3, approved by Commander | | | |
| PACE declaring authorities | J6 and J3 | | | |
| Accountability thresholds | J1, approved by Commander | | | |
| Records retention requirement | `[AUTHORITY]` | | | |

---

## Sources

- [Emergency Support Functions — Louisiana GOHSEP](https://gohsep.la.gov/divisions/emergency-management/emergency-support-functions/) — ESF structure and the Louisiana National Guard's lead of ESF-16 Military Support
- [ICS Form 213 RR, Resource Request Message — FEMA](https://training.fema.gov/emiweb/is/icsresource/assets/ics%20forms/ics%20form%20213rr,%20resource%20request%20message%20(v3).pdf) — field structure used for the Mission Request table and the paper fallback
- [Resource Typing — FEMA National Resource Hub](https://preptoolkit.fema.gov/web/national-resource-hub/resource-typing) — resource typing referenced in §4.3
- [La. Guardsmen continue 24-hour rescues, flood operations — Louisiana National Guard](https://geauxguard.la.gov/la-guardsmen-continue-24-hour-rescues-flood-operations/) — scale figures used to size the notional scenario
- [Military 101: Orders — The Council of State Governments](https://www.csg.org/2024/09/25/military-101-orders/) — State Active Duty, Title 32, and Title 10 distinctions in §5.2
