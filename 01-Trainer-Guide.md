# Trainer Guide — Operation CAJUN SHIELD

**Build a Business Solution with Plan Designer · Flood Response Mission Tracking**
**Half-day group activity · Louisiana National Guard training audience**

> **EXERCISE — TRAINING USE ONLY.** Operation CAJUN SHIELD is notional. Unit designations, rosters, contacts, and figures throughout this package are placeholders or are modeled on publicly reported flood responses. Nothing in this package is an operational plan, and nothing in it should be presented as one.

---

## 0. Read this part first

### The one idea the whole day hangs on

> **Plan Designer builds whatever you describe. The quality of what you get back is capped by the quality of what you wrote. So the discussion blocks are not warm-up — they are the work. The build is the easy part.**

Every discussion question and every worksheet section exists to make students write a better description. If somebody asks "why are we talking instead of building?", that sentence is the answer.

### Why this scenario is harder than a commercial one — and why that's good

A civilian version of this exercise tracks help-desk tickets. This one tracks people on roofs. That changes three things, and they are the three places this course teaches more than the original:

1. **Priority is not a convenience.** "Immediate" means life safety. That makes the escalation discussion real instead of theoretical.
2. **The network will fail.** A flood takes down cell towers. A system with no degraded mode is a system nobody will trust. The PACE discussion has no equivalent in a commercial course.
3. **Accountability is a safety function.** "Did everybody who went out come back" is a different kind of report than "how many tickets did we close."

Lean into all three. They are what make the day land with this audience.

### What this activity is NOT

It is not a Plan Designer feature tour. It is not a lab where everyone ends with the same working app. Teams will get *different* results, and the differences are the teaching content. A team that gets a mediocre result and understands why has learned more than a team that got a good result by copying the sample prompt.

Say that out loud at the start. It lowers the anxiety in the room and stops people asking "is mine right?"

### Five things that will break, and what to do

Check these before the room fills up.

| Risk | Check the morning of | If it's broken |
|---|---|---|
| **Feature not visible** | Sign in with a *student* account, not yours. Confirm the environment has a Dataverse database and that you can start a new plan. | Students can fall back to a developer environment, where they automatically have permission to create Dataverse tables. Have the fallback ready rather than discovering it live. |
| **One editor per plan** | By design — many people can view a plan, but only **one can edit at a time**. | Assign a **driver** per team before you release them. Announce it before teams open the tool, not after two people have fought over it. |
| **Power Pages fails** | Power Pages creation needs **System Administrator** rights and permission to register apps in **Microsoft Entra**. Training accounts usually lack this. | Tell teams upfront it may not generate in this tenant. Frame it as an environment permission issue, not a design failure — and as a real lesson about the distance between designing a thing and being allowed to field it. |
| **Power BI doesn't appear** | Plan Designer **recommends** a Power BI report; it does not build or connect one. | Handle it during the reporting discussion (§3.8), not as a disappointment at the end. |
| **Prompt too long** | Input caps at roughly **4,000 tokens / 3,000 words**; uploaded images count toward it. | The master prompt in §7 is about the right length. Hold it up as the target shape. |

### Your prep, in order

1. **Build the solution yourself, end to end, in the training tenant.** Do not skip this. You need to know what the screens actually say today.
2. Note where the current UI **differs from the student workbook** (see §2.2) and correct it for the class at the top of Phase 3.
3. Keep your own completed plan open in a spare tab. It's your rescue tool for a team that is badly stuck at hour three.
4. Have the **master prompt** (§7) ready to paste into chat.
5. Decide your **team composition** deliberately — see §4.1. With a rank-mixed room this matters more than anything else you'll do.

---

## 1. Day 2 running order

Following the Day 2 agenda block structure: 15 min intro, 45 min scenario walkthrough and discussion, 4 hours build, 15 min wrap.

| Agenda block | Time | What happens | Slides |
|---|---|---|---|
| Introduction | 15 min | Exercise caveat, objectives, scenario handout, team formation. | 1–4 |
| Scenario walkthrough and group discussion | 45 min | **Phase 1: Discovery.** Four questions. Laptops closed. | 5–10 |
| Build Solution with Plan Designer | 4 hours | **Phase 2 + Phase 3 + AAR.** Breakdown below. | 11–23 |
| Course wrap up | 15 min | Close, takeaways, where the package lives. | 24 |

### The 4-hour block, minute by minute

The two breaks are not optional. This is a long block and attention collapses without them.

| Elapsed | Duration | Activity | Slides |
|---|---|---|---|
| 0:00 | 15 min | Introduce the four design topics: workflows and escalation, agent, reporting, fallback. Brisk — these are discussion prompts, not lecture. | 11–16 |
| 0:15 | 45 min | **Teams complete the Solution Design Worksheet, Sections A–D.** You circulate constantly. | 17 |
| 1:00 | 10 min | **Share-out.** One item per team. Your quality gate before anyone opens the tool. | — |
| 1:10 | 15 min | **Break** | — |
| 1:25 | 20 min | **Instructor walkthrough.** Your screen, their eyes only. Walk the whole path once. | 18–21 |
| 1:45 | 35 min | Teams write the description, generate, and work the approval gates. | 22 |
| 2:20 | 10 min | **Checkpoint.** Every team past **Save tables**. Chase anyone who isn't. | — |
| 2:30 | 15 min | **Break** | — |
| 2:45 | 45 min | **Build and explore.** Create artifacts, work the exploration checklist. | 21 |
| 3:30 | 10 min | Teams complete the AAR sheet. Silently, in writing, before anyone talks. | — |
| 3:40 | 20 min | **After Action Review.** | 23 |

> **Note:** the AAR block is 30 minutes total — 10 minutes of silent writing plus 20 minutes of discussion. If you can steal another 10 minutes from the build, give it to the discussion; it is where the learning consolidates.

### If you're running late

Cut in this order. Protect the AAR and the fallback discussion.

1. **First cut:** exploration checklist down to three items — model-driven app, one flow, the agent.
2. **Second cut:** worksheet Section C (reporting) to two metrics instead of five.
3. **Third cut:** skip the share-out; spot-check teams individually instead.
4. **Never cut:** the AAR, Discussion Question 1, or the PACE/fallback discussion. A room that never agreed on the problem produces four hours of confused work, and a Guard audience that never discussed degraded ops will correctly conclude you don't understand their environment.

### If you're running early

- Have teams swap descriptions with another team and generate *each other's* plan. Two descriptions of the same scenario producing visibly different systems is the single most persuasive demonstration available to you.
- Or run an **inject** (§5) — a levee breach, a comms blackout, a parish going dark — and ask teams what their design does about it.

---

## 2. Plan Designer — what you need to know cold

### 2.1 The short version

Plan Designer (surfaced in the product as **Plans**) is a copilot-first experience in Power Apps. You describe a business problem in natural language, optionally attach images, and a set of AI agents produces a structured plan: user roles and stories, a Dataverse data model, and a proposed technology stack. You review and refine at each stage, save the tables, then create the artifacts.

It is **generally available** and on by default in eligible environments. It requires a **Dataverse database**, and it is currently **English only**.

**Three AI agents do the work**, matching the three stages of the wizard:

- **Requirement Agent** — user roles and user needs
- **Data Agent** — Dataverse tables, columns, relationships
- **Solution Agent** — the technology proposal

Naming them is useful: it explains why the wizard has three approval gates.

### 2.2 ⚠️ Verify these in your tenant the morning of

Entry points and wording move. Getting ahead of this costs two minutes; being contradicted by the screen costs you the room.

| Commonly documented in older material | Current documented behavior |
|---|---|
| Left navigation → **Plans** → **+ New plan** | The documented path starts from the Home screen: **Start with a plan** → **Create a plan**. Check both. |
| Describe → **Generate** → **Build** | A **staged wizard with approval gates**: generate → review user requirements (**Looks good** / **Edit**) → review data model → review technology proposal → **Save tables** → then create artifacts. |
| A single **Build** button produces everything | Artifacts are created **one at a time** from **Create** on each tile. |
| Power BI reports are generated and connected | Power BI is **recommended only**. Connecting a report with plan context is not currently supported. |

None of this breaks the activity — the thinking it teaches is unaffected. But students following printed steps literally will get lost, so narrate the real path during your walkthrough.

### 2.3 What "build" actually produces

**Starting points, not finished products. Nothing publishes automatically.** This is the most important thing to understand before the AAR, because "it wasn't finished" is the observation students will make and you want it framed as expected rather than as a failure.

| Artifact | What you get | Still required |
|---|---|---|
| **Canvas app** | Studio opens with a data-connected app: responsive screens per table plus a welcome screen | Customize, save, publish |
| **Model-driven app** | App designer opens with tables pre-added | Save, publish |
| **Power Pages site** | Design studio opens with layout and pages tailored to the problem | Finish the site, save, publish. Needs System Admin + Entra rights |
| **Power Automate flow** | The natural-language flow builder opens with a prompt **prefilled** from your problem, user story, and data sources | Generate, save, publish |
| **Copilot Studio agent** | Name, description, instructions pre-filled; all plan tables added as knowledge sources | Add triggers and actions, test, publish |
| **Power BI** | A recommendation only | Build and connect it yourself |

**Framing line for the AAR:** *"It got you from a blank page to a scaffolded solution in an hour. On a real project that's the first two weeks. What it did not do is the last mile — and in our world the last mile includes security, accreditation, and approval to operate."*

### 2.4 Quick answers to questions you will get

**"Can it use SharePoint or Excel instead of Dataverse?"** No. It requires a Dataverse database and generates Dataverse tables. Designing the data model is the point of it.

**"Is this approved for use on our networks?"** Do not guess. The honest answer: *"That's an authorization question for your J6 and your information assurance shop, not a capability question. What we're teaching today is how to specify a solution. Whether and where it can be fielded is a separate decision with a separate process."* Say this cleanly and move on — it will come up, and hedging costs you credibility.

**"What about CUI / PII / operational data?"** Same answer, same discipline. In this exercise everything is notional. In practice, data classification, records retention, and hosting boundary are decisions made before anyone opens a tool. It's worth naming as a real requirement teams should write down — see the OPSEC inject in §5.

**"Can the whole team edit at once?"** No. Many can view; one edits at a time. Others get read-only until the editor exits or goes inactive.

**"Can I share or export the plan?"** Yes — Viewer or Co-Owner, and a **PDF export** (document content, not diagrams). The PDF export is a genuinely useful point: the plan doubles as a requirements document you can hand to a contracting officer or a J6 shop.

**"Can I make a plan from something we already built?"** Yes, and it's the feature most likely to be useful back at their unit. From **Solutions**, choose **Create plan from a solution** — it reverse-engineers a document describing the problem, roles, data model, and technology stack of an existing solution. Needs at least one app and one table. Don't run it against the default solution.

**"Why did it ignore my image?"** You have to tell it to use the image: *"Use the attached 213RR as the field list for the mission request table."* Uploading alone isn't a strong enough signal.

**"Will two teams get the same answer?"** No. It's generative. Say this before somebody asks why theirs is different.

---

## 3. The discussion questions, explained

For each: why it's asked, where the answer lands in the tool, what strong sounds like, what weak sounds like and how to move it, and what to capture on the board.

**Write answers on the whiteboard and leave them up all day.** In Phase 3 you will point at the board and say "put that in your description." That visible continuity is what makes the activity land.

---

### 3.1 Q1 — What problem are we actually solving? *(Slide 6, ~10 min)*

**Why it exists.** It's the opening line of the description, and it's a test of whether students can separate a problem from a solution — the single most common failure in real projects, where somebody fields a system for a problem nobody agreed on.

**Where it lands.** The first sentences of the plan description. The Requirement Agent uses it to infer scope. Vague problem, generic user stories.

**Strong answer**

> "There is no single system of record for mission requests. They arrive on four uncoordinated channels and live on a whiteboard, so missions are lost at shift change, tasking gets duplicated, the Commander has no current picture of committed versus available assets, and the storyboard is compiled by hand and stale on arrival."

It names the absence, the mechanism of failure, and the consequences — and mentions no technology at all.

**Weak answers and redirects**

| They say | What's wrong | Say this |
|---|---|---|
| "We need an app." | Solution, not problem. | "Maybe. Why? What's broken that an app fixes?" |
| "Get off the whiteboard." | Symptom, not cause. | "The whiteboard isn't the problem. What goes wrong *because* it's a whiteboard?" |
| "It's inefficient." | True of everything. | "Inefficient how? Give me one mission that went sideways and tell me what happened to it." |
| Silence. | Reading isn't thinking. | Read the six current-state cards aloud, then: "Which one of these gets somebody hurt first?" |

**Don't skip the success question.** Push until you get something countable: *no mission unacknowledged past 15 minutes; storyboard in five minutes instead of 90; zero duplicate taskings.* Vague success statements produce vague systems.

**Capture:** one agreed problem statement, one to two sentences. Leave it up.

---

### 3.2 Q2 — Who touches this system? *(Slide 7, ~12 min — give it the extra time)*

**Why it exists.** Highest leverage question of the day. The Requirement Agent generates roles first and hangs every user story, app, and permission off them. Two vague roles produce a thin plan no matter how good the rest is.

**Where it lands.** Stage 1 of the wizard: roles and user needs, with a diagram. It also drives the technology proposal — internal roles get apps, external roles get a portal.

**Target answer — five roles**

| Role | Does | Internal / external |
|---|---|---|
| JOC Watch NCO | Receives, logs, validates incoming requests | Internal |
| J3 Battle Captain | Prioritizes, assigns, tracks, escalates | Internal |
| Task Force Commander | Receives tasking, updates status from the field | Internal, mobile |
| Parish Emergency Manager | Submits requests, checks status for their parish | **External** |
| JTF Commander | Common operating picture, read-only | Internal, dashboard |

**The question that unlocks the slide:** *"Which of these people has a state Guard account?"*

The parish emergency manager doesn't — they're a parish civilian employee. Follow with *"So how does somebody with no account submit a request?"* and the room arrives at an external portal by itself instead of being told.

**Weak answers and redirects**

| They say | What's wrong | Say this |
|---|---|---|
| They forget the parishes | The Guard-centric view. Drops the whole external population and the portal. | "Who is actually calling us? Are they in this room?" |
| They forget the Commander | Drops the dashboard requirement. | "Who signs the storyboard? Do they log into the same app as the Watch NCO?" |
| "Users and admins" | Generic in, generic out. | "A Watch NCO logging a rescue and a TF Commander standing in four feet of water need completely different screens." |
| Nobody mentions the field | The most commonly missed requirement. | "Where is the TF Commander when they update status? What's their signal like?" |

**Get verbs for each role.** The Watch NCO *receives, logs, validates*. The Battle Captain *prioritizes, assigns, escalates*. Those verbs become user stories almost word for word — tell the room to watch for that this afternoon.

**Security thread — worth two minutes, especially with senior people present.** Should one parish see another parish's requests? Should a parish see which unit was tasked, or only that a mission is underway? Should the roster be visible outside the JOC? These are decisions made here, not bolted on later.

**Capture:** three-column table — Role | What they do | Internal or external.

---

### 3.3 Q3 — What does the system have to hold? *(Slide 8, ~12 min — the long one)*

**Why it exists.** It's the data model. Everything downstream reads and writes these tables. A missing column here is a missing capability everywhere.

**Where it lands.** Stage 2 of the wizard: the Data Agent proposes tables, columns, data types, relationships, and a diagram.

**Run it in order:** tables → columns → choice values → relationships → rules.

**Target answer**

- **Mission Request** — mission number, requesting parish, mission type, priority, description, grid/location, water depth, access route, requested arrival, status, assigned unit, assigned assets, results, closeout time, remarks
- **Parish** — name, OHSEP POC, EOC location, declaration status, liaison assigned
- **Unit / Task Force** — designation, parent command, commander, current location, duty status, assigned strength
- **Asset** — asset type, bumper number, owning unit, capability (fording depth, pax), status, current location
- **Personnel** — name, rank, unit, duty status, report date, release date, accountability

**Relationships:** a mission belongs to a parish · a mission is assigned to a unit · a unit owns assets · personnel belong to a unit.

**Choice fields — insist they be written out**

- **Priority:** Immediate (life safety) · Priority (property and essential services) · Routine
- **Status:** Received → Validated → Assigned → En Route → On Scene → Complete · Unable · Cancelled
- **Mission Type:** SAR (boat) · SAR (high-water vehicle) · Aviation hoist/MEDEVAC · Route clearance · Levee and sandbag ops · Commodity distribution / POD · Shelter support · Security and traffic control · Power and generator support · Communications support
- **Asset Status:** Available · Committed · En Route · Deadlined
- **Duty Status:** State Active Duty · Title 32 · Title 10

**Three moments worth slowing down for**

1. **Choice values.** Somebody says "we need a priority field." Ask: *"Priority of what values?"* Make them say the options out loud. The lesson is portable and it's the most useful prompting habit they'll take away: **name the options, don't just name the field.**

2. **The closeout time.** Ask: *"The Commander wants to know whether we're meeting the standard on Immediate missions. Which columns give you that number?"* The room works out it needs the time received *and* the time complete. A reporting requirement just created a data requirement. Let it land.

3. **Water depth and access route.** Ask: *"What does a boat crew need to know before they roll that a normal ticket system would never capture?"* You'll get water depth, road status, bridge condition, hazards, animals, medical needs. That's the moment they realize a generic tracker won't do — the mission drives the model.

**Weak answers and redirects**

| They say | What's wrong | Say this |
|---|---|---|
| Thirty columns on the mission table | Nobody will fill them in. | "Which of these does a Watch NCO type at 0300 with a parish EM on the phone? Start there." |
| One flat table | No relationships, no reporting by unit or parish. | "How do you answer 'how many boats does Task Force Raven have committed' from one table?" |
| Status is open / closed | Kills workload visibility and the escalation logic. | "If everything not-closed is open, how does the Battle Captain see what's en route versus what nobody has touched?" |
| Free text where a choice belongs | Exactly the problem the spreadsheet already has. | "One person types Rescue, another types SAR, another types Search and Rescue. Now count them." |

**Capture:** table names, key columns, choice values written out in full, and the four relationships.

---

### 3.4 The 213RR anchor *(Slide 9, ~5 min — do not skip)*

This slide exists to defuse the "I'm not technical enough" objection, and it is the most reassuring five minutes of the day for a non-IT audience.

**The move:** *"Everybody here has filled out a 213RR. Look at what it actually is — a list of fields, a couple of them restricted to set values, and an approval step in the middle. That's a database table. You've been designing database tables your whole career. Nobody called it that."*

If you have a skeptical senior NCO, this is the slide that converts them. Ask: *"How many of these have you filled out?"* Then: *"So you already know what belongs on this table better than any developer does."*

**Tie it forward:** the paper form is also the fallback. When the network dies, the 213RR is what the system degrades to. That's not a coincidence — it's a design decision, and it comes back in §3.9.

---

### 3.5 Q4 — What does each person actually open? *(Slide 10, ~10 min)*

**Why it exists.** It maps roles to app types. Students who can say *why* a Watch NCO gets one type and a TF Commander gets another are demonstrating exactly the competency this course is built around.

**Where it lands.** Stage 3: the Solution Agent's technology proposal.

**The rule of thumb**

> **Model-driven** when the job is managing many records — queues, views, filters, dashboards.
> **Canvas** when the job is one task done fast, especially on a phone.
> **Power Pages** when the user is outside the organization and has no account.

**Then break it on purpose:** *"By that rule, what does the Watch NCO get? Argue it both ways."* There's a real argument — a Watch NCO taking a call wants speed and a tight layout (canvas); a Watch NCO working a queue of forty wants views and filters (model-driven). Let them fight. The argument is the learning.

**The question that unsticks a quiet room:** *"It's 0300. The TF Commander is standing in water with one bar and wet gloves. They open the app. What's on the screen? What do they tap first?"*

That converts an abstract question into a picture, and the answer is a user story almost verbatim.

**Weak answers and redirects**

| They say | What's wrong | Say this |
|---|---|---|
| "Canvas, it looks better." | Aesthetics aren't the criterion. | "What can it *do* here that model-driven can't? Be specific about the task." |
| "One app for everybody." | Different roles, different needs, different access. | "Same app for the Commander and the parish EM? What does the parish see when they open it?" |
| Nobody raises offline. | The requirement most teams miss. | "What happens when there's no signal? Does the app just fail?" Park the answer — it returns in §3.9. |

**If leadership is in the room,** ask them directly: *"Sir/Ma'am, what would you want on that one screen?"* Their answer is a real requirement and the room should hear it from them rather than from you.

**Capture:** role → app type → the one screen that matters most.

---

### 3.6 Design Topic 1 — Workflows and escalation *(Slides 12–13)*

**Why it exists.** Automation is where the payoff is, and the discipline is expressing it as a **trigger–action pair** — which is exactly how a flow is built.

**Where it lands.** The technology proposal lists flows. Creating one opens the natural-language flow builder with a prompt **prefilled** from the problem, the user story, and the data sources. Sharper pair, sharper flow.

**Target workflows (minimum three; the last three separate a real system from a demo)**

1. Request arrives from the parish portal → notify JOC watch, assign mission number, acknowledge to the parish
2. Mission validated and assigned → notify the TF commander *and* the requesting parish
3. Status set to Complete → notify the parish, roll results into running totals
4. No status update in 4 hours → flag stale, notify the TF commander, then the Battle Captain
5. Shift change 0600 / 1800 → generate the handover packet
6. Asset goes deadlined → notify support operations, flag every mission it's committed to

**Enforce the format:** *"WHEN [x] happens, [y] occurs."* Anything that can't be written that way gets rewritten before it goes in the description.

**The shift-change flow wins the room.** *"Right now the handover is a verbal brief and a photo of a whiteboard. What if the packet built itself at 0555?"* Watch the Battle NCOs sit up.

#### Escalation — slide 13

This is the slide with no commercial equivalent. **Make them commit to numbers and defend them.**

| | |
|---|---|
| T + 0 | Request received. Auto-acknowledge to parish, alert Watch NCO. |
| T + 10 min | Not acknowledged → page the J3 Battle Captain. |
| T + 20 min | Still not assigned → notify the J3 Operations SGM. |
| T + 30 min | Still not assigned → notify the JTF Commander, log as a reportable delay. |

**The framing:** *"In a business system 'urgent' means somebody's invoice is late. Here, Immediate means there are people on a roof and the water is still coming up."*

**Two questions that make it land**

1. *"Who gets woken up, and at what point? Name the position."* Vague escalation — "it goes up the chain" — is how things die at 0300. The system needs a named position and a clock.
2. *"What's the escalation when the escalation fails? If the Battle Captain's phone is dead, then what?"* That answer is the fallback plan, in Design Topic 4.

**Weak answers and redirects**

| They say | What's wrong | Say this |
|---|---|---|
| "Send notifications." | No trigger, no recipient. | "When? To whom? Give me the sentence." |
| "Auto-assign to whoever's closest." | Undefined rule. | "How does the system know who's closest and who's free? State the rule. If you can't, it can't run it." |
| Fifteen workflows | They'll build none of them well. | "Which three would the Watch NCO thank you for on the first shift?" |
| Only the happy path | Real operations have exceptions. | "What happens to a mission nobody has touched since midnight? Who finds out, and when?" |

---

### 3.7 Design Topic 2 — Agent *(Slide 14)*

**Why it exists.** The newest material and the part students are least equipped to reason about. The question is not "do you want AI." It is **"is there a point in this process where a conversation works better than a form?"**

**Where it lands.** The proposal can include a Copilot Studio agent. It arrives with name, description, instructions pre-filled and all plan tables added as knowledge sources. Triggers, actions, testing, and publishing are manual.

**Frame it this way:** *"Look back at the problem list from this morning. Which of those could a conversation fix that a form can't?"*

The answer is already on the board — requests arrive with no grid, no access route, no callback number. A form accepts whatever gets typed. An agent can ask the follow-up.

**Recommended answer: a parish intake agent** on the portal that asks what an experienced dispatcher would ask — how many people and where exactly, water depth at the access point, road passable and which route, anyone injured, animals on site, best callback number. The justification is that it fixes a named problem in the scenario, and that it makes sure the question gets asked every time including at 0300 on hour nineteen.

**Strong alternative: a commander query agent** for plain-language questions against live data. If leadership is present, read those four example questions off the slide and watch the reaction — *"Sir/Ma'am, that's the question you asked the J3 twice yesterday."*

**"No agent" is a legitimate answer and you must say so.** A team that argues *"our parish EMs are experienced professionals under time pressure who want a form with a confirmation number, not a chatbot"* has done better analysis than a team that adds an agent because it was on the slide. Reward the reasoning, not the feature.

**Weak answers and redirects**

| They say | What's wrong | Say this |
|---|---|---|
| "An AI chatbot." | Names a technology, not a job. | "What does it *do*? What does the user say, and what does it do about it?" |
| "It answers questions." | From what? | "Where does it get answers — mission records, the EOP, both?" |
| "It should do everything." | Unbounded. | "Name three things it must handle. What does it do with a fourth?" |

**Most useful thing you can do here:** help each team write the literal sentence they'll paste in. Then read one team's sentence to the room.

---

### 3.8 Design Topic 3 — Reporting *(Slide 15)*

**Why it exists.** Two reasons, and say both: reporting requirements *validate the data model*, and defining metrics up front is a habit that outlives this tool.

**Be honest about the product.** Plan Designer will *recommend* Power BI; it won't build and connect a report. Say so now: *"You're writing this list because the metrics shape your columns, and because you'll need this list anyway when somebody builds the report."* That turns a letdown into a planned observation.

**Target metrics**

1. **Open missions** — by status and by parish
2. **Asset availability** — committed vs available by type
3. **Personnel accountability** — assigned, present, duty status by unit
4. **Response time by priority** — are we meeting the standard on Immediate?
5. **Cumulative results** — rescues, assists, commodities, sandbags (the storyboard numbers)

**The move that makes this block worth the time:** for every metric, ask *"which columns produce that number?"* Then send them back to the data model to check. They will find gaps — response time needs both timestamps; asset availability needs a status field somebody actually updates; accountability needs duty status. That discovery is the strongest single lesson in Phase 2.

**Weak answers and redirects**

| They say | What's wrong | Say this |
|---|---|---|
| "A dashboard with everything." | Not a metric. | "Answering what question? The Commander has ten seconds. What one number?" |
| Metrics with no owner | Reports nobody reads. | "Who opens this at 0500? What do they do differently based on it?" |
| Nobody mentions accountability | The most important one for this audience. | Raise it: "How do you know everybody who went out came back?" That reframes the system from a work tracker to a safety system. |

---

### 3.9 Design Topic 4 — Fallback and degraded operations *(Slide 16)*

**This is the slide senior leaders will remember. Protect the time for it.**

**Why it exists.** Every vendor demo assumes the network is up. A flood takes down cell towers. A system with no designed degraded mode is a system nobody trusts — and if the degraded mode is worse than the whiteboard, nobody will trust the system when it *is* up either.

**Use PACE.** They already know the framework from comms.

| | Level | Means |
|---|---|---|
| **P** | Primary | Mission Tracker app over the state network or cellular data |
| **A** | Alternate | Parish portal over any commercial internet; JOC works from the model-driven app |
| **C** | Contingency | Voice or radio to the JOC; Watch NCO enters the mission on the requester's behalf |
| **E** | Emergency | Paper ICS 213RR by runner or radio relay, back-entered when connectivity returns |

**Tie it to the 213RR anchor:** *"Your database table and your paper fallback are the same fields. That's a design decision — it means falling back doesn't mean losing data, it means changing the pen."*

**The two questions that generate the best discussion of the day**

1. *"When the network comes back, who types in the twenty paper 213RRs — and while that's happening, how does the JOC avoid tasking the same mission twice?"* There is no clean answer. Good. Real systems have this problem and somebody has to own it.
2. *"What's the minimum this has to do to beat the whiteboard when it's degraded?"*

**Connect it to the app design.** This is where offline capability on the field canvas app stops being a nice-to-have. A TF Commander with no signal needs to queue updates and sync later. That belongs in the description.

---

## 4. Managing the room

### 4.1 Rank in the room — read this before you build teams

This is the one section that has no equivalent in the commercial version of this guide, and it matters more than any facilitation technique below.

**The failure mode:** a Specialist who runs the JOC watch every drill weekend knows more about how mission requests actually get lost than anyone else in the room — and will say nothing if a Major is at the table.

**What to do about it**

- **Say it out loud in Phase 1.** *"Rank does not settle a design argument. The person who has actually done the job on the ground usually knows something the staff doesn't. I need to hear from them."* Saying this from the front gives junior people permission they will not take on their own.
- **Build teams deliberately.** Two workable patterns:
  - *Mixed by design* — one senior, one staff, one operator per team, with the **junior person as driver**. Gives the room the full range of perspective and physically puts the keyboard in junior hands.
  - *Peer-grouped* — leaders together, operators together. Produces franker discussion inside each team and a much more interesting share-out, because the two groups will genuinely disagree about priorities.
  - Pick based on your room. If the command climate is open, mix. If people are visibly deferring, group by peer.
- **Give leaders a job that isn't talking.** Senior people participate best when they have a defined role. Make them the **Challenger** — their job is to ask whether the thing being built is what the mission actually needs, not to drive.
- **Ask the Commander direct questions at the right moments.** Slides 10 and 14 are built for it. A Commander answering "what would you want on that one screen" in front of the room is worth more than anything you can say, and it signals that participation is expected at every level.
- **Never let a senior person's first answer close a question.** If a Major answers first, take it, then say: *"Good — who sees it differently?"* and wait. Pointedly.

### 4.2 When nobody answers

In rough order of escalation:

1. **Wait.** Count to seven. Most trainers rescue a silence at three, which teaches the room that you'll answer your own questions. Seven feels unbearable and works.
2. **Narrow it.** Not *"what does the app look like?"* but *"it's 0300, the TF Commander opens the app — what's on the screen?"*
3. **Make it binary.** "Show of hands: canvas or model-driven for the Watch NCO?" Then ask one person from each side why.
4. **Think-pair-share.** "Thirty seconds on your own, then tell the person next to you."
5. **Ask the table, not the room.** "Table three, one pain point."
6. **Offer a wrong answer.** "I'd put all of it in one table — go." Disagreeing is much easier than generating.

### 4.3 When one person answers everything

Usually a senior person being helpful. Handle it without embarrassing them — you need their energy later.

- **Name-check forward:** "Great — hold that, let's hear from someone who hasn't gone yet."
- **Recruit them:** "You've clearly done this. Can you capture these on the flipchart?" Occupies them and honors the expertise.
- **Rotate structurally:** "Round the tables, one point each."
- **Use them in the share-out** — first, with a stated limit: "one item, thirty seconds."

### 4.4 Team roles during the build

Assign these when you release teams, not after.

| Role | Does |
|---|---|
| **Driver** | The only person editing the plan. Shares screen. |
| **Reader** | Holds the worksheet, reads the description aloud while the driver types. |
| **Challenger** | Checks generated output against what the team actually asked for. |
| **Timekeeper** | Watches the clock, calls the move to build. |

Rotate the driver after the plan generates. This also solves the usual "one person does everything while three watch" problem.

### 4.5 When a team goes down a rabbit hole

Common ones: arguing choice values for fifteen minutes, redesigning how the Guard does business, or debating whether they'd *really* use this tool. Timebox out loud: *"Two more minutes, then write what you've got and move to Section C. You can refine it in the tool."* The escape hatch is true and it works.

### 4.6 When a team is stuck and the clock is running

At 30 minutes of build time, any team still writing needs an intervention. Don't debug — unblock.

- Paste the master prompt (§7) and say: "Start from this, change three things to match your worksheet, generate."
- Or show them your pre-built plan: "Here's roughly where you're heading. Get yours generated and spend your time comparing."

A team that generates something imperfect at minute 35 has a good afternoon. A team still polishing at minute 45 has nothing to review.

### 4.7 Running the Phase 2 share-out

Not a presentation round — a quality gate. One item per team, sixty seconds. While they talk, check silently:

- Is the problem statement specific enough to generate something useful?
- At least three workflows, written as trigger–action?
- A decision on the agent, with a reason either way?
- Two or three specific metrics?
- A PACE fallback with a named emergency mode?

If a team fails one, go to their table while the next team talks. Don't correct publicly.

---

## 5. Injects — making it dynamic (optional)

If the room is strong or you're running early, drop an inject mid-build. Read it out as a message from the SEOC and give teams five minutes to answer: **what does your design do about this?** Injects are the fastest way to expose a thin design.

| Inject | What it tests |
|---|---|
| **"Levee overtopping reported at Denham Springs. Four new Immediate missions in the last ten minutes."** | Does the priority scheme and escalation hold under surge? Does anything auto-triage? |
| **"Cell service is down across two parishes. The task forces there have no data."** | The PACE plan. Offline capability. Who enters missions on their behalf. |
| **"A parish just called the JOC directly for a mission they already submitted on the portal."** | Duplicate detection. Does the parish have status visibility, and if not, why not? |
| **"Two boats are deadlined. Six missions were assigned to them."** | Does an asset status change propagate to the missions committed to it? |
| **"State Police asks for our open mission list. Media asks for rescue totals."** | Who can see what. Data release authority. External reporting as a real requirement. |
| **"Governor's office wants total rescues by parish for a press conference in 20 minutes."** | Whether the reporting design actually answers a question somebody asks under pressure. |
| **"A mission record contains a citizen's name, address, and medical condition."** | PII handling, data classification, retention. The OPSEC conversation, earned rather than lectured. |
| **"The JOC loses power for 40 minutes. When it comes back, 22 paper 213RRs are on the desk."** | Reconciliation. The question with no clean answer, which is the point. |

Use one or two, not eight. The OPSEC inject is the one most worth running with a Guard audience — it surfaces a real constraint that the tool discussion otherwise skips entirely.

---

## 6. The After Action Review

Thirty minutes — ten of silent writing, twenty of discussion — and the most valuable part of the day. **Everyone writes before anyone talks** — ten silent minutes on the AAR sheet. Otherwise the first team's answer becomes the room's answer.

Use AAR language — sustain and improve — not "debrief." This audience knows the format and will engage with it properly.

### Sustain

**"What did it build that you didn't expect?"** Listen for surprise at the **user stories**. That's the Requirement Agent showing its work and it's what experienced planners find most unexpectedly useful.

**"Where would this save the most time on a real activation?"** The honest answer is the start — the blank page, the first data model, getting something in front of a decision-maker in a day instead of three weeks. Also worth surfacing: the plan exports to PDF and doubles as a requirements document.

### Improve

**"Where did it fall short of your design?"** You want: nothing published, apps are scaffolds, the agent has no triggers, Power BI was a recommendation, the portal may not have generated. Affirm every one — §2.3 is your reference. That's expected behavior, and naming it is the mark of somebody who understands the tool rather than being impressed by it.

**"What would you still have to build by hand?"** For this audience, push past the software answer: security configuration, data classification, accreditation, approval to operate, training the watch floor, and the reconciliation process for degraded mode.

**"How would you rewrite your description?"** The central lesson. **If two teams got noticeably different results, put both descriptions side by side and read them out.** Two minutes. It's the most persuasive thing that happens all day and no amount of explaining substitutes for it.

### The three closing takeaways

1. **The description is the system.** Specific teams got specific results. Vague teams got generic ones. That relationship is the takeaway.
2. **This is a starting point, not a finished product.** Customization, security, accreditation, testing, and approval to operate are all still yours.
3. **The thinking transfers.** Roles, data, trigger-and-action, metrics before build, PACE. Those work on any tool, including the one that replaces this one.

### If you have five spare minutes

*"Go back to your shop on Monday. What's the first thing you'd point this at?"* Converts a training day into an intention, and it usually produces the best conversation in the room.

**If leadership is present, give them the last word.** Ask whether what they saw changes anything about how they'd want a requirement written. Their answer is worth more to the room than yours.

---

## 7. Master prompt — instructor answer key

This is your rescue tool and your demo. It is deliberately about two-thirds of a page — the right shape, well inside the input cap. Paste it into chat for a stuck team and tell them to change three things.

> Build a flood response mission tracking solution for a National Guard joint task force supporting a multi-parish flood. The problem: mission requests arrive from parish emergency managers by phone, email, radio, and a state system, and are tracked on a whiteboard and a spreadsheet, so missions are lost at shift change, tasking is duplicated, and leadership has no current picture of committed versus available assets.
>
> There are five user roles. (1) JOC Watch NCO receives, logs, and validates incoming mission requests using a model-driven app. (2) J3 Battle Captain prioritizes, assigns missions to units, tracks execution, and escalates, using a model-driven app with dashboards. (3) Task Force Commander receives tasking and updates mission status from the field using a mobile canvas app that must work with poor connectivity. (4) Parish Emergency Manager is external with no organizational account, and submits mission requests and checks the status of their own parish's requests through a Power Pages portal. (5) JTF Commander views a read-only dashboard showing open missions, committed versus available assets, and personnel accountability.
>
> Create these tables. Mission Request: mission number, requesting parish, mission type, priority, description, grid location, water depth, access route, requested arrival time, status, assigned unit, assigned assets, results, time received, time complete, remarks. Parish: parish name, emergency management point of contact, phone, EOC location, declaration status. Unit: unit designation, parent command, commander, current location, duty status, assigned strength. Asset: asset type, bumper number, owning unit, capability, status, current location. Personnel: name, rank, unit, duty status, report date, release date, accountability status.
>
> Priority is a choice field with values Immediate, Priority, and Routine. Status is a choice field with values Received, Validated, Assigned, En Route, On Scene, Complete, Unable, and Cancelled. Mission type is a choice field with values Search and Rescue Boat, Search and Rescue High Water Vehicle, Aviation Hoist, Route Clearance, Levee and Sandbag Operations, Commodity Distribution, Shelter Support, Security and Traffic Control, Power and Generator Support, and Communications Support. Asset status is a choice field with values Available, Committed, En Route, and Deadlined.
>
> A mission request belongs to one parish and is assigned to one unit. A unit owns many assets and many personnel.
>
> Include these flows. When a new mission request is submitted through the portal, notify the JOC watch and send an acknowledgement with the mission number to the requesting parish. When a mission is assigned to a unit, notify that unit's commander and the requesting parish. When a mission status changes to Complete, notify the requesting parish. When a mission with Immediate priority has not been acknowledged within ten minutes, notify the Battle Captain; if it is still unassigned after twenty minutes notify the Operations Sergeant Major; if it is still unassigned after thirty minutes notify the JTF Commander. When a mission has had no status update for four hours, flag it as stale and notify the assigned unit commander and then the Battle Captain. At each shift change at 0600 and 1800, generate a handover packet listing open missions, committed assets, and stale missions. When an asset status changes to Deadlined, notify support operations and flag any missions assigned to that asset.
>
> Include a Copilot Studio agent on the parish portal that guides parish emergency managers through submitting a mission request by asking for the number of people affected, the exact location, water depth at the access point, road access and route, medical needs, animals on site, and a callback number, and then creates the mission request record.
>
> Include reporting showing open missions by status and parish, asset availability by type, personnel accountability by unit, average time from receipt to completion by priority, and cumulative mission results.

---

## 8. Trainer cue card

*Print this page. Keep it on the lectern.*

**Timing:** 15 intro · 45 discovery · 240 build block · 15 wrap
**Build block:** 15 setup · 45 worksheet · 10 share-out · 15 break · 20 demo · 35 generate · 10 checkpoint · 15 break · 45 build+explore · 10 write · 20 AAR

**The one line:** *The description is the system.*

**Four discovery questions → what they feed**

| Question | Feeds |
|---|---|
| What problem? | Opening lines of the description; scope |
| Who touches it? | **Roles → user stories.** Highest leverage. Internal vs external decides app type |
| What does it hold? | Tables, columns, choice values, relationships |
| What does each open? | Technology proposal — model-driven / canvas / portal / dashboard |

**Four design topics:** workflows and escalation (trigger→action ×3 min; named position + a clock) · agent (what job, not what tech) · reporting (which columns produce that number?) · fallback (PACE, and who reconciles)

**Rescue phrases**

- "Before the solution — what's actually going wrong today?"
- "Which of these people has a state Guard account?"
- "Priority of *what values*?"
- "Give me the sentence: when this happens, that person gets this."
- "Who gets woken up, and at what point? Name the position."
- "Which columns produce that number?"
- "It's 0300, one bar of signal, wet gloves — what's on the screen?"
- "Rank doesn't settle a design argument. Who sees it differently?"
- "Two more minutes, then write what you've got and move on."

**Don't forget**

- **One editor per plan** — assign a driver per team
- Power Pages needs **System Admin + Entra** rights; may fail in the training tenant
- Power BI is **recommended, not built**
- Prompt cap ≈ **4,000 tokens / 3,000 words**, images included
- **English only**
- Nothing publishes automatically — every artifact is a **starting point**
- Verify the current UI path yourself the morning of (§2.2)
- Authorization questions → "that's a J6 and IA decision, not a capability question"

**Hard stops:** every team past **Save tables** by 2:20 of the build block · protect the fallback discussion and the AAR

---

## Sources

Product behavior in §2 is drawn from Microsoft's current documentation:

- [Use plans to create AI-powered business solutions with Copilot](https://learn.microsoft.com/en-us/power-apps/maker/plan-designer/plan-designer)
- [Use plans to create a business solution with Copilot](https://learn.microsoft.com/en-us/power-apps/maker/plan-designer/create-plan)
- [Build your solution with canvas apps, model-driven apps, flows, and agents](https://learn.microsoft.com/en-us/power-apps/maker/plan-designer/build-solution)
- [FAQ for plans in Power Apps](https://learn.microsoft.com/en-us/power-apps/maker/common/faq-plan-designer)
- [Create a plan from an existing solution](https://learn.microsoft.com/en-us/power-apps/maker/plan-designer/create-plan-from-solution)

Scenario grounding:

- [Louisiana Emergency Support Functions — GOHSEP](https://gohsep.la.gov/divisions/emergency-management/emergency-support-functions/) (ESF-16 Military Support is led by the Louisiana National Guard)
- [ICS Form 213 RR, Resource Request Message — FEMA](https://training.fema.gov/emiweb/is/icsresource/assets/ics%20forms/ics%20form%20213rr,%20resource%20request%20message%20(v3).pdf)
- [La. Guardsmen continue 24-hour rescues, flood operations — Louisiana National Guard](https://geauxguard.la.gov/la-guardsmen-continue-24-hour-rescues-flood-operations/) (scale figures used in the scenario)
