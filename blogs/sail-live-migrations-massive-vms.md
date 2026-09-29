# Performing Live Migrations of Massive VMs at Scale

**Link:** https://www.sailresearch.com/blog/performing-live-migrations-of-massive-vms-at-scale
**Author(s):** Nirvik Baruah, Charley Cunningham
**Published:** 2026-07-14 · Sail Research
**Topics:** `virtualization` `linux-internals` `firecracker` `cost-engineering`
**Added by:** @AlexCSalinas

## Why it's worth reading

Most live-migration writeups stop at "we use pre-copy and it works." This one starts from a business constraint — VMs for long-horizon AI agents priced at $0.015/vCPU-hour, roughly 70% below competitors — and walks backwards through the three mechanisms that constraint forces on you. It's a clean example of picking an SLO (a few seconds of latency during occasional migrations) and letting it buy you an order of magnitude on cost.

## Summary

Sail Research runs "Sailboxes": Firecracker microVMs that can be relocated between hosts without dropping persistent connections. Migration is built from three pieces that compose — an L4 network proxy that keeps TCP alive across the move, demand-paged peer-to-peer memory transfer so the destination boots before memory has arrived, and virtio-mem so a VM's memory footprint tracks its actual working set instead of its peak. Together they make a host swap cheap enough to do routinely, which is what makes aggressive bin-packing (and the pricing) possible.

## Key takeaways

- **L4 proxying keeps connections alive across the move.** A persistent proxy terminates TCP outside the VM while an in-guest sidecar maintains connectivity, so SSH sessions and other long-lived connections survive a migration instead of being reset.
- **Demand paging over P2P beats pre-copy for large memory.** `userfaultfd` at 2MB page granularity lets the destination VM start running and fault pages in from the source on demand, with S3 as a fallback source. Full transitions land in seconds, largely independent of total VM size.
- **virtio-mem makes memory elastic, not provisioned.** Firecracker VMs scale from a small baseline up to 64–128GB as the workload demands, and shrink back within seconds when memory is freed — you pay for the working set, not the ceiling.
- **The latency/cost trade is stated explicitly.** Accepting a few seconds of occasional latency is what funds the 70% price gap. Worth reading as a template for arguing an availability trade-off on economics rather than vibes.
- **Nice adversarial test.** They kept a Minecraft server alive through migrations every two minutes for dozens of cycles — a workload where users notice hiccups immediately.

## Notes

Pairs well with the Netflix entry as a study in serving-cost engineering, from the opposite end of the stack.
