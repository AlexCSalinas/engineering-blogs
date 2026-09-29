# Zero-Sum by Design: 10 Years of Uber's Payments Platform

**Link:** https://www.uber.com/us/en/blog/ubers-payments-platform/
**Author(s):** Nimish Sheth, Manas Kelshikar, Dhirendra Kumar Singh (with Rajan Jana, Wasim Raza)
**Published:** 2026-08-06 · Uber Engineering
**Topics:** `distributed-systems` `ledgers` `api-design` `correctness`
**Added by:** @AlexCSalinas

## Why it's worth reading

A ten-year retrospective on a system that moves hundreds of billions of dollars a year — nearly double Uber's gross bookings in total money movement — written by the people who kept it from being rewritten. The interesting claim isn't any single piece of infrastructure; it's that two invariants chosen early (immutability and zero-sum) are what let Freight, Hotels, and Ads onboard later without re-architecting the core. That's the rare blog post about which abstractions held.

## Summary

Uber's payments platform, internally Gulfstream, models every financial event as an immutable "money order" whose entries sum to zero — double-entry bookkeeping as a system invariant rather than an accounting convention. Because nothing is ever mutated and nothing can be created or destroyed, the ledger is self-auditable and reconciliation becomes a query instead of a pipeline. The post then covers what scaling that model actually cost: strongly consistent balances for 1.2B+ entities, a custom storage layer, and a fix for hot entities that serialized under contention.

## Key takeaways

- **Immutable money orders + zero-sum entries.** Every transaction is append-only and its entries must sum to zero, so money can't be created or destroyed by a bug. The invariant is cheap to check and makes the system auditable by construction.
- **Strongly consistent balances at 1.2B+ entities.** Balances live in DynamoDB as a single row per entity, with aggressive pruning of zero-balance accounts to keep row sizes bounded — a concrete answer to "how do you keep a hot row from growing forever."
- **The hot entity problem, and a 10x fix.** High-traffic B2B ledger entities serialized on writes; a batch-write mechanism raised throughput ~10x. Familiar shape for anyone who's hit per-key write limits.
- **Generic abstractions are what bought the decade.** Line-of-business-agnostic money orders and payment-instrument-agnostic integration interfaces meant new products plugged in instead of forking the platform.
- **LedgerStore: building storage instead of buying it.** Off-the-shelf databases didn't give them tamper-evident, auditable records under regulatory constraints, so they built the layer. The post is reasonably candid about that being an expensive call.

## Notes

Read alongside the standard double-entry ledger literature if you're designing anything that holds balances — the "sum to zero or reject" invariant is the part most in-house ledgers skip and later regret.
