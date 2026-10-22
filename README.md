# Conservative Pi-hole tracking add-on

102 additional exact hostnames, checked against downloaded upstream lists on October 18 and October 22, 2026. Keep your existing StevenBlack hosts and HaGeZi Normal subscriptions enabled.

This is a small, deliberately conservative supplement, not a complete tracker database. It targets dedicated analytics and visitor-identification endpoints. It does not promise a perfect Super Adblock Test score or zero site breakage.

## Upload to GitHub and subscribe

1. Unzip the bundle. Upload its contents to the root of a public GitHub repository, preserving `LICENSE`, `NOTICE.md`, the evidence files, and this README alongside `pihole-tracking-addon.txt`.
2. Open `pihole-tracking-addon.txt` on GitHub and click **Raw**. The result should show plain text, beginning with `# Conservative Pi-hole tracking add-on`.
3. Copy that Raw URL. For a file at the root of a repository using the `main` branch, the pattern is:

   ```text
   https://raw.githubusercontent.com/abhibambhaniya/pihole-tracking-addon/refs/heads/main/pihole-tracking-addon.txt
   ```

   The URL above is the published subscription. If you fork the repository, use your own Raw URL. Do not subscribe to a GitHub `/blob/` page, the ZIP, README, or evidence CSV. A private repository's ordinary Raw URL is not a reliable unauthenticated subscription.

4. In Pi-hole's web interface, open **Lists** (Pi-hole v6) or **Group Management → Adlists** (v5). Add the Raw URL as an enabled **blocking** list. Assign it to the group containing your devices; normally this is **Default**.
5. Run **Tools → Update Gravity**, or run `pihole -g` on the Pi-hole host. Confirm the new URL downloads successfully and imports **102 exact domains**. There should be no invalid domains from this file. Overall domain totals need not increase by 102 if your other subscriptions have changed or overlap.
6. In Pi-hole's domain search, look for `metrics.angi.com` to check list membership. From a client using Pi-hole, query that hostname and inspect Pi-hole's Query Log for a gravity-blocked result. The DNS response depends on your configured blocking mode; do not assume it must be `0.0.0.0`.

Pi-hole can fetch later edits to this GitHub file during gravity updates. **Hosting the file does not automatically curate or regenerate it.** This delivery is a dated snapshot.

## Selection and overlap verification

The original 53 hostnames each have an unconditional `||hostname^` rule in both **HaGeZi Pro** and **EasyPrivacy**. Only narrowly selected entries from EasyPrivacy's Adobe analytics, AT Internet audience measurement, and Lead Forensics visitor-identification sections were retained. The source section is classification evidence; it is not an independent live confirmation of the current CNAME target.

| Check | Result |
| --- | ---: |
| StevenBlack blocked hostnames parsed | 71,492 |
| HaGeZi Normal unconditional domain rules parsed | 166,141 |
| HaGeZi Pro unconditional domain rules parsed | 202,297 |
| EasyPrivacy unconditional domain rules parsed | 43,242 |
| Pro ∩ EasyPrivacy candidates after baseline coverage removal | 117 |
| Original selection | 53 |
| Reviewed additions | 3 |
| Current hostnames | 56 |
| Candidates excluded by conservative scope | 64 |
| Duplicate hostnames in delivered list | 0 |
| Exact overlap with either baseline | 0 |
| Additional coverage already supplied by a Normal parent rule | 0 |

The parent check matters: HaGeZi's `||example.com^` can already cover `metrics.example.com`. StevenBlack hosts entries were treated as exact matches, not wildcard blocks. Only unconditional domain rules were used; browser conditions such as `$third-party` were not turned into global DNS rules.

The delivered list narrows upstream rules to **exact hostnames**. A line does not automatically block all its subdomains. It contains no regex, wildcard, URL, IP address, cosmetic filter, or JavaScript rule. Pi-hole's official [FTL parser](https://github.com/pi-hole/FTL/blob/master/src/tools/gravity-parseList.c) accepts hostname tokens and skips `#` comment lines; [gravity](https://docs.pi-hole.net/main/pihole-command/) retrieves subscribed lists.

`domain-evidence.csv` gives the source rule, EasyPrivacy section and snapshot line for every included hostname. `excluded-candidates.csv` records the remaining candidate pool. `source-manifest.json` records download URLs, SHA-256 hashes, upstream version metadata and counts. Hashes identify the exact downloaded snapshots; upstream branch URLs will change.

## Fingerprinting coverage and breakage choices

The downloaded StevenBlack file already lists `fpjs.io`, `api.fpjs.io`, and `fpjscdn.net`. HaGeZi Normal already covers `customfingerprints.bablosoft.com`. These existing entries were not duplicated. This is a coverage check, not a recommendation to add further fraud-prevention domains.

No new domain is presented here as a verified fingerprinting-only endpoint. Broader fingerprinting and fraud-detection blocks can interfere with authentication, checkout and anti-bot checks. This add-on excludes consent/CMP endpoints, anti-bot services, crash/error reporting, broad cloud/CDN roots, email/deep-link endpoints, and selected financial or streaming endpoints from the candidate pool. The underlying two subscriptions may already block some such services; this add-on does not change that.

DNS filtering cannot stop fingerprinting scripts served from the same hostname as the page, fingerprint computation already running in the browser, URL-path tracking, or every first-party/CNAME tracker. Use browser tracking protections as well. [HaGeZi's documentation](https://github.com/hagezi/dns-blocklists#recommendation) also recommends pairing DNS filtering with browser filtering.

The earlier failed-domain screenshot was not available in this request, so those specific failures and a revised test score were not verified.

## Performance, troubleshooting and maintenance

102 exact entries are a small addition to your existing lists. A material increase in DNS lookup cost is not expected, but no latency, memory, throughput or site-compatibility benchmark was run on your Pi-hole. A blocked request can still cause application retries or delays.

If a site breaks, check the Query Log for the affected client and time. Allowlist only the exact hostname needed after confirming the relationship. To roll back the whole add-on, disable its list entry and update gravity; retry after DNS/browser caches expire. Existing lists can still block the same hostname.

Re-check the file when your needs change and periodically against upstream false-positive fixes. Rebuilds should remove newly overlapping or withdrawn entries and review every proposed addition. Do not append the entire Pro-minus-Normal difference: Pro deliberately includes categories omitted from Normal, including error reporting. If you replace Normal with Pro later, the original 56 entries become redundant; the October 22 additions sourced from HaGeZi native tracker lists or EasyPrivacy are not all in Pro.

Validation here covers downloaded source membership, parent/exact overlap, uniqueness and hostname syntax. The original 53-host list was published and imported successfully. A Safari test after the network connection changed scored 97% (460 blocked, 22 reachable); Pi-hole logged fresh blocked probes. The review below adds one host. No login, payment, or YouTube compatibility claim is made without live testing.

## Sources and redistribution

- [HaGeZi Pro](https://raw.githubusercontent.com/hagezi/dns-blocklists/main/adblock/pro.txt): primary selection source, GPL-3.0.
- [EasyPrivacy](https://easylist.to/easylist/easyprivacy.txt): corroborating unconditional rules and categories; The EasyList authors. Its [licensing page](https://easylist.to/pages/licence.html) offers GPL v3 or later as one option; this distribution uses that option.
- [HaGeZi Normal](https://raw.githubusercontent.com/hagezi/dns-blocklists/main/adblock/multi.txt) and [StevenBlack hosts](https://raw.githubusercontent.com/StevenBlack/hosts/master/hosts): overlap checks only; their full contents are not redistributed here.

See `NOTICE.md` and the full GPL-3.0 text in `LICENSE`. Retain attribution and license when uploading or modifying this package.

## Review of the 22 reachable probes — October 18, 2026

Added **rs.fullstory.com** as an exact hostname. It appears in the downloaded HaGeZi Pro list; EasyPrivacy has a broader third-party FullStory rule. The DNS decision is independently supported by FullStory's [recorder-host documentation](https://developer.fullstory.com/browser/fullcapture/configure-capture/) and [CSP guide](https://help.fullstory.com/hc/en-us/articles/360020622856-Can-I-use-Content-Security-Policy-CSP-with-Fullstory), which distinguish the recorder from the app host and describe visitor event capture. Blocking recording is the intended effect. This is a lower-risk choice, not a guarantee that every site's implementation tolerates a blocked recorder.

All 22 individual decisions are in `remaining-22-review.csv`. The other 21 remain outside this add-on: shared services, dashboards, vendor homepages, redirects, security/fraud checks, error reporting, or insufficient evidence for a hostname-wide block. No new fingerprinting-only collector was identified among the 22; Sift is a fraud-prevention service and was excluded to protect login/payment flows.

PostHog's [API documentation](https://posthog.com/docs/api) says its public host serves both event capture and feature flags, while other hosts serve private APIs. Therefore `us.i.posthog.com`, `app.posthog.com`, and `eu.posthog.com` were not added. [Google's instructions](https://support.google.com/tagmanager/answer/14842164) identify `tagmanager.google.com` as the signed-in dashboard. [Branch documents](https://help.branch.io/account-hub/basic-link-configuration) `bnc.lt` as a deep-link domain. YouTube and Googlevideo hosts and Facebook Graph API remain unmodified. Retained means not newly blocked by this file, not globally allowlisted or guaranteed reachable.

The per-domain evidence and manifest from the original build describe that original 53-host selection. This section supplies the evidence for the added FullStory host. The source snapshots were downloaded October 18, 2026; later upstream membership may differ. Preserve the original source-manifest hashes for that audit trail.

## Chrome 54-probe review — October 18, 2026

Added two exact telemetry hosts after reviewing the user's Chrome results:

- `events.launchdarkly.com`: LaunchDarkly event/analytics destination, present in the downloaded HaGeZi Pro list and EasyPrivacy's third-party rule. LaunchDarkly's [architecture page](https://launchdarkly.com/docs/home/getting-started/architecture), including its SDK configuration, separates `eventsUrl` from `streamUrl`. `clientstream.launchdarkly.com` remains unmodified for feature-flag delivery. Losing analytics/experimentation event reporting is intended; flag streaming is preserved.
- `rum.browser-intake-datadoghq.com`: Datadog browser Real User Monitoring intake. HaGeZi Pro covers its parent `browser-intake-datadoghq.com`. Datadog's [official browser SDK endpoint builder](https://github.com/DataDog/browser-sdk/blob/main/packages/js-core/src/transport/endpointBuilder.ts) defines RUM intake tracks and the browser-intake hostname construction. Only this exact RUM hostname is added, not the parent or dashboard/API hosts.

`chrome-54-review.csv` contains a decision and reason for all 54 entries, with `www\.awin1.com` normalized to `www.awin1.com`. The `/rtrg` URL path cannot be expressed in a Pi-hole hostname list. Retained domains are not newly allowlisted; this update simply avoids adding them. The user's pasted safety assessment was treated as a proposal, not evidence of compatibility. Its login/payment exceptions were honored over blanket 'safe' labels.

These two additions are based on maintained-list membership and distinct telemetry service roles. Universal compatibility cannot be promised; no login, checkout or financial transaction was submitted. See local validation report for measured DNS/browser results. Earlier source-manifest and evidence CSV retain the original 53-host snapshot; subsequent additions are documented in these review sections.

## Household review — October 22, 2026

Added **46 exact hostnames** that household devices actually resolved through this Pi-hole between October 15 and 22, 2026, and that StevenBlack and HaGeZi Normal did not block. Every addition is backed by a maintained list: HaGeZi Pro, a HaGeZi native tracker list (`native.apple`, `native.winoffice`, `native.amazon`), or an unconditional EasyPrivacy rule. HaGeZi's native lists are a new evidence tier for this file. They target device and OS telemetry and are maintained for low breakage, which is why `xp.apple.com`, deferred in the Chrome review, is now added.

| Group | Added | Examples |
| --- | ---: | --- |
| Microsoft 365 / Windows telemetry | 17 | `*.events.data.microsoft.com`, Office `-telemetry` hosts, NEL report collectors |
| Apple analytics and feedback | 6 | `xp.apple.com`, `fbs.smoot.apple.com`, `cstat.cdn-apple.com` |
| Amazon metrics and ad beacons | 5 | `unagi-na.amazon.com`, `aax-events-*.amazon-adsystem.com` |
| Google client tracing and promo targeting | 4 | `clienttracing-pa.googleapis.com`, `appsgrowthpromo-pa.googleapis.com` |
| Cross-site retargeting and attribution | 6 | Criteo hosts, `alb.reddit.com` (Reddit Pixel), `analytics.adjust.com` |
| Session replay, surveys, fingerprinting, browser pings | 4 | `e.logrocket.com`, `cdn.sprig.com`, `use1-turn.fpjs.io`, `usage-ping.brave.com` |
| TV analytics | 1 | `xclass-beacons.xumo.com` |
| Pop-under ad redirects | 3 | hosts loaded by streaming sites, all in HaGeZi Pro |

`household-2026-10-22-review.csv` records all 185 observed candidates with hits, decision, reason and the matching upstream rule:

- **keep (93):** functional or mixed-use hosts. This covers anti-fraud and bot-defense fingerprinting (ThreatMetrix, Forter, Sift, PerimeterX, DataDome, AWS WAF, Google BotGuard), feature flags, consent tools, deep links and click redirects, dashboards, YouTube stats, Comcast TV device management, error and crash reporting, and every earlier keep decision.
- **defer (40):** tracking-like hosts with no maintained-list evidence yet, for example `tvinteractive.tv` (Samba TV viewing data), `pi.reddit.com`, `events.segment.io`, LG and Comcast TV ad endpoints, and randomly named `.rest` redirect hosts. They need vendor documentation or a live test before inclusion.
- **already-covered / already-in-addon (6):** blocked by the baseline lists or by earlier additions; the logged queries predate those updates.

`use1-turn.fpjs.io` is the one fingerprinting addition. Its parent `fpjs.io` is already in StevenBlack, so it adds no new breakage class. All other fingerprinting services stay excluded to protect logins and payments. The `source-manifest.json` key `review_2026_10_22` records the hashes of the upstream snapshots used for this review.

## Network settings this list cannot cover

From October 18, devices on this network queried `_dns.resolver.arpa` (Apple's Discovery of Designated Resolvers) and then `dns.quad9.net` almost 1,000 times. That pattern means clients were upgrading to Quad9 encrypted DNS, which sends their lookups around Pi-hole. iCloud Private Relay hosts were also active. A hostname list cannot stop either one. On Pi-hole v6, enable the built-in handling:

```bash
sudo pihole-FTL --config dns.specialDomains.designatedResolver true
sudo pihole-FTL --config dns.specialDomains.iCloudPrivateRelay true
```

## Repeating the household review

Export a week of allowed queries on the Pi-hole host, then review the result against the current baselines in the same way as above:

```bash
sudo pihole-FTL sqlite3 -header -csv /etc/pihole/pihole-FTL.db "
SELECT domain, COUNT(*) AS hits, COUNT(DISTINCT client) AS clients,
       GROUP_CONCAT(DISTINCT client) AS client_ips,
       datetime(MIN(timestamp),'unixepoch','localtime') AS first_seen,
       datetime(MAX(timestamp),'unixepoch','localtime') AS last_seen
FROM queries
WHERE timestamp >= strftime('%s','now','-7 days')
  AND status IN (2,3,12,13,14,17)
GROUP BY domain ORDER BY hits DESC;" > allowed_7d.csv
```

The raw export identifies household devices and browsing, so it is not committed to this public repository; only the reviewed hostnames are.
