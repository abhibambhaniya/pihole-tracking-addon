# Attribution and modification notice

This package's blocklist is a modified, reduced, exact-hostname selection from HaGeZi's DNS Blocklists, corroborated by EasyPrivacy.

- HaGeZi DNS Blocklists: https://github.com/hagezi/dns-blocklists
  Original list: https://raw.githubusercontent.com/hagezi/dns-blocklists/main/adblock/pro.txt
  Distributed upstream under GNU GPL version 3.
- The EasyList authors: https://easylist.to/
  EasyPrivacy: https://easylist.to/easylist/easyprivacy.txt
  Licensing: https://easylist.to/pages/licence.html
  The GPL version 3 or later option is used for this selection.

Modifications made October 18, 2026: retain a conservative subset of mutually corroborated unconditional domain rules; remove hostnames covered by the downloaded StevenBlack hosts and HaGeZi Normal snapshots; narrow remaining rules to exact hostnames; sort and deduplicate; add documentation and source evidence. No upstream endorsement is implied.

The selected list and accompanying original documentation/evidence are supplied under GPL-3.0. A complete license is included in LICENSE. The editable text blocklist is the preferred form for modification; the CSV contains every selected rule and classification reference. Full baseline lists are not bundled.

This package is provided without warranty. Source membership does not establish that a domain is still active, solely used for tracking, or safe to block in every application. See README.md for verification limits.

Additional modification October 18, 2026: add the exact FullStory recorder host rs.fullstory.com after vendor-documentation review of 22 reachable probes; retain 21 functional, mixed-use, diagnostics or insufficiently verified hosts.

Chrome review: add events.launchdarkly.com and rum.browser-intake-datadoghq.com as exact telemetry hosts; preserve functional, consent, redirect, fraud-prevention and video service hosts.
