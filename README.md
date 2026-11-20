# Rules_US

- `设备：港版iPhone17 Pro Max
- `账号：美区

面向美区/外版 iPhone 的 Shadowrocket 规则集，主要用于 Apple Intelligence、Claude、Apple TV 双语字幕、Apple News、普通 Apple 服务、国内 App 分流和广告误杀修复。

## 仓库文件

| 文件 | 策略 | 作用 |
| --- | --- | --- |
| `AppleAI.list` | `PROXY` | Apple Intelligence、Private Cloud Compute 和 Siri |
| `Claude.list` | `PROXY,force-remote-dns` | Claude 与 Anthropic 域名优先代理并强制远程解析 |
| `Apple_PROXY.list` | `PROXY` | Apple TV、DualSubs、视频 CDN 和 Apple News |
| `Apple_DIRECT.list` | `DIRECT` | 除 AI、Apple TV 和 News 外的普通 Apple 域名与 IP |
| `PreRepair_DIRECT.list` | `DIRECT` | 在广告规则前放行被误杀的直连项目 |
| `PreRepair_PROXY.list` | `PROXY` | 在广告规则前放行需要代理的项目 |
| `PreRepair_REJECT.list` | `REJECT-DROP` | 补充拦截分析和日志请求，避免部分 App 反复弹窗 |
| `DomesticApps.list` | `DIRECT` | 常用中国大陆 App 的明确直连规则 |
| `GeositeCN.list` | `DIRECT` | 作者修正版 GeositeCN 的 Shadowrocket 转换版 |

## 上游来源

以下转换规则均保留原项目出处：

- `Apple_DIRECT.list`：[Accademia/Additional_Rule_For_Clash - Apple](https://github.com/Accademia/Additional_Rule_For_Clash/tree/main/Apple)
- `PreRepair_*.list`：[Accademia/Additional_Rule_For_Clash - PreRepairEasyPrivacy](https://github.com/Accademia/Additional_Rule_For_Clash/tree/main/PreRepairEasyPrivacy)
- `GeositeCN.list`：[Accademia/Additional_Rule_For_Clash - GeositeCN](https://github.com/Accademia/Additional_Rule_For_Clash/tree/main/GeositeCN)
- `Claude.list`：合并并去重 [blackmatrix7 Claude](https://github.com/blackmatrix7/ios_rule_script/tree/master/rule/Shadowrocket/Claude) 与 [blackmatrix7 Anthropic](https://github.com/blackmatrix7/ios_rule_script/tree/master/rule/Shadowrocket/Anthropic)，补充 `claude.com`。
- Apple TV 双语字幕分流用于配合 [DualSubs Universal](https://dualsubs.github.io/guide/universal) 和 [NSRingo TV](https://github.com/NSRingo/TV)。
- `AppleAI.list`、`Apple_PROXY.list` 和 `DomesticApps.list` 是针对本配置整理的 Shadowrocket 分流规则。
- `Apple_DIRECT.list` 已去除与 `AppleAI.list` 完全重复的 3 条 PCC 域名；具体 Apple TV 和 News 代理规则必须排在普通 Apple 直连规则之前。

主配置仍直接引用以下上游 Shadowrocket 规则，不在本仓库重复复制：

- LAN：[blackmatrix7/ios_rule_script - Lan](https://github.com/blackmatrix7/ios_rule_script/tree/master/rule/Shadowrocket/Lan)
- AdvertisingLite：[blackmatrix7/ios_rule_script - AdvertisingLite](https://github.com/blackmatrix7/ios_rule_script/tree/master/rule/Shadowrocket/AdvertisingLite)
- Proxy：[blackmatrix7/ios_rule_script - Proxy](https://github.com/blackmatrix7/ios_rule_script/tree/master/rule/Shadowrocket/Proxy)

## 使用方法

这些文件需要以 `RULE-SET` 方式引用，并使用上表所列策略。

```conf
RULE-SET,https://raw.githubusercontent.com/fafatop/Rules_US/main/AppleAI.list,PROXY
```

规则顺序应保持为：

1. Apple Intelligence
2. Claude / Anthropic：`PROXY,force-remote-dns`
3. Apple：先 `Apple_PROXY`，再 `Apple_DIRECT`
4. LAN
5. 广告误杀修复：`DIRECT`、`PROXY`、`REJECT-DROP`
6. AdvertisingLite
7. 明确国内 App
8. 修正版 GeositeCN
9. Proxy
10. `GEOIP,CN`
11. `FINAL,PROXY`

广告误杀修复必须放在 AdvertisingLite 前面；Apple Intelligence、Claude、Apple TV 和 Apple News 必须放在普通 Apple 及中国区规则前面。

主配置 `Rules_US.conf` 暂不发布到本仓库。
