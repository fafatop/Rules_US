# Rules_US

Shadowrocket rule providers for a US-oriented iPhone configuration, with Apple Intelligence, Apple TV bilingual subtitles, Apple News, Apple services, domestic-app routing, and ad-filter repair rules.

## Hosted rule files

| File | Policy | Purpose |
| --- | --- | --- |
| `AppleAI.list` | `PROXY` | Apple Intelligence, Private Cloud Compute, and Siri |
| `AppleTV_DualSubs.list` | `PROXY` | Apple TV APIs, DualSubs endpoints, and video CDN traffic |
| `AppleNews.list` | `PROXY` | Apple News traffic |
| `Apple_Domain_IP.list` | `DIRECT` | Remaining Apple domains and Apple IP ranges |
| `PreRepair_DIRECT.list` | `DIRECT` | Direct exceptions placed before the ad rules |
| `PreRepair_PROXY.list` | `PROXY` | Proxy exceptions placed before the ad rules |
| `PreRepair_REJECT.list` | `REJECT` | Additional analytics and logging blocks |
| `DomesticApps.list` | `DIRECT` | Explicit rules for commonly used mainland Chinese apps |
| `GeositeCN.list` | `DIRECT` | Cleaned mainland-China domain rules converted for Shadowrocket |

## Upstream sources

The converted rule files retain their upstream attribution:

- `Apple_Domain_IP.list`: [Accademia/Additional_Rule_For_Clash - Apple](https://github.com/Accademia/Additional_Rule_For_Clash/tree/main/Apple)
- `PreRepair_*.list`: [Accademia/Additional_Rule_For_Clash - PreRepairEasyPrivacy](https://github.com/Accademia/Additional_Rule_For_Clash/tree/main/PreRepairEasyPrivacy)
- `GeositeCN.list`: [Accademia/Additional_Rule_For_Clash - GeositeCN](https://github.com/Accademia/Additional_Rule_For_Clash/tree/main/GeositeCN)
- Apple TV bilingual-subtitle routing is designed for [DualSubs Universal](https://dualsubs.github.io/guide/universal) and [NSRingo TV](https://github.com/NSRingo/TV).
- `AppleAI.list`, `AppleTV_DualSubs.list`, `AppleNews.list`, and `DomesticApps.list` are Shadowrocket-specific routing selections assembled for this configuration.

The main configuration continues to reference these upstream Shadowrocket rule sets directly instead of copying them into this repository:

- LAN: [blackmatrix7/ios_rule_script - Lan](https://github.com/blackmatrix7/ios_rule_script/tree/master/rule/Shadowrocket/Lan)
- AdvertisingLite: [blackmatrix7/ios_rule_script - AdvertisingLite](https://github.com/blackmatrix7/ios_rule_script/tree/master/rule/Shadowrocket/AdvertisingLite)
- Proxy: [blackmatrix7/ios_rule_script - Proxy](https://github.com/blackmatrix7/ios_rule_script/tree/master/rule/Shadowrocket/Proxy)

## Shadowrocket usage

Use each file as a `RULE-SET` and assign the policy shown in the table. The repair files must appear before AdvertisingLite. Apple Intelligence, Apple TV, and Apple News must appear before the general Apple rule file.

Example:

```conf
RULE-SET,https://raw.githubusercontent.com/fafatop/Rules_US/main/AppleAI.list,PROXY
```

The main `Rules_US.conf` configuration is intentionally not published in this repository yet.
