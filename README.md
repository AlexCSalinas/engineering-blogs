# Engineering Blogs

A curated reading list of software engineering blog posts worth your time — read, summarized, and kept somewhere better than a Slack thread.

Everything lives in this one file. Adding a post means adding a section below; no new files, no directory to navigate. See [Adding a post](#adding-a-post).

**Jump to:** [Infrastructure & systems](#infrastructure--systems) · [Distributed systems & data](#distributed-systems--data) · [ML systems](#ml-systems)

---

## Infrastructure & systems

### Performing Live Migrations of Massive VMs at Scale

**[sailresearch.com](https://www.sailresearch.com/blog/performing-live-migrations-of-massive-vms-at-scale)** · Sail Research · Nirvik Baruah, Charley Cunningham · 2026-07-14
`virtualization` `linux-internals` `firecracker` `cost-engineering` · added by @AlexCSalinas

Most live-migration writeups stop at "we use pre-copy and it works." This one starts from a business constraint — VMs priced at $0.015/vCPU-hour, roughly 70% below competitors — and walks backwards through the three mechanisms that constraint forces on you. A clean example of picking an SLO and letting it buy you an order of magnitude on cost.

- **L4 proxying keeps connections alive across the move.** A persistent proxy terminates TCP outside the VM while an in-guest sidecar maintains connectivity, so SSH and other long-lived sessions survive a migration instead of resetting.
- **Demand paging over P2P beats pre-copy for large memory.** `userfaultfd` at 2MB granularity lets the destination start running and fault pages in from the source, with S3 as fallback. Transitions land in seconds, largely independent of VM size.
- **virtio-mem makes memory elastic, not provisioned.** Firecracker VMs scale from a small baseline to 64–128GB on demand and shrink back within seconds — you pay for the working set, not the ceiling.
- **The latency/cost trade is stated outright.** A few seconds of occasional latency is what funds the 70% price gap. Worth stealing as a template for arguing an availability trade-off on economics rather than vibes.
- Nice adversarial test: a Minecraft server kept alive through migrations every two minutes, for dozens of cycles.

---

## Distributed systems & data

### Zero-Sum by Design: 10 Years of Uber's Payments Platform

**[uber.com](https://www.uber.com/us/en/blog/ubers-payments-platform/)** · Uber · Nimish Sheth, Manas Kelshikar, Dhirendra Kumar Singh · 2026-08-06
`distributed-systems` `ledgers` `api-design` `correctness` · added by @AlexCSalinas

A ten-year retrospective on a system that moves hundreds of billions of dollars a year — nearly double Uber's gross bookings in total money movement — by the people who kept it from being rewritten. The interesting claim isn't any single piece of infrastructure; it's that two invariants chosen early are what let Freight, Hotels, and Ads onboard later without touching the core. Rare post about which abstractions actually held.

- **Immutable money orders + zero-sum entries.** Every transaction is append-only and its entries must sum to zero, so money can't be created or destroyed by a bug. Cheap to check, and makes the ledger auditable by construction.
- **Strongly consistent balances at 1.2B+ entities.** One DynamoDB row per entity, with aggressive pruning of zero-balance accounts to keep row sizes bounded — a concrete answer to "how do you stop a hot row from growing forever."
- **The hot entity problem, and a 10x fix.** High-traffic B2B entities serialized on writes; a batch-write mechanism raised throughput ~10x. Familiar shape if you've hit per-key write limits.
- **Generic abstractions bought the decade.** LOB-agnostic money orders and payment-instrument-agnostic integrations meant new products plugged in instead of forking the platform.
- **LedgerStore: built, not bought.** Off-the-shelf databases couldn't give tamper-evident records under their regulatory constraints. The post is reasonably candid that this was expensive.

---

## ML systems

### GenRec: Towards LLM-Native Recommendation at Netflix

**[netflixtechblog.com](https://netflixtechblog.com/genrec-towards-llm-native-recommendation-at-netflix-f20be6f643e3)** · Netflix · Ying Li, Arjun Rao, Shradha Sehgal · 2026-07-30
`ml-systems` `recsys` `llm-serving` `post-training` · added by @AlexCSalinas

Plenty of "LLMs for recsys" posts describe a prototype. This one describes a ranker that beat a well-tuned production baseline in a large-scale A/B test on both short- and long-term metrics — a much higher bar, since Netflix's existing ranker is not a straw man. Unusually direct about serving, which is where most LLM-ranking ideas quietly die.

- **Two-phase training.** Phase 1 adapts an open-source LLM to Netflix data; Phase 2 post-trains for ranking with reward weighting tied to long-term satisfaction rather than immediate clicks.
- **Context engineering replaces feature engineering.** Histories are verbalized as text under an explicit token budget, with selective compression trading quality against cost — a different discipline than maintaining a feature store, not obviously an easier one.
- **Catalog-aware scoring head.** A decoder-only backbone produces pooled representations; a ranking head scores in-catalog items by dot product or MLP. No semantic IDs, no generating item identifiers and hoping they exist.
- **10–40x fewer labeled Phase-2 examples** to match the production baseline, depending on configuration. The real argument: the win is data efficiency and transfer, not raw capacity.
- **Prefill-only serving on vLLM.** Whole candidate sets scored in one forward pass, no autoregressive decoding — what makes the cost arithmetic work at Netflix scale.
- Companion paper with the details the post compresses: [arXiv:2608.10257](https://arxiv.org/abs/2608.10257).

---

## Adding a post

Edit this file. Drop a new `###` section under whichever topic fits, matching the format above — title, source line, tags, a short why-it's-worth-reading, and a few specific takeaways. Add a new `##` topic section if none fit, and link it in **Jump to** at the top.

Copy-paste skeleton and the style bar: [CONTRIBUTING.md](CONTRIBUTING.md). One post per pull request.
