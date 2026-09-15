# Student Workbook — Operation CAJUN SHIELD

**Build a Business Solution with Plan Designer**
**Half-day group activity · Flood Response Mission Tracking**

Team: `_______________________`   Driver: `_______________________`   Date: `_____________`

> **EXERCISE — TRAINING USE ONLY.** Operation CAJUN SHIELD is notional. All units, names, contacts, and figures are placeholders or are modeled on publicly reported flood responses. Nothing in this workbook is an operational plan.

---

## What you're doing today

Your team is a joint task force staff cell. You are going to take a problem this organization actually has — mission requests arriving from seven parishes on four different channels and being tracked on a whiteboard — and build a working system for it before the end of the day.

**You do not need to be a developer.** Nobody writes code today. What you need to be is someone who can describe a mission clearly.

### The one idea

> **The tool builds whatever you describe. What you get back is only as good as what you wrote.**

That is why the first half of the day is discussion and worksheet, and the second half is build. The discussion is not warm-up. It is the work.

### How the day runs

| | Block | Time |
|---|---|---|
| 1 | **Discovery** — define the problem, the users, what the system holds. Laptops closed. | 45 min |
| 2 | **Design** — workflows, escalation, agent, reporting, fallback | 70 min |
| 3 | **Build** — generate it in Plan Designer and explore what you got | 2 hr |
| 4 | **After Action Review** | 30 min |

### Your team roles

Assign these now. The driver is the **only person who edits the plan** — the tool allows one editor at a time.

| Role | Who | Does |
|---|---|---|
| **Driver** | | The only one editing. Shares screen. |
| **Reader** | | Holds this workbook, reads the description aloud while the driver types. |
| **Challenger** | | Checks what the tool built against what you actually asked for. |
| **Timekeeper** | | Watches the clock, calls the move to build. |

Rotate the driver after the plan generates.

---

## The situation

Seventy-two hours of rainfall across the Amite and Comite basins has put **seven parishes** under a declared state of emergency. The Governor has activated the National Guard under State Active Duty. A Joint Task Force is running ESF-16 Military Support from the Joint Operations Center.

| 7 | 1,400+ | 160 | 44 | 3 |
|---|---|---|---|---|
| parishes affected | Guardsmen on SAD | high-water vehicles | rescue boats | rotary-wing with hoist |

**How mission requests are handled today**

- Requests arrive by **phone, email, radio, and the state incident system**. There is no single system of record.
- The **0600 / 1800 handover** is a verbal brief and a photo of a whiteboard. Missions fall off.
- Requests arrive with **no grid, no access route, no callback number**.
- Nobody can say **how many boats are uncommitted right now**.
- Parishes **can't see status**, so they call a second channel. Duplicate tasking results.
- The **0500 and 1700 storyboard** takes 90 minutes to compile by hand and is stale on arrival.

**Your task:** design and build a system that fixes this — while the operation is running.

---

# Phase 1 — Discovery

Your instructor leads this as a group discussion. Laptops closed. Take notes here — everything you write in this phase feeds directly into what you type into the tool this afternoon.

### Q1 — What problem are we actually solving?

Write the problem in **one or two sentences**. No technology words.

```
_________________________________________________________________________

_________________________________________________________________________

_________________________________________________________________________
```

**It's six months later and this worked. What is different?** Make it countable.

```
_________________________________________________________________________

_________________________________________________________________________
```

---

### Q2 — Who touches this system?

This is the most important question of the day. The tool generates **user roles first** and hangs everything else off them.

| # | Role | What they do (use verbs) | Internal or external? |
|---|---|---|---|
| 1 | | | |
| 2 | | | |
| 3 | | | |
| 4 | | | |
| 5 | | | |

**Which of these people has an organizational account?** *(This is what decides who gets an app and who gets a portal.)*

```
_________________________________________________________________________
```

**Who must NOT see what?**

```
_________________________________________________________________________

_________________________________________________________________________
```

---

### Q3 — What does the system have to hold?

**Tables and their key columns**

| Table | Key columns |
|---|---|
| | |
| | |
| | |
| | |
| | |

**Choice fields — write out every option, not just the field name**

| Field | Options |
|---|---|
| Priority | |
| Status | |
| Mission type | |
| Asset status | |
| Duty status | |

**Relationships** — how do the tables connect?

```
_________________________________________________________________________

_________________________________________________________________________
```

**Rules the system should enforce**

```
_________________________________________________________________________

_________________________________________________________________________
```

> **Check:** the Commander wants to know whether you're meeting the standard on Immediate missions. Which two columns produce that number? Are they both on your table?

---

### Q4 — What does each person actually open?

**The rule of thumb:** model-driven for managing many records · canvas for one task done fast · portal for users with no account.

| Role | App type | The one screen that matters most |
|---|---|---|
| | | |
| | | |
| | | |
| | | |
| | | |

**It's 0300. The task force commander is standing in water with one bar of signal and wet gloves. What's on the screen? What do they tap first?**

```
_________________________________________________________________________

_________________________________________________________________________
```

---

# Phase 2 — Solution Design Worksheet

Work as a team. **Be specific** — what you write here becomes what you type into the tool. Vague here means generic output.

## Section A — Workflows and escalation

### A1. Workflows

Every one must be written as **"WHEN [x] happens, [y] occurs."** If you can't say it in that shape, it isn't ready. Minimum three.

| # | WHEN (trigger) | → | THEN (action, and who gets notified) |
|---|---|---|---|
| 1 | | → | |
| 2 | | → | |
| 3 | | → | |
| 4 | | → | |
| 5 | | → | |
| 6 | | → | |

### A2. Escalation

**Immediate** priority means life safety. Set your own clock and be ready to defend the numbers.

| Condition | Time | Who gets notified — name the position |
|---|---|---|
| Immediate mission received | T + 0 | |
| Not acknowledged | T + `____` | |
| Still not assigned | T + `____` | |
| Still not assigned | T + `____` | |
| Any mission with no update | `____` hrs | |

**What is the escalation when the escalation fails?** *(The phone is dead. Then what?)*

```
_________________________________________________________________________

_________________________________________________________________________
```

---

## Section B — Agent

**The question is not "do we want AI."** It is: *is there a point in this process where a conversation works better than a form?* Look back at the problem list. Which of those problems could a conversation fix that a form can't?

**Include an agent?**  ☐ Yes   ☐ No

**If no — justify it.** *(A defended "no" is a better answer than an undefended "yes.")*

```
_________________________________________________________________________

_________________________________________________________________________
```

**If yes:**

| Question | Your answer |
|---|---|
| Who does it talk to? | |
| What job does it do? | |
| What does it need to know to do that job? | |
| Name three things it must handle | |
| What does it do with a fourth thing, outside those three? | |

**Write the literal sentence you will paste into the tool:**

```
_________________________________________________________________________

_________________________________________________________________________
```

---

## Section C — Reporting

For every metric, answer the second column. **If the column isn't on your table, the report cannot exist.**

| # | Metric — what question does it answer? | Which columns produce this number? | Who reads it, and when? |
|---|---|---|---|
| 1 | | | |
| 2 | | | |
| 3 | | | |
| 4 | | | |
| 5 | | | |

> **Reality check:** Plan Designer will *recommend* a Power BI report but does not build or connect one — that stays a manual step. Define these metrics anyway. They decide which columns your tables must carry, and you will need this list when somebody builds the report.

**Go back to Q3. Are all of those columns actually on your tables?** List anything you now have to add:

```
_________________________________________________________________________
```

---

## Section D — Fallback and degraded operations

The network **will** go down. Design the degraded mode on purpose.

| | Level | Method | Who acts | How the data gets captured |
|---|---|---|---|---|
| **P** | Primary | | | |
| **A** | Alternate | | | |
| **C** | Contingency | | | |
| **E** | Emergency | | | |

**Who declares a change of level, and how is it announced?**

```
_________________________________________________________________________
```

**When the system comes back up: who back-enters the paper, and how do you stop double-tasking while that's happening?**

```
_________________________________________________________________________

_________________________________________________________________________

_________________________________________________________________________
```

**What does the field app do when there's no signal?**

```
_________________________________________________________________________
```

---

# Phase 3 — Build

## Step 1 — Describe the problem

1. Sign in at **make.powerapps.com**. Confirm you are in the correct environment.
2. Start a new plan. *Your instructor will show today's exact path — entry points move.*
3. Type your description in plain language. No special syntax.
4. You may attach an image — a process diagram, a 213RR, a screenshot of a legacy system. **If you attach one, say what it is and tell the tool to use it.**
5. Select **Generate**.

**Your description must contain all eight of these.** Tick them off as you write — they all come straight from this workbook.

- [ ] The problem, in two sentences *(Q1)*
- [ ] Every user role and what each one does *(Q2)*
- [ ] The app type for each role *(Q4)*
- [ ] Your tables and columns, with every choice option spelled out *(Q3)*
- [ ] How the tables relate *(Q3)*
- [ ] Each workflow as a trigger and an action *(Section A)*
- [ ] The agent and what it's for *(Section B)*
- [ ] The reporting metrics *(Section C)*

> **Length:** input caps at roughly 4,000 tokens — about 3,000 words. Images count toward that. Aim for about two-thirds of a page. Not an essay, not a sentence.

---

## Step 2 — Work the approval gates

The tool stops for your approval at each stage. **Do not click straight through.** This is the cheapest place in the whole process to fix something — correcting the data model here takes thirty seconds; correcting it after you've built four apps costs you the afternoon.

| Stage | What it shows | Check this |
|---|---|---|
| **1. User requirements** | Roles and user needs, with a diagram | Do these match all the roles you defined in Q2? Is your external user in there? |
| **2. Data model** | Tables, columns, relationships | Did your choice values survive? Is the completion timestamp there? |
| **3. Technology proposal** | Which apps, flows, sites, agents | Did the external user get a portal? Is the field app mobile? |
| **4. Save tables** | Name the solution and save | Now you can create the artifacts |

**Refine in plain language.** Examples:

- *"Add a water depth column to the mission request table."*
- *"Make the task force commander app mobile-first."*
- *"Add a flow that notifies the Battle Captain if an Immediate mission is not acknowledged within ten minutes."*

**What did you correct at each gate?** *(If the answer is "nothing," you clicked through. Go back.)*

```
Gate 1: ________________________________________________________________

Gate 2: ________________________________________________________________

Gate 3: ________________________________________________________________
```

---

## Step 3 — Build and explore

Create each artifact from its tile, then **open every one and check it against this workbook.**

| ✓ | Artifact | What to check |
|---|---|---|
| ☐ | **Canvas app** | Navigate the screens. Does the field app work on a phone? |
| ☐ | **Model-driven app** | Check the views. Can you filter by priority? Are the JOC columns right? |
| ☐ | **Power Pages site** | Review the submission form and status page. *May not generate — permissions.* |
| ☐ | **Power Automate flows** | Open one. Read the trigger. Does it match your Section A? |
| ☐ | **Copilot Studio agent** | Review the instructions and knowledge sources. *It has no triggers yet.* |
| ☐ | **Data diagram** | Does the ERD match what your team drew in Q3? |

> **Expect scaffolding, not a finished system.** Nothing publishes itself. Every artifact needs finishing, testing, and approval before anyone would use it. That's normal — on a real project, what you just did in an hour is the first two weeks.

**Find the thing it got wrong.** Hunt for it deliberately — it's the best material for the AAR.

```
_________________________________________________________________________

_________________________________________________________________________
```

---

# After Action Review

**Fill this in before the group discussion.** Write first, talk second.

## Sustain

| Question | Your team's answer |
|---|---|
| What did it build that you didn't expect? | |
| Where would this save the most time on a real activation? | |
| What part of your design came through exactly right? | |

## Improve

| Question | Your team's answer |
|---|---|
| Where did it fall short of your design? | |
| What would you still have to build by hand? | |
| What would you still have to decide or get approved before this could be fielded? | |
| How would you rewrite your description? | |

## The description you actually used

Write or paste your final description here. **This is a requirement document. Take it with you.**

```
_________________________________________________________________________

_________________________________________________________________________

_________________________________________________________________________

_________________________________________________________________________

_________________________________________________________________________

_________________________________________________________________________

_________________________________________________________________________

_________________________________________________________________________

_________________________________________________________________________

_________________________________________________________________________

_________________________________________________________________________

_________________________________________________________________________
```

---

# Quick reference — description checklist

Use this every time you write a Plan Designer description, on any project.

| ✓ | Item |
|---|---|
| ☐ | **Problem** — stated in one or two sentences, with no technology words |
| ☐ | **Roles** — every user named, including anyone outside the organization |
| ☐ | **Verbs** — what each role does, not just who they are |
| ☐ | **App type** — specified per role |
| ☐ | **Tables** — named, with the columns each one needs |
| ☐ | **Choice fields** — every option written out, not just the field name |
| ☐ | **Relationships** — how the tables connect |
| ☐ | **Rules** — what the system must enforce |
| ☐ | **Workflows** — each written as a trigger and an action |
| ☐ | **Escalation** — named positions and actual times |
| ☐ | **Agent** — whether, and what job it does |
| ☐ | **Reporting** — the specific metrics, traced to columns |
| ☐ | **External users** — if any exist, say they need a portal |
| ☐ | **Offline** — if anyone works without connectivity, say so |

---

# Glossary

For anyone new to the Power Platform side of this.

| Term | What it means here |
|---|---|
| **Dataverse** | The database behind the solution. Your tables live here. |
| **Table** | A list of records with defined columns — like a spreadsheet tab, but with rules. A 213RR is a table. |
| **Column / field** | One piece of information on a record. "Priority" is a column. |
| **Choice field** | A column restricted to a set list of options. Stops one person typing "SAR" and another typing "Search and Rescue." |
| **Relationship** | A link between tables — a mission belongs to a parish. |
| **Model-driven app** | An app built around your data. Views, filters, dashboards. Good for managing many records. |
| **Canvas app** | An app where you control the layout. Good for one task done fast, especially on a phone. |
| **Power Pages** | A public-facing website for people who don't have an account in your organization. |
| **Power Automate flow** | An automation. A trigger and then actions. |
| **Copilot Studio agent** | A conversational assistant that can ask questions and act on the answers. |
| **Power BI** | The reporting and dashboard tool. |
| **Solution** | The container that holds everything you built, so it can be moved between environments. |
| **Environment** | A separate workspace. Your training environment is not production. |
| **Publish** | Making a change live. Nothing you build today is published unless you publish it. |
| **ERD** | Entity relationship diagram — the picture of how your tables connect. |
