# x-understand Examples

Use these examples to preserve the spirit of the skill, not as rigid templates.

The cases below are based on public write-ups. When replacing them, prefer similarly verifiable cases over invented but plausible scenarios.

The goal is always the same:
- Build the smallest grounded model
- Use a gap -> fill -> next gap -> fill rhythm to hold attention
- When source material is provided, extract the claim -> premise -> mechanism -> implication chain first
- Anchor it in one real or clearly labeled concrete case
- Explain the mechanism, not just the label
- Give the user one practical move
- Surface one non-obvious point when it matters
- Mark one boundary
- End with one transfer check

## Example 1: Source Material

User:

> Here is a long article about Prime Video moving part of its audio/video monitoring system from a distributed serverless design to a single process on ECS/EC2. Help me understand the core logic and what I can reuse from it.

Good answer shape:

> The useful question is not "did Prime Video prove monoliths are better?" It is "what kind of coordination cost made distribution the wrong boundary for this workload?"
>
> Core logic chain: the article's main claim is that the team reduced cost and improved scale by moving a specific high-frequency workflow out of a distributed serverless architecture and into a single process. The starting premise is that the old design used Step Functions, Lambda, and S3 to coordinate several analysis steps and move intermediate video-frame data between components. The key mechanism is that frequent state transitions and repeated S3 calls made coordination itself expensive. The constraint is that this workload needed tight, repeated internal data transfer more than independent service boundaries. The implication is not "avoid microservices"; it is "place the boundary where the dominant cost is lowest."
>
> The simple model is: architecture is a boundary-placement decision. If components need to coordinate constantly and do not gain much from independent scaling or ownership, pushing them across network and storage boundaries can turn internal communication into your bottleneck. In the Prime Video case, moving intermediate transfer into memory removed a large part of that coordination tax.
>
> In practice, reuse this by asking three questions before splitting or merging a system: what crosses the boundary most often, what benefit does the boundary buy, and what does the boundary make expensive? If the answer is "lots of hot-path data crosses it, and the boundary buys little," the split is suspect.
>
> The part people often miss is that the case is about one workload boundary, not a universal architecture reversal. A product can still need services for team ownership, compliance isolation, independent release cadence, or different scale profiles.
>
> Source anchor: [InfoQ, "Prime Video Switched from Serverless to EC2 and ECS to Save Costs"](https://www.infoq.com/news/2023/05/prime-ec2-ecs-saves-costs/)
>
> Quick check: if a system has two components that exchange large intermediate files many times per request, but are owned by the same team and scale together, what would you inspect before making them separate services?

## Example 2: Conceptual Topic

User:

> Help me understand what a database index really is.

Good answer shape:

> The first useful question is not "why is an index fast?" It is "what work does the database no longer have to do?" An index is not free speed. It is an extra lookup structure that makes one access pattern cheaper, usually by letting the database avoid scanning rows that cannot match.
>
> That creates the next question: why does an index sometimes not help even when it exists? A public EnterpriseDB case described a slow PostgreSQL query over a JSON field. The team had created an index on a department name expression inside the JSON document, but the query wrapped the JSON in `jsonb_array_elements()`. PostgreSQL could not use the index because the query no longer matched the indexed expression. After rewriting the predicate to match the indexed path, `EXPLAIN` showed an `Index Scan` using the existing index.
>
> The mechanism is the point: an index is useful only when the query gives the planner a path that lines up with the index. In practice, do not ask "is this column indexed?" Ask "does this frequent query have an index that matches its filter, sort, or join shape?" Then verify with `EXPLAIN ANALYZE`, not with hope.
>
> The part people often miss is that an index is not mainly about making a database faster in general. It is about making a specific access path cheaper. If the query still needs most rows, or if the predicate is written in a way the planner cannot connect to the index, the index may help little or be skipped entirely.
>
> This model breaks if you assume more indexes are always better. On a small or write-heavy table, another index can slow inserts and updates more than it helps reads.
>
> Source anchor: [EnterpriseDB, "Query Performance Tuning in PostgreSQL: EXPLAIN ANALYZE Guide"](https://www.enterprisedb.com/blog/postgresql-query-optimization-performance-tuning-with-explain-analyze)
>
> Quick check: if an index exists on `lower(email)` but the query filters with `email = ?`, what would you check before assuming PostgreSQL will use that index?

## Example 3: Procedural Topic

User:

> Help me understand how to debug a slow API.

Good answer shape:

> The first gap to close is this: "slow" is not a cause. It is only a symptom that time disappeared somewhere. Latency is time spent across stages: network, application code, database work, downstream services, and queueing. You only get leverage once you know which stage dominates and whether the problem is normal latency or tail latency.
>
> That creates the next question: how do you find the stage that owns the delay? In a public production write-up about a real estate platform, the author noticed that averages looked fine in Grafana while P95 told a different story. Cross-year ranking queries reached multi-second tail latency, with one reported path around 7.24 seconds. By using Prometheus, Grafana, and Tempo traces, the investigation separated database time, code sections, cache behavior, and external calls instead of treating "the API" as one black box.
>
> The practical move is to instrument first, then optimize. Compare p50, p95, and p99. Pull a slow trace and a normal trace. Look for the longest span, repeated spans, serial external calls, slow database queries, cache misses, and gaps that suggest queueing or pool exhaustion. In that case study, the fixes were different for different paths: query changes, caching, and avoiding serial waits each mattered in a different place.
>
> The part people often miss is that the slowest line in a local profile is not always the production bottleneck. If requests mostly wait on an external dependency, cache miss, database scan, or queue, micro-optimizing local code mostly changes noise.
>
> This breaks when your measurements are too coarse. A single "request took 2s" metric cannot tell you where the time went.
>
> Source anchor: [Jeongil-Jeong, "API Performance P95 7s -> 0.1s Backend Optimization"](https://jeongil.dev/en/blog/backend/performance/backend-api-performance-optimization/)
>
> Quick check: if p50 stays near 200ms but p99 jumps to 4s only during traffic spikes, what category of problem should you suspect before rewriting business logic?

## Example 4: Trade-Off Topic

User:

> How should I think about monoliths vs microservices?

Good answer shape:

> The real question is not "which architecture is more modern?" It is "where should coordination live?" A monolith keeps coordination inside one deployable unit or process. Microservices move coordination across network and ownership boundaries. That can help when teams, scale profiles, or release cadences genuinely differ, but it also adds orchestration, serialization, observability, retry, and partial-failure cost.
>
> That creates the next question: when is the extra coordination cost worth paying? Prime Video's audio/video monitoring team published a case where their distributed serverless design used Step Functions, Lambda, and S3 for intermediate data. At scale, frequent state transitions and many S3 calls became expensive, and the architecture hit scaling limits. They packed the components into a single process running on ECS/EC2, moved intermediate transfer into memory, simplified orchestration, and reported over 90% infrastructure cost reduction.
>
> The mechanism is not "monolith beats microservices." The mechanism is that their workload had high-frequency internal coordination and little benefit from distributing those particular steps. Moving the boundary inward made the hot path cheaper. In practice, split a system when a boundary has a concrete reason: independent scale, isolation, team ownership, compliance, or release cadence. Do not split just because "services" sound cleaner.
>
> The part people often miss is that microservices can increase local team pain before they increase autonomy. You gain independent scaling and ownership only after you can absorb service discovery, observability, retries, versioning, and partial-failure handling.
>
> This model breaks if the monolith has already become a coordination bottleneck for independently evolving domains. At that point, refusing to split can also be expensive. The boundary should follow pressure, not fashion.
>
> Source anchor: [InfoQ, "Prime Video Switched from Serverless to EC2 and ECS to Save Costs"](https://www.infoq.com/news/2023/05/prime-ec2-ecs-saves-costs/)
>
> Quick check: if one subsystem needs strict isolation and audits but traffic is low, what could justify splitting it even before scale pressure appears?

## Rule Of Thumb

If the answer sounds neat but the user still would not know what to look for, what to do, or what to mistrust, the model is still too shallow.
