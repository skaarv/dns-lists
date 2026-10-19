# dns-lists

Personal DNS block and allow lists, layered on top of [HaGeZi Pro++](https://github.com/hagezi/dns-blocklists).

| File | Purpose | Raw URL |
|---|---|---|
| `blocklist.txt` | Extra blocks | https://raw.githubusercontent.com/skaarv/dns-lists/main/blocklist.txt |
| `allowlist.txt` | Fixes for HaGeZi false positives | https://raw.githubusercontent.com/skaarv/dns-lists/main/allowlist.txt |

## Where they're used

| Server | Software | Base list | Block list | Allow list |
|---|---|---|---|---|
| 10.99.10.4 | AdGuard Home | DNS blocklists | DNS blocklists | DNS allowlists |
| 10.99.10.5 | Pi-hole (unRAID container `pihole-dot-doh`) | Lists, type Block | Lists, type Block | Lists, type Allow |
| 10.99.10.6 | Pi-hole (`pihole2`) | Lists, type Block | Lists, type Block | Lists, type Allow |

All three refresh their subscriptions daily, so a pushed change reaches every server within 24 hours. The custom-rule boxes in each UI stay empty: every tweak lives here.

## Rules

- Use `||domain^` (block) and `@@||domain^` (allow). Both match the domain and all its subdomains, and both AdGuard Home and Pi-hole v6 understand them.
- Don't add modifiers like `$important`: Pi-hole ignores any line that has one. The `$dnsrewrite` line in `blocklist.txt` is the one deliberate exception (Pi-hole handles that domain natively).
- Allow the narrowest host that fixes the problem, never a whole platform.
- Allows win over blocks on both products, so an allow here overrides HaGeZi and `blocklist.txt` alike.
