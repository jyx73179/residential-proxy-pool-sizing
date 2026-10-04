# residential proxy pool: What Actually Matters Beyond the IP Count, and How to Size One for Scraping, SERP Tracking, or Multi-Account Work

You type "residential proxy pool" into a search box and land on a pricing page that says 20 million IPs. Or 90 million. Or 400 million. The number is big, it's bold, and it tells you almost nothing about whether your scrape will succeed next Tuesday.

That's the gap this piece tries to close. Pool size is a marketing figure. What decides your success rate is how the pool is assembled, how it hands out addresses, how you're billed for using it, and whether your workload matches the rotation model you bought. Get those four things right and a smaller pool will outperform a bigger one. Get them wrong and a 400-million-IP network will still serve you 403s all afternoon.

Below: how residential proxy pools actually work, the arithmetic for sizing one, the three ways providers charge for them, and a concrete look at one provider — 9Proxy — including its full current plan list, so the abstract parts have numbers attached.

## What a residential proxy pool actually is

A residential proxy pool isn't a list of IPs you download. It's a gateway. You connect to one endpoint, and the provider assigns an exit address from its network based on the parameters you asked for — country, state, city, ZIP, ISP, or session identifier. The requests come out of real consumer connections on cable, fiber, or mobile networks, so target sites see ASN-level traffic that looks like an ordinary household rather than a hosting provider.

That distinction is the whole reason the category costs more than datacenter proxies. A datacenter IP belongs to an ASN registered to a cloud provider, which any anti-bot system can flag in bulk. A residential IP belongs to a consumer ISP, and blocking consumer ranges wholesale means blocking paying customers. That asymmetry is the product.

Pools are assembled in a few different ways, and the sourcing method is where providers diverge on both price and ethics: opt-in bandwidth-sharing apps that pay participants, third-party SDKs bundled into free software with varying degrees of disclosure, ISP-leased ranges for static residential products, and — at the bottom of the market — devices enrolled without consent. A pool that costs well under market should prompt a question, not a checkout.

## The pool size number is the least useful number on the page

Bright Data advertises 400M+ residential IPs, Oxylabs 177M+, and 9Proxy advertises over 20 million across 90+ countries. Multiply-the-headline differences like that sound like a quality ranking. They mostly aren't.

Three things matter more than the total:

**Geographic resolution.** A 400M-IP network covering 195 countries and a 20M-IP network covering 90+ countries are not interchangeable. If your work is US, UK, Germany, and a handful of Southeast Asian markets, both will do. If you need localized SERPs from thirty small markets, the smaller network's coverage list is the first thing to read.

**Per-address reputation.** What you actually want is an address that hasn't been burned on your target domain. Pool size is a proxy for the odds of getting one, but only a proxy. Two networks with identical counts can have very different blacklist exposure depending on how the addresses were acquired and how fast they get rotated back out.

**Session behavior.** Whether the gateway gives you a new address every request, holds one for a defined window, or lets you pin one for the duration of a job. More on this below, because it's the single most common cause of "the proxies are broken" tickets that turn out not to be proxy problems at all.

## Rotation models decide more than pool size ever will

There are three practical behaviors, and picking the wrong one is expensive in a quiet way — the requests succeed, sessions break, and the symptom looks like a bug in your own code.

- **Per-request rotation.** A fresh address for every request. Right for stateless collection of independent pages. Wrong for anything with continuity.
- **Sticky sessions.** The same address held for a defined window — often minutes, sometimes hours. Right for logins, multi-step flows, cart operations, paginated results tied to one session.
- **Static or long-lived addresses.** The same IP indefinitely. Right when you want a stable identity you maintain yourself; typically priced per address rather than per gigabyte.

The classic mistake is running per-request rotation against a workflow that needs state. Four requests from four countries in ninety seconds is not a pattern a real shopper produces, and it's precisely the kind of sequence that triggers an account flag rather than a block.

9Proxy's two products map onto this divide in a way that's worth understanding before you compare prices. Its IP-based packages give you individual residential IPs with unlimited bandwidth; each IP stays usable for a few hours up to roughly 24 hours, and the addresses don't expire if you don't consume them. Its GB-based packages generate unlimited endpoints that rotate per request or per session, with sticky and rotating modes both configurable.

That means the IP-based model suits account work, where you want one identity held steady. The GB model suits breadth, where you want to touch a thousand different addresses in an hour and don't care which.

## How many addresses do you actually need?

Far fewer than the marketing implies, and the honest way to find the number is empirical rather than theoretical.

Run your workload from a single address and push the rate until you start seeing 429s, challenge pages, or degraded responses. That threshold is your per-address capacity for that target. Divide your required throughput by it, and you have a rough concurrency figure.

Suppose a target tolerates about one request every two seconds from one address — roughly 1,800 requests an hour. You need 50,000 requests a day. Spread across 24 hours that's about 2,100 an hour, so two addresses technically suffice and four gives you headroom for retries.

Two addresses against a pool advertised in the millions.

Where that arithmetic breaks is geography and reputation decay. If you need presence in forty countries, you need at least forty addresses. If you run bursts instead of spread-out load, you need more concurrency for a shorter window. And if addresses go bad on your target over time, you need spares to rotate out.

Even then, most workloads land in the tens to low hundreds of addresses, not thousands. Which is why the pricing model you pick matters more than the tier you pick.

## Paying for a residential proxy pool: per GB, per IP, or both

Providers price residential pools three ways, and each one shifts risk to a different party.

**Per GB** puts the provider's cost on your traffic. You pay for what you consume, threads and sessions are usually unlimited, and unused balance typically has an expiry window. This is the standard structure in the category, and market rates run roughly $0.79 to $7.00 per GB across providers.

**Per IP with unlimited bandwidth** puts the risk on you instead: fixed cost per address, and bandwidth is not a line item. If your workload transfers heavy data through few addresses, this is where the economics invert in your favour. If your workload touches thousands of addresses lightly, you're paying for capacity you won't use.

**Bundles** combine both, usually at a discount against buying the two separately, which suits projects that need stable identities and flexible rotation in the same week.

## Where 9Proxy sits in this picture

9Proxy is a residential-only network — no datacenter line to fall back on — advertising 20M+ verified residential IPs across 90+ countries with targeting down to country, state, city, ZIP, and ISP, on HTTP/HTTPS and SOCKS5.

It prices on both axes. IP-based packages are one-time purchases with no subscription and unlimited bandwidth per address; unused IPs never expire. GB-based packages run on a balance model with 180-day traffic validity, extended to unlimited validity on Enterprise tiers, which also add a team mode of one owner plus up to five members with per-member traffic controls.

Billing is balance-based across the board, which is a real difference from the subscription norm: you top up and draw down. IPs are only deducted once a proxy connection actually establishes, so a failed session doesn't cost you an address.

There's one operational wrinkle worth knowing. The IP-based product has traditionally required the 9Proxy desktop app, which handles local port forwarding on your machine — that's a genuine friction point on multi-device setups compared to browser-based or dashboard-only providers. 9Proxy has since added Proxy2Web, which creates sessions on their infrastructure and hands you a host, port, and credentials to use directly, no local install. If you're evaluating the IP-based tier, that's the feature to check first.

👉 [See 9Proxy's current residential proxy packages and rates](https://bit.ly/9-Proxy)

## Full plan and pricing comparison

One thing to flag before the tables: 9Proxy adjusted its pricing on 1 June 2026 for IP-based and Bundle packages only — GB-based prices were left untouched. The figures below are the post-adjustment ones. Every package is a one-time balance purchase, not a recurring subscription.

### Residential by IP (unlimited bandwidth, unused IPs never expire)

| Plan | Price per IP | Total | Billing | Purchase |
| --- | --- | --- | --- | --- |
| 100 IPs | $0.24 | $24 | One-time | [Get 100 IPs](https://bit.ly/9-Proxy) |
| 500 IPs | $0.144 | $72 | One-time | [Get 500 IPs](https://bit.ly/9-Proxy) |
| 1,000 + 500 bonus IPs | $0.084 | $126 | One-time | [Get 1,500 IPs](https://bit.ly/9-Proxy) |
| 2,500 IPs | $0.084 | $210 | One-time | [Get 2,500 IPs](https://bit.ly/9-Proxy) |
| 5,000 IPs | $0.072 | $360 | One-time | [Get 5,000 IPs](https://bit.ly/9-Proxy) |
| 15,000 IPs | $0.048 | $720 | One-time | [Get 15,000 IPs](https://bit.ly/9-Proxy) |
| 25,000 IPs | $0.035 | $863 | One-time | [Get 25,000 IPs](https://bit.ly/9-Proxy) |
| 50,000 IPs | $0.029 | $1,438 | One-time | [Get 50,000 IPs](https://bit.ly/9-Proxy) |
| 100,000 IPs | $0.023 | $2,300 | One-time | [Get 100,000 IPs](https://bit.ly/9-Proxy) |
| 200,000 IPs | $0.021 | $4,140 | One-time | [Get 200,000 IPs](https://bit.ly/9-Proxy) |
| 500,000 IPs | $0.018 | $8,625 | One-time | [Get 500,000 IPs](https://bit.ly/9-Proxy) |

### Residential by GB (rotating endpoints, balance-based)

| Plan | Price per GB | Total | Validity | Purchase |
| --- | --- | --- | --- | --- |
| 5 GB | $3.00 | $15 | 180 days | [Buy 5 GB](https://bit.ly/9-Proxy) |
| 50 + 5 GB bonus | $2.10 | $105 | 180 days | [Buy 55 GB](https://bit.ly/9-Proxy) |
| 100 GB | $1.50 | $150 | 180 days | [Buy 100 GB](https://bit.ly/9-Proxy) |
| 200 GB | $1.00 | $200 | 180 days | [Buy 200 GB](https://bit.ly/9-Proxy) |
| 1,000 GB | $0.80 | $800 | 180 days | [Buy 1,000 GB](https://bit.ly/9-Proxy) |
| 2,000 GB | $0.75 | $1,500 | 180 days | [Buy 2,000 GB](https://bit.ly/9-Proxy) |
| 3,000 GB (Enterprise) | $0.72 | $2,160 | Unlimited | [Buy 3,000 GB](https://bit.ly/9-Proxy) |
| 6,000 GB (Enterprise) | $0.70 | $4,200 | Unlimited | [Buy 6,000 GB](https://bit.ly/9-Proxy) |
| 10,000 GB (Enterprise) | $0.68 | $6,800 | Unlimited | [Buy 10,000 GB](https://bit.ly/9-Proxy) |

### Bundle packages (IPs + traffic)

| Plan | Contents | Price | Note | Purchase |
| --- | --- | --- | --- | --- |
| Starter | 100 IPs + 5 GB | $30 | Entry bundle | [Get the Starter bundle](https://bit.ly/9-Proxy) |
| Popular | 1,500 IPs + 50 GB | $180 | Mixed workloads | [Get the Popular bundle](https://bit.ly/9-Proxy) |
| Pro | 5,000 IPs + 500 GB | $720 | Listed at $860, ~16% off | [Get the Pro bundle](https://bit.ly/9-Proxy) |

Bundled traffic carries the same 180-day validity as standalone GB packages.

## Which plan fits which job

The cheapest tier isn't automatically the right one, and the most expensive tier isn't automatically bad value. It comes down to what your workload does.

**SERP tracking across a handful of markets.** You need many addresses, light traffic, fast rotation. The 200 GB or 1,000 GB GB-based tier at $1.00–$0.80 per GB is the natural fit — you're paying for breadth, not for stable identities you'll never hold.

**E-commerce price monitoring at moderate volume.** Bursty, bounded by traffic, spread over enough addresses that no single one gets rate-limited. Same model, smaller tier: 50 + 5 GB at $105 or 100 GB at $150.

**Multi-account management and antidetect browser profiles.** You need one identity to survive a session, not a fresh address every request. This is the IP-based product. 100 IPs at $24 is a legitimate starting point for testing; 500 IPs at $72 covers a solo operator running several profiles without reusing addresses.

**Long-running scraping with unpredictable bandwidth.** Heavy transfer through relatively few addresses is exactly where per-IP billing with unlimited bandwidth wins, because your traffic stops being a line item. The 5,000-IP tier at $360 exists for this shape of work.

**Agency work with several clients on one account.** The 15,000-IP tier at $720 and the Pro bundle at $720 (5,000 IPs + 500 GB) cost the same, so the pick is about shape, not price: heavy traffic per identity points to the IP package, mixed workloads point to the bundle.

Above 100,000 IPs the per-address price flattens near $0.02, which is reseller and platform territory rather than single-project territory.

👉 [Compare all 9Proxy plans on the current pricing page](https://bit.ly/9-Proxy)

## Trials, promos and what the reviews actually say

9Proxy doesn't offer a self-serve free trial on its website. A limited trial for new users exists depending on availability, and it's requested through support rather than claimed from a dashboard button — you have to say whether you want the IP-based or GB-based trial. The provider also runs periodic community giveaways, including a "Daily Hunt" promotion that distributed 1 GB residential proxy codes.

Separately, 9Proxy has run a recurring "Green Sunday" promo offering +10% back on IP and GB consumed each Sunday, capped per week. It's an ongoing campaign rather than a permanent plan feature, so check the dashboard for whether it's live before planning around it.

On pricing itself: 9Proxy's affiliate program description states that users who sign up through a referral link get a 5% discount, alongside lifetime commission for the referrer. That's the mechanism behind invite links, and it's worth taking since it costs nothing.

Third-party testing is thinner than the enterprise providers get, but a few data points exist:

- Geekflare's 2026 review reports a 97.7% success rate against Cloudflare-protected targets, and describes the billing flexibility as the strongest part of the offer.
- An independent tester writing for ProxyBros reported roughly 99.5% success and around 0.6 seconds average response time on the network, with bundled traffic valid for 180 days.
- iTWire's review flags the mandatory desktop app as a multi-device inconvenience, notes that free trials depend on promotions, and reports the pool can struggle with streaming platforms like Netflix.
- Geekflare also observes that the Trustpilot score reflects friction with the refund policy more than infrastructure problems — users who bought a plan that didn't fit their use case couldn't recover the spend. The practical takeaway is unglamorous: use whatever test access you can get before committing, and match the billing model to your workload first.

## Where the pool has limits

Two honest constraints, in case the tables above look too clean.

Coverage is 90+ countries, not 195+. For US, UK, European, and Southeast Asian work, that's plenty. For niche geographies, verify your specific market exists before buying a large tier — this is the single most common mismatch that leads to refund complaints.

The pool is also meaningfully smaller than Bright Data's or Oxylabs'. That's the trade-off you're accepting in exchange for per-address pricing that starts at $0.24 and bottoms out near $0.018 at volume. If your targets are aggressively defended and you need the largest possible address diversity, the bigger networks cost more for a reason.

## Quick answers

**Is a residential proxy pool the same as a rotating proxy?** Not exactly. The pool is the inventory. Rotating is one way of drawing from it. Many pools also support sticky and static sessions, which is why "rotating proxy" is a narrower term than "residential proxy pool."

**Should I buy per IP or per GB?** Ask what your workload actually constrains on. If bandwidth is the bottleneck and identity stability matters, per IP. If address turnover is the bottleneck and traffic per request is small, per GB. 9Proxy's IP tiers are $24–$8,625 and its GB tiers are $15–$6,800, so the entry prices are close — the shape of your workload, not the sticker, decides.

**Do unused IPs expire?** On 9Proxy's IP-based packages, no. Unused IPs stay on the balance until you forward them. GB-based balance carries 180-day validity, unlimited on Enterprise tiers.

**What payment methods are accepted?** Credit cards, bank cards, cryptocurrency including USDT, BTC, ETH, LTC and DOGE, plus Alipay, Apple Pay and Google Pay.

The pool size number is the part of this category that's easiest to advertise and hardest to verify. The parts you can actually control are the ones worth spending time on: pick the billing model that matches how your job consumes resources, pick the rotation mode that matches whether your job needs state, and test against your real target before you buy the tier you think you need.
