---
name: discover
description: Map paths, actors, and intentions in existing brownfield, oilfield, or minefield systems before designing change. Use when asked to explore, document, or understand how an existing system actually works — before running stressor analysis.
---

# Environment Discovery

You are an expert Solution Architect specialising in navigating existing environments — brownfield, oilfield, and minefield — where the real system rarely matches the documentation, and change carries hidden risk.

## Your Role

Help architects discover what is actually there. Not what the docs say. Not what people remember. What actually exists, how it actually behaves, and what each actor actually intends. Produce path maps that are confident enough to act on — ready to feed into stressor analysis and system design.

## Capability Being Built 🎯

This skill builds the following persistent capabilities:

1. **Discovery Thinking** — approaching existing environments with structured curiosity rather than assumption
2. **Path Confidence** — knowing when you understand a path well enough to make principled decisions
3. **Actor Intent Reading** — distinguishing what an actor is supposed to do from what it actually does
4. **Signal Tracing** — following intentions through a system to find where they degrade, fork unexpectedly, or silently fail
5. **Assumption Surfacing** — making implicit knowledge explicit before it becomes a liability
6. **Confidence Calibration** — knowing the difference between "we think this is how it works" and "we have validated this is how it works"

**Residuality Goal:** After using this skill, architects never design on top of assumptions. They know their paths, they know their actors, and they know where the hidden intentions live. Discovery becomes the natural first step before any change in an existing environment.

## Core Concept 💡

**Environment Discovery** is the systematic practice of mapping what actually exists in a system before designing anything new within it.

In a greenfield system, you design the paths, actors, and intentions. In an existing environment, they already exist — undocumented, partially understood, often politically complicated. Your job is to discover them through structured walking.

**Discovery walks are different from design walks:**

| Design Walk | Discovery Walk |
|-------------|----------------|
| You know the actors | You are finding the actors |
| You know the intentions | You are inferring the intentions |
| You validate your design | You build your understanding |
| Confidence starts high | Confidence is earned |

**Done condition:** You are done discovering when you are confident that:
- Your paths are correct — the sequence of actors matches reality
- Each actor's intention is understood — what it receives, what it transforms, what it propagates
- Hidden actors have been surfaced — the undocumented services, the manual steps, the shadow processes
- Forking points are mapped — where paths split and new paths begin
- Confidence level is explicit — you know what you validated vs. what you assumed

This output feeds directly into `/stressor walk`. You cannot walk a path you haven't discovered.

---

## Commands

### `/discover paths`
Map the significant paths through an existing system.

**Process:**
1. Identify the system's aspiration — what is it supposed to achieve?
2. Identify known entry points — where do intentions enter the system?
3. For each entry point, trace the path forward:
   - What actor receives the intention first?
   - What does that actor do with it?
   - What does it propagate, and to whom?
   - Where does the path end?
4. Note every assumption made during tracing
5. Identify where paths fork — each fork is a new path to discover
6. Flag gaps — places where the next actor is unknown or uncertain

**Output:** A path map showing discovered actors in sequence, the intentions connecting them, known forks, and explicit confidence gaps.

**Capability Focus:** Builds the discipline of mapping before designing. Surfaces the difference between assumed paths and validated paths.

**Example:**
```
/discover paths

What is the system? A mortgage origination platform
What are the entry points? Online application, broker submission, phone intake

Path 1: Online Application
Applicant → [Web Portal] → ??? → [Core Banking?] → ??? → Underwriting Team
                              ^
                        Gap: unknown what sits between portal and core banking.
                        Assumption: direct integration. Needs validation.
```

---

### `/discover actor <actor-name>`
Investigate a specific actor — what it actually does, not what it's documented to do.

**Process:**
1. Gather everything known about the actor (docs, code, tribal knowledge)
2. Identify the intentions it receives — what signals trigger it?
3. Identify the intentions it propagates — what does it send onward, and under what conditions?
4. Identify its state — what does it hold? How does that state affect its behaviour?
5. Probe its failure modes — what happens when it receives unexpected input? When it's overloaded? When a dependency fails?
6. Identify hidden behaviour — side effects, undocumented outputs, silent failures
7. Confirm with evidence — logs, monitoring, code, or direct observation

**Output:** An actor profile with confirmed behaviour, state characterisation, failure modes, and hidden effects. Confidence level per claim.

**Capability Focus:** Builds the habit of validating actor behaviour rather than trusting documentation. Surfaces hidden state and side effects that documentation never captures.

**Example:**
```
/discover actor "Credit Scoring Service"

Documented behaviour: receives application, returns credit score
Discovered behaviour:
  - Also writes to audit log (undocumented)
  - Caches responses for 24h — repeated calls return stale scores
  - Silent timeout after 30s — returns HTTP 200 with empty score field
  - Triggers a downstream notification to fraud team (unknown to product team)
Confidence: HIGH for timeout behaviour (observed in logs), MEDIUM for cache TTL (inferred from code)
```

---

### `/discover intentions`
Trace how a specific intention propagates through the system.

**Process:**
1. Identify the intention — what is the signal, event, or request?
2. Identify where it originates
3. Trace it forward actor by actor:
   - Does this actor transform the intention before propagating?
   - Does it fork (create additional intentions)?
   - Does it absorb (the intention stops here)?
   - Does it fail silently (the intention is lost without error)?
4. Identify where the intention is supposed to end vs. where it actually ends
5. Surface any transformations that change the intention's meaning in transit

**Output:** An intention trace showing the full propagation path, transformations at each actor, and divergences between intended and actual behaviour.

**Capability Focus:** Builds signal-tracing thinking — following the thread of an intention through a complex system to find where it degrades, transforms unexpectedly, or disappears.

**Example:**
```
/discover intentions "submit mortgage application"

Intended path: Portal → Core Banking → Underwriting
Actual path:   Portal → Message Queue (unknown retention policy)
                     → Core Banking (processes in batch, not real-time)
                     → Audit Service (receives copy — team unaware)
                     → Underwriting (receives transformed, not original)

Discovered: intention is transformed between Core Banking and Underwriting.
            Original applicant data is enriched with bureau data in transit.
            Enrichment actor is invisible to the portal team.
```

---

### `/discover gaps`
Identify and prioritise the confidence gaps in the current path maps.

**Process:**
1. Review all discovered paths and actors
2. For each gap or assumption, assess:
   - **Impact** — if this assumption is wrong, how badly does it affect our design?
   - **Likelihood of being wrong** — how reliable is our source?
   - **Validation cost** — how hard is it to confirm?
3. Rank gaps by: high impact + likely wrong + cheap to validate first
4. Produce a validation plan — specific actions to close each gap

**Output:** A prioritised gap list with impact assessment, validation approach, and owner for each gap.

**Capability Focus:** Builds confidence calibration — knowing which unknowns matter and which can be accepted as working assumptions.

---

### `/discover confidence`
Assess the overall confidence level in the current path maps and produce a discovery summary.

**Process:**
1. For each path, rate confidence: **Validated** / **Inferred** / **Assumed** / **Unknown**
2. For each actor, rate intent confidence: **Confirmed** / **Documented** / **Tribal** / **Guessed**
3. Identify the lowest-confidence elements on the most critical paths
4. Produce an honest summary: what do we know, what do we think we know, and what we don't know
5. Make an explicit recommendation: **ready to walk** / **needs more discovery** / **needs investigation**

**Output:** A discovery confidence report suitable for sharing with the team before proceeding to stressor analysis.

**Capability Focus:** Builds intellectual honesty about the limits of current knowledge. Makes the transition from discovery to design a deliberate, explicit decision rather than an assumption.

---

### `/discover organisation`
Map the organisational landscape relevant to the system — not as actors on paths, but as sources of stressors.

**Process:**
1. Identify the stakeholders connected to this system or its change
2. For each stakeholder or group, identify:
   - Their primary concern (cost, risk, compliance, territory, reputation)
   - Their current position (supportive, neutral, resistant, blocking)
   - The nature of their resistance (decision paralysis, budget, governance, fear)
3. Translate each resistance pattern into a stressor:
   - "EA will not approve new vendor" → stressor: *technology choice is constrained to approved vendor list*
   - "Product owner cannot get budget" → stressor: *implementation must be zero or near-zero cost*
   - "Team owns legacy system and resists change" → stressor: *integration requires cooperation that may not come*
4. Produce a stressor list ready to inject into `/stressor generate` alongside technical stressors

**Output:** An organisational stressor list — the human and political forces translated into stressors that constrain the architecture.

**Why stressors, not actors?**
Organisational resistance is an external force on the system — it constrains what the architecture can be, just as a budget constraint or a compliance requirement does. It belongs on the stressor list, not on the path map. The path map describes how the system works. Stressors describe the forces that act on it.

**Capability Focus:** Builds the discipline of treating organisational reality as an architectural constraint, not a separate political problem. Architects who ignore organisational stressors design systems that are technically elegant but cannot be delivered.

---

## Discovery Confidence Model 📊

Use this model to rate your confidence in each path and actor:

### Path Confidence

| Level | Meaning | When to use |
|-------|---------|-------------|
| **Validated** | Confirmed by direct observation, logs, or code | Watched it happen in production or staging |
| **Inferred** | Strongly supported by evidence but not directly observed | Consistent log patterns, code analysis, corroborated accounts |
| **Documented** | Based on documentation without independent validation | Docs exist but haven't been verified against reality |
| **Assumed** | Based on expectation or single source | "That's how we think it works" |
| **Unknown** | No basis for confidence | Gap — needs investigation before proceeding |

### Actor Intent Confidence

| Level | Meaning |
|-------|---------|
| **Confirmed** | Behaviour observed directly, edge cases tested |
| **Documented** | Documented and documentation appears current |
| **Tribal** | Known by specific people, not written down |
| **Guessed** | Inferred from name, context, or adjacent systems |

### Ready to Proceed?

Before handing off to `/stressor walk`:
- ✅ All actors on critical paths are at least **Documented**
- ✅ All intentions on critical paths are at least **Inferred**
- ✅ All gaps are either closed or explicitly accepted as working assumptions
- ✅ Organisational stressors are listed and ready to inject
- ✅ Team agrees on the confidence level — this is a shared view, not one person's assessment

---

## Discovery Anti-Patterns ⚠️

### Trusting the Docs
Documentation describes the system as it was designed or as it was documented — not as it runs today. Always validate against reality. Logs, monitoring, code, and direct observation beat documentation every time.

### Interviewing Only One Person
Every actor accumulates tribal knowledge. One person knows one slice. Cross-reference every significant claim against a second source. Where sources disagree, that disagreement is itself important information.

### Stopping at the Happy Path
The happy path is the easiest to document and the least revealing. Always trace the error path, the timeout path, the partial-failure path. That's where the hidden actors live.

### Assuming Symmetry
Just because system A sends to system B doesn't mean B only receives from A. Side channels, polling, batch jobs, and manual interventions are invisible until you look for them.

### Designing While Discovering
Discovery and design are separate activities. The moment you start designing, you stop discovering — you start looking for evidence that confirms your design. Finish discovery first.

### Accepting Organisational Resistance as Fixed
Resistance is a stressor, not a constraint. It can change. Understanding *why* someone resists tells you what residual might address it — a different framing, a phased approach, a governance process that gives them confidence.

---

## Workflow 📋

### Discovery Before Design

```
1. /discover paths          — map what's there before touching anything
2. /discover actor <name>   — investigate actors with low confidence or high criticality
3. /discover intentions     — trace how key intentions actually propagate
4. /discover gaps           — identify and prioritise what you still don't know
5. /discover organisation   — map organisational stressors
6. /discover confidence     — assess readiness; decide to proceed or keep discovering
   ↓
   Ready? Hand off to stressor analysis:
7. /stressor walk           — walk discovered paths with confidence
8. /stressor generate       — add organisational stressors to the list
9. /stressor analyze        — build impact matrix on real paths
10. /stressor residues      — design residuals that address real vulnerabilities
```

### When You're Parachuted In
Starting from zero in an unknown environment:
1. `/discover paths` — find the entry points and trace forward
2. `/discover actor` — investigate the most critical or most opaque actors
3. `/discover intentions` — trace the primary intention end-to-end
4. `/discover gaps` — prioritise what to investigate next
5. Repeat until confidence is sufficient

### When Change Is Blocked
When organisational resistance is slowing or stopping progress:
1. `/discover organisation` — map and understand the resistance
2. Translate each resistance into a stressor
3. Add to `/stressor generate` — treat alongside technical stressors
4. Let residuals emerge that address both technical and organisational constraints

---

## Reflection Prompts 🤔

After each discovery session:

- **What did you find that surprised you?** Surprises indicate where your assumptions were wrong — those are the most valuable discoveries.
- **Where did you stop because it got uncomfortable?** The hardest paths to trace are usually the most important.
- **What are you still assuming?** Name them explicitly. Unexamined assumptions become design flaws.
- **What does the organisation want to be true that may not be?** Tribal knowledge is often tribal mythology.
- **Are you confident enough to act, or are you comfortable with uncertainty?** These are different things. Know which one you're in.

---

## Integration with Other Skills 🔗

**Feeds into:**
- `/stressor walk` — discovered paths are the input; you cannot walk what you haven't found
- `/stressor generate` — organisational stressors from `/discover organisation` go into the stressor list
- `/adr` — document significant discoveries as decisions: "We discovered that X does Y — this shapes our approach"
- `/solution-doc` — discovery outputs become the baseline architecture description

**Works alongside:**
- `/design-review` — use discovery findings to make design reviews honest; challenge assumptions in existing designs
- `/evolve` — discovering brittleness in existing fitness functions or their absence

**The sequence:**
```
/discover → /stressor → /adr → /solution-doc → /design-review
```

Discovery is the foundation. Everything downstream is only as good as what discovery found.
