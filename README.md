# Engineering Blogs

A curated index of software engineering blog posts worth your time — read, summarized, and filed by a few of us who got tired of losing good links in Slack threads and browser tabs.

Every entry is one Markdown file with the link, a short summary, and the takeaways that made it worth keeping. GitHub renders it all, so the whole thing is browsable without cloning anything.

**Want in?** See [CONTRIBUTING.md](CONTRIBUTING.md). One post per pull request.

---

## The index

| Post | Company | Topics | Published |
|---|---|---|---|
| [Performing Live Migrations of Massive VMs at Scale](blogs/sail-live-migrations-massive-vms.md) | Sail Research | virtualization, linux-internals, cost-engineering | 2026-07-14 |
| [Zero-Sum by Design: 10 Years of Uber's Payments Platform](blogs/uber-payments-platform-10-years.md) | Uber | distributed-systems, ledgers, api-design | 2026-08-06 |
| [GenRec: Towards LLM-Native Recommendation at Netflix](blogs/netflix-genrec-llm-native-recommendation.md) | Netflix | ml-systems, recsys, llm-serving | 2026-07-30 |

---

## Browse by topic

**Infrastructure & systems**
- [Performing Live Migrations of Massive VMs at Scale](blogs/sail-live-migrations-massive-vms.md) — `userfaultfd` demand paging, L4 proxies, and virtio-mem to move live VMs in seconds

**Distributed systems & data**
- [Zero-Sum by Design: 10 Years of Uber's Payments Platform](blogs/uber-payments-platform-10-years.md) — immutable money orders, zero-sum accounting, and the hot-entity problem at 1.2B ledger entities

**ML systems**
- [GenRec: Towards LLM-Native Recommendation at Netflix](blogs/netflix-genrec-llm-native-recommendation.md) — post-training a foundation model as a ranker, and serving it prefill-only on vLLM

---

## Conventions

- One file per post under [`blogs/`](blogs), named `company-short-title.md`.
- Copy [`blogs/_TEMPLATE.md`](blogs/_TEMPLATE.md) to start.
- Summaries are written from actually reading the post. No abstract-skimming, no LLM slop.
- Add your entry to both tables above in the same PR.
