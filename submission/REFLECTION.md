# Reflection
## My FullName: Mac Phuong Nga
## Student ID: 2A202600124

The anti-pattern we are most at risk of is writing directly to a "gold" table from multiple ad-hoc jobs without a controlled silver contract. It is tempting because dashboard consumers ask for fast changes, but this creates schema drift, silent duplicates, and non-reproducible business metrics.

In our data, retries are common (~5 percent duplicate request_id). If dedup is skipped or done inconsistently in different jobs, p95 latency and cost_usd can shift without any real product change. That would break trust in the observability dashboard.

The Day 18 medallion split prevents this. Bronze keeps raw immutable events, silver enforces typed/deduped records, and gold only aggregates from silver. Combined with Delta history and restore, we can audit what changed, rollback bad writes quickly, and explain metric differences version by version.

So the core lesson for us is: optimize later, but lock the contract between silver and gold early.
