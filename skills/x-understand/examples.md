# x-understand Examples

Use these examples to preserve the spirit of the skill, not as rigid templates.

The goal is always the same:
- Build the smallest grounded model
- Use a gap -> fill -> next gap -> fill rhythm to hold attention
- Anchor it in one real or clearly concrete case
- Explain the mechanism, not just the label
- Give the user one practical move
- Surface one non-obvious point when it matters
- Mark one boundary
- End with one transfer check

## Example 1: Conceptual Topic

User:

> Help me understand what a database index really is.

Good answer shape:

> The first useful question is not "why is an index fast?" It is "what work does the database no longer have to do?" An index is not free speed; it is paying storage and write cost to avoid repeated scanning. The database keeps an extra lookup structure ordered by one or more fields, so it can jump near matching rows instead of checking every row.
>
> That creates the next question: when is that extra structure worth maintaining? A concrete case: imagine an `orders` table with 20 million rows. Support agents often search `WHERE customer_email = ?` to find one customer's order history. Without an index on `customer_email`, the database may need to scan row after row. With the index, it can narrow to the relevant rows quickly because the lookup path is already organized around that field.
>
> In practice, the move is simple: add indexes for queries you run often and that filter down to a small subset of rows, then re-check write cost and storage. Do not add an index just because a column sounds important.
>
> The part people often miss is that an index is not mainly about "making the database faster." It is about making a specific access pattern cheaper. If a query still needs most of the table, the index may help little or be skipped entirely.
>
> This model breaks if you assume more indexes are always better. On a small or write-heavy table, another index can slow inserts and updates more than it helps reads.
>
> Quick check: if a table is filtered mostly by `status` and 95% of rows share the same status, why might an index on `status` help less than expected?

## Example 2: Procedural Topic

User:

> Help me understand how to debug a slow API.

Good answer shape:

> The first gap to close is this: "slow" is not a cause. It is only a symptom that time disappeared somewhere. Latency is time spent across stages: network, application code, database work, downstream services, and queueing. You only get leverage once you know which stage dominates and whether the problem is normal latency or tail latency.
>
> That creates the next question: how do you find the stage that owns the delay? A concrete case: a `POST /checkout` endpoint shows 1.8s at p95. Tracing reveals only 150ms in application code, 900ms waiting on the payment provider, 500ms in the inventory database, and the rest in serialization and network overhead. That immediately changes the question from "which function is slow?" to "which dependency owns the latency budget?"
>
> In practice, measure before optimizing: add tracing or timing around major stages, compare p50, p95, and p99, then attack the biggest bucket first. If p50 is fine but p99 is terrible, suspect queueing, lock contention, connection pool starvation, or retries before rewriting business logic.
>
> The part people often miss is that the slowest line in a local profile is not always the real bottleneck. If requests mostly wait on an external dependency, micro-optimizing local code mostly changes noise.
>
> This breaks when your measurements are too coarse. A single "request took 2s" metric cannot tell you where the time went.
>
> Quick check: if p50 is 200ms but p99 jumps to 4s only during traffic spikes, what category of problem should you suspect first, and why?

## Example 3: Trade-Off Topic

User:

> How should I think about monoliths vs microservices?

Good answer shape:

> The real question is not "which architecture is more modern?" It is "where should coordination live?" A monolith keeps most coordination inside one codebase and one deployable unit. Microservices move some of that coordination across network boundaries, which can help independent scaling and ownership, but only by adding operational, debugging, and failure-handling cost.
>
> That creates the next question: when is the extra coordination cost worth paying? A concrete case: imagine a 6-engineer B2B SaaS team shipping from one monolith several times a day. They split billing into a separate service because it needs stricter compliance controls and a different release cadence from the rest of the app. That is a focused reason. Splitting the whole product at once would create many service contracts and deployment dependencies before the team had enough pressure to justify them.
>
> In practice, stay monolithic until one boundary has a concrete reason to separate: a different scale profile, a hard isolation requirement, a clear ownership boundary, or a different release cadence. "We want cleaner architecture" alone is usually not enough reason to pay distributed-system tax.
>
> The part people often miss is that microservices can increase local team pain before they increase autonomy. You gain scaling options only after you can absorb service discovery, observability, retries, versioning, and partial-failure handling.
>
> This model breaks if the monolith has already become a coordination bottleneck for independently evolving domains. At that point, refusing to split can also be expensive.
>
> Quick check: if one subsystem needs strict isolation and audits but traffic is low, what could justify splitting it even before scale pressure appears?

## Rule Of Thumb

If the answer sounds neat but the user still would not know what to look for, what to do, or what to mistrust, the model is still too shallow.
