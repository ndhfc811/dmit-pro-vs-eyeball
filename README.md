# dmit pro vs eyeball: CN2 GIA vs CMIN2 routing, the real price gap, and which one to buy for your ISP

DMIT sells the same physical boxes under three different network labels, and two of them are the ones people keep comparing: Premium (shows up in plan names as `.Pro`) and Eyeball (`.EB`). Both are marketed as China-optimized. They are not the same product, and the difference has less to do with "speed" in the abstract than with what happens to your traffic between 20:00 and 23:00 Beijing time, and which carrier your users are on.

Here's the thing that makes dmit pro vs eyeball worth an article rather than a one-line answer: the two profiles frequently cost the exact same amount for the same CPU and RAM, so the decision isn't "cheap vs expensive." It's "better return route vs more traffic and a bigger port." That's a real trade, and the right side of it depends entirely on who's connecting to your server.

## What DMIT actually means by Pro and Eyeball

Neither label describes hardware. DMIT splits connectivity into Premium, Eyeball, and Tier 1 profiles, and the same AMD EPYC + KVM + SSD chassis gets sold under any of them depending on location.

The official wording matters here, because it sets expectations:

- **Premium**: "includes Tier 1 + all Premium Transit providers, such as DMIT's backbone, and China Telecom CN2 GIA."
- **Eyeball**: "includes Tier 1 + **Reasonable Effort** For China Routing via CMIN2 or similar Chinese ISPs."
- **Tier 1**: international transit, no China-specific optimization at all.

That phrase "reasonable effort" is doing a lot of work. Premium commits to specific premium transit — CN2 GIA on the return path. Eyeball combines ordinary Tier 1 transit with an honest attempt at routing toward Chinese consumer networks. Eyeball is not sold as a guarantee, and DMIT's own Hong Kong Eyeball listing has carried a Beta warning saying performance and routes may still change and that it isn't recommended for workloads needing high stability.

If you take nothing else from this section: Pro is a commitment, Eyeball is an effort. Both can look identical on a Tuesday afternoon speed test.

## The route difference, in plain terms

For the Los Angeles line, the reported paths look like this:

**LAX Premium (Pro)** — outbound: China Telecom via CN2 GIA (AS4809), China Unicom direct via AS4837, China Mobile via China Mobile Hong Kong (AS58453). Return: all three carriers via CN2 GIA.

**LAX Eyeball (EB)** — outbound: Telecom and Unicom via CN2 or a Tier 1 provider such as AS1299, Mobile via CMIN2. Return: all three via CMIN2. On the AS3 Eyeball listing the carriers are spelled out as Telecom on AS9929/AS58807, Unicom on AS9929, Mobile on CMIN2.

AS9929 and CMIN2 are genuinely good networks — well above the default 163 backbone that makes cheap VPS feel broken at night. But they sit below CN2 GIA in congestion priority. That's the entire product difference in one sentence: when everything is quiet, EB and Pro feel the same; when the international gateways are slammed, GIA traffic is the traffic that keeps moving.

One caveat that gets lost in these comparisons: routing doesn't beat physics. Reported mainland latency to Los Angeles sits around 130–170 ms on both profiles — the same order of magnitude, because the cable is the same length. Third-party test write-ups put Hong Kong Premium at roughly 43 ms average across the three carriers with near-zero loss. So if raw milliseconds are the thing you care about, the location decision dominates the profile decision.

## Same money, different amount of traffic

This is the part that makes Eyeball interesting. On DMIT's Los Angeles AS3 lineup, Pro and EB are priced identically at each tier — you're choosing between routing quality and capacity, not between budget and premium.

### Los Angeles Premium (Pro) — AMD EPYC 7003, KVM, 1 IPv4 + 1 IPv6 /64

| Plan | CPU / RAM / SSD | Monthly traffic | Port | After quota | Price | Order |
| --- | --- | --- | --- | --- | --- | --- |
| LAX.AS3.Pro.TINY | 1 core / 2 GB / 20 GB | 1000 GB | 1 Gbps | 4 Mbps, unmetered | $10.90/mo | [ Order Pro TINY](https://www.dmit.io/aff.php?aff=12046) |
| LAX.AS3.Pro.Pocket | 2 cores / 2 GB / 40 GB | 1500 GB | 4 Gbps | 4 Mbps, unmetered | $16.90/mo | [ Order Pro Pocket](https://www.dmit.io/aff.php?aff=12046) |
| LAX.AS3.Pro.STARTER | 2 cores / 2 GB / 80 GB | 3000 GB | 10 Gbps | 4 Mbps, unmetered | $34.90/mo | [ Order Pro STARTER](https://www.dmit.io/aff.php?aff=12046) |
| LAX.AS3.Pro.MINI | 4 cores / 4 GB / 80 GB | 5000 GB | 10 Gbps | 8 Mbps, unmetered | $62.90/mo | [ Order Pro MINI](https://www.dmit.io/aff.php?aff=12046) |
| LAX.AS3.Pro.MICRO | 4 cores / 4 GB / 160 GB | 7000 GB | 10 Gbps | 8 Mbps, unmetered | $87.90/mo | [ Order Pro MICRO](https://www.dmit.io/aff.php?aff=12046) |
| LAX.AS3.Pro.MEDIUM | 6 cores / 8 GB / 160 GB | 14000 GB | 10 Gbps | 10 Mbps, unmetered | $199.90/mo | [ Order Pro MEDIUM](https://www.dmit.io/aff.php?aff=12046) |

### Los Angeles Eyeball (EB) — same platform, CMIN2/9929 return

| Plan | CPU / RAM / SSD | Monthly traffic | Port | After quota | Price | Order |
| --- | --- | --- | --- | --- | --- | --- |
| LAX.AS3.EB.TINY | 1 core / 2 GB / 20 GB | 1500 GB | 2 Gbps | 4 Mbps, unmetered | $10.90/mo | [ Order EB TINY](https://www.dmit.io/aff.php?aff=12046) |
| LAX.AS3.EB.Pocket | 2 cores / 2 GB / 40 GB | 3000 GB | 4 Gbps | 4 Mbps, unmetered | $16.90/mo | [ Order EB Pocket](https://www.dmit.io/aff.php?aff=12046) |
| LAX.AS3.EB.STARTER | 2 cores / 2 GB / 80 GB | 5000 GB | 10 Gbps | 4 Mbps, unmetered | $34.90/mo | [ Order EB STARTER](https://www.dmit.io/aff.php?aff=12046) |
| LAX.AS3.EB.MINI | 4 cores / 4 GB / 80 GB | 10000 GB | 10 Gbps | 8 Mbps, unmetered | $62.90/mo | [ Order EB MINI](https://www.dmit.io/aff.php?aff=12046) |
| LAX.AS3.EB.MICRO | 4 cores / 4 GB / 160 GB | 14000 GB | 10 Gbps | 8 Mbps, unmetered | $87.90/mo | [ Order EB MICRO](https://www.dmit.io/aff.php?aff=12046) |
| LAX.AS3.EB.MEDIUM | 6 cores / 8 GB / 160 GB | 30000 GB | 10 Gbps | 10 Mbps, unmetered | $199.90/mo | [ Order EB MEDIUM](https://www.dmit.io/aff.php?aff=12046) |

Line them up and the pattern is obvious. At $10.90 you get 1 TB on a 1 Gbps port with Pro, or 1.5 TB on a 2 Gbps port with EB. At $34.90 it's 3 TB vs 5 TB. At $87.90 it's 7 TB vs 14 TB — double. The MICRO and MEDIUM tiers are where Eyeball stops being "the cheaper option" and starts being a different class of machine for the same invoice.

Worth knowing before you pick a tier: DMIT also runs newer AN4/AN5 platforms (AMD EPYC 9004/9005) alongside the AS3 generation, and the LAX plan list rotates as those restock. If you're chasing the lowest possible entry price, check what's actually in stock rather than trusting a table.

## Hong Kong and Tokyo don't follow the same math

The Pro-vs-EB relationship holds across locations, but the absolute numbers change a lot, and Hong Kong is the expensive one.

Hong Kong Premium starts at $39.90/month for 1 core, 1 GB RAM, 20 GB SSD and only 500 GB of traffic on a 1 Gbps port. Hong Kong Eyeball starts lower — commonly listed at $29.90/month for 1 core, 1 GB and 1000 GB of traffic — and the EB tiers climb with noticeably more bandwidth (2 Gbps and up). So in Hong Kong, Eyeball isn't just more traffic per dollar; it's a much lower door price for a China-facing node with real latency figures.

What the Hong Kong Eyeball series buys you is CMI-based routing toward the mainland, tested at roughly 10–25 ms from the southern coast in third-party ping sweeps. What it doesn't buy you is the guarantee — DMIT has re-specced the HKG Eyeball line more than once, and its own description of the profile is best-effort. If you're comparing older articles against current pricing, expect mismatches.

Tokyo is the interesting middle. TYO Premium starts around $21.90/month for 500 GB, and TYO Eyeball around $25.90/month for 1000 GB on a 1 Gbps port. Tokyo Pro undercuts Hong Kong Pro by a wide margin while still offering a premium return route. The catch, per provider listings, is that the Tokyo Pro and Eyeball lines **suspend** the instance when traffic runs out rather than throttling it — unlike the Los Angeles Pro/EB line, where overage drops you to a slow-but-alive 4–10 Mbps. For a production site that's a meaningful difference in failure mode.

## The restock tier that quietly beats both

Two flash-sale plans come back in batches and change the price conversation entirely:

| Plan | Profile | CPU / RAM / SSD | Traffic / Port | Price | Order |
| --- | --- | --- | --- | --- | --- |
| LAX.Pro.MALIBU | Premium | 1 core / 1 GB / 20 GB | 1000 GB / 1 Gbps | $49.90/year | [ Grab LAX.Pro.MALIBU](https://www.dmit.io/aff.php?aff=12046&pid=186) |
| LAX.EB.WEE | Eyeball | 1 core / 1 GB / 20 GB | 1000 GB / 1 Gbps | $39.90/year | [ Grab LAX.EB.WEE](https://www.dmit.io/aff.php?aff=12046&pid=188) |

$49.90 a year for a CN2 GIA return route works out to about $4.15/month, which is a different universe from the $10.90 monthly TINY. These plans appear and disappear, and they don't accept coupons. If a restock notice shows up, it's worth a look.

## Coupon codes: what's worth typing into the box

DMIT's coupon system is product-line and billing-cycle specific, which is why half the codes floating around don't apply to what you're buying.

- `LAX-EB-LAUNCH-NON-MONTHLY-RECURRING-20OFF` — 20% recurring on Los Angeles Eyeball, TINY and above, quarterly or longer. Recurring means it applies on renewals, not just the first invoice. Skip it if you're paying monthly.
- Promo codes applied to the LAX Pro/EB line, such as `LAX-EB-LAUNCH-NON-MONTHLY-RECURRING-20OFF` equivalents, and holiday codes shared for Pro plans. Promo code is `2025-XMAS-LAX-PRO-EB-10-OFF-RECURRING`, but I haven't verified that one independently.

To use any of these, configure the plan, choose a non-monthly cycle, paste the code, then hit Validate. If it applies, the price updates; if not, you've lost nothing. Two things to keep in mind: the flash-sale and special-price plans generally aren't eligible for coupons at all, and the recurring codes for other product families don't apply to Pro or EB — DMIT has separate discount tiers for Lite/Standard, which is a different network profile entirely.

One concrete point: on LAX Premium and Eyeball, over-quota traffic doesn't take you offline. On Tokyo Premium and Eyeball, it does.

Third, the refund window is short and conditional. DMIT's terms carry a 3-day assurance window: if you're inside it, haven't burned through an unreasonable amount of traffic, and your assigned IP is intact, you can open a ticket for a full refund. Paying by Alipay is the safer route — refunds through some channels come back with fees attached.

Finally, a structural warning that's genuinely useful: DMIT doesn't send maintenance emails. Host upgrades have been reported to cause short unannounced interruptions. If your service needs planned-maintenance communication, this isn't the provider for that.

## How to decide in five minutes

1. **Identify your audience's carrier.** China Telecom users? Premium. China Mobile? Eyeball's CMIN2 return is genuinely strong and costs less. Unicom? Test first — AS9929 through EB is decent, but CN2 GIA on Pro is the more consistent choice at peak.
2. **Decide whether you need milliseconds or megabytes.** A Hong Kong node at ~43 ms average beats any Los Angeles profile on latency. If you need low latency for interactive use, buy location; if you need affordable stability toward a mainland audience, LAX Pro is the better value than HKG Pro.
3. **Test before you commit to annual.** DMIT publishes test IPs per location — 154.17.30.96 for LAX Premium, 154.17.229.24 for LAX Eyeball, 103.117.100.199 for HKG Pro, 154.12.188.3 for HKG Eyeball, plus Looking Glass endpoints. Ping them from the actual ISP your users use, at night, not at noon.
4. **Start small, scale after verification.** The $10.90 TINY tier is cheap enough to be an experiment. Upgrade once the route has survived a few evening peaks on your network.
5. **Then take the longer cycle.** Month-to-month is the wrong way to buy this. Quarterly or annual is where the Eyeball coupon applies and where the price per GB of traffic starts making sense — [👉 compare current price cycles and availability](https://www.dmit.io/aff.php?aff=12046) before you settle.

## FAQ

**Is Eyeball slower than Pro?**
Not in raw throughput — the same 10 Gbps ports are available on both. The difference is route priority and consistency. Premium holds a specific premium return path; Eyeball does its best with CMIN2/9929 and can be re-tuned. At 21:00 on a congested gateway, that distinction becomes visible.

**Can I use Eyeball on China Telecom?**
Yes. The return route for Telecom on LAX Eyeball is reported as AS9929/AS58807, which is a step above the default backbone. It's just not CN2 GIA. If your users are mostly Telecom and peak-hour consistency is the requirement, Pro is the safer pick.

**Can I run a coupon on Pro?**
Public coupons for Pro are rare, and the flash-sale plans (MALIBU and the WEE series) generally aren't eligible at all. Eyeball, by contrast, has a live recurring 20% code for non-monthly cycles. That widens the price gap between the two lines beyond what the table shows.

**What's the difference between Eyeball and Tier 1?**
Tier 1 has no China routing optimization at all — it's international transit, and it's the cheapest thing DMIT sells, with annual entry pricing in the $36.90 range. Eyeball is Tier 1 plus the best-effort China routing layer. If you're serving a mainland audience directly, Tier 1 is the wrong product; it's a good landing node or backend when paired with a relay.

**Do the plan names change?**
They do. Plan names, platform generations (AS3 vs AN4/AN5), stock, and prices all shift as DMIT restocks. Anything in this article should be treated as the picture at the time of writing — the order page is the only source of truth for what's in stock and what it costs today.

The short version of dmit pro vs eyeball: you're not choosing between a good product and a compromised one. You're choosing whether you want the more consistent premium return path or roughly 1.5–2x the traffic and a larger port for the same monthly invoice. Telecom-heavy, peak-hour-sensitive, or contractually obliged to be online? Pro. Mobile-heavy traffic, bandwidth-hungry workload, or a budget that doesn't stretch to CN2 GIA? Eyeball, and use the recurring code while it's live.
