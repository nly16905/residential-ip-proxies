# antidetect browser proxies: How to match the right residential IP to every Multilogin, GoLogin, AdsPower or Dolphin Anty profile

The profile that looked bulletproof in a fingerprint checker gets a login challenge on day three, and the fingerprint usually isn't the reason. It's the IP.

Antidetect browsers got very good at the things detection scripts look at first: canvas noise, WebGL renderers, font stacks, timezone offsets, audio contexts, hardware concurrency. Set up a profile in Multilogin, GoLogin, AdsPower or Dolphin Anty and it will pass most of the cheap checks. What none of them do is give you an exit IP. That part you buy, configure and maintain yourself, and it's the half of the disguise that platforms weigh hardest — a residential-looking fingerprint arriving from a flagged datacenter range is a mismatch that doesn't need much machine learning to catch.

So the real question behind *antidetect browser proxies* isn't "which browser", it's which IP type, how long it should stick, and what that costs per profile at your scale. Below is the practical version, with real numbers from one provider so you can see how the maths works.

## What the antidetect browser covers, and what the proxy has to cover

Split the work in two:

**Browser layer** — fingerprint consistency, cookies, local storage, per-profile cookie jars, WebRTC behaviour, user agent, screen metrics. This is the browser's job, and modern tools handle it well.

**Network layer** — the IP address, its reputation, its geo consistency with the profile's timezone and locale, its ASN type (home ISP vs cloud host), and how long it stays the same. This is your job.

A profile claiming to be a Windows user in Berlin, browsing through a datacenter IP registered to a hosting company in Frankfurt, is internally contradictory. Every additional contradiction — a timezone set to Berlin but an exit IP in Virginia, a "home" connection that reverse-DNSes to a VPS provider — reduces the number of actions the account can take before someone asks for a phone number.

## The four IP types people put behind a profile

| Proxy type | What the exit looks like | Good for | Where it breaks |
| --- | --- | --- | --- |
| Datacenter | A cloud host's range | Bulk scraping of unprotected pages, quick checks | Almost instantly flagged on social, e-commerce and ad platforms |
| Residential, rotating by GB | A real home connection, new IP every request or session | High-volume crawling, SERP checks, price monitoring | A changing IP mid-session breaks logged-in accounts |
| Residential, sticky per IP | A real home connection that stays put for hours | Account profiles, marketplaces, anything with a session | Costs more per unit than GB billing for pure crawling |
| Mobile / 4G | A carrier IP shared by thousands of phones | The hardest targets: big social platforms, streaming, app testing | Expensive, and usually the wrong look for a desktop profile |

Most antidetect browser users end up mixing the middle two: sticky residential IPs for the profiles that hold accounts, GB-based rotating residential for the collection jobs that just need volume.

## Sticky or rotating is the setting that decides whether an account survives

This is where people lose accounts. Rotating proxies are excellent for scraping and terrible for logged-in sessions. If a profile logs into a marketplace, loads six pages and then appears from a different city 40 seconds later, you've manufactured the exact pattern fraud systems look for.

Three rules that hold up in practice:

1. **One profile, one IP, for as long as the account lives.** Not one IP shared across five "different" people.
2. **Match the IP's city, not just the country.** A Berlin profile should exit in Germany, ideally in the same metro the profile's timezone implies.
3. **Don't rotate during a session.** Rotation belongs on the collection profiles, not on the ones holding ad accounts or storefronts.

Residential IPs die on their own schedule — a real home connection drops when the homeowner reboots the router. What matters is what the provider does when that happens. With 9Proxy, a forwarded IP that fails gets replaced within 60 seconds, and the "Today List" lets you reuse any IP you've already used in the last 24 hours at no extra cost, which the provider says cuts IP spend by 20–30% on recurring work.

## Checklist before you hand a provider your card

Antidetect browser proxies are a commodity in the sense that everyone sells "residential IPs" and a liability in the sense that the details decide whether your profiles last a week or a year. Run this list:

- **Protocol support.** SOCKS5 for the browser, HTTP/HTTPS for tools that insist. Some providers only do one.
- **Targeting granularity.** Country-level targeting is close to useless for profiles that claim a city in their timezone. You want state, city, ZIP and ISP.
- **Authentication method.** Username/password works everywhere. IP whitelisting is convenient until you move to a cloud VM and everything breaks.
- **Bandwidth model.** Per-GB billing punishes exactly the wrong workloads: dashboards, feeds and image-heavy sites. Per-IP billing with unlimited traffic on the active IP is friendlier to browser profiles.
- **Replacement policy in writing.** "Contacts support and maybe gets a new IP" is not a policy.
- **Expiry terms.** If unused balance burns in 30 days, you're renting, not buying.

## Where 9Proxy fits into an antidetect browser setup

9Proxy is a residential proxy provider — the company behind it is ConnectWise Ltd. — selling against a 20M+ IP pool across 90+ countries at roughly $0.018 per IP at the high-volume end, which is squarely in the budget tier rather than the Bright Data / Oxylabs tier. It runs two different products, and the distinction matters more for antidetect work than for scraping:

**Residential proxy by IPs** — you buy a pack of IPs, each with unlimited bandwidth while active. Unused IPs don't expire. IPs live from a few hours up to about 24 hours, and the desktop app forwards them to local ports so anything on the machine can use them, including software with no proxy settings of its own.

**Residential proxy by GB** — you buy traffic, generate as many endpoints as you like, and choose sticky or rotating per session. Authentication is username/password or IP whitelist, targeting goes down to ZIP and ISP, everything runs from the dashboard with no app installed, and traffic is valid for 180 days.

Both support HTTP, HTTPS and SOCKS5 — the last one being what you actually want in an antidetect browser, since fingerprint tools pass SOCKS5 credentials straight through to the network stack rather than through an extension. Users report it working with Dolphin Anty and AdsPower, and the vendor lists multi-accounting and antidetect browser workflows among its intended use cases.

One thing to know before you buy: the IP-based product needs the desktop app. If you're running profiles on a headless Linux VM, you want the GB-based product instead, which is dashboard-only.

### Current pricing after the June 1 adjustment

9Proxy raised prices on IP-based and bundle packages on 1 June 2026 — the first increase in its history — and explicitly left GB-based packages untouched. That's why you'll see older numbers in reviews written before that date. What's below is the post-adjustment picture.

| Product | Package | What you get | Price | Billing | Where to buy |
| --- | --- | --- | --- | --- | --- |
| Residential by IPs | 100 IPs | 100 residential IPs, unlimited bandwidth each, no expiry on unused IPs | $24 ($0.24/IP) | One-off, balance-based | [ Get the 100 IP package](https://bit.ly/9-Proxy) |
| Residential by IPs | 500 IPs | 500 IPs, unlimited bandwidth | $72 ($0.144/IP) | One-off | [ Get the 500 IP package](https://bit.ly/9-Proxy) |
| Residential by IPs | 1,000 IPs + 500 bonus | 1,500 IPs total, unlimited bandwidth | $126 ($0.084/IP) | One-off | [ Get the 1,000 IP package with bonus IPs](https://bit.ly/9-Proxy) |
| Residential by IPs | Mid volume: 2,500 / 5,000 / 15,000 / 25,000 / 50,000 IPs | Same product, per-IP rate falls with volume | Tiered, quoted in-account | One-off | [ See the current tier ladder](https://bit.ly/9-Proxy) |
| Residential by IPs | Business volume: 100,000 IPs | Unlimited bandwidth, wholesale rate | $2,300 | One-off | [ Check business volume pricing](https://bit.ly/9-Proxy) |
| Residential by IPs | Business volume: 500,000 IPs | Unlimited bandwidth, lowest listed per-IP rate (~$0.018) | $8,625 | One-off | [ Check business volume pricing](https://bit.ly/9-Proxy) |
| Residential by GB | 5 GB | Rotating or sticky sessions, unlimited endpoints | $15 ($3.00/GB) | Prepaid traffic, 180-day validity | [ Get the 5 GB package](https://bit.ly/9-Proxy) |
| Residential by GB | 50 GB + 5 GB bonus | 55 GB usable | $105 ($2.10/GB) | 180-day validity | [ Get the 50 GB package](https://bit.ly/9-Proxy) |
| Residential by GB | 100 GB | Country/state/city/ZIP/ISP targeting | $150 ($1.50/GB) | 180-day validity | [ Get the 100 GB package](https://bit.ly/9-Proxy) |
| Residential by GB | 200 GB | As above | $200 ($1.00/GB) | 180-day validity | [ Get the 200 GB package](https://bit.ly/9-Proxy) |
| Residential by GB | 1,000 GB | For daily monitoring at scale | $800 ($0.80/GB) | 180-day validity | [ Get the 1,000 GB package](https://bit.ly/9-Proxy) |
| Residential by GB | 2,000 GB | Multi-region, multi-tool workloads | $1,500 ($0.75/GB) | 180-day validity | [ Get the 2,000 GB package](https://bit.ly/9-Proxy) |
| Residential by GB | Enterprise | Unlimited data validity, team mode (1 owner + up to 5 members), per-member traffic controls, activity logs, VIP pricing | On request | Contract | [ Ask about the Enterprise plan](https://bit.ly/9-Proxy) |
| Bundles | Starter | 100 IPs + 5 GB | $30 | Traffic valid 180 days | [ Get the Starter bundle](https://bit.ly/9-Proxy) |
| Bundles | Popular | 1,500 IPs + 50 GB | $180 | Traffic valid 180 days | [ Get the Popular bundle](https://bit.ly/9-Proxy) |
| Bundles | Pro | 5,000 IPs + 500 GB | $720 | Traffic valid 180 days | [ Get the Pro bundle](https://bit.ly/9-Proxy) |

Two notes on that table. First, GB pricing above the 2,000 GB tier drops further — the provider quotes around $0.68/GB at the 10,000 GB level — so a very heavy crawler shouldn't anchor on the small-pack rates. Second, 9Proxy's listed extras include a 5% IP bonus when you pay in crypto and a lifetime commission-based affiliate programme; trials are promotional rather than automatic, so ask support rather than assuming a free tier.

## The per-profile maths nobody does before buying

Here's where per-IP billing earns its place in an antidetect workflow.

Say you're running 120 profiles: 60 accounts that need to stay put, 60 throwaway profiles for research. Each account profile needs its own sticky IP, and you want spares because residential IPs drop. That's around 100–150 IPs.

At $24 for 100 IPs, that's roughly $0.24 per profile, once. The IPs don't expire and each one carries unlimited bandwidth while active, so a profile that scrolls video-heavy feeds all day costs the same as a profile that opens one page.

Now price the same workload on a per-GB provider. Fifty profiles loading social feeds and marketplace dashboards, each pulling 300 MB a day, is 15 GB a day — 450 GB a month. At a typical $1–3/GB residential rate, that's $450–$1,350 a month, and your cost tracks how much your users browse rather than how many of them there are.

That asymmetry is the whole argument for IP-based billing on account work. It's the opposite for crawling: 200,000 short requests spread over thousands of rotating IPs burn little bandwidth and need no stickiness, so GB billing wins there.

One caveat worth stating plainly: at $0.24 per IP on the entry pack, you're paying roughly eight times the per-IP rate of the 500,000-IP tier. Small packs are for testing the pool against your targets, not for running a farm.

## Wiring it into the browser

The GB-based path is the simple one:

1. Buy a traffic package, create a sub-user, assign it some of that traffic.
2. Open the proxy generator, pick country — and state, city, ZIP or ISP if you need them.
3. Choose sticky (same IP for X minutes) or rotating (new IP per request or session).
4. Copy the endpoint in `host:port:username:password` form.
5. In the antidetect browser, add a new proxy, select SOCKS5, paste the four fields, run the built-in proxy check, then launch the profile.

The IP-based path adds the desktop app. You pick IPs, bind each to a local port, and the app exposes them as `127.0.0.1:port`, which you then enter in the browser's proxy field with no credentials. That local-port approach is what makes 9Proxy usable inside software that has no proxy support at all — but it also means the app has to be running whenever the profiles are.

Whichever path you take, verify the exit before you log in anywhere. Point the profile at an IP-checking page and look at three things: the country matches the profile's timezone, the ASN is a consumer ISP rather than a hosting company, and WebRTC doesn't leak your real address. The "Check Proxy" button in most antidetect browsers confirms reachability but doesn't test WebRTC — that one you check manually.

## Mistakes that still get profiles banned with clean residential IPs

- **Reusing one IP across accounts "on the same site, different profiles".** Platforms link accounts by IP and subnet long before fingerprints matter. One IP, one account.
- **Timezone drift.** Browser says Tokyo, IP says Dallas. Fix the profile's timezone to follow the exit IP, or set your proxy targeting to the profile's claimed city.
- **Stale profile data.** Importing a profile's cookie jar into a new IP is itself a signal. Keep the pairing stable instead of mixing.
- **Choosing mobile proxies for desktop profiles.** A 4G carrier IP behind a profile claiming desktop Chrome on a residential-looking setup is its own contradiction.
- **Ignoring DNS and WebRTC.** Chrome's default DNS behaviour and WebRTC ICE candidates both leak in ways a proxy alone doesn't fix.
- **Treating bans as proxy failures.** Sometimes the IP is fine and the session behaviour — instant logins, rapid posting, zero typing latency — is what got you noticed.

## Where 9Proxy is the wrong answer

Straight talk, because the useful part of a review is knowing when to skip it.

The pool is around 20M residential IPs, which is small next to providers advertising 100M+. Third-party reviews also note that streaming services frequently block its IPs, so it's not a Netflix tool, and there's no mobile/4G product line for the platforms that effectively require carrier IPs. The IP-based product needs the desktop app, which is a real constraint on headless or cloud setups. And if you need a compliance-heavy enterprise contract with SLAs in the fine print, its 24/7 support and Enterprise team plan are a thinner offering than the top-tier vendors'.

Where it lands well: antidetect browser farms at small-to-mid scale, e-commerce account management, price and ad monitoring, SERP tracking, and multi-account workflows where a clean residential exit with unlimited bandwidth matters more than pool size or brand recognition. If your monthly proxy bill is dominated by how much your profiles browse rather than how many requests they fire, per-IP billing is the cheaper shape.

## Common questions

**Do antidetect browsers include proxies?** Usually no. They include a proxy manager — fields for host, port, username and password — and expect you to bring the IPs. A few vendors resell partner networks, but the pool and its quality are still a separate purchase.

**How many IPs do I need?** One per account-holding profile, plus spares for the ones that drop. A 30-profile setup with churn usually sits comfortably inside a 100-IP pack.

**SOCKS5 or HTTP?** SOCKS5 for the browser; it handles any traffic type and authenticates inside the network stack. HTTP/HTTPS for tools that don't speak SOCKS5.

**Can I start with free proxies?** You can, and you'll spend the money you saved on replacements. Free pools are shared, slow, already blacklisted and often inspect your traffic.

If you want to test the pool against your actual targets before committing to a volume tier, the entry level is cheap enough to buy once and measure: [👉 Start a 9Proxy account and run a small IP pack against your real targets](https://bit.ly/9-Proxy). Check retention on the platform you care about, then size up — the per-IP rate falls fast once you're past the entry tiers.
