# Exercise Patterns

Six exercise types ordered by cognitive demand, plus an executable variant of Predict.

### 1. Predict (Mandatory — at least once per topic)

Force the learner to run their mental model forward.

**Format:** "Given [setup], what happens when [change]? Why?"

**What it tests:** Whether the learner has a working internal model, not just facts.

**Examples:**
- "Your Raft cluster has 5 nodes. The leader goes down mid-heartbeat. Node C has a stale log. Walk me through what happens next, message by message."
- "You have a B+ tree index with fill factor 80%. You insert 1000 sequential keys. What does the tree look like after? What about 1000 random keys?"
- "Your Django app handles 100 req/s. You add a Celery task that takes 3s per request for 20% of traffic. What happens to your RabbitMQ queue depth over 10 minutes?"

**Evaluation:** The learner must describe the mechanism, not just the outcome. "The queue grows" is insufficient. "Ingress is 20 tasks/s; with N workers the drain is N/3 tasks/s, so with fewer than 60 workers the queue grows by 20 − N/3 per second" shows understanding.

### 1b. Predict → Run → Reconcile (preferred when the concept is executable)

Same as Predict, but reality grades the answer.

1. Write a minimal script (under ~20 lines) or command in the scratchpad that exhibits the behaviour. Show it.
2. The learner commits to a prediction *with reasoning* before anything runs.
3. Run it.
4. Reconcile: if the prediction was wrong, the learner explains the discrepancy before you do. If right, change one variable and repeat.

**Examples:**
- "Here's a script with two threads incrementing a shared counter 1M times each, no lock. What's the final value? Will it be the same each run?" (Then try with the GIL-releasing variant.)
- "Here's an `EXPLAIN ANALYZE` of a query on a 1M-row table. I'm going to add a composite index on `(status, created_at)`. Predict the new plan."
- "I'll `git commit` one file change. Predict exactly which new objects appear in `.git/objects` and why."

**Evaluation:** A wrong prediction followed by a correct reconciliation is a great outcome — that's the model updating.

### 2. Break It

Find failure modes. Reveals whether they understand boundaries, not just the happy path.

**Format:** "Here's a working [system/algorithm/design]. How would you make it fail?"

**Examples:**
- "Here's a two-phase commit protocol. Design a scenario where it blocks indefinitely."
- "This rate limiter uses a fixed window. Craft a request pattern that lets you send 2x the limit."
- "This microservice uses eventual consistency. Describe a user-visible bug this creates."

**Evaluation:** Award strong marks for non-obvious failure modes. Anyone can say "what if the server crashes." The interesting failures are subtle: race conditions, edge-case ordering, semantic violations.

### 3. Teach Back

Compression reveals gaps.

**Format:** "Explain [concept] to [audience] in [constraint]."

**Audience variants:** A junior engineer, a smart non-technical person, a peer who knows adjacent concepts.
**Constraint variants:** 3-4 sentences max, without using [key jargon terms], using only an analogy.

**Evaluation:** Check for: correctness of core insight, appropriate level for audience, absence of hand-waving, whether it would actually help someone understand.

### 4. Design From Scratch

Remove the known solution and make the learner invent.

**Format:** "You need to solve [problem]. You don't know about [standard solution]. Design something."

**Follow-up (always):** Show the standard solution and ask: "What did your design get right? What did it miss? Why did the real solution make different choices?"

**Evaluation:** Quality of the comparison matters more than quality of initial design.

### 5. Debug the Reasoning

Present a flawed explanation. Make the learner find the error.

**Format:** "Here's an explanation of [concept]. It has a subtle error. Find it."

**Difficulty levels:**
- Easy: Factual error (wrong mechanism named)
- Medium: Logical error (confusing related but different concepts)
- Hard: Plausible but subtly wrong reasoning (ignoring second-order effects)

**Evaluation:** Identifying the error is 40%. Explaining *why* it's wrong is 60%.

**Always close the loop:** after their answer, state the planted error and the correct version explicitly — even if they found it — so no wrong version survives the session.

### 6. Constrained Redesign

Adapt a known solution under new constraints.

**Format:** "You're using [standard approach]. Now [new constraint]. How do you adapt?"

**Examples:**
- "Your system uses a centralized message queue. Now no single point of failure allowed. Redesign."
- "Your API returns paginated results using offset. Now you have 100M rows and offset is too slow. What changes?"

**Evaluation:** Strong answers consider what the constraint eliminates, explore tradeoffs, don't just jump to the first valid solution.

### Exercise Selection Guide

| Concept Type | Best Exercises | Why |
|---|---|---|
| Algorithms/data structures | Predict, Break It, Design From Scratch | Need mechanism understanding |
| System design patterns | Constrained Redesign, Break It, Teach Back | Need tradeoff reasoning |
| Protocols/standards | Predict, Debug the Reasoning | Need state transition understanding |
| Architectural concepts | Design From Scratch, Constrained Redesign | Need "why this" not just "what" |
| New language/framework | Predict, Teach Back | Need working mental model |
| Theory/math | Predict, Debug the Reasoning, Design From Scratch | Need axiom-based reasoning |

### Exercise Sequencing

1. Start with **Predict** — establishes whether the basic model works
2. Follow with **Break It** or **Debug** — probes edges of understanding
3. Close with **Teach Back** or **Design From Scratch** — forces synthesis
