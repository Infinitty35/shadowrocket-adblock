# Infinitty Adblock (Shadowrocket)

Remote ad/tracker blocking for **iPhone and iPad**. Stacks with your existing nodes and the Peacock / cable-TVE modules.

Upstream lists rebuild **daily**. This repo is **health-checked every Monday** (GitHub Actions) and the module timestamp is bumped so Shadowrocket re-fetches.

## Install (recommended — module)

Does **not** replace your current config or proxy nodes.

1. Copy:

```
https://raw.githubusercontent.com/Infinitty35/shadowrocket-adblock/main/adblock.module
```

2. Shadowrocket → **Config** → **Modules** → **+** → paste URL → Download.
3. Turn the module **on**.
4. Home → connect → force-quit Safari / the app you care about → reopen.

Leave your existing Peacock / cable-TVE config as-is. First-match-wins: Apple, Peacock playback, and Adobe Pass are allowlisted at the top of this module.

## Optional: full config

Only if you want a standalone config (no nodes included):

```
https://raw.githubusercontent.com/Infinitty35/shadowrocket-adblock/main/adblock.conf
```

Config → **+** → Download from URL. Re-enable your node subscription afterward if Home is empty.

## Auto-update (once a week is enough)

1. **Settings → General → Background App Refresh** → allow Shadowrocket.
2. Shadowrocket → **Settings → Subscribe** → enable **Update in background**.
3. Config list → tap **ⓘ** on the active config → enable **Automatic Update**.
4. Modules refresh when the config does. This repo’s GitHub Action runs **Monday 07:00 CDT**, probes the feeds, vendors HaGeZi, and stamps `#!updated=` so Shadowrocket sees a new file.

The module’s remote lists:

| Source | What it is | Cadence | Why this one |
|---|---|---|---|
| [Johnshall `sr_ad_only`](https://github.com/Johnshall/Shadowrocket-ADBlock-Rules-Forever) | EasyList + EasyList China + Peter Lowe, native Shadowrocket (~56k) | Daily 00:00 UTC+8 | Best-maintained SR ad list (30k+ stars). |
| [HaGeZi Pro Mini](https://github.com/hagezi/dns-blocklists) | DNS ad/tracker domains (~51k), `DOMAIN-SET` | Several times/day | Plain domain list; works as DOMAIN-SET. |
| [anti-AD surge](https://github.com/privacy-protection-tools/anti-AD) | Extra DNS ads (~99k `DOMAIN-SUFFIX`) | Daily | App + web coverage on top of EasyList. |
| This repo | Apple allowlist, Peacock SSAI shards, cable TVE (FreeWheel/TrueX/IMA), US mobile ad SDKs | Weekly stamp | Your streaming rules stay above the big lists. |

See [STATUS.md](STATUS.md) for the latest Monday probe.

### Lists researched and **not** used

- **blackmatrix7 AdvertisingLite** — README says ~38k rules; the actual `AdvertisingLite.list` on GitHub is a 387-line stub last touched 2025-12-08.
- **blackmatrix7 Advertising (full)** — claimed 281k; GitHub raw returns ~26 KB (truncated / LFS).
- **217heidai Lite** — China-domain-only.
- **h2y/Shadowrocket-ADBlock-Rules** — archived 2021.
- **GMOogway `sr_reject_list`** — 188k, updated daily, but too heavy stacked with the three lists above.

## What this will and will not do

- **Will:** block a large share of website ads, app-open ads, trackers, and many streaming ad SDKs (FreeWheel, Google IMA, Amazon TAM, AppLovin, Unity Ads, ironSource).
- **Will not:** skip ads that are stitched into the video (SSAI). Peacock / some TVE titles still leak those — same as before.
- **Do not enable HTTPS decryption** for this module. Domain REJECT does not need MITM. MITM breaks banking and some apps (SSL pinning).

If Safari or an app feels slow after import, delete the `anti-ad.net/surge.txt` line from the module (that list is the largest).

If a site or app **breaks**, add at the **top** of a personal module:

```
DOMAIN-SUFFIX,broken-site.com,DIRECT
```

## License

MIT. Upstream lists keep their own licenses (EasyList, HaGeZi, anti-AD, Johnshall).
